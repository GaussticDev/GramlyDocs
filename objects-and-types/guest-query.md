---
description: The GuestQuery object — queries from users who haven't started the bot.
icon: user
---

# GuestQuery

Passed to `@bot.onGuest` handlers.

| Property    | Type          | Description    |
| ----------- | ------------- | -------------- |
| `.id`       | `str`         | Guest query ID |
| `.fromUser` | `User`        | Caller user    |
| `.fromChat` | `Chat`        | Caller chat    |
| `.user_id`  | `int \| None` | Caller user ID |
| `.text`     | `str \| None` | Query text     |

{% code title="Answer helper" %}
```python
q.answer("Hello!", parseMode="HTML")
# equivalent to: bot.answerGuestQuery(q.id, "Hello!", parseMode="HTML")
```
{% endcode %}
