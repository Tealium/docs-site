---
title: Adobe Advertising Cookie Sync Tag Setup Guide
description: This article describes how to set up the Adobe Advertising Cookie Sync tag in your tag management account.
url: https://docs.tealium.com/client-side-tags/adobe-advertising-cookie-sync-tag/
---

<blockquote>
When using this tag with `utag` version 4.50 or later, you must set the `utag.js` [`always_set_v_id` setting](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id) to `true`. This setting ensures that the visitor ID is available for cookie synchronization. For more information, see the [utag 4.50 release notes](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later) and [Considerations for tealium_visitor_id when upgrading to utag 4.50+](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-).
</blockquote>


Adobe Advertising Cookie Sync associates the Adobe Advertising cookie ID with the Tealium Visitor ID for audience syncing and activation.

## Tag tips

* This tag fires once per Tealium visit session and waits until a Tealium Visitor ID is available.
* Sends the following attribute back to Tealium:
  * `adobe_advertising_user_id`

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Tealium Account**: Your Tealium account name. Defaults to your Tealium iQ account.
* **Tealium Profile**: Your Tealium profile name. Defaults to your Tealium iQ profile.

## Load rules

Load the tag on all pages or set conditions for when your tag loads. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Configuration

Select a destination to override a value set in the tag configuration.

| Variable | Type | Description |
|:---------|:-----|:------------|
| `tealium_account` | String | Overrides the Tealium Account set in the tag configuration. |
| `tealium_profile` | String | Overrides the Tealium Profile set in the tag configuration. |
