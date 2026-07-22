---
title: Amazon Advertising Cookie Matching Service Tag Setup Guide
description: This article describes how to set up the Amazon Advertising Cookie Matching Service tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/amazon-advertising-cookie-matching-service-tag/
---

<blockquote>
When using this tag with `utag` version 4.50 or later, you must set the `utag.js` [`always_set_v_id` setting](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id) to `true`. This setting ensures that the visitor ID is available for cookie synchronization. For more information, see the [utag 4.50 release notes](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later) and [Considerations for tealium_visitor_id when upgrading to utag 4.50+](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-).
</blockquote>


Amazon Advertising Cookie Matching Service enables a user to associate the Tealium Visitor ID with an Amazon cookie ID within the Amazon system. The Tealium Visitor ID can then be used as an identifier in the Amazon Advertising DSP AudienceStream connector configuration.

## Tag tips

* This tag fires only once per Tealium Visit Session.
* Amazon receives the Tealium Visitor ID and matches it to an Amazon Cookie ID. The Tealium Visitor ID can then be used as a cookie identifier in the Amazon Advertising DSP AudienceStream connector.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Region**: The geographic region for data collection.

## Load rules

Load the tag on all pages or set conditions for when your tag loads. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Type | Description |
|:---------|:------------|:------------|
| `region`  | String | Region  |
| `tealium_visitor_id`  | String | Tealium Visitor ID  |

    