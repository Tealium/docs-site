---
title: Quantum Metric Tag Setup Guide
description: This article describes how to set up the Quantum Metric tag.
url: https://docs.tealium.com/client-side-tags/quantum-metric-tag/
---
 When using this tag with `utag` version 4.50 or later, you must set the `utag.js` [`always_set_v_id` setting]() to `true`. This setting ensures that the visitor ID is available for cookie synchronization. For more information, see the [utag 4.50 release notes]() and [Considerations for tealium_visitor_id when upgrading to utag 4.50&#43;](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-).

## Tag Tips

*  If Tealium Account and Tealium Profile are left blank, they will be automatically populated with your current account and profile. Only applies when using **Send Replay URL**.
*  The default value for **Time Stamp** is `30days`.
*  For information about how to integrate this tag with AudienceStream, see [Tealium &#43; Quantum Metric Integration Guide]().

## Tag Configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Subscription Name**: Provided by your Quantum Metric representative.
* **Send Replay URL**: Select `True` to make the Quantum Metric replay URL available as the server-side attribute `quantum_metric_replay_url`.
* **Time Stamp**: The time stamp for the replay URL. Only applies if using **Send Replay URL**. The default value is `30days`.
* **Tealium Account**: (Optional) Override the `tealium_account` used for server-side requests.
* **Tealium Profile**: (Optional) Override the `tealium_profile` used for server-side requests.

## Load Rules

Load the tag on all pages or set conditions for when your tag loads. For more information, see [About load rules]().

## Data Mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

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