---
title: Version 4.50+ notes
description: Learn about the changes in version 4.50+ and how to update to the latest version.
url: https://docs.tealium.com/platforms/javascript/version-4-50/
---
For all release notes, see [Tealium for Javascript release notes](?filter=tealium-universal-tag).

----

[Update your `utag.js` template](https://support.tealiumiq.com/en/support/solutions/articles/36000363470) to take advantage of the latest fixes and enhancements.

### Updating to version 4.50 or later

We recommend the following steps to ensure a smooth transition when updating to version 4.50 or later:


<blockquote>
Be sure to update the Tealium Collect tag and all active Consent management templates, especially the Event Logging feature.
</blockquote>


* If you have multiple iQ profiles running on the same site, complete these steps to ensure that all instances of `utag.js` on your site start using the new cookie behavior simultaneously, preventing conflicts or compatibility issues:
    1. Update all `utag.js` templates to the latest version.
    1. Set the [`split_cookie`](https://docs.tealium.com/settings/#split_cookie) override to `false` on each profile to use legacy cookie behavior and maintain compatibility with older versions of utag.js still running on your site for the duration of the transition.
    1. Once all `utag.js` templates have been updated and are setting the `split_cookie` override to maintain the legacy cookie behavior, you can remove the cookie override on all profiles at the same time.

* If you have dependencies on the Visitor ID (`v_id`) outside of the Tealium Collect tag, set the `always_set_v_id` option to `true`  to ensure that value continues to be set in time. The most common examples of Visitor ID use are:
  * Cookie sync tags.
  * Mapping `tealium_visitor_id` to an analytics tag such as Adobe or GA4 for troubleshooting and use in downstream data warehouses.

For more information, see [Settings: `always_set_v_id`](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id).
