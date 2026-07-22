---
title: intelliAd Cookie Matching Service Tag Setup Guide
description: This article describes how to set up the intelliAd Cookie Matching Service tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/intelliad-cookie-matching-service-tag/
---
The intelliAd Cookie Matching Service associates the Tealium Visitor ID with the intelliAd User ID.


<blockquote>
When using this tag with `utag` version 4.50 or later, you must set the `utag.js` [`always_set_v_id` setting](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id) to `true`. This setting ensures that the visitor ID is available for cookie synchronization. For more information, see the [utag 4.50 release notes](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later) and [Considerations for tealium_visitor_id when upgrading to utag 4.50+](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-).
</blockquote>


## Tag tips

* This tag will only fire once per Tealium Visit Session.
* Sends the following server-side attribute back to Tealium:
  * `intelliad_uid`
* If left blank, Tealium Account and Tealium Profile will be automatically populated with your current account and profile.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Tealium Account**
  * (Optional) Override the `tealium_account` used for server-side requests.
* **Tealium Profile**:
  * (Optional) Override the `tealium_profile` used for server-side requests.
* **Store in Data Layer**
  * Stores the user's intelliAd ID as `intelliad_uid` in the current web page's data layer object.
* **Send to Tealium (server-side)**
  * Makes the `intelliad_uid` intelliAd ID available as a server-side attribute.

## Data mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`tealium_account`|  <ul><li>Tealium Account</li></ul> |
|`tealium_profile`|  <ul><li>Tealium Profile</li></ul> |
|`store_in_datalayer`|  <ul><li>Store in Data Layer</li><li>Values are **yes** or **no**.</li></ul> |
|`send_to_tealium`|  <ul><li>Send to Tealium</li><li>Values are **yes** or **no**.</li></ul> |
