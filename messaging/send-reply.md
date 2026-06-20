---
description: Send new messages and reply to existing ones.
icon: message
---

# Send & Reply

## `bot.send`

Send a message to any chat.

{% code title="Signature" %}
```python
bot.send(
    target,                # int (chat_id), Message, CallbackQuery, or dict
    text: str,
    keyboard=None,         # reply keyboard structure
    inline=None,           # inline keyboard structure
    photo=None,            # photo URL or file_id (sends as photo + caption)
    **kwargs,              # extra Telegram API parameters
)
```
{% endcode %}

{% code title="Basic text" %}
```python
bot.send(chat_id, "Hello!")
bot.send(msg, "Hello!")                   # msg is a Message object
```
{% endcode %}

{% code title="With keyboard" %}
```python
from gramly import btn, row, kbd

bot.send(msg, "Menu:", inline=kbd(
    row(btn("Profile", data=f"{msg.user_id}:profile")),
    row(btn("Settings", data=f"{msg.user_id}:settings")),
))
```
{% endcode %}

{% code title="With photo" %}
```python
bot.send(msg, "Photo caption", photo="https://example.com/image.jpg")
```
{% endcode %}

{% code title="With kwargs" %}
```python
bot.send(msg, "Link preview off", disable_web_page_preview=True)
bot.send(msg, "Protected", protect_content=True)
```
{% endcode %}

## `bot.reply`

Reply to a specific message (adds `reply_to_message_id`).

{% code title="Signature" %}
```python
bot.reply(
    message,              # Message, CallbackQuery, or dict
    text: str,
    keyboard=None,
    inline=None,
    photo=None,
    **kwargs,
)
```
{% endcode %}

{% code title="Reply example" %}
```python
@bot.onMessage(commands="hello")
def on_hello(msg):
    bot.reply(msg, f"Hello {msg.from_user.first_name}!")  # replies to the command
```
{% endcode %}

## Parse mode

The default parse mode is `"HTML"` (set in the constructor). You can override it per-message:

{% code title="Parse modes" %}
```python
bot.send(msg, "<b>bold</b> <i>italic</i>")                    # HTML (default)
bot.send(msg, "*bold* _italic_", parse_mode="MarkdownV2")     # MarkdownV2
bot.send(msg, "Plain text", parse_mode=None)                  # No formatting
```
{% endcode %}
