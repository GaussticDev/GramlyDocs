---
description: Get started with Gramly — installation, quickstart, and configuration.
icon: rocket
---

# Overview

| Page                              | Description                                          |
| --------------------------------- | ---------------------------------------------------- |
| [Quickstart](quickstart.md)       | Create and run your first bot in minutes             |
| [Configuration](configuration.md) | Bot token, webhook vs polling, and advanced settings |

{% code title="Quick reference" %}
```python
from gramly import Gramly

bot = Gramly("YOUR_BOT_TOKEN")

@bot.command("start")
def on_start(msg):
    bot.send(msg, "Hello!")

bot.run()
```
{% endcode %}
