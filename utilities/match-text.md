---
description: Low-level text matching — commands, exact, starts, ends, contains, regex.
icon: code
---

# matchText

Low-level text matcher used internally by `@bot.onMessage`. Can be used independently for custom matching logic.

{% code title="Signature" %}
```python
matchText(
    text,
    commands=None,
    exact=None,
    starts=None,
    ends=None,
    contains=None,
    regex=None,
    withSlash: bool = True,
    withoutSlash: bool = True,
) -> (list | None, re.Match | None)
```
{% endcode %}

Returns a tuple of `(args, match)`:

* If matched: `([arg1, arg2, ...], None)` or `(["captured"], regex_match_object)`
* If not matched: `(None, None)`

{% code title="Examples" %}
```python
from gramly import matchText

# Commands
matchText("/start", commands="start")     # ([], None)
matchText("help me", commands="help")     # (["me"], None)

# Exact
matchText("hello", exact="hello")         # ([], None)
matchText("hello there", exact="hello")   # (None, None

# Starts with
matchText("find something", starts="find")  # (["something"], None

# Ends with
matchText("say please", ends=" please")     # (["say"], None)

# Contains
matchText("50% discount!", contains="discount")  # (["50%", "discount!"], None

# Regex
matchText("order #123", regex=r"order #(\d+)")  # (["123"], <re.Match>)
```
{% endcode %}

## TextRoute

`TextRoute` is the building block used by `CommandBlock.textRoutes`. It wraps a matching rule and a handler function.

{% code title="Signature" %}
```python
route = TextRoute(fn, exact="hello")
args, match = route.match("hello world")  # (["world"], None)
```
{% endcode %}
