---
title: Rubicon Cookie Matching Service Tag Setup Guide
description: This article describes how to set up the Rubicon Cookie Matching Service tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/rubicon-cookie-matching-service-tag/
---

<blockquote>
When using this tag with `utag` version 4.50 or later, you must set the `utag.js` [`always_set_v_id` setting](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id) to `true`. This setting ensures that the visitor ID is available for cookie synchronization. For more information, see the [utag 4.50 release notes](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later) and [Considerations for tealium_visitor_id when upgrading to utag 4.50+](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-).
</blockquote>


## Tag tips

* Sends the following server-side attribute back to Tealium:
  * `rubicon_vid`

* All parameters can be configured with mappings.
* The GDPR and GDPR Consent variables must be mapped in the European Economic Area (EEA).
* GDPR should be set to `1` when the user is in a EEA country, and `0` otherwise.)
* GDPR Consent is a string containing the Base64 encoded "DaisyBit" consent string.
* See [IAB Europe](https://advertisingconsent.eu/) for additional details on GDPR.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Tealium Account**
  * Pass-through parameter for the vdata endpoint specifying the account name for Event Streaming.

* **Tealium Profile**
  * Pass-through parameter for the vdata endpoint specifying the profile name for Event Streaming.

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`tealium_account`|  <ul><li>Tealium Account</li></ul> |
|`tealium_profile`|  <ul><li>Tealium Profile</li></ul> |
|`gdpr`|  <ul><li>GDPR</li></ul> |
|`gdpr_consent`|  <ul><li>GDPR Consent</li></ul> |
