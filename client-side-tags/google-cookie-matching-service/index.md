---
title: Google Cookie Matching Service for Google Ad Manager and DV360 (Tealium-hosted) Tag Setup Guide
description: This article describes how to set up the Google Cookie Matching Service for Google Ad Manager and DV360 (Tealium-hosted) tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/google-cookie-matching-service/
---

<blockquote>
When using this tag with `utag` version 4.50 or later, you must set the `utag.js` [`always_set_v_id` setting](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id) to `true`. This setting ensures that the visitor ID is available for cookie synchronization. For more information, see the [utag 4.50 release notes](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later) and [Considerations for tealium_visitor_id when upgrading to utag 4.50+](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-).
</blockquote>


Google's Cookie Matching Service lets a buyer associate the cookie that identifies a Tealium visitor and the doubleclick.net cookie that identifies the user for Google. The Tealium-hosted tag allows clients to persist the Google cookie value in AudienceStream for use in the relevant connectors.

## Tag tips

* Use mappings to override the standard configuration.
* If left blank, the Tealium account and Tealium profile are automatically populated.
* In allowed regions, this tag sends the server-side attribute `google_gid` back to Tealium.
* Use [consent management](https://docs.tealium.com/about-consent-management/) or your CMP integration to ensure that the tag runs only when the visitor has granted consent for Advertising or equivalent categories.
* Map `process_consent` to the value `T` only when consent has been obtained.
* If you do not follow the IAB Transparency and Consent Framework (TCF) and are mapping `process_consent`, you must omit `gdpr` and `gdpr_consent` because Google ignores `process_consent` when those parameters are present. For more information, see [Google: Match Tag URL Parameters](https://developers.google.com/authorized-buyers/rtb/cookie-guide#match-tag-url-parameters).

For more information, see the [Google Cookie Matching](https://developers.google.com/ad-exchange/rtb/cookie-guide) documentation.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Network ID**: Use `tealium_dmp` to pass `google_gid` in the server-side request, or your Google provided Network or Buyer ID for other solutions.
* **Tealium Account**: Your Tealium account.
* **Tealium Profile**: Your Tealium profile.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules](https://docs.tealium.com/about-load-rules/) documentation.

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

| Variable | Description |
| --- | --- |
| `google_nid` | Network or Buyer ID. |
| `tealium_trace_id`| Trace ID.  |
| `tealium_selector`| Tealium selector.  |
| `tealium_account` | Tealium account. |
| `tealium_profile` | Tealium profile.  |
| `process_consent` | Indicates that consent has been obtained from the end user. Map to `T` when the end user has given consent. If you do not follow the IAB Transparency and Consent Framework (TCF), do not include `gdpr` or `gdpr_consent`, because Google ignores `process_consent` when those parameters are present. For more information, see [Google: Match Tag URL Parameters](https://developers.google.com/authorized-buyers/rtb/cookie-guide#match-tag-url-parameters). |