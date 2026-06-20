---
description: Full Telegram Business Mode support — connect, message, and manage.
icon: briefcase
---

# Overview

Gramly provides full support for Telegram Business Mode. Handle business connections, send and receive messages as a business account.

## Pages

| Page                                                               | Description                    |
| ------------------------------------------------------------------ | ------------------------------ |
| [Connection](../objects-and-types/business-connection.md)          | `BusinessConnection` object    |
| [Business Messages](../guides/event-handlers/business-handlers.md) | Handlers for business messages |

## Handlers

| Decorator                          | Description               |
| ---------------------------------- | ------------------------- |
| `@bot.onBusinessMessage(commands)` | Handle business messages  |
| `@bot.onBusinessEdited()`          | Edited business messages  |
| `@bot.onBusinessConnection()`      | Connection events         |
| `@bot.onBusinessDeleted()`         | Deleted business messages |

## Methods

| Method                                                   | Description                     |
| -------------------------------------------------------- | ------------------------------- |
| `bot.businessConnection(bcId)`                           | Get connection info             |
| `bot.businessSend(target, text, bcId, inline, keyboard)` | Send as business account        |
| `bot.businessAction(target, bcId, action)`               | Send chat action (typing, etc.) |
| `bot.businessRead(bcId, chatId, maxMsgId)`               | Mark messages as read           |
| `bot.businessDelete(bcId, chatId, messageIds)`           | Delete business messages        |

{% code title="Quick reference" %}
```python
# Handlers
@bot.onBusinessMessage(commands="start")   # Handle business messages
@bot.onBusinessEdited()                     # Edited business messages
@bot.onBusinessConnection()                 # Connection events
@bot.onBusinessDeleted()                    # Deleted business messages

# Methods
bot.businessConnection(bcId)                # Get connection info
bot.businessSend(chat, text, bcId)          # Send as business
bot.businessAction(chat, bcId, "typing")    # Business chat action
bot.businessRead(bcId, chatId, maxMsgId)    # Mark messages as read
bot.businessDelete(bcId, chatId, msgIds)    # Delete business messages
```
{% endcode %}

## Parameters

| Parameter         | Type         | Description                                           |
| ----------------- | ------------ | ----------------------------------------------------- |
| `bcId`            | `str`        | Business connection ID                                |
| `target` / `chat` | `int \| str` | Chat ID or username                                   |
| `action`          | `str`        | Chat action type (`"typing"`, `"upload_photo"`, etc.) |
| `maxMsgId`        | `int`        | Maximum message ID to mark as read                    |
| `messageIds`      | `list`       | List of message IDs to delete                         |
