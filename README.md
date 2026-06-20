---
description: Async-first Telegram Bot framework for Python.
icon: message-bot
---

# Gramly

{% columns %}
{% column %}
**Version**

<code class="expression">space.vars.gramly_version</code>
{% endcolumn %}

{% column %}
**Python**

<i class="fa-python">:python:</i> 3.10+
{% endcolumn %}

{% column %}
**Bot API**

<i class="fa-telegram">:telegram:</i> `10.1`
{% endcolumn %}
{% endcolumns %}

### Quick install

{% code title="Terminal" %}
```bash
pip install gramly
```
{% endcode %}

### Features

| Feature                    | Details                                                                                                                     |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| **Asynchronous**           | Built on [asyncio](https://docs.python.org/3/library/asyncio.html), with transparent sync handler support via a thread pool |
| **Zero-boilerplate async** | Write plain functions — no `async`/`await` required unless you want them                                                    |
| **Auto-routing**           | Decorators match commands, text patterns, regex, media types, callbacks and more                                            |
| **CommandBlock**           | Nested router: one trigger word → sub-routes and callback actions in one place                                              |
| **Rate-limiting**          | Built-in per-user message and inline cooldown with LRU tracking                                                             |
| **Keyboard builders**      | Type-safe helpers for inline and reply keyboards                                                                            |
| **Business API**           | Full Telegram Business Mode support                                                                                         |
| **Payments & Stars**       | Invoices, pre-checkout, refunds, subscriptions, gifts                                                                       |
| **Inline queries**         | Rich article builders and answer helpers                                                                                    |
| **Webhook support**        | `setWebhook` / `deleteWebhook` / `processUpdate` for server-side deployments                                                |
| **Timers**                 | Repeating background tasks with clean stop handles                                                                          |
| **Guards & Interceptors**  | Global middleware layers for filtering and logging                                                                          |
| **File uploads**           | Raw `bytes`, file-like objects, Telegram file IDs and URLs                                                                  |
| **LRU caches**             | Lock-safe caches for callback deduplication and business connections                                                        |

### Minimal bot

{% code title="main.py" %}
```python
from gramly import Gramly

bot = Gramly("TOKEN")

@bot.onMessage(commands="start")
def start(msg):
    bot.send(msg, f"Hello {msg.from_user.first_name}!")

bot.run()
```
{% endcode %}

***

### Documentation

| Section                                                                                                  | Description                                                           |
| -------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------- |
| [Guides](guides/async-model.md)                                                                          | Async model, constructor, running, handlers, command block, keyboards |
| [Event Handlers](guides/event-handlers/)                                                                 | All handler decorators                                                |
| [CommandBlock](guides/command-block.md)                                                                  | Nested router                                                         |
| [Guards & Interceptors](guides/guards-interceptors.md)                                                   | Global middleware                                                     |
| [Messaging](https://github.com/GaussticDev/gramly/blob/main/sending-messages/README.md)                  | Send, reply, edit, media, actions                                     |
| [User & Chat Management](https://github.com/GaussticDev/gramly/blob/main/user-chat-management/README.md) | Ban, kick, promote, invites, forums                                   |
| [Objects & Types](https://github.com/GaussticDev/gramly/blob/main/objects/README.md)                     | Message, CallbackQuery, TelegramError, Obj, and more                  |
| [Keyboards](guides/keyboards/)                                                                           | Button and keyboard builders                                          |
| [Payments & Stars](https://gramly.gitbook.io/gramly-docs/payments-and-stars/invoices)                    | Invoices, refunds, gifts                                              |
| [Business API](business-api/business-api.md)                                                             | Business mode methods                                                 |
| [Inline Queries](inline-queries/inline-queries.md)                                                       | Answer inline, web app, and guest queries                             |
| [Bot Settings](bot-settings/bot-settings.md)                                                             | Bot info, commands, profile                                           |
| [Sticker Sets](sticker-sets/sticker-sets.md)                                                             | Manage sticker sets                                                   |
| [User Profile](bot-settings/user-profile.md)                                                             | User photos, audios, emoji status                                     |
| [Utilities](https://github.com/GaussticDev/gramly/blob/main/utilities/README.md)                         | Helper functions and tools                                            |
| [Examples](examples/examples.md)                                                                         | Complete example bots                                                 |
