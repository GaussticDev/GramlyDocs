---
description: Convert button structures to Telegram keyboard markup.
icon: grid
---

# Keyboard Builders

These functions convert button structures (created with `btn()`, `row()`, `kbd()`) into the Telegram API `reply_markup` dict.

## `buildInlineKeyboard`

Converts inline button structures into Telegram's inline keyboard format.

{% code title="Signature" %}
```python
buildInlineKeyboard(rows) -> dict
```
{% endcode %}

{% code title="Usage with btn/row/kbd" %}
```python
from gramly import btn, row, kbd, buildInlineKeyboard

markup = buildInlineKeyboard(kbd(
    row(btn("Yes", data="123:yes"), btn("No", data="123:no")),
    row(btn("Cancel", data="123:cancel")),
))
# Result: {"inline_keyboard": [[...], [...]]}
```
{% endcode %}

{% code title="Direct usage" %}
```python
markup = buildInlineKeyboard([
    [{"text": "Button", "callback_data": "123:action"}],
])
```
{% endcode %}

## `buildReplyKeyboard`

Converts strings or dicts into Telegram's reply keyboard markup.

{% code title="Signature" %}
```python
buildReplyKeyboard(rows) -> dict
```
{% endcode %}

{% code title="With strings" %}
```python
markup = buildReplyKeyboard([
    ["Option A", "Option B"],
    ["Option C"],
])
# Result: {"keyboard": [[{"text": "Option A"}, ...]], "resize_keyboard": True}
```
{% endcode %}

{% code title="With dicts (request contact, location, etc.)" %}
```python
markup = buildReplyKeyboard([
    [{"text": "Send Contact", "request_contact": True}],
    [{"text": "Send Location", "request_location": True}],
])
```
{% endcode %}

{% code title="Remove reply keyboard" %}
```python
markup = buildReplyKeyboard(False)
# Result: {"remove_keyboard": True}
```
{% endcode %}

{% code title="Single string shortcut" %}
```python
markup = buildReplyKeyboard("Cancel")
# Result: {"keyboard": [[{"text": "Cancel"}]], "resize_keyboard": True}
```
{% endcode %}
