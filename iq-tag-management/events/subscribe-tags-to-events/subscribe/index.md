---
title: Subscribe a tag to an event
description: This article explains how to subscribe a tag to an event listener.
url: https://docs.tealium.com/iq-tag-management/events/subscribe-tags-to-events/subscribe/
---You can subscribe a tag to an event in the **Rules and Events** section of a tag. Combine load rules and event rules to control when a tag loads and which events it tracks.

1. From the **Tags** screen, expand the tag details and click **Edit** in the **Rules and Events** section.
1. In the right side of the **Edit Rules and Events** slideout, click the **Events** tab.
1. To edit the logical conditions for the event listener, drag and drop the event listeners and rules from the list on the right side of the dialog to the left side. 
1. Click **Done**.

## Compatibility between tags and events

Be sure to coordinate the event listener&#39;s tracking event and publish locations with any tags that subscribe to the event.

* If the event listener uses a tracking call that is not supported by a subscribed tag, the event will trigger, but the tag will not fire.
* If a tag and event listener use different publish locations, the tag or event listener may not function for your developers, testers, or site visitors.