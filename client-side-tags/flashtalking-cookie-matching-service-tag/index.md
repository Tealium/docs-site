---
title: Flashtalking Cookie Matching Service Tag Setup Guide
description: This article describes how to set up the Flashtalking Cookie Matching Service tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/flashtalking-cookie-matching-service-tag/
---

<blockquote>
When using this tag with `utag` version 4.50 or later, you must set the `utag.js` [`always_set_v_id` setting](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id) to `true`. This setting ensures that the visitor ID is available for cookie synchronization. For more information, see the [utag 4.50 release notes](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later) and [Considerations for tealium_visitor_id when upgrading to utag 4.50+](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-).
</blockquote>


## Tag tips

* Use mappings to override standard config values.
* Custom mappings will be included in the cookie sync request to Tealium.
* This tag will only execute once per session, using the `utag_main_flashtalking_cms_<tag UID>` cookie to control that execution.
* Sends the following server-side attribute back to Tealium:
  * `flashtalking_id`

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Flashtalking Key**
  * Your Flashtalking Key.
* **Tealium Account**:
  * Optional
  * Override the `tealium_account` used for server-side requests.
* **Tealium Profile**:
  * Optional
  * Override the `tealium_profile` used for server-side requests.

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`key`|  <ul><li>Flashtalking Key</li></ul> |
|`tealium_account`|  <ul><li>Tealium Account</li></ul> |
|`tealium_profile`|  <ul><li>Tealium Profile</li></ul> |
|`tealium_event`|  <ul><li>Tealium Event</li></ul> |
