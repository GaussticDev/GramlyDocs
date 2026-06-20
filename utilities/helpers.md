---
description: chatId, userId, toList, isNotModified, mimeType.
icon: code
---

# Helpers

## `chatId(target) → int`

Extracts a chat ID from any supported type:

{% code title="Signature" %}
```python
chatId(12345)             # int passthrough
chatId({"id": 12345})    # dict
chatId(msg)              # Message, CallbackQuery, JoinRequest, etc.
chatId(q)                # also works on any object with .chat_id or .chat.id
```
{% endcode %}

## `userId(target) → Optional[int]`

Extracts a user ID from any supported type:

{% code title="Signature" %}
```python
userId(12345)
userId(msg)               # Message — reads .from_user.id
userId(q)                 # CallbackQuery
```
{% endcode %}

## `toList(value) → list`

Wraps a value in a list, or returns it unchanged if already a list.

{% code title="Signature" %}
```python
toList(None)         # []
toList("start")      # ["start"]
toList(["a", "b"])   # ["a", "b"]
```
{% endcode %}

## `isNotModified(e: Exception) → bool`

Returns `True` if the exception is the Telegram "message is not modified" error. Useful for silent edit retries:

{% code title="Signature" %}
```python
try:
    bot.edit(q, new_text)
except TelegramError as e:
    if not isNotModified(e):
        raise
```
{% endcode %}

## `mimeType(ext: str) → str`

Returns the MIME type string for a file extension.

{% code title="Signature" %}
```python
mimeType("jpg")    # "image/jpeg"
mimeType("jpeg")   # "image/jpeg"
mimeType("png")    # "image/png"
mimeType("webp")   # "image/webp"
mimeType("gif")    # "image/gif"
mimeType("mp4")    # "video/mp4"
mimeType("mov")    # "video/quicktime"
mimeType("pdf")    # "application/pdf"
mimeType("mp3")    # "audio/mpeg"
mimeType("ogg")    # "audio/ogg"
mimeType("xyz")    # "application/octet-stream"  (fallback)
```
{% endcode %}
