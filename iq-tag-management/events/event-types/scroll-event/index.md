---
title: Scroll event
description: The scroll event sends tracking data when a visitor scrolls through a screen. You can specify whether to measure the scroll amount by pixels or screen percentage. You can also specify whether to track vertical scrolling, horizontal scrolling, or both.
url: https://docs.tealium.com/iq-tag-management/events/event-types/scroll-event/
---
## Requirements

* utag v4.38 or later. For more information about updating the `utag.js` template, see our knowledge base article [Best Practices for Updating to the Latest Version of utag.js](https://support.tealiumiq.com/en/support/solutions/articles/36000363470).

## How it works

A scroll event tracks when a visitor scrolls through a screen. When a visitor performs the action, the tracking call is triggered.

For more information about how to add an event listener, see [Manage events]().

## Event triggers

Event triggers are the specific actions the event listener tracks.

This event can track the following triggers:

* **Vertical Scroll Depths** – Fire when the user scrolls down the screen.
* **Horizontal Scroll Depths** – Fire when the user scrolls across the screen.

Set the following thresholds to control when to trigger each event:

* **Percent** - Measure scroll distance by a percentage of the screen.
* **Pixels** - Measure scroll distance by a number of pixels.

Enter multiple values as a comma-separated list to trigger at different screen locations. For example, to measure percentages enter `25, 50, 75, 100`, or to measure pixels enter `2000, 5000`.

### Element selector

The element selector specifies which element on a page you want to trigger the event listener. For more information, see [Event element selector]().

## Event trigger variables

Event trigger variables are the values the event listener sends with the tracking call. The scroll event has the following default event trigger variables:

|Variable| Description| Example| Type|
|---| ---| ---| ---|
|`tealium_event`| Tealium event name.| `scroll`| String|
|`scroll_depth`| The amount of scroll.| `50`| Number|
|`scroll_depth_type`| The measurement of scroll, by `percent` or `pixels`.| `percent`| String|
|`scroll_direction`| The direction of scroll, `vertical` or `horizontal`.| `vertical`| String|
|`iq_event_id` | The UID of the event listener that sent the event.|

### Event tracking

#### Horizontal Scroll

|Identifier| Description|
|---| ---|
|`tealium_event=&#34;scroll&#34;`| The visitor scrolled through the screen in a specified direction and amount.|

**Example**

```json
{
   &#34;tealium_event&#34;  : &#34;scroll&#34;,
   &#34;scroll_depth&#34; : &#34;500&#34;,
   &#34;scroll_depth_type&#34; : &#34;pixels&#34;,
   &#34;scroll_direction&#34; : &#34;horizontal&#34;,
   &#34;iq_event_id:&#34; : &#34;scroll_depth_events_1&#34;
}
```

#### Vertical Scroll

|Identifier| Description|
|---| ---|
|`tealium_event=&#34;scroll&#34;`| The visitor scrolled through the screen in a specified direction and amount.|

**Example**

```json
{
   &#34;tealium_event&#34;  : &#34;scroll&#34;,
   &#34;scroll_depth&#34; : &#34;50&#34;,
   &#34;scroll_depth_type&#34; : &#34;percent&#34;,
   &#34;scroll_direction&#34; : &#34;vertical&#34;,
   &#34;iq_event_id:&#34; : &#34;scroll_depth_events_2&#34;
}
```
