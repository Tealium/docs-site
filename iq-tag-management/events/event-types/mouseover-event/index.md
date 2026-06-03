---
title: Mouseover event
description: The mouseover event sends tracking data when a visitor hovers their cursor over an element on a page. You can specify how long the visitor needs to hover the cursor over that element.
url: https://docs.tealium.com/iq-tag-management/events/event-types/mouseover-event/
---
## Requirements

* utag v4.38 or later. For more information about updating the `utag.js` template, see our knowledge base article [Best Practices for Updating to the Latest Version of utag.js](https://support.tealiumiq.com/en/support/solutions/articles/36000363470).

## How it works

The mouseover event tracks when visitors hover their mouse cursor over a specified element. When a visitor performs the action, the tracking call is triggered.

For more information about how to add an event listener, see [Manage events]().

## Event triggers

Event triggers are the specific actions the event listener tracks.

This event can track the following event triggers:

* **Mouseover** – Trigger when the visitor hovered the cursor over the specified element for a minimum amount of time.

You can set the following threshold for the trigger:

* **Duration of Hover** - The amount of time in milliseconds to hover over the element to trigger the event.

### Element selector

The element selector specifies which element on a page you want to trigger the event listener. For more information, see [Event element selector]().

### Trigger frequency

The trigger frequency determines how many times the event trigger will result in a tracking call. For more information, see [Event triggers]().

## Event trigger variables

Event trigger variables are the values the event listener sends with the tracking call. The mouseover event event has the following default event trigger variable:

### Mouseover

|Identifier| Description|
|---| ---|
|`tealium_event=&#34;mouseover&#34;`| The visitor hovered their mouse cursor over the specified element for the minimum amount of time.|
|`iq_event_id` | The UID of the event listener that sent the event.|

**Example**

```json
{
   &#34;tealium_event&#34;  : &#34;mouseover&#34;,
   &#34;iq_event_id:&#34; : &#34;mouseover_events_1&#34;
}

```
