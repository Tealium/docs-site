---
title: Quantum Metric Tag Setup Guide
description: This article describes how to set up the Quantum Metric tag.
url: https://docs.tealium.com/client-side-tags/quantum-metric-tag/
---

<blockquote>
When using this tag with `utag` version 4.50 or later, you must set the `utag.js` [`always_set_v_id` setting](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id) to `true`. This setting ensures that the visitor ID is available for cookie synchronization. For more information, see the [utag 4.50 release notes](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later) and [Considerations for tealium_visitor_id when upgrading to utag 4.50+](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-).
</blockquote>


## Tag tips

*  If Tealium Account and Tealium Profile are left blank, they will be automatically populated with your current account and profile. Only applies when using **Send Replay URL**.
*  The default value for **Time Stamp** is `30days`.
*  For information about how to integrate this tag with Customer Data Platform (CDP), see [Tealium + Quantum Metric Integration Guide](https://docs.tealium.com/tealium-quantum-metric-integration-guide/).

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Subscription Name**: Provided by your Quantum Metric representative.
* **Send Replay URL**: Select `True` to make the Quantum Metric replay URL available as the server-side attribute `quantum_metric_replay_url`.
* **Time Stamp**: The time stamp for the replay URL. Only applies if using **Send Replay URL**. The default value is `30days`.
* **Tealium Account**: (Optional) Override the `tealium_account` used for server-side requests.
* **Tealium Profile**: (Optional) Override the `tealium_profile` used for server-side requests.

## Load rules

Load the tag on all pages or set conditions for when your tag loads. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Description |
|:---------|:------------|
| `subscription_name` | Subscription name. |
| `tealium_account` | Tealium account. |
| `tealium_profile` | Tealium profile. |

### Replay URL Parameters

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `send_replay_url` | Boolean | Whether to send the replay. Values can be `true` or `false`. |
| `autoreplay` | Boolean | Auto replay flag. Values can be `true` or `false`.|
| `replaysecond` | String | The number of seconds to set the playhead into the replay session. |
| `qmUserCookie` |  String| Quantum metric user cookie override. |
| `qmSessionCookie` | String | Quantum metric session cookie override. |
| `ts` |  String | The time stamp for the replay URL. |