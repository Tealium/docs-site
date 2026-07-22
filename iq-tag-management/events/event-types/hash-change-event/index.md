---
title: Hash change event
description: The hash event sends tracking data when the anchor of the page's URL after the hash symbol (`#`) changes.
url: https://docs.tealium.com/iq-tag-management/events/event-types/hash-change-event/
---
## Requirements

* utag v4.38 or later. For more information about updating the `utag.js` template, see our knowledge base article [Best Practices for Updating to the Latest Version of utag.js](https://support.tealiumiq.com/en/support/solutions/articles/36000363470).

## How it works

The hash change event tracks when the anchor part of the page's URL after the hash symbol (`#`) changes. For example, in the URL `https://www.example.com/page#part2`, the anchor part of the URL is `#part2`. When a the anchor part of page's hash changes, the tracking call is triggered.

The hash change event listener is primarily for use in single page applications (SPA).

For more information about how to add an event listener, see [Manage events](https://docs.tealium.com/manage-events/).

## Event triggers

Event triggers are the specific actions the event listener tracks.

The hash change event can track the following event triggers:

* **Hash Change** – Trigger when the anchor part of the page's URL after the hash symbol (`#`) changes.

You can set the following threshold for the trigger:

* **Delay** - The amount of time in milliseconds to delay the tracking call.

### Trigger frequency

The trigger frequency determines how many times the event trigger will result in a tracking call. We recommend that you set the trigger frequency for hash change events to **Always** because an SPA only has one DOM load, and you will want the event listener to track every hash change.

For more information, see [Event triggers](https://docs.tealium.com/event-triggers/).

## Event trigger variables

Event trigger variables are the values the event listener sends with the tracking call. The hash change event has the following default event trigger variables:

### Hash change

|Identifier| Description|
|---| ---|
|`tealium_event="hash_change"`| The anchor part of the page's URL changed. |
|`iq_event_id`| The UID of the event listener that sent the event.|

**Example**

```json
{
   "tealium_event"  : "hash_change",
   "iq_event_id"   : "hash_change_events_3"
}

```
