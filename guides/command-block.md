---
description: Nested router — group a command with all its sub-routes and callbacks.
icon: command
---

# CommandBlock

`CommandBlock` groups a command with all its sub-routes and callback actions in one place. The block is triggered first and then routes internally.

{% code title="Signature" %}
```python
from gramly import Gramly, btn, row, kbd

@bot.command(
    "market",           # trigger word(s) — str or multiple positional args
    deny         = None,  # text to show when owner check fails in onCallback
    withSlash    = True,  # match /settings
    withoutSlash = True,  # match  settings (without slash)
    guard        = None,  # callable(Message) → bool
    argsMin      = None,  # int — min args for the block itself
    argsError    = None,  # str — message when argsMin not met
)
def market_cmd(cmd: CommandBlock):
    
    @cmd.default
    def show_menu(target):
        markup = kbd(
            row(btn("🍎 Food",      data=f"{target.user_id}:category:food")),
            row(btn("🧙‍♂️ Cookie", data=f"{target.user_id}:category:cookie")),
        )
        if isinstance(target, CallbackQuery):
            bot.edit(target, "🛒 <b>Welcome to the market!</b>", inline=markup)
        else:
            bot.send(target, "🛒 <b>Welcome to the market!</b>", inline=markup)
            
    ## Calling show_menu(q) edits the existing interface message instead of sending a new duplicate

    @cmd.onCallback("category", owner=True)
    def category_callback(q: CallbackQuery):
        category = q.cb.extra(0) 
            
        if category == "food":
            text = "🍎 <b>Food Department:</b>\n1. Bread — 5 coins\n2. Apple — 2 coins"
        elif category == "cookie":
            text = "🧙‍♂️ <b>Cookie:</b>\n1. Magic cookie - 125 coins\n2. Damage cookie - 165 coins"
        else:
            text = "This section is empty."
    
        bot.edit(q, text, inline=kbd(
            row(btn("🔙 Back", data=f"{q.user_id}:back_to_market"))
        ))
            
    @cmd.onCallback("back_to_market", owner=True)
    def back_market(q: CallbackQuery):
        show_menu(q)
            
    @cmd.on("promo", args=1, error="enter promo code")   ## /market promo [agrs]
    def market_promo(msg: Message):
        promo = msg.arg(0)
         if promo == "gramly": 
             bot.send(msg, f"Promo code: {promo} activate, bonus: 1000 coins!")
        else: bot.send(msg, f"No find promo")


### If you are creating an owner-only menu, don't set owner=True on every separate handler. Instead, define deny globally once inside @bot.command()
```
{% endcode %}

## `cmd.default` — fallback sub-handler

Receives the `Message` when no sub-route matched (or when no sub-args were provided at all).

{% code title="Signature" %}
```python
@cmd.default
def fallback(msg): ...
```
{% endcode %}

## `cmd.on` — text sub-route

{% code title="Signature" %}
```python
@cmd.on(
    *keys,           # exact text match keys (positional strings)
    exact    = None, # explicit exact match string
    starts   = None, # starts-with string
    ends     = None, # ends-with string
    contains = None, # contains string
    regex    = None, # regex pattern
    args     = None, # int — minimum argument count
    error    = None, # str — error message if args not met
    guard    = None, # callable(Message) → bool
)
def sub_handler(msg): ...
```
{% endcode %}

## `cmd.onCallback` — callback sub-route

{% code title="Signature" %}
```python
@cmd.onCallback(
    *actions,       # one or more action strings (second part of callback_data)
    owner = True,   # check that cb.owner matches the pressing user
    guard = None,   # callable(CallbackQuery) → bool
    args  = None,   # int — minimum number of extra parts required
    error = None,   # str — message sent when args not met
)
def cb_handler(q): ...
```
{% endcode %}
