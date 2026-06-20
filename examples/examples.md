---
description: Complete, ready-to-run example bots.
icon: code
---

# Complete Example

| Example                              | Description                           |
| ------------------------------------ | ------------------------------------- |
| [Complete Example](async-example.md) | Full async bot with multiple features |

{% code title="Minimal synchronous bot" %}
```python
from gramly import Gramly

bot = Gramly("YOUR_BOT_TOKEN")

@bot.onMessage(commands="start")
def start(msg):
    bot.send(msg, f"Hello, {msg.from_user.first_name}!")

bot.run()
```
{% endcode %}

{% code title="Bot with commands and callbacks" %}
```python
from gramly import Gramly, btn, row, kbd

bot = Gramly("YOUR_BOT_TOKEN")

@bot.onMessage(commands="start")
def start(msg):
    bot.send(msg, "Welcome!", inline=kbd(
        row(btn("Click me", data=f"{msg.user_id}:hello")),
    ))

@bot.onCallback("hello")
def hello_cb(cb):
    bot.alert(cb, "Hello! 👋", popup=True)

bot.run()
```
{% endcode %}

{% code title="Bot with CommandBlock" %}
```python
from gramly import Gramly, btn, row, kbd

bot = Gramly("YOUR_BOT_TOKEN")

@bot.command("calc")
def calculator(cmd):

    @cmd.default
    def _(msg):
        bot.send(msg, "Usage: /calc add 5 3")

    @cmd.on(regex=r"(add|sub|mul|div) (\d+) (\d+)")
    def _(msg):
        op, a, b = msg.args[0], int(msg.args[1]), int(msg.args[2])
        results = {"add": a+b, "sub": a-b, "mul": a*b, "div": a//b if b else 0}
        bot.send(msg, f"{a} {op} {b} = {results[op]}")

bot.run()
```
{% endcode %}
