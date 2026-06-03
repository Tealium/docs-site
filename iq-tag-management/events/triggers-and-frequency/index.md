---
title: Event triggers and frequency
description: This article describes event triggers.
url: https://docs.tealium.com/iq-tag-management/events/triggers-and-frequency/
---
Event triggers determine which events to track and which tracking call to fire. The triggers vary for each event type.

Some event listeners have multiple triggers or thresholds for those triggers. For example, the scroll event supports triggers for vertical and horizontal scroll direction, as well as scroll length by percentage or pixels.

## Trigger frequency

The trigger frequency determines how many times the event trigger will result in a tracking call.

The trigger frequency options are:

* **Always** - A tracking call is fired every time the event is triggered.  
* **Once** - A tracking call is only fired after the first event is triggered. All subsequent triggers of the event are ignored until the page is refreshed.