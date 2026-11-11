---
title: Adition Cookie Matching Tag Setup Guide
description: This article describes how to set up the Adition Cookie Matching tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/adition-cookie-matching-tag/
---

<blockquote>
When using this tag with `utag` version 4.50 or later, you must set the `utag.js` [`always_set_v_id` setting](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id) to `true`. This setting ensures that the visitor ID is available for cookie synchronization. For more information, see the [utag 4.50 release notes](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later) and [Considerations for tealium_visitor_id when upgrading to utag 4.50+](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-).
</blockquote>


## Tag tips

* This is the Cookie Matching version of Adition, allowing you to synchronize Visitor ID information between Tealium and Adition.
* This tag is used in conjunction with another Adition tag.
* Sends the following server-side attribute back to Tealium:
  * `adition_user_id`

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Tealium Account**
  * Name of your Tealium account.
  * Required to redirect to the correct vdata endpoint.
  * Defaults to your Tag Management account name.

* **Tealium Profile**
  * Name of your Tealium profile.
  * Required to redirect to the correct vdata endpoint.
  * Defaults to your Tag Management profile name.

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`tealium_account`|  <ul><li>Tealium Account</li></ul> |
|`tealium_profile`|  <ul><li>Tealium Profile</li></ul> |
