---
description: One function for both inline and reply keyboard buttons.
icon: square-small
---

# btn()

`btn()` creates **inline** buttons (attached to a message) and **reply keyboard** buttons (shown at the bottom of the screen). The type is determined automatically by the action you pass.

{% code title="Signature" %}
```python
btn(
    text: str,
    action: str | _UserRequest | _ChatRequest = None,
    *,
    # — inline only —
    url: str = None,
    miniApp: str = None,
    loginUrl: dict = None,
    switchInline: str = None,
    switchInlineCurrent: str = None,
    switchInlineChosen: dict = None,
    copyText: str = None,
    pay: bool = False,
    # — reply keyboard only —
    requestPoll: str = None,        # "regular" | "quiz"
    requestContact: bool = False,
    requestLocation: bool = False,
    # — appearance —
    style: str = None,              # "primary" | "danger" | "success"
    emoji: str = None,
)
```
{% endcode %}

***

## Inline buttons

Pass a `"prefix:value"` string — Telegram sends it back as a `callback_query`.

{% code title="Examples" overflow="wrap" %}
```python
btn("Confirm",    "act:confirm")
btn("Cancel",     "act:cancel")

btn("Save",       "act:save",   style="primary")
btn("Delete",     "act:delete", style="danger")
btn("Done",       "act:done",   style="success")

btn("Open site",  url="https://example.com")
btn("Open app",   miniApp="https://example.com/app")
btn("Copy token", copyText="abc-123")
btn("Share",      switchInline="")
btn("Pay",        pay=True)
```
{% endcode %}

***

## Reply keyboard buttons

One-tap buttons that send a special message back automatically.

{% code title="Examples" overflow="wrap" %}
```python
btn("Send phone",    requestContact=True)
btn("Send location", requestLocation=True)
btn("Quiz",          requestPoll="quiz")
btn("Poll",          requestPoll="regular")
```
{% endcode %}

***

## `userRequest()` — pick a user

Opens Telegram's built-in user picker. Result arrives as a `message` with `users_shared`.

{% code title="Signature" %}
```python
userRequest(
    requestId: int,               # your id — tells buttons apart inside the handler
    *,
    isBot: bool = None,           # True → bots only  /  False → no bots
    isPremium: bool = None,       # True → premium users only
    maxQuantity: int = None,      # how many to pick (1–10, default 1)
    requestName: bool = None,     # include first_name in result
    requestUsername: bool = None, # include username in result
    requestPhoto: bool = None,    # include photo in result
)
```
{% endcode %}

{% code title="Buttons" overflow="wrap" %}
```python
btn("Pick user",     userRequest(1, requestName=True, requestUsername=True))
btn("Pick 3 users",  userRequest(2, maxQuantity=3, requestName=True))
btn("Bots only",     userRequest(3, isBot=True))
btn("Premium only",  userRequest(4, isPremium=True, requestName=True))
```
{% endcode %}

{% code title="Handler" overflow="wrap" %}
```python
@bot.onMedia("users_shared")
def on_user(msg):
    rid   = msg.users_shared.request_id       # which button was pressed (1, 2, 3...)
    users = msg.users_shared.users            # list of picked users

    u     = users[0]                          # first user (or loop for maxQuantity > 1)
    uid   = u.user_id                         # always present
    name  = getattr(u, "first_name", "?")     # present if requestName=True
    uname = getattr(u, "username",   None)    # present if requestUsername=True
```
{% endcode %}

***

## `chatRequest()` — pick a chat

Opens Telegram's built-in chat picker. Result arrives as a `message` with `chat_shared`.

{% code title="Signature" %}
```python
chatRequest(
    requestId: int,                   # your id — tells buttons apart inside the handler
    *,
    isChannel: bool = None,           # True → channels only  /  False → groups only
    isForum: bool = None,             # True → forum supergroups only
    hasUsername: bool = None,         # True → must have @username
    isCreated: bool = None,           # True → only chats the user owns
    botIsMember: bool = None,         # True → bot must already be a member
    requestTitle: bool = None,        # include title in result
    requestUsername: bool = None,     # include username in result
    requestPhoto: bool = None,        # include photo in result
    userAdminRights: dict = None,     # required admin rights for the user
    botAdminRights: dict = None,      # required admin rights for the bot
)
```
{% endcode %}

{% code title="Buttons" overflow="wrap" %}
```python
btn("Any chat",   chatRequest(1))
btn("Channel",    chatRequest(2, isChannel=True,  requestTitle=True, requestUsername=True))
btn("Group",      chatRequest(3, isChannel=False, requestTitle=True))
btn("My chat",    chatRequest(4, isCreated=True,  requestTitle=True))
btn("Forum",      chatRequest(5, isForum=True, botIsMember=True))
```
{% endcode %}

{% code title="Handler" overflow="wrap" %}
```python
@bot.onMedia("chat_shared")
def on_chat(msg):
    rid     = msg.chatShared.request_id       # which button was pressed (1, 2, 3...)
    chat_id = msg.chatShared.chat_id          # always present
    title   = getattr(msg.chatShared, "title",    "?")   # present if requestTitle=True
    uname   = getattr(msg.chatShared, "username", None)  # present if requestUsername=True
```
{% endcode %}

***

## Full example

{% code title="bot.py" overflow="wrap" %}
```python
from gramly import Gramly, btn, userRequest, chatRequest

bot = Gramly("TOKEN")


@bot.onMessage(commands="start")
def start(msg):
    bot.send(
        msg.chat_id,
        "Choose:",
        keyboard=[
            [btn("Pick a user", userRequest(1, requestName=True, requestUsername=True))],
            [btn("Pick a chat", chatRequest(2, requestTitle=True, requestUsername=True))],
        ],
    )


@bot.onMedia("users_shared")
def got_user(msg):
    u     = msg.users_shared.users[0]
    name  = getattr(u, "first_name", "?")
    uname = f"@{u.username}" if getattr(u, "username", None) else "—"
    bot.send(msg.chat_id, f"<b>{name}</b>  {uname}\n<code>{u.user_id}</code>", keyboard=False)


@bot.onMedia("chat_shared")
def got_chat(msg):
    s     = msg.chatShared
    title = getattr(s, "title",    "?")
    uname = f"@{s.username}" if getattr(s, "username", None) else "—"
    bot.send(msg.chat_id, f"<b>{title}</b>  {uname}\n<code>{s.chat_id}</code>", keyboard=False)


bot.run()
```
{% endcode %}
