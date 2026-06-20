---
description: Location, venue, contact, dice, poll, game, checklist, and more.
icon: message-captions
---

# Special Content

## `bot.location`

{% code title="Signature" %}
```python
bot.location(target, latitude: float, longitude: float, **kwargs)
```
{% endcode %}

## `bot.venue`

{% code title="Signature" %}
```python
bot.venue(target, latitude: float, longitude: float, title: str, address: str, **kwargs)
```
{% endcode %}

## `bot.contact`

{% code title="Signature" %}
```python
bot.contact(target, phone: str, firstName: str, lastName: str = None, **kwargs)
```
{% endcode %}

## `bot.poll`

Create and send a poll.

{% code title="Signature" %}
```python
bot.poll(
    target,
    question: str,
    options: list,                    # list of str or dict
    isAnonymous: bool = True,
    pollType: str = "regular",       # "regular" or "quiz"
    correctOptionIds: list = None,
    explanation: str = None,         # quiz explanation
    allowsMultipleAnswers: bool = False,
    allowsRevoting: bool = None,
    shuffleOptions: bool = None,
    allowAddingOptions: bool = None,
    hideResultsUntilCloses: bool = None,
    description: str = None,
    openPeriod: int = None,
    closeDate: int = None,
    membersOnly: bool = None,
    countryCodes: list = None,
    **kwargs,
)
```
{% endcode %}

{% code title="Regular poll" %}
```python
bot.poll(msg, "Favorite color?", ["Red", "Blue", "Green"])
```
{% endcode %}

{% code title="Quiz" %}
```python
bot.poll(msg, "What is 2+2?", ["3", "4", "5"],
    pollType="quiz", correctOptionIds=[1], explanation="Basic math!")
```
{% endcode %}

## `bot.stopPoll`

{% code title="Signature" %}
```python
bot.stopPoll(chatIdVal: int, messageId: int, **kwargs)
```
{% endcode %}

## `bot.dice`

Send a dice with optional emoji.

{% code title="Signature" %}
```python
bot.dice(target, emoji: str = "🎲", **kwargs)
```
{% endcode %}

{% code title="Dice emojis" %}
```python
bot.dice(msg)                       # 🎲 random 1-6
bot.dice(msg, "🎯")                # 🎯 random 1-6
bot.dice(msg, "🏀")               # 🏀 random 1-5
bot.dice(msg, "⚽")               # ⚽ random 1-5
bot.dice(msg, "🎰")               # 🎰 random 1-64
```
{% endcode %}

## `bot.game`

{% code title="Signature" %}
```python
bot.game(target, gameShortName: str, inline=None, keyboard=None, **kwargs)
```
{% endcode %}

## `bot.livePhoto`

{% code title="Signature" %}
```python
bot.livePhoto(target, photo, animation, caption: str = None, inline=None, keyboard=None, **kwargs)
```
{% endcode %}

## Checklist

{% code title="Send checklist" %}
```python
bot.checklist(target, "Shopping", [
    {"text": "Milk", "finished": False},
    {"text": "Bread", "finished": True},
])
```
{% endcode %}

{% code title="Edit checklist" %}
```python
bot.editChecklist(chat_id, message_id, "Updated", [
    {"text": "Milk", "finished": True},
])
```
{% endcode %}

## Message drafts

{% code title="Send message drafts" %}
```python
bot.messageDraft(target, "Draft text")
bot.richMessage(target, rich_message_data)
bot.richMessageDraft(target, rich_message_data)
```
{% endcode %}
