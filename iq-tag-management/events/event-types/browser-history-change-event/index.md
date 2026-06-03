---
title: Browser History Change Event
description: The browser history change event monitors the browser history API for changes in navigation for single-page applications (SPA).
url: https://docs.tealium.com/iq-tag-management/events/event-types/browser-history-change-event/
---
## Requirements

* utag v4.38 or later. For more information about updating the `utag.js` template, see our knowledge base article [Best Practices for Updating to the Latest Version of utag.js](https://support.tealiumiq.com/en/support/solutions/articles/36000363470).
* The page or app uses `history.pushState()` and `history.replaceState()` functions in the browser&#39;s history API for navigation.

## How it works

The browser history change event listener monitors the functions `history.pushState()` and `history.replaceState()` in the browser&#39;s history API. These two functions are used to manage navigation in SPA without full page reloads. When the visitor navigates to a new page within the app or goes back, the tracking call is triggered.

For more information about how to add an event listener, see [Manage events]().

## Event triggers

Event triggers are the actions the event listener tracks.

You can set the following threshold for the trigger:

* **Delay** - The amount of time in milliseconds to delay the tracking call.

### History change

This event is triggered by the browser change history. 

|Identifier| Description|
|---| ---|
|`tealium_event=&#34;history_change&#34;`| The visitor navigated to a new page within the app or went back a page.|

## Event trigger variables

Event trigger variables are the values the event sends with the tracking call. This event has the following default variables:

|Variable| Description| Example| Type|
|---| ---| ---| ---|
|`tealium_event`| Tealium event name.| `history_change`| String|
|`iq_event_id` | The UID of the event listener that sent the event.| `history_change_events_1` | String |

**Example**

```json
{
   &#34;tealium_event&#34;  : &#34;history_change&#34;,
   &#34;iq_event_id:&#34; : &#34;history_change_events_1&#34;
}
```
