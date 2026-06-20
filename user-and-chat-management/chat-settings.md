---
description: Set chat title, description, photo, and sticker set.
---

# Chat Settings

{% code title="Signature" %}
```python
bot.setChatTitle(chatIdVal, title)
bot.setChatDescription(chatIdVal, description)
bot.setChatPhoto(chatIdVal, photo)
bot.deleteChatPhoto(chatIdVal)
bot.setChatStickerSet(chatIdVal, stickerSetName)
bot.deleteChatStickerSet(chatIdVal)
```
{% endcode %}

{% code title="Examples" %}
```python
bot.setChatTitle(chat_id, "New Group Name")
bot.setChatDescription(chat_id, "This is our group description")
bot.setChatPhoto(chat_id, "https://example.com/photo.jpg")
bot.deleteChatPhoto(chat_id)
bot.setChatStickerSet(chat_id, "my_sticker_set")
bot.deleteChatStickerSet(chat_id)
```
{% endcode %}
