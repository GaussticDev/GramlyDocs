---
description: Generic Telegram object wrapper for dynamic fields.
icon: code
---

# Obj

All Telegram objects not wrapped in a dedicated dataclass are returned as `Obj`. Supports attribute access, dict-like access, and iteration.

{% code title="Signature" %}
```python
msg = Obj({"id": 1, "text": "hi", "from": {"id": 42, "first_name": "Alice"}})

msg.id            # 1
msg.text          # "hi"
msg.from_         # Obj({"id": 42, "first_name": "Alice"})
msg["id"]         # 1  (dict-style)
"text" in msg     # True
list(msg.keys())  # ["id", "text", "from"]
list(msg.items()) # [("id", 1), ("text", "hi"), ("from", {...})]
len(msg)          # 3
```
{% endcode %}

Nested dicts are automatically wrapped as nested `Obj` instances, and lists of dicts become lists of `Obj`.
