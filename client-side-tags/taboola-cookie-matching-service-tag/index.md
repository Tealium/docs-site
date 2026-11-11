---
title: Taboola Cookie Matching Service Tag Setup Guide
description: This article describes how to set up the Taboola Cookie Matching Service tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/taboola-cookie-matching-service-tag/
---

<blockquote>
When using this tag with `utag` version 4.50 or later, you must set the `utag.js` [`always_set_v_id` setting](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id) to `true`. This setting ensures that the visitor ID is available for cookie synchronization. For more information, see the [utag 4.50 release notes](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later) and [Considerations for tealium_visitor_id when upgrading to utag 4.50+](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-).
</blockquote>


## Tag tips

* By default, this tag sends the Taboola ID in the server-side attribute `taboola_id`, but this can be customized.
* Supports first-party domains.
* This tag fires once per session.

For more information about cookie matching in Event Streaming, see: [Understanding Persistent Cookie Matching in Event Streaming](https://docs.tealium.com/about-persistent-cookie-matching/).

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Tealium Account**
    * The account used in the Tealium Collect endpoint.
    * Set this value when the cookie sync request should go to a different account.
    * Default: The account where this tag is published.
* **Tealium Profile**
    * The profile used in the Tealium Collect endpoint.
    * Set this value when you have multiple client-side profiles sending data to a single server-side profile.
    * Default: The profile where this tag is published.
* **Tealium Collect Endpoint**
    * The endpoint used to sync cookies with Tealium.
    * Enter a custom domain to override the default value. This value is usually set to a first-party domain, such as `collect.yourdomain.com/event`.
    * Default: `collect.tealiumiq.com/event`
* **Taboola ID Attribute Name**
    * Set a custom name for the server-side attribute containing the Taboola ID.
    * Default: `taboola_id`.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see [Load Rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`tealium_account`| Tealium account|
|`tealium_profile`| Tealium profile|
|`taboola_id`| Taboola ID|