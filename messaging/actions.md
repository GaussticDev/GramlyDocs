---
description: Chat actions, forward, copy, delete, pin, reactions.
icon: message-code
---

# Message Actions

## Chat actions

Send a chat action (typing indicator, etc.).

{% code title="Signature" %}
```python
bot.action(target, action: str = "typing")
```
{% endcode %}

{% code title="Available actions" %}
```python
bot.action(chat, "typing")             # typing...
bot.action(chat, "upload_photo")       # sending photo...
bot.action(chat, "record_video")       # recording video...
bot.action(chat, "upload_video")       # sending video...
bot.action(chat, "record_voice")       # recording voice...
bot.action(chat, "upload_voice")       # sending voice...
bot.action(chat, "upload_document")    # sending file...
bot.action(chat, "choose_sticker")     # choosing sticker...
bot.action(chat, "find_location")      # finding location...
bot.action(chat, "record_video_note")  # recording video note...
bot.action(chat, "upload_video_note")  # sending video note...
```
{% endcode %}

## Forward & Copy

{% code title="Forward a message" %}
```python
bot.forward(target, message)                        # Forward single
bot.forwardMessages(target, from_chat_id, msg_ids)  # Forward multiple
```
{% endcode %}

{% code title="Copy a message" %}
```python
bot.copy(target, message, **kwargs)                 # Copy single
bot.copyMessages(target, from_chat_id, msg_ids)     # Copy multiple
```
{% endcode %}

## Delete

{% code title="Delete messages" %}
```python
bot.delete(message)                    # Delete single message (returns True/False)
bot.deleteLater(message, delay_sec)    # Delete after delay
bot.deleteMessages(chat_id, msg_ids)   # Delete multiple messages
```
{% endcode %}

## Pin & Unpin

{% code title="Pin messages" %}
```python
bot.pin(message, notify=False)         # Pin without notification
bot.pin(message, notify=True)          # Pin with notification
bot.unpin(chat_id)                     # Unpin all
bot.unpin(chat_id, msg_id)             # Unpin specific
```
{% endcode %}

## Reactions

{% code title="Set and delete reactions" %}
```python
bbot.react(msg, "👍")                    # Single reaction
bot.react(msg, "🔥", "❤️")              # Multiple reactions

bot.react(msg, "5368324170671202286")   # Custom emoji by ID
bot.react(msg, "❤️", isBig=True)        # Big reaction

bot.react(msg)                          # Remove reaction
```
{% endcode %}

## Leave chat

{% code title="Leave a group or channel" %}
```python
bot.leave(chat_id)
```
{% endcode %}
