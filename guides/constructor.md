---
description: Bot lifecycle, middleware, and shutdown hooks.
---

# Lifecycle & Middleware

The `Gramly` class provides middleware layers, background timers, and lifecycle hooks.

{% code title="Bot lifecycle setup" %}
```python
from gramly import Gramly

bot = Gramly("TOKEN")

# Guards — run before every update
@bot.guard
def allow_only_private(raw: dict) -> bool:
    chat = raw.get("chat") or {}
    return chat.get("type") == "private"

# Interceptors — run after guards, before handlers
@bot.intercept
def log_everything(raw: dict):
    print(f"Update: {raw.get('update_id')}")

# Stop callback — runs when bot shuts down
@bot.onStop
def on_shutdown():
    print("Bot stopped")

bot.run()
```
{% endcode %}

### Guards & Interceptors

See: [Guards & Interceptors](guards-interceptors.md)

### Timers

See: [Timers](timers.md)
