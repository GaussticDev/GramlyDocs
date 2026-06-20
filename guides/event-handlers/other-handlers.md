---
description: >-
  All remaining event handlers — media, edited, join, boost, reactions, and
  more.
---

# Other Handlers

## `@bot.onEdited`

Fires on edited messages and edited channel posts.

{% code title="Signature" %}
```python
@bot.onEdited(business: bool = False)
def handler(msg: Message): ...
```
{% endcode %}

## `@bot.onPost`

Fires on channel posts (messages sent to a channel).

{% code title="Signature" %}
```python
@bot.onPost
def handler(msg: Message): ...
```
{% endcode %}

## `@bot.onMedia`

Fires when a message contains specific media types.

{% code title="Signature" %}
```python
@bot.onMedia(*contentTypes)
def handler(msg: Message): ...
```
{% endcode %}

{% code title="Example" %}
```python
@bot.onMedia("photo")
def on_photo(msg: Message):
    bot.send(msg, "Nice photo!")

@bot.onMedia("photo", "video", "document")
def on_any_media(msg: Message):
    bot.send(msg, "You sent media!")
```
{% endcode %}

## `@bot.onAny`

Catch-all handler for messages not handled by any other handler. Skips messages already handled by `onMessage` or `CommandBlock`.

{% code title="Signature" %}
```python
@bot.onAny
def handler(msg: Message): ...
```
{% endcode %}

{% code title="Example" %}
```python
@bot.onAny
def fallback(msg: Message):
    bot.send(msg, "I don't understand that command.")
```
{% endcode %}

## `@bot.onCheckout`

Handles `PreCheckoutQuery` — the step before payment is confirmed. Accept or reject.

{% code title="Signature" %}
```python
@bot.onCheckout
def handler(q: PreCheckout):
    q.accept()           # Approve payment
    q.reject("reason")   # Reject with reason
```
{% endcode %}

## `@bot.onPayment`

Fires on messages containing `successful_payment`.

{% code title="Signature" %}
```python
@bot.onPayment
def handler(msg: Message):
    payment = msg.payment
    print(f"{payment.currency} {payment.totalAmount}")
```
{% endcode %}

## `@bot.onWebApp`

Fires when a user sends data from a Web App.

{% code title="Signature" %}
```python
@bot.onWebApp
def handler(msg: Message):
    data = msg.webAppData
```
{% endcode %}

## `@bot.onJoinRequest`

Fires when someone requests to join a chat (requires admin rights).

{% code title="Signature" %}
```python
@bot.onJoinRequest
def handler(rq: JoinRequest):
    bot.approveJoin(rq)    # Accept
    bot.declineJoin(rq)    # Reject
```
{% endcode %}

## `@bot.onMyStatus`

Fires when the bot's own member status changes in a chat.

## `@bot.onChatMember`

Fires when any chat member's status changes.

## `@bot.onReaction`

Fires when a message reaction is changed.

## `@bot.onPoll`

Fires when a user answers a poll (private chat only).

## `@bot.onBoost`

Fires on chat boosts and unboosts.

{% code title="Signature" %}
```python
@bot.onBoost
def handler(boost_data): ...
```
{% endcode %}

## `@bot.onPaidMedia`

Fires on purchased paid media.

## `@bot.onGuest`

Fires on guest messages — users interacting without starting the bot.

{% code title="Signature" %}
```python
@bot.onGuest
def handler(q: GuestQuery):
    q.answer(f"Hello {q.fromUser.first_name}!")
```
{% endcode %}

## `@bot.onManaged`

Fires on managed bot events.

## `@bot.onBusinessConnection`

Fires on business connection updates.

## `@bot.onBusinessDeleted`

Fires when business messages are deleted.
