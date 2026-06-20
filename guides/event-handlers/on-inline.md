---
description: Handle inline queries — @botname query.
---

# @bot.onInline

Fires on inline queries (when the user types `@botname query`).

{% code title="Signature" %}
```python
@bot.onInline(minLength=0)   # minLength — ignore queries shorter than N chars
def on_inline(q: InlineQuery): ...
```
{% endcode %}

{% code title="Example" %}
```python
@bot.onInline(minLength=2)
def on_inline(q: InlineQuery):
    results = [
        q.article("Result 1", "Message content 1", description="Subtitle"),
        q.article("Result 2", "Message content 2"),
    ]
    q.answer(results, cacheTime=10)
```
{% endcode %}
