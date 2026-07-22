---
title: Consent change event specifications
description: Consent events identify a visitors interactions with the Tealium consent manager.
url: https://docs.tealium.com/consent/server-side/event-specs/
---
These events can be found as event specifications under the category **Privacy**.

Consent events are used for auditing purposes and to enforce which connectors can run server-side.

To learn more, see the following:

* [Opt-out privacy banner and popup](https://docs.tealium.com/about-ccpa-privacy-banner-and-popup/)
* [Consent management: Event logging](https://docs.tealium.com/event-logging-for-consent-management/)

## Consent change events

The following consent events use these parameters:

|Name| Description| Example|
|---| ---| ---|
|`policy`|  The context of the consent, usually specific to the terms presented to the visitor upon gaining consent. Values: `gdpr` (opt-in), `ccpa` (opt-out) | `gdpr`|
|`consent_categories`| The category names of approved types of tracking and data collection.| `["affiliates", "social"]`|
|`do_not_sell`| The list of tag IDs to be blocked from selling personal information.| `[1, 42, 51]`|

### `grant_full_consent`

The `grant_full_consent` event indicates that the visitor has granted full consent to tracking and data collection.

#### Opt-in example

```json
{
    "tealium_event"      : "grant_full_consent",
    "policy"             : "gdpr",
    "consent_categories" : [
        "analytics",
        "affiliates",
        "display_ads",
        "search",
        "email",
        "personalization",
        "social",
        "big_data",
        "misc",
        "cookiematch",
        "cdp",
        "mobile",
        "engagement",
        "monitoring",
        "crm"
    ],
    "tealium_visitor_id": "0184a9cef4ce000c9173745530e705075007706d00fb8"
}
```

#### Opt-out example (Explicit OK to Sell decision)

```json
{
    "tealium_event"      : "grant_full_consent",
    "policy"             : "ccpa",
    "consent_categories" : [],
    "tealium_visitor_id": "0184a9cef4ce000c9173745530e705075007706d00fb8"
}
```

### `grant_partial_consent`

The `grant_partial_consent` event indicates that the visitor has only granted partial consent. For consent granted from the **Consent Preferences** interface, the event is accompanied by a list of category names that the user has consented to. For the consent granted from the opt-out consent manager interface, the event is accompanied by a list of IDs of the tags to be blocked from selling personal information.

#### Opt-in example

```json
{
    "tealium_event"      : "grant_partial_consent",
    "policy"             : "gdpr",
    "consent_categories" : ["affiliates", "social"],
    "tealium_visitor_id": "0184a9cef4ce000c9173745530e705075007706d00fb8"
}
```

#### Opt-out example (Do Not Sell decision)

```json
{
    "tealium_event"      : "decline_consent",
    "policy"             : "gdpr",
    "consent_categories" : [],
    "tealium_visitor_id": "0184a9cef4ce000c9173745530e705075007706d00fb8"
}
```

### `decline_consent`

This `decline_consent` event indicates that the visitor has declined consent to tracking and data collection.

#### Opt-in example

```json
{
    "tealium_event"      : "decline_consent",
    "policy"             : "gdpr",
    "consent_categories" : [],
    "tealium_visitor_id": "0184a9cef4ce000c9173745530e705075007706d00fb8"
}
```
