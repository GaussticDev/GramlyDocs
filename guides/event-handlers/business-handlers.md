---
description: Business API message handlers — messages, edits, connections, and deletions.
---

# Business Handlers

Handlers for Telegram Business Mode. Connect to business accounts and manage business messages.

## `@bot.onBusinessMessage`

Handle business messages with the same filtering as `@bot.onMessage`.

{% code title="Signature" %}
```python
@bot.onBusinessMessage(
    exact    = None,   # match exact text
    starts   = None,   # text starts with
    contains = None,   # text contains
    regex    = None,   # regex pattern
    guard    = None,   # callable(BusinessMessage) → bool
)
def handler(msg: BusinessMessage): ...
```
{% endcode %}

{% code title="Business message with text filter" %}
```python
@bot.onBusinessMessage(exact="hello")
def on_biz_msg(msg: BusinessMessage):
    msg.reply("Hello from business!")
```
{% endcode %}

{% code title="All business messages" %}
```python
@bot.onBusinessMessage()
def on_all_biz(msg: BusinessMessage):
    if msg.isOwner:
        print(f"Owner said: {msg.text}")
    bot.send(ADMIN_CHAT, f"Business msg: {msg.text}")
```
{% endcode %}

## `@bot.onBusinessEdited`

Handle edited business messages.

{% code title="Signature" %}
```python
@bot.onBusinessEdited()
def on_biz_edit(msg: BusinessMessage): ...
```
{% endcode %}

## `@bot.onBusinessConnection`

Handle business connection lifecycle events.

{% code title="Signature" %}
```python
@bot.onBusinessConnection
def on_biz_conn(conn: BusinessConnection):
    print(f"Connection {conn.id} enabled={conn.isEnabled}")
    print(f"User: {conn.user.first_name}")
    print(f"Can reply: {conn.canReply}")
```
{% endcode %}

## `@bot.onBusinessDeleted`

Handle business messages deleted notification.

{% code title="Signature" %}
```python
@bot.onBusinessDeleted
def on_biz_del(update):
    print(f"Deleted: {update}")
```
{% endcode %}

## Business methods

```python
# Send as business
bot.businessSend(chat_id, "text", bc_id)

# Chat actions
bot.businessAction(chat_id, bc_id, "typing")

# Mark as read
bot.businessRead(bc_id, chat_id, max_message_id)

# Delete business messages
bot.businessDelete(bc_id, chat_id, [msg_ids])

# Get connection
bot.businessConnection(bc_id)
```
