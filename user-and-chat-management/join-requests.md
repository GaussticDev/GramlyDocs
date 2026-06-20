---
description: Approve, decline, and answer chat join requests.
icon: user-plus
---

# Join Requests

## Handling join requests

{% code title="Signature" %}
```python
bot.approveJoin(chatOrRq, userId: int = None)
bot.declineJoin(chatOrRq, userId: int = None)
```
{% endcode %}

{% code title="With JoinRequest object" %}
```python
@bot.onJoinRequest
def on_join(rq: JoinRequest):
    bot.approveJoin(rq)    # Accept
    # or
    bot.declineJoin(rq)    # Reject
```
{% endcode %}

{% code title="With chat + user IDs" %}
```python
bot.approveJoin(chat_id, user_id)
bot.declineJoin(chat_id, user_id)
```
{% endcode %}

## Answer join request query

{% code title="Signature" %}
```python
bot.answerJoinRequestQuery(chatIdVal, userId, queryId, result)
```
{% endcode %}

## Send join request web app

{% code title="Signature" %}
```python
bot.sendJoinRequestWebApp(chatIdVal, userId, webAppUrl, **kwargs)
```
{% endcode %}

## JoinRequest object

| Property        | Description                |
| --------------- | -------------------------- |
| `rq.user`       | User who requested to join |
| `rq.user_id`    | User ID                    |
| `rq.chat`       | Target chat                |
| `rq.chat_id`    | Chat ID                    |
| `rq.userChatId` | User's personal chat ID    |
| `rq.inviteLink` | Invite link used (if any)  |
| `rq.date`       | Request timestamp          |
