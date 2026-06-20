---
description: The BusinessConnection object — business account connection.
icon: globe
---

# BusinessConnection

Passed to `@bot.onBusinessConnection` handlers.

| Property      | Type          | Description               |
| ------------- | ------------- | ------------------------- |
| `.id`         | `str`         | Connection ID             |
| `.user`       | `User`        | Business account owner    |
| `.userChatId` | `int \| None` | Owner's private chat ID   |
| `.date`       | `int`         | Unix timestamp            |
| `.isEnabled`  | `bool`        | Connection is active      |
| `.canReply`   | `bool`        | Bot has reply permissions |
| `.rights`     | `Obj`         | Full rights object        |
