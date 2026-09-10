---
title: Amplitude Cohorts data source setup guide
description: How to configure the Amplitude Cohorts data source in Tealium to receive cohort membership updates from Amplitude.
url: https://docs.tealium.com/server-side/data-sources/webhooks/setup-guides/amplitude-cohorts/
---
The Amplitude Cohorts data source lets Amplitude send cohort membership updates to your Tealium profile. Cohort membership events arrive as flattened events that you can use in rules, enrichments, and audiences.

## Requirements

The Amplitude Cohorts data source requires an Amplitude account with access to the Destinations catalog.

## How it works

When Amplitude syncs a cohort, it sends membership updates to the Amplitude Cohorts data source endpoint for your Tealium profile. The initial sync sends the full cohort membership. Subsequent syncs send only membership changes, including users added to or removed from the cohort.

Data flows only from Amplitude to Tealium. Tealium does not send data back to Amplitude.

The inbound URL contains a unique data source key. The endpoint does not require an authentication header.

## Set up the data source in Tealium

To create the Amplitude Cohorts data source, see [About data sources](https://docs.tealium.com/about-data-sources/).

After you create the data source, the **Get Code** screen displays the values you need to configure Amplitude:

* **Account Name:** Your Tealium account name.
* **Profile Name:** Your Tealium profile name.
* **Datasource Key:** Your data source key.
* **Region:** Your Tealium collect subdomain (for example, `collect-eu-central-1.tealiumiq.com/`).

Save and publish your profile to activate the data source.

## Configure Amplitude

After you set up the data source in Tealium, configure the Amplitude destination:

1. In Amplitude, go to **Data > Catalog > Destinations**.
1. Open the **Amplitude Cohorts (Tealium)** destination.
1. Enter the **Account Name**, **Profile Name**, **Datasource Key**, and **Region** values from the Tealium data source.
1. Save the destination.

## Events and attributes

Amplitude sends cohort membership data as an array of JSON objects. Tealium flattens each object into a single-level event.

Amplitude prefixes all non-Tealium attributes with `amp_`. The `tealium_visitor_id` and `tealium_event` fields are not prefixed.

Tealium also flattens nested objects using underscore-separated keys. For example, the `email` property in `amp_user_props` becomes `amp_user_props_email`.

The `amp_status` field indicates whether the user was added to or removed from the cohort. A value of `true` means the user was added to the cohort. A value of `false` means the user was removed.

Amplitude sends a payload in the following format:

```json
[
  {
    "tealium_visitor_id": "abc123def456",
    "tealium_event": "amplitude_cohort_sync",
    "amp_cohort_id": "rg123456",
    "amp_cohort_name": "High Value Users",
    "amp_status": true,
    "amp_user_props": {
      "email": "user@example.com",
      "country": "US",
      "plan": "premium"
    }
  }
]
```

Tealium flattens the payload into the following event:

```json
{
  "tealium_visitor_id": "abc123def456",
  "tealium_event": "amplitude_cohort_sync",
  "amp_cohort_id": "rg123456",
  "amp_cohort_name": "High Value Users",
  "amp_status": true,
  "amp_user_props_email": "user@example.com",
  "amp_user_props_country": "US",
  "amp_user_props_plan": "premium"
}
```

The following table describes the key event attributes.

| Attribute | Type | Description |
|---|---|---|
| `tealium_event` | String | Event name. Value is `amplitude_cohort_sync`. |
| `tealium_visitor_id` | String | Visitor identifier passed through from Amplitude. |
| `amp_cohort_id` | String | Unique identifier of the Amplitude cohort. |
| `amp_cohort_name` | String | Name of the Amplitude cohort. |
| `amp_status` | Boolean | Indicates the cohort membership change. `true` means the user was added to the cohort; `false` means the user was removed. |
| `amp_user_props_*` | Varies | Flattened user properties. For example, `amp_user_props_email`. |

## Vendor documentation

* [Amplitude: Create a cohort sync integration](https://amplitude.com/docs/partners/create-a-cohort-sync-integration)
* [Amplitude: Receiving behavioral cohorts](https://amplitude.com/docs/partners/receiving-behavioral-cohorts)
