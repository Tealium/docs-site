---
title: Version 4.52+ notes
description: Learn about the changes in version 4.52+ and how to update to the latest version.
url: https://docs.tealium.com/platforms/javascript/version-4-52/
---
For all release notes, see [Tealium for Javascript release notes](?filter=tealium-universal-tag).

----

## Overview

Version 4.52 introduces improved support for single-page applications (SPAs), optimizations for Google’s Interaction to Next Paint (INP) scores, improvements in session counting for first-party setups, and several bug fixes and performance updates.

## Important notes for version 4.52+

Be sure to review the following notes before implementing changes in version 4.52+:

* **Queue for early tracking events:** Only use the queue snippet with version 4.52 and later. Adding it with earlier versions will prevent `utag.js` from running.
* **Session counting for first-party, reverse proxy, or self-hosted setups:** Customers using first-party or reverse-proxy setups should remove any previous custom session counting logic to avoid duplicate sessions. For self-hosted setups, contact Tealium support to deactivate your billing requests.

## Queue for early tracking events

This version adds a queuing system for tracking functions (`utag.view`, `utag.link`, `utag.track`), making them available immediately on page load. Previously, these functions would not work until `utag.js` fully loaded, causing errors or lost events in single page applications (SPA) when called too early.

To ensure reliable capture of early tracking events, the following queueing snippet must be placed as early as possible in the page code before [`utag.js` loader script](https://docs.tealium.com/platforms/javascript/install/#universal-tag-utagjs):


<blockquote>
Only use this snippet with version 4.52 and later. Adding it with earlier versions will prevent `utag.js` from running.
</blockquote>


```javascript
<script type="text/javascript">
  (function(w){
    if(w.utag) return; var u=w.utag={}; u.e=[]; u.view=function(a,b,c){u.e.push({a:a,b:b,c:c,d:"view"})};
    u.link=function(a,b,c){u.e.push({a:a,b:b,c:c,d:"link"})};
    u.track=function(d,a,b,c){typeof d==="object" ? u.e.push({a:d.data,b:(d.cfg?d.cfg.cb:null),c:(d.cfg?d.cfg.uids:undefined),d:d.event}): u.e.push({a:a,b:b,c:c,d:d});
    };
  })(window);
</script>
```

Adding this snippet ensures early tracking events are queued and processed as soon as `utag.js` executes. The queued events are processed in the order received.

Do not modify the uTag loader script itself, as this can break `utag.js` by interfering with its initialization process or causing unexpected behavior in tracking and tag execution.

## Non-blocking tags option

The new `nonblocking_tags` setting provides a way to make tags non-blocking, helping improve the Interaction to Next Paint (INP) score by allowing tags to load asynchronously. By default, tags are blocking, which ensures tracking can execute, but may delay page load times for large or resource-intensive tags. Enabling `nonblocking_tags` optimizes performance for customers prioritizing INP scores for SEO.

For more information, see [Settings: `nonblocking_tags`](https://docs.tealium.com/platforms/javascript/settings/#nonblocking_tags) and [Interaction to Next Paint (INP) and Tealium iQ](https://tealium.com/blog/customer-data-platform/interaction-to-next-paint-inp-and-tealium-iq/).

## Session counting for first-party setups

Adds session counting for first-party or reverse-proxy setups that previously needed custom configurations to measure sessions. The new setup standardizes session counting without requiring custom scripts, improving accuracy for first-party environments.

* Customers with first-party or reverse-proxy setups should remove any previous custom session counting logic to avoid duplicate sessions.
* For self-hosted setups, please contact Tealium support to deactivate your billing requests.

## Performance enhancements

This release includes the following performance enhancements:

* **Minimize cookie reads**  
Updates to minimize unnecessary cookie reads, improving performance on pages with multiple or complex cookies. The `utag_main` cookie now avoids repetitive reads without affecting cookie-based tracking or data storage. This enhancement is applied automatically with version 4.52.
* Addresses long-standing inconsistent behaviors that could create unexpected tracking issues. These fixes make Tealium iQ more predictable, particularly for advanced implementations:
    * **Before Load Rules scoped Javascript extension**: All extensions scoped to Before Load Rules now execute once per page load, even for tags called by UID. To retain the legacy behavior, set `suppress_before_load_rules_with_uids` to `true`. For more information, see [Settings: `suppress_before_load_rules_with_uids`](https://docs.tealium.com/platforms/javascript/settings/#suppress_before_load_rules_with_uids).
    * **Event attribute overwrites**: All `tealium_*` event attributes are now automatically overwritten by Tealium-generated values, except for `tealium_visitor_id` and `tealium_event`. This prevents conflicts from manually set `tealium_*` attributes in the data layer.