---
title: IBM UBX Cookie Matching Service Tag Setup Guide
description: This article describes how to set up the IBM UBX Cookie Matching Service tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/ibm-ubx-cookie-matching-service-tag/
---
The IBM UBX Cookie Matching Service associates the cookie that identifies a Tealium visitor with the cookie that identifies an IBM UBX visitor.


<blockquote>
When using this tag with `utag` version 4.50 or later, you must set the `utag.js` [`always_set_v_id` setting](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id) to `true`. This setting ensures that the visitor ID is available for cookie synchronization. For more information, see the [utag 4.50 release notes](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later) and [Considerations for tealium_visitor_id when upgrading to utag 4.50+](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-).
</blockquote>


## Tag tips

* This tag will only fire once per Tealium Visit Session when an IBM UBX Visitor ID is found.
* Sends the following server-side attribute back to Tealium:
  * `ibm_ima_uid`
* If left blank, Tealium Account and Tealium Profile will be automatically populated with your current account and profile.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Tealium Account**:
  * (Optional) Override the `tealium_account` used for server-side requests.
* **Tealium Profile**
  * (Optional) Override the `tealium_profile` used for server-side requests.

## Data mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`tealium_account`|  <ul><li>Tealium Account.</li></ul> |
|`tealium_profile`|  <ul><li>Tealium Profile.</li></ul> |
