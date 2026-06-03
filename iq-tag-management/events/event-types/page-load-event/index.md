---
title: Page Load Event
description: The page load event sends tracking data when a visitor loads a page.
url: https://docs.tealium.com/iq-tag-management/events/event-types/page-load-event/
---
 The page load event listener replaces the deprecated [page view event listener](). 

## Requirements

* utag v4.38 or later. For more information about updating the `utag.js` template, see our knowledge base article [Best Practices for Updating to the Latest Version of utag.js](https://support.tealiumiq.com/en/support/solutions/articles/36000363470).

## How it works

The page load event tracks when a visitor loads a page. When a visitor performs the action, the tracking call is triggered.

For more information about how to add an event listener, see [Manage events]().

### Use case

Use this event listener when there are no default or configured tracking calls for page views. For example, if the publish configuration `no-view` is set, use this event listener to listen for when content loads or the page finishes loading.

Add the page load event in an OR relationship with the other events so that when a visitor loads the page, the page load event fires the tag and includes the page load event variables with the tag payload.

## Event triggers

Event triggers are the specific actions the event listener tracks.

This event can track the following event triggers:

* **DOM Ready**: All of the objects, properties, and methods have been loaded. This may be before the page is actually finished loading.
* **DOM Complete**: The entire page, including any external resources, has been loaded and is fully rendered.

You can set the following threshold for the trigger:

* **Delay** - The amount of time in milliseconds to delay the firing of the tracking call after the visitor loads the page. This delay can help you remove any accidental clicks and fast page closes to ensure that you only measure legitimate traffic.

### Trigger frequency

The trigger frequency determines how many times the event trigger will result in a tracking call. The page load event listener&#39;s frequency is configured to **Once**. For more information, see [Event triggers]().

## Event trigger variables

Event trigger variables are the values the event listener sends with the tracking call. The page load event has the following default event trigger variables:

### Page View

|Identifier| Description|
|---| ---|
|`tealium_event=&#34;page_view&#34;`| The visitor loaded the specified page.|
|`iq_event_id` | The UID of the event listener that sent the event.|

**Example**

```json
{
   &#34;tealium_event&#34;  : &#34;page_view&#34;,
   &#34;iq_event_id:&#34; : &#34;page_view_events_1&#34;
}

```
