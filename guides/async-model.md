---
description: How Gramly's async model works — sync and async handlers side by side.
icon: arrow-right
---

# Async Model

Gramly runs a **single asyncio event loop** under the hood.\
**You never have to write `async` or `await` yourself** — every handler, whether it is a plain function or a coroutine, is dispatched through the same pipeline automatically.

## Plain (sync) handler — recommended for most bots

{% code title="main.py" %}
```python
from gramly import Gramly

bot = Gramly("TOKEN")

@bot.onMessage(commands="start")
def start(msg):
    bot.send(msg, "Hello!")   # no await needed

bot.run()
```
{% endcode %}

Gramly wraps the plain function in `asyncio.to_thread`, so it runs in a thread pool without blocking the event loop. All `bot.*` methods detect the sync context and return the result directly.

## Async handler — use when you need to `await` something

{% code title="main.py" %}
```python
import asyncio
from gramly import Gramly

bot = Gramly("TOKEN")

@bot.onMessage(commands="start")
async def start(msg):
    await asyncio.sleep(1)          # perfectly fine — already in a coroutine
    await bot.send(msg, "Hello!")   # calling bot methods with await is also fine

bot.run()
```
{% endcode %}

> **Rule:** once you use `await` anywhere inside a function, keep using `await` for every call inside it. Mixing sync and async calls inside the same handler works but is harder to reason about.

## Why both styles work

```
handler called
     │
     ▼
bot._wrap(fn, *args)
     │
     ├─ asyncio.iscoroutinefunction(fn)?  YES → await fn(*args)
     │
     └─ NO → await asyncio.to_thread(fn, *args)   # runs in thread pool
```

`bot.send(...)`, `bot.edit(...)` and every other method on `Gramly` detect whether they are being called from inside an async context:

* **Inside an `async` function** → they return a coroutine you can `await`.
* **Outside (plain sync handler)** → they block until the API call resolves and return the result directly.

The same method call works correctly in both handler styles without any changes.
