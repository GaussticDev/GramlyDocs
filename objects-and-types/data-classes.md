---
description: Dataclass types — User, Chat, SuccessfulPayment.
icon: database
---

# Data Classes

## User

{% code title="Signature" %}
```python
@dataclass
class User:
    id: int
    is_bot: bool
    first_name: str
    last_name: Optional[str]
    username: Optional[str]
    language_code: Optional[str]
    is_premium: Optional[bool]
    added_to_attachment_menu: Optional[bool]
    can_join_groups: Optional[bool]
    can_read_all_group_messages: Optional[bool]
    supports_inline_queries: Optional[bool]
    supports_guest_queries: Optional[bool]
    can_connect_to_business: Optional[bool]
    has_main_web_app: Optional[bool]
    can_manage_bots: Optional[bool]
```
{% endcode %}

## Chat

{% code title="Signature" %}
```python
@dataclass
class Chat:
    id: int
    type: str                   # "private", "group", "supergroup", "channel"
    title: Optional[str]
    username: Optional[str]
    first_name: Optional[str]
    last_name: Optional[str]
    is_forum: Optional[bool]
    is_direct_messages: Optional[bool]
```
{% endcode %}

## SuccessfulPayment

{% code title="Signature" %}
```python
@dataclass
class SuccessfulPayment:
    currency: str
    total_amount: int
    invoice_payload: str
    telegram_payment_charge_id: str
    provider_payment_charge_id: Optional[str]
    is_recurring: Optional[bool]
    is_first_recurring: Optional[bool]
    subscription_expiration_date: Optional[int]
```
{% endcode %}

## `fromDict` class method

All three support a class method:

{% code title="Usage" %}
```python
user = User.fromDict(d)   # constructs from a raw dict, ignoring unknown keys
```
{% endcode %}
