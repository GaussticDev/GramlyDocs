---
description: TelegramError — exception raised on API failures.
icon: circle-exclamation
---

# TelegramError

Raised by all API calls on failure.

{% code title="Signature" %}
```python
try:
    bot.send(msg, "test")
except TelegramError as e:
    print(e.description)    # human-readable error message
    print(e.error_code)     # Telegram error code (int)
    print(e.retry_after)    # seconds to wait if HTTP 429, else None
```
{% endcode %}

Gramly automatically retries requests with a `retry_after` delay up to 3 times before re-raising.
