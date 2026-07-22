---
title: Google Analytics Cookie Matching Service Tag Setup Guide
description: This article describes how to set up the Google Analytics Cookie Matching Service tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/google-analytics-cookie-matching-service-tag/
---

<blockquote>
When using this tag with `utag` version 4.50 or later, you must set the `utag.js` [`always_set_v_id` setting](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id) to `true`. This setting ensures that the visitor ID is available for cookie synchronization. For more information, see the [utag 4.50 release notes](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later) and [Considerations for tealium_visitor_id when upgrading to utag 4.50+](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-).
</blockquote>


The Google Analytics Cookie Matching Service tag lets you associate a visitor with the default Google client ID cookie (`_ga`) or default to the Tealium visitor ID.

## Tag tips

* Under **Advanced Settings**, ensure the **Bundle Flag** is set to **Yes** and the **Wait Flag** is set to **No**.
* Move this tag above your Tealium Collect tag in the [Load Order Manager]](https://docs.tealium.com/load-order-manager/) .
* For more information, see the [Google Cookie Matching](https://developers.google.com/ad-exchange/rtb/cookie-guide) documentation.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules](https://docs.tealium.com/about-load-rules/) documentation.
