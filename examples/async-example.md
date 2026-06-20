---
description: Complete async example bot.
icon: terminal
---

# Async Example

{% code title="main.py" %}
```python
import asyncio
from gramly import Gramly, btn, row

bot = Gramly("TOKEN")


@bot.onMessage(commands="start")
async def start(msg):
    await asyncio.sleep(0.1)           # await anything you like
    await bot.send(msg, "Hello!")      # await bot methods when inside async


@bot.onCallback("pay:", owner=True)
async def on_pay(q):
    await asyncio.sleep(0.5)
    await bot.edit(q, "Processing…")
    await bot.alert(q, "Done!", popup=True)


bot.run()
```
{% endcode %}

> **Rule reminder:** if you use `await` inside a handler, keep using `await` for all subsequent calls in that function. You are free to mix sync and async handlers in the same bot — each handler is independent.
