---
description: The BusinessMessage object — business account messages.
---

# BusinessMessage

Passed to `@bot.onBusinessMessage` handlers.

| Property      | Type          | Description                                      |
| ------------- | ------------- | ------------------------------------------------ |
| `.bc_id`      | `str`         | Business connection ID                           |
| `.text`       | `str \| None` | Message text                                     |
| `.chat_id`    | `int`         | Chat ID                                          |
| `.message_id` | `int \| None` | Message ID                                       |
| `.from_user`  | `User`        | Sender                                           |
| `.chat`       | `Chat`        | Chat                                             |
| `.isOwner`    | `bool`        | True if the sender is the business account owner |

{% code title="Reply helper" %}
```python
msg.reply("Hello!")
# equivalent to: bot.businessSend(msg.chat_id, "Hello!", msg.bc_id)

msg.reply("Hello!", inline=kbd(row(btn("OK", data="123:ok"))))
```
{% endcode %}
