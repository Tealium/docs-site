---
title: Amobee Cookie Matching Service Tag Setup Guide
description: This article describes how to set up the Amobee Cookie Matching Service tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/amobee-cookie-matching-service-tag/
---

<blockquote>
When using this tag with `utag` version 4.50 or later, you must set the `utag.js` [`always_set_v_id` setting](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id) to `true`. This setting ensures that the visitor ID is available for cookie synchronization. For more information, see the [utag 4.50 release notes](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later) and [Considerations for tealium_visitor_id when upgrading to utag 4.50+](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-).
</blockquote>


## Tag tips

* Sends the following server-side attribute back to Tealium:
  * `amobee_id`
* If left blank, the Tealium account and profile names are automatically populated.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* Amobee Token (Your Amobee Token)
* Tealium Account:
* Tealium Profile

## Data mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`amobee_token`|  <ul><li>Amobee token</li><li>Your Amobee token, as provided by Amobee.</li></ul> |
|`tealium_account`|  <ul><li>Tealium account name</li></ul> |
|`tealium_profile`|  <ul><li>Tealium profile name</li></ul> |
