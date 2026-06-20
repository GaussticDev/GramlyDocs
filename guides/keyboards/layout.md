---
description: Row, keyboard builder, and markup converters.
icon: list
---

# Layout Helpers

## `row` / `kbd`

{% code title="Signature" %}
```python
row(*buttons)    # creates one row from multiple buttons
kbd(*rows)       # combines rows into a keyboard structure

# Usage:
inline = kbd(
    row(btn("Yes", data=f"{uid}:yes"), btn("No", data=f"{uid}:no")),
    row(btn("Cancel", data=f"{uid}:cancel")),
)
bot.send(msg, "Are you sure?", inline=inline)
```
{% endcode %}

## `buildInlineKeyboard`

Converts a `kbd(...)` structure (or a raw list of lists) into the Telegram `reply_markup` dict.

{% code title="Signature" %}
```python
markup = buildInlineKeyboard(
    kbd(
        row(btn("Yes", data="123:yes"), btn("No", data="123:no")),
    )
)
```
{% endcode %}

## `buildReplyKeyboard`

Converts rows of strings or dicts into a reply keyboard markup.

{% code title="Signature" %}
```python
markup = buildReplyKeyboard([
    ["Option A", "Option B"],
    ["Option C"],
])

# Remove keyboard
markup = buildReplyKeyboard(False)
```
{% endcode %}
