---
description: Start polling, use webhooks, or handle updates manually.
icon: play
---

# Running the Bot

## Long polling (default)

Call `bot.run()` to start long polling. This blocks the main thread.

{% code title="Simple polling" %}
```python
from gramly import Gramly
bot = Gramly("TOKEN")
# ...
bot.run()  # starts polling, blocks forever
```
{% endcode %}

### Run parameters

{% code title="Signature" %}
```python
bot.run(
    skipPending: bool = False,
    pollTimeout: int = 20,
    allowedUpdates: list = None,
)
```
{% endcode %}

| Parameter        | Default | Description                                     |
| ---------------- | ------- | ----------------------------------------------- |
| `skipPending`    | `False` | Skip any pending updates from before startup    |
| `pollTimeout`    | `20`    | Long polling timeout (seconds)                  |
| `allowedUpdates` | `None`  | List of update types to receive (auto-detected) |

{% code title="Advanced polling" %}
```python
bot.run(
    skipPending=True,
    pollTimeout=30,
    allowedUpdates=["message", "callback_query"],
)
```
{% endcode %}

### Non-blocking start

If you need the bot to run alongside other tasks, use `bot.start()`:

{% code title="Non-blocking" %}
```python
bot.start()  # starts polling in background
# do other things...
bot.close()  # stop the bot
```
{% endcode %}

## Webhook mode

For production deployments, set a webhook and process updates from your web server.

{% code title="Webhook setup" %}
```python
# Configure webhook (do this once)
bot.setWebhook(
    url="https://yourdomain.com/webhook",
    secretToken="your-secret",
    maxConnections=40,
)
# Or delete it
bot.deleteWebhook(dropPending=True)

# In your web framework:
@app.post("/webhook")
async def handle_webhook(request):
    update = await request.json()
    bot.processUpdate(update)
```
{% endcode %}

{% code title="Webhook parameters" %}
```python
bot.setWebhook(
    url: str,                          # Webhook URL
    secretToken: str = None,           # Secret for verification
    allowedUpdates: list = None,       # Update types to receive
    maxConnections: int = None,        # Max simultaneous connections
    ipAddress: str = None,             # Fixed IP
    certificate=None,                  # Self-signed certificate
    dropPending: bool = False,         # Drop pending updates
)
```
{% endcode %}

## Polling algorithm

```
bot.run()
    │
    ▼
getMe() — verify token
    │
    ▼
(skipPending) — skip old updates
    │
    ▼
loop:
    getUpdates(offset, timeout, allowed_updates)
        │
        ▼
    for each update:
        processUpdate(update)  → dispatch to handlers
        offset = update_id + 1
    │
    ▼
    (on stop event) → _shutdown()
```
