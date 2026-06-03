---
title: Neustar Fabrick ID Tag Setup Guide
description: This article describes how to configure the Neustar Fabrick ID tag in your iQ Tag Management (TiQ) account.
url: https://docs.tealium.com/client-side-tags/neustar-fabrick-id-tag/
---
 When using this tag with `utag` version 4.50 or later, you must set the `utag.js` [`always_set_v_id` setting]() to `true`. This setting ensures that the visitor ID is available for cookie synchronization. For more information, see the [utag 4.50 release notes]() and [Considerations for tealium_visitor_id when upgrading to utag 4.50&#43;](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-).

## Tag tips

* If left blank, the Tealium Account and Profile are automatically populated
* The following attributes are sent to Tealium server-side through `neustar_fabrickId_sync`:
  * `fabrickId`
  * `visitor_id`
  * `element_one` (Optional)

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **API Key**: (Required) Neustar-provided API key.
* **FabrickId Timespan Days**: How often the `fabrickId` will change. Default is seven days. 
* **Tealium Account**: Your Tealium Account.
* **Tealium Profile**: Your Tealium Profile.
* **Data Source Key**: (Required) The data source key from Tealium server-side.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Standard

| Variable | Description |
|:---------|:------------|
| Base Url (`base_url`) | String |
| Event Url (`event_url`) | String |
| Api Key (`apiKey`) | String |
| FabrickId Timespan Days (`daysSyncPeriod`) | Number |
| Tealium Account (`tealium_account`) | String |
| Tealium Profile (`tealium_profile`) | String |
| Data Source Key (`tealium_datasource`) | String |
| Hashed email address (`e`) | String |
| E.164 standard hashed phone number (`p`) | String |
| IPv4 Address (`raw` i4) | String |
| IPv6 Address (`raw` i6) | String |
| Mobile Advertising ID (`m`) | String |
| Identifier for Advertising (`ia`) | String |
| Denotes the source for the IFA (`ifa_type`) | String |
| Indicates whether the user can be tracked or not (`lmt`) | String |
| Partner or advertiser&#39;s first-party user ID (`1pd`) | String |

    