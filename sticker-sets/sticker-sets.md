---
description: Create, edit, and manage sticker sets.
icon: file-image
---

# Overview

{% code title="Quick reference" %}
```python
# Get info
bot.getStickerSet("name")                          # Get sticker set
bot.getCustomEmojiStickers(["emoji_ids"])           # Get custom emoji stickers

# Create & add
bot.uploadStickerFile(userId, sticker, "static")   # Upload sticker file
bot.createNewStickerSet(userId, "name", "Title", stickers)
bot.addStickerToSet(userId, "name", sticker)        # Add sticker to set

# Edit stickers
bot.setStickerPosition("sticker", position)         # Reorder
bot.deleteStickerFromSet("sticker")                 # Remove
bot.replaceStickerInSet(userId, "name", "old", new) # Replace
bot.setStickerEmojiList("sticker", ["😀"])          # Set emoji list
bot.setStickerKeywords("sticker", ["keyword"])      # Set keywords
bot.setStickerMaskPosition("sticker", mask)         # Set mask position

# Edit set
bot.setStickerSetTitle("name", "New Title")         # Set title
bot.setStickerSetThumbnail("name", userId)           # Set thumbnail
bot.setCustomEmojiStickerSetThumbnail("name", "emoji_id")
bot.deleteStickerSet("name")                         # Delete set

# Chat sticker set
bot.setChatStickerSet(chatId, "set_name")
bot.deleteChatStickerSet(chatId)
```
{% endcode %}
