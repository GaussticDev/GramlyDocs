---
description: Edit, replace, and manage inline keyboard markup.
icon: message-pen
---

# Edit & Replace

## `bot.edit`

Edit a message's text, caption, or media.

{% code title="Signature" %}
```python
bot.edit(
    call,          # Message, CallbackQuery, or dict
    text: str,
    inline=None,   # new inline keyboard
    photo=None,    # swap to photo (edits media)
    **kwargs,
)
```
{% endcode %}

{% code title="Edit text" %}
```python
bot.edit(msg, "Updated text!")
```
{% endcode %}

{% code title="Edit with new inline keyboard" %}
```python
bot.edit(cb, "New menu", inline=kbd(
    row(btn("Option 1", data=f"{uid}:opt1")),
))
```
{% endcode %}

{% code title="Edit caption (photo message)" %}
```python
bot.edit(msg, "New caption")  # auto-detects photo → uses editMessageCaption
```
{% endcode %}

{% code title="Edit media with photo" %}
```python
bot.edit(msg, "New photo", photo="https://example.com/new.jpg")
```
{% endcode %}

## `bot.editMarkup`

Edit only the inline keyboard without changing the message content.

{% code title="Signature" %}
```python
bot.editMarkup(call, inline=None)
```
{% endcode %}

{% code title="Remove keyboard" %}
```python
bot.editMarkup(cb, [])  # removes all inline buttons
```
{% endcode %}

## `bot.replace`

Replace a message — uses `editMessageText` when possible, falls back to `deleteMessage` + `sendMessage` for photo messages.

{% code title="Signature" %}
```python
bot.replace(
    call,
    text: str,
    inline=None,
    photo=None,   # forces delete + send
    **kwargs,
)
```
{% endcode %}

{% code title="Replace photo message" %}
```python
bot.replace(msg, "Replaced with text")  # deletes photo msg, sends text
```
{% endcode %}

## Live location editing

{% code title="Update live location" %}
```python
bot.editLiveLocation(call, 55.75, 37.62)  # new lat, lng
```
{% endcode %}

{% code title="Stop live location" %}
```python
bot.stopLiveLocation(call)
```
{% endcode %}
