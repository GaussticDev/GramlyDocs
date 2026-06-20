---
description: Handle inline queries, web app queries, and guest queries.
---

# Overview

Handle inline mode queries from users, answer web app queries, and process guest queries.

## Pages

| Page                                                             | Description                                   |
| ---------------------------------------------------------------- | --------------------------------------------- |
| [Handling Inline Queries](../guides/event-handlers/on-inline.md) | `@bot.onInline` — receive inline queries      |
| [InlineQuery Object](../objects-and-types/inline-query.md)       | The `InlineQuery` object with article builder |

## Methods

| Method                                                                       | Description                     |
| ---------------------------------------------------------------------------- | ------------------------------- |
| `bot.answerInlineQuery(queryId, results, cacheTime, isPersonal, nextOffset)` | Answer an inline query          |
| `bot.answerWebAppQuery(webAppQueryId, result)`                               | Answer a Web App query          |
| `bot.answerGuestQuery(queryId, text, parseMode)`                             | Answer a guest query            |
| `bot.answerShippingQuery(shippingQueryId, ok)`                               | Answer a shipping query         |
| `bot.savePreparedInlineMessage(userId, result, ...)`                         | Save a prepared inline message  |
| `bot.savePreparedKeyboardButton(text, ...)`                                  | Save a prepared keyboard button |

## Parameters

| Parameter       | Type          | Description                               |
| --------------- | ------------- | ----------------------------------------- |
| `queryId`       | `str`         | Inline query ID                           |
| `results`       | `list`        | List of result objects                    |
| `cacheTime`     | `int`         | Cache duration in seconds (default `30`)  |
| `isPersonal`    | `bool`        | Show results only for the requesting user |
| `nextOffset`    | `str`         | Pagination offset for additional results  |
| `webAppQueryId` | `str`         | Web App query ID                          |
| `result`        | `dict`        | `InlineQueryResult` object                |
| `text`          | `str`         | Response text for guest queries           |
| `parseMode`     | `str \| None` | Parse mode for guest query response       |

{% code title="Quick reference" %}
```python
# Handle inline queries
@bot.onInline(minLength=3)
def on_inline(q: InlineQuery):
    results = [
        q.article("Result 1", "Content 1", description="Desc 1"),
        q.article("Result 2", "Content 2", description="Desc 2"),
    ]
    q.answer(results)

# Answer web app queries
bot.answerWebAppQuery(webAppQueryId, result_dict)

# Answer guest queries
bot.answerGuestQuery(queryId, "Response text")

# Save prepared inline messages
bot.savePreparedInlineMessage(userId, result)
```
{% endcode %}
