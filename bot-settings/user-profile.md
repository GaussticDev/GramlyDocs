---
description: Access user profile photos, audios, personal messages, and emoji status.
icon: user
---

# User Profile

{% code title="Quick reference" %}
```python
# Profile photos
bot.getUserPhotos(userId, offset=0, limit=100)

# Profile audios
bot.getUserAudios(userId, offset=0, limit=100)

# Personal messages
bot.getPersonalMessages(userId)

# Emoji status
bot.setEmojiStatus(userId, "custom_emoji_id")
bot.setEmojiStatus(userId)  # Clear status
```
{% endcode %}

## Methods

| Method                                     | Description                                      |
| ------------------------------------------ | ------------------------------------------------ |
| `bot.getUserPhotos(userId, offset, limit)` | Get profile photos of a user                     |
| `bot.getUserAudios(userId, offset, limit)` | Get profile audios of a user                     |
| `bot.getPersonalMessages(userId)`          | Get personal messages from a user                |
| `bot.setEmojiStatus(userId, emojiId)`      | Set or clear (call without emojiId) emoji status |

## Parameters

| Parameter | Type          | Description                       |
| --------- | ------------- | --------------------------------- |
| `userId`  | `int`         | Target user ID                    |
| `offset`  | `int`         | Pagination offset (default `0`)   |
| `limit`   | `int`         | Maximum results (default `100`)   |
| `emojiId` | `str \| None` | Custom emoji ID, or omit to clear |
