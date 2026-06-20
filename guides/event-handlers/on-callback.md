---
description: Handle inline keyboard button presses.
icon: eye
---

# @bot.onCallback

Fires on inline keyboard button presses.

{% code title="Signature" %}
```python
@bot.onCallback(
    *prefixes,         # optional — only fire if callback_data starts with this prefix
    owner    = True,   # check that pressing user matches message owner (from parts[0])
    ownerPos = None,   # int — read owner ID from a different position in callback_data
    deny     = None,   # callable(CallbackQuery) — called when owner check fails
    guard    = None,   # callable(CallbackQuery) → bool
)
def handler(q: CallbackQuery): ...
```
{% endcode %}

## Examples

{% code title="Basic callback with prefix" %}
```python
@bot.onCallback("buy:")
def on_buy(q: CallbackQuery):
    product_id = q.cb.extra(0)   # third part: "user_id:buy:product_123"
    bot.edit(q, f"Buying product {product_id}")
    bot.ack(q)
```
{% endcode %}

{% code title="Owner check" %}
```python
# Only the user who received the message can press
@bot.onCallback("menu:", owner=True, deny=lambda q: bot.alert(q, "Not your button!", popup=True))
def on_menu(q: CallbackQuery):
    bot.edit(q, "Menu opened")
    bot.ack(q)
```
{% endcode %}

{% code title="No prefix — handle all callbacks" %}
```python
@bot.onCallback()
def all_callbacks(q: CallbackQuery):
    print(f"Callback: {q.data}")
    bot.ack(q)
```
{% endcode %}

{% code title="Custom owner position" %}
```python
# Callback data format: "action:owner_id:extra"
@bot.onCallback("edit:", ownerPos=1)
def on_edit(q: CallbackQuery):
    bot.edit(q, "Edited!")
    bot.ack(q)
```
{% endcode %}

{% code title="Per-handler guard" %}
```python
@bot.onCallback("admin:", guard=lambda q: q.user_id in ADMIN_IDS)
def on_admin(q: CallbackQuery):
    bot.edit(q, "Admin panel")
    bot.ack(q)
```
{% endcode %}

## CallbackQuery object

The handler receives a [`CallbackQuery`](../../objects-and-types/callback-query.md) object with:

| Property                  | Description                        |
| ------------------------- | ---------------------------------- |
| `q.id`                    | Callback query ID                  |
| `q.data`                  | Raw callback\_data string          |
| `q.cb`                    | Parsed `CallbackData` object       |
| `q.cb.owner`              | Owner ID (first part)              |
| `q.cb.action`             | Action (second part)               |
| `q.cb.extra(n)`           | Extra data (nth part after action) |
| `q.from_user`             | `User` who pressed the button      |
| `q.chat_id` / `q.user_id` | IDs                                |
| `q.message`               | Associated message (as `Obj`)      |
| `q.isInline`              | True if inline message             |
| `q.inlineMessageId`       | Inline message ID                  |

## Responding

| Method                             | Description                  |
| ---------------------------------- | ---------------------------- |
| `bot.ack(q)`                       | Acknowledge with no feedback |
| `bot.alert(q, "text")`             | Show a toast notification    |
| `bot.alert(q, "text", popup=True)` | Show an alert popup          |
| `bot.edit(q, "new text")`          | Edit the message             |
| `bot.editMarkup(q, new_inline)`    | Edit only the keyboard       |
