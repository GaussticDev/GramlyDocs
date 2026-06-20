---
description: Build inline and reply keyboards — button builders and layout helpers.
icon: bars
---

# Keyboards

Gramly provides a complete set of tools for building Telegram keyboards.

## Quick comparison

| Approach                               | Example                        | Use case                               |
| -------------------------------------- | ------------------------------ | -------------------------------------- |
| [`btn()`](btn.md)                      | `btn("Click", data="x")`       | Universal button builder               |
| Named constructors                     | `callbackButton("Click", "x")` | Explicit individual buttons            |
| [`row()` / `kbd()`](layout.md)         | `row(btn(...)), kbd(row(...))` | Layout helpers                         |
| [`buildInlineKeyboard()`](builders.md) | `buildInlineKeyboard(rows)`    | Convert btn objects to Telegram format |
| [`buildReplyKeyboard()`](builders.md)  | `buildReplyKeyboard(rows)`     | Build reply keyboards                  |

## Pages

| Page                                                      | Description                                           |
| --------------------------------------------------------- | ----------------------------------------------------- |
| [`btn()`](btn.md)                                         | Universal button builder — one function for all types |
| [`row()` / `kbd()`](layout.md)                            | Layout helpers for arranging buttons                  |
| [Button Constructors](/broken/pages/nPINBUld5XUm4XobPC8q) | Individual named button constructors                  |
| [Keyboard Builders](builders.md)                          | `buildInlineKeyboard` and `buildReplyKeyboard`        |

{% code title="Common pattern" %}
```python
from gramly import Gramly, btn, row, kbd

bot = Gramly("TOKEN")

@bot.onMessage(commands="menu")
def menu(msg):
    bot.send(msg, "Menu:", inline=kbd(
        row(btn("Open", url="https://example.com")),
        row(btn("Callback", data=f"{msg.user_id}:action")),
        row(btn("Pay", pay=True)),
    ))
```
{% endcode %}
