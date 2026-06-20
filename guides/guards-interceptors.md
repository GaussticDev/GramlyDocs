---
description: Global middleware — filter and intercept every update.
icon: shield
---

# Guards & Interceptors

Guards and interceptors run on **every** update before any handler. They are useful for filtering, logging, analytics, or rate-limiting.

## Global guard

A guard receives the raw update `dict` and must return `True` to allow processing. If it returns `False`, the update is silently dropped.

{% code title="Signature" %}
```python
@bot.guard
def only_private(raw: dict) -> bool:
    return (raw.get("chat") or {}).get("type") == "private"

# Or as a method call:
bot.guard(my_guard_function)
```
{% endcode %}

{% code title="Multiple guards" %}
```python
bot.guard(is_allowed_user)
bot.guard(check_rate_limit)
```
{% endcode %}

## Global interceptor

Runs after guards pass, before any handler. Use for logging, analytics, or side effects.

{% code title="Signature" %}
```python
@bot.intercept
def log_message(raw: dict):
    uid = (raw.get("from") or {}).get("id")
    text = raw.get("text", "")
    print(f"[{uid}] {text}")

# Or as a method call:
bot.intercept(my_interceptor_function)
```
{% endcode %}

## Per-handler guard

Each handler can also have its own guard. See [onMessage](event-handlers/on-message.md#per-handler-guard).

## Stop callback

{% code title="onStop — runs when bot shuts down" %}
```python
@bot.onStop
def cleanup():
    print("Bot is shutting down")
```
{% endcode %}

## Execution order

```
raw update
    │
    ▼
bot.guard() 1 → True / False (drop)
    │
    ▼
bot.guard() 2 → True / False (drop)
    │
    ▼
bot.intercept()  (logging, side effects)
    │
    ▼
handler-specific guard
    │
    ▼
handler function
```
