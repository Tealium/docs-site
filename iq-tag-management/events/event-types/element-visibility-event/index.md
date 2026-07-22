---
title: Element visibility event
description: The element visibility event sends tracking data when a visitor sees a specific element on a page. You can specify how much of the element needs to be visible and for how long before the event listener triggers.
url: https://docs.tealium.com/iq-tag-management/events/event-types/element-visibility-event/
---
## Requirements

* utag v4.38 or later. For more information about updating the `utag.js` template, see our knowledge base article [Best Practices for Updating to the Latest Version of utag.js](https://support.tealiumiq.com/en/support/solutions/articles/36000363470).

## How it works

A element visibility event tracks when a visitor sees a specific element on a page. When an element is visible to the visitor, the tracking call is triggered.

For more information about how to add an event listener, see [Manage events](https://docs.tealium.com/manage-events/).

## Event triggers

Event triggers are the specific actions the event listener tracks.

The event default is the element visibility event trigger. You can set the following thresholds for this trigger:

* **Percent Visible** - The percentage of the element that needs to be visible for the event listener to trigger.
* **Minimum Duration** - The amount of time in seconds that the element needs to be visible for the event listener to trigger. The default is 0 seconds, which triggers the event listener immediately.

### Element selector

The element selector specifies which element on a page you want to trigger the event listener. For more information, see [Event element selector](https://docs.tealium.com/event-element-selector/).

## Event trigger variables

Event trigger variables are the values the event sends with the tracking call. The element visibility event has the following default event trigger variable:

|Variable| Description| Example| Type|
|---| ---| ---| ---|
|`tealium_event`| Tealium event name.| `element_visible`| String|
|`percent_visible`| The percentage of the element that was visible.| `100` | Number |
|`duration`| The amount of time the element was visible in seconds. | `5` | Number |
|`iq_event_id` | The UID of the event listener that sent the event.| `element_visibility_events_1` | String |


### Element Visible

|Identifier| Description|
|---| ---|
|`tealium_event="element_visible"`| The visitor revealed the specified element by a certain percentage of visibility and for the minimum amount of time.|

**Example**

```json
{
   "tealium_event"  : "element_visible",
   "percent_visible" : "100",
   "duration" : "5",
   "iq_event_id:" : "element_visibility_events_1"
}

```
