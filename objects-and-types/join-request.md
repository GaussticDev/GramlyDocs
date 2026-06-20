---
description: The JoinRequest object — chat join requests.
icon: user-plus
---

# JoinRequest

Passed to `@bot.onJoinRequest` handlers.

| Property              | Type          | Description                      |
| --------------------- | ------------- | -------------------------------- |
| `.user` / `.fromUser` | `User`        | Requesting user                  |
| `.user_id`            | `int \| None` | User ID                          |
| `.chat`               | `Chat`        | The chat being joined            |
| `.chat_id`            | `int`         | Chat ID                          |
| `.userChatId`         | `int \| None` | User's private chat ID (for DMs) |
| `.inviteLink`         | `Obj \| None` | Invite link used                 |
| `.date`               | `int \| None` | Unix timestamp of the request    |
