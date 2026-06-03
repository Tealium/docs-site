---
title: iSpot TV Cookie Matching Service Tag Setup Guide
description: This article describes how to set up the iSpot TV Cooke Matching Service tag.
url: https://docs.tealium.com/client-side-tags/ispot-tv-cookie-matching-service-tag/
---
 When using this tag with `utag` version 4.50 or later, you must set the `utag.js` [`always_set_v_id` setting]() to `true`. This setting ensures that the visitor ID is available for cookie synchronization. For more information, see the [utag 4.50 release notes]() and [Considerations for tealium_visitor_id when upgrading to utag 4.50&#43;](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-).

## Tag tips

* This tag will only trigger once per session, assuming it successfully retrieves the iSpot ID.
* If left blank, Tealium account and Tealium profile will be automatically populated with your current account and profile.
* The resulting server-side call sends the following parameters:
  * `tealium_cookie_sync`: true
  * `tealium_account` : Your Tealium account
  * `tealium_profile` : Your Tealium profile
  * `tealium_visitor_id` : The visitor&#39;s Tealium ID
  * `tealium_event` : `cookie_match_ispot`
  * `ispot_id` : The visitor&#39;s iSpot ID
  * `tealium_datasource` : The Tealium data source ID, if set
  * `tealium_trace_id` : The Tealium Trace ID, if set

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Site ID**: Your iSpot-provided Site ID
* **Tealium Account**: (Optional) Your Tealium account
* **Tealium Profile**: (Optional) Your Tealium profile
* **Tealium Data Source ID**: (Optional) Your Tealium Data Source ID

## Data mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|Site ID| (site\_id)|
|Tealium Account| (tealium\_account)|
|Tealium Profile| (tealium\_profile)|
|Tealium Data Source ID| (tealium\_datasource)|
