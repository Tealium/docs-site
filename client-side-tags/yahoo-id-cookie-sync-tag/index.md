---
title: Yahoo ID Cookie Sync Tag
description: This article describes how to set up the Yahoo User ID Cookie Sync tag.
url: https://docs.tealium.com/client-side-tags/yahoo-id-cookie-sync-tag/
---

<blockquote>
When using this tag with `utag` version 4.50 or later, you must set the `utag.js` [`always_set_v_id` setting](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id) to `true`. This setting ensures that the visitor ID is available for cookie synchronization. For more information, see the [utag 4.50 release notes](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later) and [Considerations for tealium_visitor_id when upgrading to utag 4.50+](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-).
</blockquote>


The Yahoo Cookie Sync tag enables data partners to initiate a cookie sync and receive a unique encrypted Yahoo Cookie ID (AXID) for each partner. This encrypted ID can be used to post cookie data through the Yahoo DataX Connector. This Tag sends the AXID to the server-side for ingestion.

## Tag tips

* This tag only triggers once per session.
* This Tag sends the `visitor_id` to Yahoo to receive a response to our Server-Side with the matching `yahoo_id` to the `visitor_id`.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Pixel ID**: Numeric ID that denotes the Pixel ID.
* **Partner ID**: Yahoo identity of the respective data provided.
* **GDPR**: Indicates if the user is from a GDPR regulated region or not.
* **GDPR Consent**: GDPR user consent string. Required if GDPR parameter is set to `True`.
* **Tealium Account**: Your current Tealium account by default.
* **Tealium Profile**: Your current Tealium profile by default.
* **Tealium Event**: `yahoo_cookie_sync` by default.

## Load rules

Load the tag on all pages or set conditions for when your tag loads. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Description |
|:---------|:------------|
| Visitor ID `visitor_id`  | String |
| Pixel ID `pixel_id`  | String |
| Partner ID `partner_id`  | String |
| GDPR `gdpr`  | Boolean |
| GDPR Consent `gdpr_consent`  | String |
| Tealium Account `tealium_account`  | String |
| Tealium Profile `tealium_profile`  | String |
| Tealium Event `tealium_event`  | String |

    