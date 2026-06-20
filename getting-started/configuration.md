---
description: Create and configure a Gramly bot instance.
icon: gears
---

# Configuration

Create a bot instance by passing your Telegram bot token to `Gramly()`.

{% code title="Signature" %}
```python
Gramly(
    token: str,
    msgCooldown: float = 0.35,
    inlineCooldown: float = 0.5,
    connectTimeout: int = 10,
    readTimeout: int = 30,
    locksMaxsize: int = 10000,
    parseMode: str = "HTML",
    debug: bool = False,
)
```
{% endcode %}

## Parameters

| Name             | Type    | Default  | Description                                                  |
| ---------------- | ------- | -------- | ------------------------------------------------------------ |
| `token`          | `str`   | required | Telegram bot token from [@BotFather](https://t.me/BotFather) |
| `msgCooldown`    | `float` | `0.35`   | Minimum seconds between message updates from the same user   |
| `inlineCooldown` | `float` | `0.5`    | Minimum seconds between inline queries from the same user    |
| `connectTimeout` | `int`   | `10`     | Seconds to wait when connecting to Telegram                  |
| `readTimeout`    | `int`   | `30`     | Seconds to wait for a response from Telegram                 |
| `locksMaxsize`   | `int`   | `10000`  | Max users stored in LRU cooldown cache                       |
| `parseMode`      | `str`   | `"HTML"` | Default parse mode — `"HTML"` or `"MarkdownV2"`              |
| `debug`          | `bool`  | `False`  | Enable verbose debug logging                                 |

## Example

{% code title="main.py" %}
```python
from gramly import Gramly

bot = Gramly(
    token="YOUR_BOT_TOKEN",
    parseMode="HTML",
    debug=True,
)

@bot.onMessage(commands="start")
def on_start(msg):
    bot.send(msg, "Hello!")

bot.run()
```
{% endcode %}

## Properties

| Property         | Type   | Description                               |
| ---------------- | ------ | ----------------------------------------- |
| `bot.parse_mode` | `str`  | Current parse mode (defaults to `"HTML"`) |
| `bot.debug`      | `bool` | Whether debug logging is enabled          |

## Version info

<pre class="language-python" data-title=""><code class="lang-python">from gramly import __version__, __bot_api_version__
<strong>
</strong>print(__version__)      # "1.2.4"
print(__bot_api_version__)  # "10.1"
</code></pre>
