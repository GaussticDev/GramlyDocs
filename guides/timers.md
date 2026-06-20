---
description: Run functions on a repeating schedule in the background.
icon: clock
---

# Timers

Timers let you run functions periodically in a background thread. They integrate with the bot's event loop, so you can safely call `bot.*` methods from inside a timer function.

{% code title="Signature" %}
```python
bot.timer(
    seconds: float,          # Interval between executions
    fn: Callable,            # Function to call
    fireNow: bool = False,   # Call immediately on start
) -> TimerHandle
```
{% endcode %}

## Basic usage

{% code title="main.py" %}
```python
from gramly import Gramly

bot = Gramly("TOKEN")

def remind():
    bot.send(CHAT_ID, "⏰ Time's up!")

# Run every 60 seconds
handle = bot.timer(60.0, remind)

# Stop when needed
handle.stop()
```
{% endcode %}

## Fire immediately

{% code title="Fire now, then repeat" %}
```python
handle = bot.timer(300.0, backup_database, fireNow=True)
# Runs immediately, then every 5 minutes
```
{% endcode %}

## TimerHandle

| Method / Property | Description                         |
| ----------------- | ----------------------------------- |
| `handle.stop()`   | Stop the timer loop                 |
| `handle.stopped`  | `bool` — `True` if timer is stopped |

{% code title="Timer with commands" %}
```python
timer_handle = None

@bot.onMessage(commands="start_timer")
def start_timer(msg):
    global timer_handle
    timer_handle = bot.timer(10.0, lambda: bot.send(msg, "Tick!"))
    bot.send(msg, "Timer started!")

@bot.onMessage(commands="stop_timer")
def stop_timer(msg):
    if timer_handle:
        timer_handle.stop()
        bot.send(msg, "Timer stopped!")
```
{% endcode %}
