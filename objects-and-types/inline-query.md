---
description: The InlineQuery object — inline mode queries.
icon: box-magnifying-glass
---

# InlineQuery

Passed to `@bot.onInline` handlers.

| Property      | Type          | Description                  |
| ------------- | ------------- | ---------------------------- |
| `q.id`        | `str`         | Inline query ID              |
| `q.query`     | `str`         | Raw query text               |
| `q.text`      | `str`         | Query text (stripped)        |
| `q.from_user` | `User`        | User who typed the query     |
| `q.user_id`   | `int \| None` | Shorthand for `from_user.id` |
| `q.offset`    | `str`         | Pagination offset            |

## Building results

{% code title="Signature" %}
```python
result = q.article(
    title       = "Title",
    text        = "Message content to send",
    description = "Optional subtitle shown below title",
    thumbUrl    = "https://example.com/thumb.jpg",
    resultId    = None,   # defaults to title when None
    # **kwargs passed through to Telegram
)
```
{% endcode %}

## Answering

{% code title="Signature" %}
```python
q.answer(results, cacheTime=30, personal=True)
# equivalent to: bot.answerInlineQuery(q, results, cacheTime=30, isPersonal=True)
```
{% endcode %}
