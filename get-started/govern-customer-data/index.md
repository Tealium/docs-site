---
title: Govern customer data
description: Learn where Tealium applies consent and restricted data controls as customer data moves through the platform, and the limits of each control.
url: https://docs.tealium.com/get-started/govern-customer-data/
---
Tealium applies consent and restricted data controls at specific points in the data path. Each control covers some processes and not others.

## Enforce consent

Tealium manages consent on both the client side and the server side:

* **Client side**: A consent manager on your website blocks vendor tags that a visitor has not consented to and queues events while consent is pending.
* **Server side**: Consent orchestration enforces consent policies on each event before Tealium processes or activates it. Enforcement covers event connectors, functions, event data storage, and visitor profile processing.

Consent orchestration does not enforce consent on audience connectors. To enforce consent at the visitor level, use manual enforcement. Create visitor attributes that hold each visitor's most recent consent across devices, and add those attributes as conditions to each audience, so audience connectors activate only consented visitors. Audience conditions do not stop Tealium from building visitor profiles.


![](https://docs.tealium.com/images/icons/icon-shield.svg)

#### Consent overview

Learn how Tealium captures and enforces consent.



![](https://docs.tealium.com/images/icons/icon-user-check.svg)

#### Consent orchestration

Enforce server-side consent policies on each event.



![](https://docs.tealium.com/images/icons/icon-users-slash.svg)

#### Manual consent enforcement

Enforce consent at the visitor level in audiences.


## Restrict sensitive attributes

Mark an attribute as restricted to keep it out of event data storage and Context API by default. Connectors and audience data storage still receive restricted attributes.


![](https://docs.tealium.com/images/icons/icon-lock.svg)

#### Restricted data

Keep sensitive attributes out of event data storage and Context API.

