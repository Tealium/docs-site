---
title: Form submission event
description: The form submission event sends tracking data when a visitor submits a form on a page.
url: https://docs.tealium.com/iq-tag-management/events/event-types/form-submission-event/
---
## Requirements

* utag v4.38 or later. For more information about updating the `utag.js` template, see our knowledge base article [Best Practices for Updating to the Latest Version of utag.js](https://support.tealiumiq.com/en/support/solutions/articles/36000363470).

## How it works

The form submission event type tracks when a visitor submits a form on a page. When a visitor performs the action, the tracking call is triggered.

For more information about how to add an event listener, see [Manage events]().

## Event triggers

Event triggers are the specific actions the event listener tracks.

This event can track the following event triggers:

* **Form Submit** – Trigger when the form is submitted.

### Element selector

The element selector specifies which element on a page you want to trigger the event listener. For more information, see [Event element selector]().

### Trigger frequency

The trigger frequency determines how many times the event trigger will result in a tracking call. For more information, see [Event triggers]().

## Event trigger variables

Event trigger variables are the values the event listener sends with the tracking call. The form submission event has following default event trigger variable:

### Form Submission

|Identifier| Description|
|---| ---|
|`tealium_event=&#34;form_submission&#34;`| The visitor submitted a form.|
|`iq_event_id` | The UID of the event listener that sent the event.|

**Example**

```json
{
   &#34;tealium_event&#34;  : &#34;form_submission&#34;,
   &#34;iq_event_id:&#34; : &#34;form_submit_events_1&#34;
}

```
