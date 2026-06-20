---
description: Create, edit, and revoke invite links and subscription invites.
icon: link
---

# Invite Links

## Regular invite links

{% code title="Signature" %}
```python
bot.exportInvite(chatIdVal)                        # Get primary invite link
bot.createInvite(chatIdVal, **kwargs)              # Create new invite link
bot.editInvite(chatIdVal, inviteLink, **kwargs)    # Edit invite link
bot.revokeInvite(chatIdVal, inviteLink)            # Revoke invite link
```
{% endcode %}

{% code title="Create invite link with options" %}
```python
bot.createInvite(chat_id,
    name="Welcome link",
    expire_date=1700000000,
    member_limit=10,
    creates_join_request=True,
)
```
{% endcode %}

## Subscription invite links

{% code title="Signature" %}
```python
bot.createSubscriptionInvite(
    chatIdVal,
    subscriptionPeriod: int,    # seconds
    subscriptionPrice: int,     # Telegram Stars
    **kwargs,
)
bot.editSubscriptionInvite(chatIdVal, inviteLink, **kwargs)
```
{% endcode %}

{% code title="Example" %}
```python
link = bot.createSubscriptionInvite(chat_id,
    subscriptionPeriod=2592000,    # 30 days
    subscriptionPrice=100,         # 100 Stars
    name="Monthly subscription",
)
```
{% endcode %}
