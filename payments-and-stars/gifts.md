---
description: Send, upgrade, convert, and transfer gifts.
icon: gift
---

# Gifts

{% code title="Signature" %}
```python
bot.getGifts()                              # Get available gifts
bot.gift(userId, giftId, payForUpgrade=False) # Send a gift
bot.giftPremium(userId)                     # Gift Premium subscription
bot.convertGiftToStars(giftId)              # Convert gift to Stars
bot.upgradeGift(giftId)                     # Upgrade a gift
bot.transferGift(giftId, userId)            # Transfer gift to user
```
{% endcode %}

{% code title="Example" %}
```python
gifts = bot.getGifts()
for g in gifts:
    print(g.id, g.title, g.stars)

# Send a gift
bot.gift(user_id, "gift_id_here")

# Send with upgrade
bot.gift(user_id, "gift_id", payForUpgrade=True)

# Convert to Stars
bot.convertGiftToStars("gift_id")
```
{% endcode %}
