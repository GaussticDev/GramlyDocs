---
description: Send photos, videos, audio, documents, and media groups.
icon: message-image
---

# Media

## `bot.photo`

Send one or more photos.

{% code title="Signature" %}
```python
bot.photo(
        target, 
        photos, 
        caption: str = None, 
        inline=None, 
        keyboard=None, 
        **kwargs )
```
{% endcode %}

{% code title="Single photo" %}
```python
bot.photo(msg, "https://example.com/image.jpg")
bot.photo(msg, "https://...", caption="Nice view!")
```
{% endcode %}

{% code title="Multiple photos (media group)" %}
```python
bot.photo(chat_id, photos=["url1", "url2", "url3"], caption="Album")
```
{% endcode %}

## `bot.media`

Send up to 10 mixed-media items (photos, videos, audio, documents) in a single album.

{% code title="Signature" %}
```python
bot.media(target, items, caption: str = None, **kwargs)
```
{% endcode %}

{% code title="Mixed album with URLs" %}
```python
bot.media(msg, [
    {"file": "https://.../photo.jpg", "type": "photo"},
    {"file": "https://.../video.mp4", "type": "video"},
    {"file": "https://.../doc.pdf", "type": "document"},
], caption="Album caption (first item only)")
```
{% endcode %}

{% code title="Mixed album with bytes" %}
```python
with open("photo.jpg", "rb") as f:
    photo_bytes = f.read()

bot.media(msg, [
    {"type": "photo", "media": photo_bytes},
    {"type": "video", "file": "https://.../video.mp4"},
])
```
{% endcode %}

## `bot.video`

{% code title="Signature" %}
```python
bot.video(target, video, caption: str = None, inline=None, keyboard=None, **kwargs)
```
{% endcode %}

{% code title="Example" %}
```python
bot.video(msg, "https://example.com/video.mp4", caption="My video")
```
{% endcode %}

## `bot.document`

{% code title="Signature" %}
```python
bot.document(target, doc, caption: str = None, inline=None, keyboard=None, **kwargs)
```
{% endcode %}

## `bot.audio`

{% code title="Signature" %}
```python
bot.audio(target, audio, caption: str = None, inline=None, keyboard=None, **kwargs)
```
{% endcode %}

## `bot.voice`

{% code title="Signature" %}
```python
bot.voice(target, voice, caption: str = None, inline=None, keyboard=None, **kwargs)
```
{% endcode %}

## `bot.animation`

{% code title="Signature" %}
```python
bot.animation(target, animation, caption: str = None, **kwargs)
```
{% endcode %}

## `bot.videoNote`

{% code title="Signature" %}
```python
bot.videoNote(target, videoNote, **kwargs)
```
{% endcode %}

## `bot.sticker`

{% code title="Signature" %}
```python
bot.sticker(target, sticker, **kwargs)
```
{% endcode %}

## Media sources

All media methods accept:

| Source    | Example                           |
| --------- | --------------------------------- |
| File ID   | `"AgACAgIAAxkB..."`               |
| URL       | `"https://example.com/image.jpg"` |
| File path | `open("image.jpg", "rb")`         |
| Bytes     | `bytes` or `bytearray`            |

## `bot.paidMedia`

Send paid media that users must purchase with Telegram Stars.

{% code title="Signature" %}
```python
bot.paidMedia(target, starCount: int, media: list, **kwargs)
```
{% endcode %}
