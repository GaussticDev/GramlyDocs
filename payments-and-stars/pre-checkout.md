---
description: Pre-checkout flow — accept or reject payments before they complete.
icon: star
---

# Pre-checkout

## `bot.onCheckout`

The pre-checkout step fires before a payment is charged. Use `@bot.onCheckout` to accept or reject it.

<table><thead><tr><th width="174.888916015625">Property</th><th width="120.111083984375">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>pco.id</code></td><td><code>str</code></td><td>Pre-checkout query ID</td></tr><tr><td><code>pco.fromUser</code></td><td><code>User</code></td><td>Buyer</td></tr><tr><td><code>pco.user_id</code></td><td><code>int | None</code></td><td>Buyer user ID</td></tr><tr><td><code>pco.currency</code></td><td><code>str</code></td><td>Currency code (e.g. <code>"XTR"</code> for Stars)</td></tr><tr><td><code>pco.totalAmount</code></td><td><code>int</code></td><td>Amount in smallest currency units</td></tr><tr><td><code>pco.payload</code></td><td><code>str</code></td><td>Invoice payload</td></tr></tbody></table>

{% code title="Handler" %}
```python
@bot.onCheckout
def on_checkout(pco: PreCheckout):
    if pco.totalAmount < 50:
        pco.reject("Minimum order is 50 stars")
    else:
        pco.accept()
```
{% endcode %}

```
pco.accept()              # approve — payment proceeds
pco.reject("reason")     # reject — reason shown to the user
```

{% code title="Exemple,   Invoice → pre-checkout → payment" %}
```python
##  bot.invoice()       → user sees the invoice
##   ↓ pressed Pay
##  @bot.onCheckout     → you validate, call pco.accept()
##   ↓ confirmed
##  @bot.onPayment()    → money charged, deliver the product

# ── 1. Send invoice ───────────────────────────────────────────────
@bot.onMessage("buy")
def buy(msg):
    bot.invoice(msg, "PapaCofe", "Arabica", "coffee_arabica", stars=150,
        photoUrl="coffee-arabica.jpg")

# ── 2. User pressed Pay — BEFORE charge ───────────────────────────
@bot.onCheckout
def checkout(pco):
    # pco.payload → "coffee_arabica"
    # pco.user_id → who is paying
    if is_banned(pco.user_id):
        pco.reject("You are banned")
        return
    pco.accept()  # ← without this the charge won't go through

# ── 3. Payment done — money charged ───────────────────────────────
@bot.onPayment()
def payment(msg):
    payload = msg.successful_payment.invoice_payload  # → "coffee_arabica"
    give_product(msg.from_user["id"], payload)
    bot.send(msg, "☕ Arabica is on its way!")
```
{% endcode %}

See [Payments](payments.md) for the full payment flow.
