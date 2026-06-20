---
description: Payment handlers — pre-checkout and successful payment.
icon: star
---

# Payments

## `@bot.onPayment`

Payment fires after a charge is confirmed. Use `@bot.onPayment()` to deliver the product.

<table><thead><tr><th width="318">Property</th><th width="120.1112060546875">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>msg.from_user</code></td><td><code>User</code></td><td>Buyer</td></tr><tr><td><code>msg.user_id</code></td><td><code>int</code></td><td>Buyer user ID</td></tr><tr><td><code>msg.payment.currency</code></td><td><code>str</code></td><td>Currency code, for example <code>"XTR"</code> for Stars</td></tr><tr><td><code>msg.payment.totalAmount</code></td><td><code>int</code></td><td>Amount in smallest currency units</td></tr><tr><td><code>msg.payment.stars</code></td><td><code>int | None</code></td><td>Stars amount, <code>None</code> if not Stars</td></tr><tr><td><code>msg.payment.payload</code></td><td><code>str</code></td><td>Invoice payload</td></tr><tr><td><code>msg.payment.chargeId</code></td><td><code>str</code></td><td>Telegram charge ID. Use it for refunds</td></tr><tr><td><code>msg.payment.providerChargeId</code></td><td><code>str</code></td><td>Provider charge ID</td></tr><tr><td><code>msg.payment.isRecurring</code></td><td><code>bool</code></td><td>Recurring subscription payment</td></tr><tr><td><code>msg.payment.isFirstRecurring</code></td><td><code>bool</code></td><td>First payment of a subscription</td></tr><tr><td><code>msg.payment.subscriptionExpiration</code></td><td><code>int | None</code></td><td>Subscription expiry as a Unix timestamp</td></tr></tbody></table>

{% code title="Handler" %}
```python
@bot.onPayment
def on_payment(msg: Message):
    p = msg.payment
    bot.send(msg, f"Thanks! Received {p.stars} ⭐  (charge: {p.chargeId})")
```
{% endcode %}



{% code title="Examples" %}
```python
@bot.onPayment()
def on_payment(msg):
    pay = msg.payment

    # basic
    print(pay.payload)        # "coffee_arabica"
    print(pay.stars)          # 150
    print(pay.chargeId)       # "12345678_123"
    print(msg.user_id)        # 123456789

    bot.send(msg, "✅ Payment received!")


# ── react by payload ──────────────────────────────────────────────
@bot.onPayment()
def on_payment(msg):
    pay = msg.payment

    if pay.payload == "coffee_arabica":
        give_product(msg.from_user["id"], payload)
        bot.send(msg, "☕ Arabica is on its way!")

    elif pay.payload == "vip_30d":
        grant_vip(msg.user_id, days=30)
        bot.send(msg, "✅ VIP activated for 30 days!")


# ── subscription ──────────────────────────────────────────────────
@bot.onPayment()
def on_payment(msg):
    pay = msg.payment

    if pay.isFirstRecurring:
        bot.send(msg, "🎉 Welcome! Subscription started.")
    elif pay.isRecurring:
        bot.send(msg, "🔄 Subscription renewed.")


# ── refund ────────────────────────────────────────────────────────
@bot.onPayment()
def on_payment(msg):
    pay = msg.payment

    if not can_deliver(pay.payload):
        bot.refund(msg.user_id, pay.chargeId)
        bot.send(msg, "❌ Out of stock. Refunded.")
        return

    deliver(msg.user_id, pay.payload)
    bot.send(msg, "✅ Done!")
```
{% endcode %}
