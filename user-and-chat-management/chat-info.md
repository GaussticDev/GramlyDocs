---
description: Get chat info, member status, admins, and boosts.
---

# Chat Info

{% code title="Signature" %}
```python
bot.getChat(target)                        # Get full chat info
bot.getChatMember(chatIdVal, userId)       # Get member status
bot.getChatMemberCount(chatIdVal)          # Get member count
bot.isAdmin(chatIdVal, userId)             # Check if admin
bot.getAdmins(chatIdVal, includeBots=False) # Get admin list
bot.getUserBoosts(chatIdVal, userId)       # Get user boosts
```
{% endcode %}

{% code title="Examples" %}
```python
chat = bot.getChat(msg)
print(chat.title, chat.type, chat.username)

member = bot.getChatMember(chat_id, user_id)
print(member.status)  # "member", "administrator", "creator", "left", "kicked"

count = bot.getChatMemberCount(chat_id)

if bot.isAdmin(chat_id, user_id):
    bot.send(chat_id, "You are an admin!")

admins = bot.getAdmins(chat_id)
for admin in admins:
    print(admin.user.id, admin.status)

boosts = bot.getUserBoosts(chat_id, user_id)
```
{% endcode %}
