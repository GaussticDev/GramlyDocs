---
description: The Message object — properties, arguments, and helpers.
icon: message
---

# Message

Passed to all message-level handlers.

## Properties

| Property                  | Type               | Description                                         |
| ------------------------- | ------------------ | --------------------------------------------------- |
| `msg.message_id`          | `int`              | Unique message ID                                   |
| `msg.text`                | `str \| None`      | Message text or caption                             |
| `msg.chat_id`             | `int`              | Chat ID                                             |
| `msg.user_id`             | `int \| None`      | Sender user ID                                      |
| `msg.from_user`           | `User`             | Sender as `User` dataclass                          |
| `msg.chat`                | `Chat`             | Chat as `Chat` dataclass                            |
| `msg.chat_type`           | `str`              | `"private"`, `"group"`, `"supergroup"`, `"channel"` |
| `msg.isPrivate`           | `bool`             | Chat is a private conversation                      |
| `msg.isGroup`             | `bool`             | Chat is a group or supergroup                       |
| `msg.isChannel`           | `bool`             | Chat is a channel                                   |
| `msg.args`                | `list[str]`        | Words after the command / regex capture groups      |
| `msg.match`               | `re.Match \| None` | Regex match object (when `regex=` was used)         |
| `msg.replyTo`             | `Message \| None`  | Message being replied to                            |
| `msg.forwardFrom`         | `User \| None`     | Original sender of a forwarded message              |
| `msg.payment`             | `Payment \| None`  | Payment data on successful payment                  |
| `msg.webAppData`          | `Obj \| None`      | Data submitted from a Web App                       |
| `msg.userShared`          | `Obj \| None`      | User shared via keyboard button                     |
| `msg.chatShared`          | `Obj \| None`      | Chat shared via keyboard button                     |
| `msg.checklist`           | `Obj \| None`      | Checklist data                                      |
| `msg.checklistTasksAdded` | `Obj \| None`      | Tasks added to a checklist                          |
| `msg.livePhoto`           | `Obj \| None`      | Live photo data                                     |
| `msg.isGuest`             | `bool`             | True if this is a guest query message               |
| `msg.guestQueryId`        | `str \| None`      | Guest query ID                                      |
| `msg.guestCallerUser`     | `User \| None`     | User who initiated the guest query                  |
| `msg.guestCallerChat`     | `Chat \| None`     | Chat that initiated the guest query                 |

Any Telegram field not listed above is accessible as a dynamic attribute: `msg.photo`, `msg.document`, `msg.voice`, `msg.entities`, `msg.caption_entities`, etc.

## Argument helpers (`ArgsMixin`)

{% code title="Signature" %}
```python
msg.arg(0)                      # str  — first argument (safe, returns None if missing)
msg.arg(0, cast=int, default=0) # int  — cast to type, fallback to default
msg.argInt(0, default=None)     # int  — shorthand for arg(index, int)
msg.argFloat(0, default=None)   # float
msg.has(2)                      # bool — True if at least 2 arguments are present
msg.argsJoined(" ")             # str  — all arguments joined into one string
```
{% endcode %}
