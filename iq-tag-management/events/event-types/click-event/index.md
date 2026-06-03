---
title: Click event
description: The click event sends tracking data when a visitor clicks an element on a page. You can specify a full click and release, mousedown, or mouseup trigger.
url: https://docs.tealium.com/iq-tag-management/events/event-types/click-event/
---
## Requirements

* utag v4.38 or later. For more information about updating the `utag.js` template, see our knowledge base article [Best Practices for Updating to the Latest Version of utag.js](https://support.tealiumiq.com/en/support/solutions/articles/36000363470).

## How it works

The click event tracks visitors for a full click-and-release, mousedown, or mouseup event on a specified element. When a visitor performs the action, the tracking call is triggered.

For more information about how to add an event listener, see [Manage events]().

## Event triggers

Event triggers are the specific actions the event listener tracks.

The click event can track the following event triggers:

* **Click** – Trigger when the user clicks and releases the element.
* **Mousedown** – Trigger when the user clicks the element.
* **Mouseup** – Trigger when the user releases the mouse from the element.

### Element selector

The element selector specifies which element on a page you want to trigger the event listener. For more information, see [Event element selector]().

### Trigger frequency

The trigger frequency determines how many times the event trigger will result in a tracking call. For more information, see [Event triggers]().

## Event trigger variables

Event trigger variables are the values the event listener sends with the tracking call. The click event has the following default event trigger variables:

### Click

|Identifier| Description|
|---| ---|
|`tealium_event=&#34;click&#34;`| The visitor clicked and released the specified element.|
|`iq_event_id` | The UID of the event listener that sent the event.|

**Example**

```json
{
   &#34;tealium_event&#34;  : &#34;click&#34;,
   &#34;iq_event_id:&#34;   : &#34;click_events_1&#34;
}

```

### Mousedown

|Identifier| Description|
|---| ---|
|`tealium_event=&#34;mousedown&#34;`| The visitor clicked the specified element.|
|`iq_event_id`| The UID of the event listener that sent the event.|

**Example**

```json
{
   &#34;tealium_event&#34;  : &#34;mousedown&#34;,
   &#34;iq_event_id:&#34;   : &#34;click_events_2&#34;
}

```

### Mouseup

|Identifier| Description|
|---| ---|
|`tealium_event=&#34;mouseup&#34;`| The visitor released a click from the specified element.|
|`iq_event_id`| The UID of the event listener that sent the event.|

**Example**

```json
{
   &#34;tealium_event&#34;  : &#34;mouseup&#34;,
   &#34;iq_event_id:&#34;   : &#34;click_events_3&#34;
}

```
