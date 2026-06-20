---
description: Send invoices and create invoice links for Telegram Stars.
icon: file-invoice
---

# Invoices

## `bot.invoice`

Send an invoice for Telegram Stars.

{% code title="Signature" %}
```python
bot.invoice(
    target,                            # who to send — chat_id, message
    title: str,                        # invoice title
    description: str,                  # short product description
    payload: str,                      # your internal identifier, returned after payment
    stars: int,                        # price in Stars, min: 10
    photoUrl: str = None,              # product image url
    inline=None,                       # buttons under invoice
    protectContent: bool = False,      # disable message forwarding
    **kwargs,                          # extra telegram api params
)
```
{% endcode %}

{% code title="Exemple" %}
```python
bot.invoice(msg, "Digital Art", "Beautiful artwork", "order_123", stars=10)

bot.invoice(msg, "PapaCofe", "☕ Arabica", "coffee_arabica", stars=150,
        photoUrl="coffee-arabica.jpg",
    )
```
{% endcode %}

## `bot.createInvoiceLink`

Create a reusable invoice link (no need to send a message).

{% code title="Signature" %}
```python
bot.createInvoiceLink(
    title: str,
    description: str,
    payload: str,
    stars: int,
    photoUrl: str = None,
    subscriptionPeriod: int = None,  # seconds for subscriptions
    **kwargs,
) -> str  # returns the invoice link
```
{% endcode %}

{% code title="Create link" %}
```python
link = bot.createInvoiceLink("Subscription", "Monthly sub", "sub_1", stars=50,
    subscriptionPeriod=2592000,  # 30 days
)
bot.send(msg, f"Subscribe: {link}")
```
{% endcode %}
