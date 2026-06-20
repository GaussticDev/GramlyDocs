---
description: All event handler decorators — a quick reference.
icon: list
---

# Event Handlers

All decorators return the original function unchanged, so they can be stacked.

| Decorator                                                 | Trigger                      | Key Features                                                                 |
| --------------------------------------------------------- | ---------------------------- | ---------------------------------------------------------------------------- |
| [`@bot.onMessage`](on-message.md)                         | Incoming messages            | commands, exact, starts, ends, contains, regex, argsMin, guard, business     |
| [`@bot.onEdited`](other-handlers.md)                      | Edited messages              | business flag                                                                |
| [`@bot.onPost`](other-handlers.md)                        | Channel posts                | —                                                                            |
| [`@bot.onMedia`](other-handlers.md)                       | Media content                | photo, video, document, audio, voice, sticker, etc.                          |
| [`@bot.onAny`](other-handlers.md)                         | Unhandled messages           | Catch-all fallback                                                           |
| [`@bot.onCallback`](on-callback.md)                       | Inline keyboard clicks       | prefix matching, owner check, guard                                          |
| [`@bot.onInline`](on-inline.md)                           | Inline queries               | minLength filter                                                             |
| [`@bot.onCheckout`](../../payments-and-stars/payments.md) | Pre-checkout queries         | accept / reject                                                              |
| [`@bot.onPayment`](../../payments-and-stars/payments.md)  | Successful payments          | Payment object on msg.payment                                                |
| [`@bot.onWebApp`](other-handlers.md)                      | Web App data                 | msg.webAppData                                                               |
| [`@bot.onJoinRequest`](other-handlers.md)                 | Chat join requests           | approve / decline                                                            |
| [`@bot.onMyStatus`](other-handlers.md)                    | Bot's own chat member status | —                                                                            |
| [`@bot.onChatMember`](other-handlers.md)                  | Chat member changes          | —                                                                            |
| [`@bot.onReaction`](other-handlers.md)                    | Message reactions            | —                                                                            |
| [`@bot.onPoll`](other-handlers.md)                        | Poll answers                 | —                                                                            |
| [`@bot.onBoost`](other-handlers.md)                       | Chat boosts                  | —                                                                            |
| [`@bot.onPaidMedia`](other-handlers.md)                   | Paid media purchases         | —                                                                            |
| [`@bot.onGuest`](other-handlers.md)                       | Guest queries                | —                                                                            |
| [`@bot.onManaged`](other-handlers.md)                     | Managed bot events           | —                                                                            |
| [Business handlers](business-handlers.md)                 | Business messages            | onBusinessMessage, onBusinessEdited, onBusinessConnection, onBusinessDeleted |

{% code title="Stacking example" %}
```python
@bot.onMessage(commands="start")
@bot.onMessage(exact="hello")
def on_start_or_hello(msg):
    bot.send(msg, "Hello!")
```
{% endcode %}
