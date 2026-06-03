---
title: Xandr Cookie Matching Service Tag Setup Guide
description: This article describes how to set up the Xandr Cookie Matching Service tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/xandr-cookie-matching-service-tag/
---
 When using this tag with `utag` version 4.50 or later, you must set the `utag.js` [`always_set_v_id` setting]() to `true`. This setting ensures that the visitor ID is available for cookie synchronization. For more information, see the [utag 4.50 release notes]() and [Considerations for tealium_visitor_id when upgrading to utag 4.50&#43;](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-).

Xandr Cookie Matching Service enables a buyer to associate the cookie that identifies a Tealium visitor and the cookie that identifies the user for Xandr. 

## Tag tips

* This tag will only fire once per Tealium Visit Session.
* Sends the following server-side attribute back to Tealium:
    * `adnxs_uid`
* If left blank, Tealium Account and Tealium Profile is automatically populated.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* Tealium Account
* Tealium Profile

## Data mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
| `tealium_account` | Tealium Account|
| `tealium_profile` | Tealium Profile|
