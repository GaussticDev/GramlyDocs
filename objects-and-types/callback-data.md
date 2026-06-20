---
description: Parsed callback_data — owner, action, extras.
icon: code
---

# CallbackData

Parses `callback_data` formatted as `"owner_id:action:extra1:extra2:..."`.

{% code title="Signature" %}
```python
cb = CallbackData("12345:buy:99:usd")

cb.raw          # "12345:buy:99:usd"
cb.parts        # ["12345", "buy", "99", "usd"]
cb.owner        # 12345  (int) — first part as int, or None if not numeric
cb.action       # "buy"  — second part (or first if only one part)
cb.get(0)       # "12345"  (str, any index)
cb.get(2)       # "99"     (str)
cb.get(2, int)  # 99       (int — cast with second argument)
cb.get(2, int, default=0)   # 99 or 0 on error
cb.extra(0)     # "99"   — shorthand for get(2 + index)
cb.extra(1)     # "usd"
cb[0]           # "12345"  (index access)
len(cb)         # 4
```
{% endcode %}
