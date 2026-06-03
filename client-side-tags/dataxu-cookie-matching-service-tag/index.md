---
title: DataXu Cookie Matching Service Tag Setup Guide
description: This article describes how to set up the DataXu Cookie Matching Service tag.
url: https://docs.tealium.com/client-side-tags/dataxu-cookie-matching-service-tag/
---
 When using this tag with `utag` version 4.50 or later, you must set the `utag.js` [`always_set_v_id` setting]() to `true`. This setting ensures that the visitor ID is available for cookie synchronization. For more information, see the [utag 4.50 release notes]() and [Considerations for tealium_visitor_id when upgrading to utag 4.50&#43;](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-).

## Tag Tips

* If left blank, Tealium Account and Tealium Profile will be automatically populated with your current TiQ account and profile.
* Sends the following server-side attribute back to Tealium:
  * `dataxuId`

## Tag Configuration

First, go to Tealium&#39;s tag marketplace and add the DataXu Cookie Matching Service tag (Learn more about [how to add a tag]()).

After adding the tag, configure the following settings:

* **Tealium Account**
  * (Optional) Your Tealium Account name.

* **Tealium Profile**:
  * (Optional) Your Tealium Profile name.

## Data Mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`tealium_account`| Tealium Account|
|`tealium_profile`| Tealium Profile|
