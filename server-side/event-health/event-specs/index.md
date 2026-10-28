---
title: Event specifications
description: Event specifications are a way to validate the quality of incoming data.
url: https://docs.tealium.com/server-side/event-health/event-specs/
---
## How it works

Event specifications (also referred to as "event specs") represent your [data layer](https://docs.tealium.com/an-introduction-to-the-data-layer/) for events. Event specifications allow the data quality of your events to be validated in real-time using the [live events chart](https://docs.tealium.com/about-live-events/) or event specification detail view.

Event specifications contain a set of definitions, which consist of:

* The `tealium_event` attribute, which represents the name of the event and the specification associated with it. For example, if the `tealium_event` attribute has a value of `video_complete`, the system looks for an event specification with the name `video_complete` to validate the incoming event against. Use event specifications to categorize and manage your events based on their purpose and expected data structure.
* A list of attributes that describe the data expected for that event. Attributes are individual pieces of information, such as `video_id`, `video_length`, or `video_platform`. By defining these attributes, you create a clear expectation of the data your system should receive. Defined attributes help teams maintain consistent data structures, reduce errors, and simplify troubleshooting.
* Their expected data types, such as string, number, or boolean. Defining data types helps ensure that each attribute contains the correct kind of information. Defined data types reduce errors, improve data consistency, and make it easier to validate and process events across different systems.
* Whether they are required for a valid event. Required attributes must be present in an event for it to be considered valid. Required attributes ensure that critical information is always included, which is essential for accurate analysis and decision-making.

During validation, each attribute is evaluated for presence, data type, and any configured data value rules. A required attribute that is missing or fails validation produces an invalid event. An optional attribute that is present but fails a type check or data value rule also produces an invalid event. Optional attributes that are absent from the event are not evaluated and do not affect the result. For information about configuring data value rules, see [Add a validation rule to an attribute](https://docs.tealium.com/manage-event-specifications/#add-a-validation-rule-to-an-attribute).


<blockquote>
Validation is limited to 100 attributes per event. Required attributes are evaluated first in alphabetical order, followed by optional attributes in alphabetical order. Attributes beyond the limit are not validated.
</blockquote>


Event specifications do not filter out data. Even if an event is invalid, the system still processes the event.

### Example event specification

For example, a `video_complete` event contains the following attributes and data:

```json
{
    "tealium_event"  : "video_complete", // name of event and specification
    "video_id"       : "xWlEk2i9r5Q",
    "video_length"   : 300,
    "video_name"     : "How to track videos in Tealium",
    "video_platform" : "YouTube",
}
```

An event specification for this `video_complete` event contains the following:

![](https://docs.tealium.com/images/server-side/whiteui-eventspecifications-videocomplete.png)
<!-- GAP: replace whiteui-eventspecifications-videocomplete.png with a screenshot of the video_complete spec showing defined types (String, Number) for each attribute, required toggles enabled for the four required attributes, and video_quality as an optional String attribute -->

* The `tealium_event` attribute identifies the event as `video_complete`.
* The **Definitions** table provides contextual information about the event and defines the required attributes, their expected data types, and whether they are required for a valid event.

### Benefits

Event specifications provide two primary benefits for data management:

* To standardize the implementation of events across all platforms.
* To evaluate the data quality of incoming events.

## Validation status attribute

After validation runs, events that match a specification carry the reserved `tealium_event_spec_status` string attribute in their payload.

The attribute has the following values:

| Status | Description |
|---|---|
| `PASS` | The event matches a specification and passes validation. |
| `FAIL` | The event matches a specification and fails validation. |
| Not present | The event does not match a specification, so the attribute is not added to the payload. |

The `tealium_event_spec_status` attribute is reserved. If an incoming event already contains this attribute, the value is removed before processing to prevent spoofing.

To use the validation status in downstream systems, define `tealium_event_spec_status` as an [event attribute](https://docs.tealium.com/manage-es-attributes/). No enrichment is required.

After you define the attribute, you can use it in connectors, event feeds, and other features that support event attributes.

## View event specification statistics

![](https://docs.tealium.com/images/server-side/event-health-table.png)

The **Event Health** window displays the total statistics for all event specifications. The table shows the statistics for each individual event specification. You can select a time frame to view the statistics for that period.

The **Event Health** window displays the following statistics:

* **Total Volume**  
The total number of events received in the selected time frame.
* **Valid Events**  
The number of events that satisfy the requirements of an active event specification. Valid events have a known value for the `tealium_event` attribute and all the required attributes from the specification. The more valid events you see, the better your data quality. Higher counts indicate your installations are sending the data expected in your specifications.
* **Invalid Events**  
The number of events that match an event specification but have at least one attribute that is missing or invalid. Required attributes that are missing or have the wrong data type, and optional attributes that are present with the wrong data type or that fail a configured data value rule, all produce an invalid event. These issues can be resolved by fixing the installation code that is sending the events or adjusting the event specification.
* **No Spec**  
The number of events that do not have a matching event specification. No Spec events either do not have the `tealium_event` attribute or do not have a corresponding event specification.

The **Defined Events** table lists all existing event specifications and the **Total Volume**, **Valid Events**, **Invalid Events**, and **No Spec** statistics for each event specification.

## View event specification details

Click any event specification in the **Defined Events** table to view its details.

Statistics about the event specification are displayed at the top of the page, including the total volume of events matching the specification, and the percentage of valid, invalid, and no-spec events.

The **Definitions** table provides contextual information about the event and defines the required attributes, their expected data types, and whether they are required for a valid event.

### Code sample  

From the event specification details window, click **Code** and select the data source you are using to display the base code and examples to use for this event specification.

The following code sample demonstrates the tracking code for the `video_complete` event for a data source named `My iOS App`:

![](https://docs.tealium.com/images/server-side/whiteui-eventstream-eventspecifications-viewcode.png)

## Event specifications in live events

After you create an event specification and implement the tracking code, use the live events chart to view incoming events in real-time and evaluate their data quality.

For more information, see [Live events](https://docs.tealium.com/about-live-events/#event-specification-display-filters).