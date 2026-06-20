---
description: Manage bot profile, commands, menu button, and default admin rights.
icon: gear
---

# Overview

Configure your bot's identity, commands, menu button, and default rights.

{% code title="Quick reference" %}
```python
# Bot info
bot.getMe()                          # Get bot info
bot.getFile("file_id")               # Get file info
bot.getWebhookInfo()                 # Get webhook status

# Bot profile
bot.setMyName("My Bot")              # Set bot name
bot.getMyName()                      # Get bot name
bot.setMyDescription("A cool bot")   # Set description
bot.getMyDescription()               # Get description
bot.setMyShortDescription("Cool")    # Set short description
bot.getMyShortDescription()          # Get short description

# Profile photo
bot.setMyProfilePhoto(photo)         # Set profile photo
bot.removeMyProfilePhoto(emojiId)    # Remove profile photo

# Commands
bot.setMyCommands([{"command": "start", "description": "Start"}])
bot.getMyCommands()
bot.deleteMyCommands()

# Menu button
bot.setMenuButton(chatId, {"type": "commands"})
bot.getMenuButton(chatId)

# Admin rights
bot.setDefaultAdminRights(rights)
bot.getDefaultAdminRights()

# Advanced
bot.logOut()                         # Log out from Bot API
bot.closeBot()                       # Close the bot instance
bot.getAccessSettings()              # Managed bot access
bot.setAccessSettings(settings)      # Set managed bot access
bot.getManagedToken()                # Get managed bot token
bot.replaceManagedToken()            # Replace managed bot token
```
{% endcode %}
