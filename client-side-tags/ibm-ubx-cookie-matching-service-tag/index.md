---
title: IBM UBX Cookie Matching Service Tag Setup Guide
description: This article describes how to set up the IBM UBX Cookie Matching Service tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/ibm-ubx-cookie-matching-service-tag/
---
The IBM UBX Cookie Matching Service associates the cookie that identifies a Tealium visitor with the cookie that identifies an IBM UBX visitor.

 When using this tag with `utag` version 4.50 or later, you must set the `utag.js` [`always_set_v_id` setting]() to `true`. This setting ensures that the visitor ID is available for cookie synchronization. For more information, see the [utag 4.50 release notes]() and [Considerations for tealium_visitor_id when upgrading to utag 4.50&#43;](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-).

## Tag tips

* This tag will only fire once per Tealium Visit Session when an IBM UBX Visitor ID is found.
* Sends the following server-side attribute back to Tealium:
  * `ibm_ima_uid`
* If left blank, Tealium Account and Tealium Profile will be automatically populated with your current account and profile.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Tealium Account**:
  * (Optional) Override the `tealium_account` used for server-side requests.
* **Tealium Profile**
  * (Optional) Override the `tealium_profile` used for server-side requests.

## Data mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`tealium_account`|  &lt;ul&gt;&lt;li&gt;Tealium Account.&lt;/li&gt;&lt;/ul&gt; |
|`tealium_profile`|  &lt;ul&gt;&lt;li&gt;Tealium Profile.&lt;/li&gt;&lt;/ul&gt; |
