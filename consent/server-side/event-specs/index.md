---
title: Consent change event specifications
description: Consent events identify a visitors interactions with the Tealium consent manager.
url: https://docs.tealium.com/consent/server-side/event-specs/
---
These events can be found as event specifications under the category **Privacy**.

Consent events are used for auditing purposes and to enforce which connectors can run server-side.

To learn more, see the following:

* [Opt-out privacy banner and popup]()
* [Consent management: Event logging]()

## Consent change events

The following consent events use these parameters:

|Name| Description| Example|
|---| ---| ---|
|`policy`|  The context of the consent, usually specific to the terms presented to the visitor upon gaining consent. Values: `gdpr` (opt-in), `ccpa` (opt-out) | `gdpr`|
|`consent_categories`| The category names of approved types of tracking and data collection.| `[&#34;affiliates&#34;, &#34;social&#34;]`|
|`do_not_sell`| The list of tag IDs to be blocked from selling personal information.| `[1, 42, 51]`|

### `grant_full_consent`

The `grant_full_consent` event indicates that the visitor has granted full consent to tracking and data collection.

#### Opt-in example

```json
{
    &#34;tealium_event&#34;      : &#34;grant_full_consent&#34;,
    &#34;policy&#34;             : &#34;gdpr&#34;,
    &#34;consent_categories&#34; : [
        &#34;analytics&#34;,
        &#34;affiliates&#34;,
        &#34;display_ads&#34;,
        &#34;search&#34;,
        &#34;email&#34;,
        &#34;personalization&#34;,
        &#34;social&#34;,
        &#34;big_data&#34;,
        &#34;misc&#34;,
        &#34;cookiematch&#34;,
        &#34;cdp&#34;,
        &#34;mobile&#34;,
        &#34;engagement&#34;,
        &#34;monitoring&#34;,
        &#34;crm&#34;
    ],
    &#34;tealium_visitor_id&#34;: &#34;0184a9cef4ce000c9173745530e705075007706d00fb8&#34;
}
```

#### Opt-out example (Explicit OK to Sell decision)

```json
{
    &#34;tealium_event&#34;      : &#34;grant_full_consent&#34;,
    &#34;policy&#34;             : &#34;ccpa&#34;,
    &#34;consent_categories&#34; : [],
    &#34;tealium_visitor_id&#34;: &#34;0184a9cef4ce000c9173745530e705075007706d00fb8&#34;
}
```

### `grant_partial_consent`

The `grant_partial_consent` event indicates that the visitor has only granted partial consent. For consent granted from the **Consent Preferences** interface, the event is accompanied by a list of category names that the user has consented to. For the consent granted from the opt-out consent manager interface, the event is accompanied by a list of IDs of the tags to be blocked from selling personal information.

#### Opt-in example

```json
{
    &#34;tealium_event&#34;      : &#34;grant_partial_consent&#34;,
    &#34;policy&#34;             : &#34;gdpr&#34;,
    &#34;consent_categories&#34; : [&#34;affiliates&#34;, &#34;social&#34;],
    &#34;tealium_visitor_id&#34;: &#34;0184a9cef4ce000c9173745530e705075007706d00fb8&#34;
}
```

#### Opt-out example (Do Not Sell decision)

```json
{
    &#34;tealium_event&#34;      : &#34;decline_consent&#34;,
    &#34;policy&#34;             : &#34;gdpr&#34;,
    &#34;consent_categories&#34; : [],
    &#34;tealium_visitor_id&#34;: &#34;0184a9cef4ce000c9173745530e705075007706d00fb8&#34;
}
```

### `decline_consent`

This `decline_consent` event indicates that the visitor has declined consent to tracking and data collection.

#### Opt-in example

```json
{
    &#34;tealium_event&#34;      : &#34;decline_consent&#34;,
    &#34;policy&#34;             : &#34;gdpr&#34;,
    &#34;consent_categories&#34; : [],
    &#34;tealium_visitor_id&#34;: &#34;0184a9cef4ce000c9173745530e705075007706d00fb8&#34;
}
```
