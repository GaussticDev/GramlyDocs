---
description: Create, edit, close, reopen, and manage forum topics.
icon: folder
---

# Forum Topics

## Topic management

{% code title="Signature" %}
```python
bot.createTopic(chatIdVal, name: str, **kwargs)
bot.editTopic(chatIdVal, messageThreadId, **kwargs)
bot.closeTopic(chatIdVal, messageThreadId)
bot.reopenTopic(chatIdVal, messageThreadId)
bot.deleteTopic(chatIdVal, messageThreadId)
bot.unpinTopicMessages(chatIdVal, messageThreadId)
```
{% endcode %}

{% code title="Examples" %}
```python
topic = bot.createTopic(chat_id, "General Discussion")
topic_id = topic.message_thread_id

bot.editTopic(chat_id, topic_id, name="New Name")
bot.closeTopic(chat_id, topic_id)
bot.reopenTopic(chat_id, topic_id)
bot.deleteTopic(chat_id, topic_id)
bot.unpinTopicMessages(chat_id, topic_id)
```
{% endcode %}

## General topic

{% code title="Signature" %}
```python
bot.editGeneralTopic(chatIdVal, name: str)
bot.closeGeneralTopic(chatIdVal)
bot.reopenGeneralTopic(chatIdVal)
bot.hideGeneralTopic(chatIdVal)
bot.unhideGeneralTopic(chatIdVal)
bot.unpinGeneralTopicMessages(chatIdVal)
```
{% endcode %}
