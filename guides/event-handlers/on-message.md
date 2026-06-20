---
description: Flexible text matching on incoming messages.
icon: message
---

# @bot.onMessage

Fires on incoming messages with flexible text matching.

{% code title="Signature" %}
```python
@bot.onMessage(
    commands        = None,    # str or list — "/start", "start", ["start", "go"]
    exact           = None,    # match full text exactly
    starts          = None,    # text starts with this string
    ends            = None,    # text ends with this string
    contains        = None,    # text contains this string
    regex           = None,    # str or compiled regex pattern
    withSlash       = True,    # accept "/command" form
    withoutSlash    = True,    # accept "command" form (no slash)
    argsMin         = None,    # int — minimum number of arguments required
    argsError       = None,    # str — message sent when argsMin not met
    guard           = None,    # callable(Message) → bool
    business        = False,   # handle business messages instead
)
def handler(msg: Message): ...
```
{% endcode %}

## Examples

{% code title="Command matching" %}
```python
# /start or start
@bot.onMessage(commands="start")
def on_start(msg):
    bot.send(msg, f"Hello {msg.from_user.first_name}!")

# Multiple commands
@bot.onMessage(commands=["help", "info"])
def on_help(msg):
    bot.send(msg, "Help text here")
```
{% endcode %}

{% code title="Text matching" %}
```python
# Exact text match
@bot.onMessage(exact="помощь")
def on_help_ru(msg):
    bot.send(msg, "Help text here")

# Starts with — args contain the remainder
@bot.onMessage(starts="find ")
def on_find(msg):
    query = msg.argsJoined()
    bot.send(msg, f"Searching for: {query}")

# Ends with
@bot.onMessage(ends=" please")
def on_polite(msg):
    bot.send(msg, "You said please!")

# Contains substring
@bot.onMessage(contains="discount")
def on_discount(msg):
    bot.send(msg, "Here's our discount page!")
```
{% endcode %}

{% code title="Regex matching" %}
```python
@bot.onMessage(regex=r"order #(\d+)")
def on_order(msg):
    order_id = msg.args[0]   # first capture group
    bot.send(msg, f"Order: {order_id}")
```
{% endcode %}

{% code title="Argument validation" %}
```python
# Require at least 1 argument
@bot.onMessage(commands="ban", argsMin=1, argsError="Usage: /ban <user_id>")
def on_ban(msg):
    user_id = msg.argInt(0)
    bot.ban(msg.chat_id, user_id)
```
{% endcode %}

{% code title="Per-handler guard" %}
```python
@bot.onMessage(commands="admin", guard=lambda msg: msg.user_id == 12345)
def on_admin(msg):
    bot.send(msg, "Admin panel")
```
{% endcode %}
