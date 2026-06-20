---
description: Build your first Telegram bot in minutes.
icon: bolt
---

# Quickstart

### Installation

{% code title="Terminal" %}
```bash
pip install gramly
```
{% endcode %}

### Minimal bot

{% code title="main.py" %}
```python
from gramly import Gramly

bot = Gramly("YOUR_BOT_TOKEN")

@bot.onMessage(commands="start")
def on_start(msg):
    bot.send(msg, f"Hello {msg.from_user.first_name}! 👋")

bot.run()
```
{% endcode %}

### Bot with keyboard

{% code title="main.py" %}
```python
from gramly import Gramly, btn, row, kbd

bot = Gramly("YOUR_BOT_TOKEN")

@bot.onMessage(commands="start")
def on_start(msg):
    bot.send(msg, "Choose an option:", inline=kbd(
        row(btn("Profile", data=f"{msg.user_id}:profile")),
        row(btn("Settings", data=f"{msg.user_id}:settings")),
    ))

@bot.onCallback("profile")
def on_profile(cb):
    bot.alert(cb, "Your profile is safe!", popup=True)

@bot.onCallback("settings")
def on_settings(cb):
    bot.edit(cb, "Settings page")

bot.run()
```
{% endcode %}

### Bot with media

{% code title="main.py" %}
```python
from gramly import Gramly

bot = Gramly("YOUR_BOT_TOKEN")

# Send a photo
@bot.onMessage(commands="photo")
def send_photo(msg):
    bot.send(msg, "Here's a photo:", photo="https://example.com/image.jpg")

# Send a poll
@bot.onMessage(commands="poll")
def send_poll(msg):
    bot.poll(msg, "Favorite color?", ["Red", "Blue", "Green"])

bot.run()
```
{% endcode %}
