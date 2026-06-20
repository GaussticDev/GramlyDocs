---
description: The CallbackQuery object — inline button press data.
icon: eye
---

# CallbackQuery

Passed to `@bot.onCallback` handlers.

| Property            | Type           | Description                                         |
| ------------------- | -------------- | --------------------------------------------------- |
| `q.id`              | `str`          | Callback query ID                                   |
| `q.data`            | `str`          | Raw callback data string                            |
| `q.cb`              | `CallbackData` | Parsed callback data object                         |
| `q.from_user`       | `User`         | User who pressed the button                         |
| `q.user_id`         | `int \| None`  | Shorthand for `from_user.id`                        |
| `q.chat_id`         | `int`          | Chat ID of the message                              |
| `q.message_id`      | `int`          | ID of the message the button belongs to             |
| `q.message`         | `Obj`          | Full message object                                 |
| `q.isInline`        | `bool`         | True if this was an inline message button           |
| `q.inlineMessageId` | `str \| None`  | Inline message ID (only when `isInline` is True)    |
| `q.args`            | `list[str]`    | Extra parts of callback\_data after `owner:action:` |

Argument helpers from `ArgsMixin` also apply: `q.arg()`, `q.argInt()`, `q.argFloat()`, `q.has()`, `q.argsJoined()`.
