---
title: Page view event
description: The page view event sends tracking data when a visitor views a page.
url: https://docs.tealium.com/iq-tag-management/events/event-types/page-view-event/
---
 The page view event listener is now deprecated. For the current event listener, see [Page load event listener](). 

## Requirements

* utag v4.38 or later. For more information about updating the `utag.js` template, see our knowledge base article [Best Practices for Updating to the Latest Version of utag.js](https://support.tealiumiq.com/en/support/solutions/articles/36000363470).

## How it works

The page view event tracks when a visitor views a page. When a visitor performs the action, the event listener appends its data to existing tracking calls.

This behavior is similar to a [Set Data Values]() extension that defines a payload for page views and has a load rule which fires the tag when a specified page or pages are viewed.

For more information about how to add an event listener, see [Manage events]().

### Use case

Use this event listener with tags that already subscribe to other event listeners.

Add the page view event in an OR relationship with the other events so that when a visitor views the page, the page view event fires the tag and includes the page view event variables with the tag payload.

## Tracking events

The page view event performs a `utag.ut.merge()` function to merge this page view event with another event. For more information, see [Utility functions](/platforms/javascript/api/utility-functions/#utagutmerge).

## Event triggers

Event triggers are the specific actions the event listener tracks.

The event default is the page view event trigger.

## Event trigger variables

Event trigger variables are the values the event listener sends with the tracking call. The page view event has the following default event trigger variable:

### Page View

|Identifier| Description|
|---| ---|
|`tealium_event=&#34;page_view&#34;`| The visitor viewed the specified page.|
|`iq_event_id` | The UID of the event listener that sent the event.|

**Example**

```json
{
   &#34;tealium_event&#34;  : &#34;page_view&#34;,
   &#34;iq_event_id:&#34; : &#34;page_view_events_1&#34;
}

```
