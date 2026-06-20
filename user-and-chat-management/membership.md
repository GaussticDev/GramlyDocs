---
description: Ban, kick, mute, restrict, promote, and manage sender bans.
icon: lock
---

# Membership & Moderation

## `bot.ban`

Ban a user from a chat.

{% code title="Signature" %}
```python
bot.ban(chatIdVal: int, userId: int, until: int = 0, revokeMessages: bool = False)
```
{% endcode %}

{% code title="Examples" %}
```python
bot.ban(chat_id, user_id)                # Permanent ban
bot.ban(chat_id, user_id, until=1700000000)  # Temporary ban
bot.ban(chat_id, user_id, revokeMessages=True)  # Delete all messages
```
{% endcode %}

## `bot.unban`

{% code title="Signature" %}
```python
bot.unban(chatIdVal: int, userId: int)
```
{% endcode %}

## `bot.kick`

Ban then immediately unban (temporary kick).

{% code title="Signature" %}
```python
bot.kick(chatIdVal: int, userId: int)
```
{% endcode %}

## `bot.mute`

Restrict a user from sending messages.

{% code title="Signature" %}
```python
bot.mute(chatIdVal: int, userId: int, until: int = 0)
```
{% endcode %}

## `bot.unmute`

{% code title="Signature" %}
```python
bot.unmute(chatIdVal: int, userId: int)
```
{% endcode %}

## `bot.restrict`

Apply custom permissions to a user.

{% code title="Signature" %}
```python
bot.restrict(chatIdVal: int, userId: int, permissions: dict, until: int = 0)
```
{% endcode %}

{% code title="Custom permissions example" %}
```python
bot.restrict(chat_id, user_id, {
    "can_send_messages": True,
    "can_send_media_messages": False,
    "can_send_polls": False,
})
```
{% endcode %}

## `bot.promote`

Promote a user to admin with specific permissions.

{% code title="Signature" %}
```python
bot.promote(chatIdVal: int, userId: int, **permissions)
```
{% endcode %}

{% code title="Example" %}
```python
bot.promote(chat_id, user_id,
    can_change_info=True,
    can_delete_messages=True,
    can_invite_users=True,
    can_pin_messages=True,
    can_restrict_members=True,
    can_promote_members=False,
    can_manage_chat=True,
    can_manage_video_chats=True,
    can_post_stories=True,
    can_edit_stories=True,
    can_delete_stories=True,
    can_post_messages=True,
    can_edit_messages=True,
    can_manage_topics=True,
)
```
{% endcode %}

## `bot.setAdminTitle`

Set a custom title for an admin.

{% code title="Signature" %}
```python
bot.setAdminTitle(chatIdVal: int, userId: int, title: str)
```
{% endcode %}

## `bot.setMemberTag`

Set a member tag.

{% code title="Signature" %}
```python
bot.setMemberTag(chatIdVal: int, userId: int, tag: str)
```
{% endcode %}

## `bot.setChatPermissions`

Set default chat permissions for all members.

{% code title="Signature" %}
```python
bot.setChatPermissions(chatIdVal: int, permissions: dict)
```
{% endcode %}

## Sender bans

{% code title="Ban/unban sender chat" %}
```python
bot.banSender(chatIdVal, senderChatId)      # Ban a channel from posting
bot.unbanSender(chatIdVal, senderChatId)    # Unban a channel
```
{% endcode %}
