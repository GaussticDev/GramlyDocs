---
description: TimerHandle — control repeating background tasks.
icon: clock
---

# TimerHandle

Returned by `bot.timer(...)`.

{% code title="Signature" %}
```python
handle = bot.timer(60, my_fn)
handle.stop()       # stop the repeating timer
handle.stopped      # → bool — True once stopped
```
{% endcode %}
