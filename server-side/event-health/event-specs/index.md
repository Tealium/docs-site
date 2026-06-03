---
title: Event specifications
description: Event specifications are a way to validate the quality of incoming data.
url: https://docs.tealium.com/server-side/event-health/event-specs/
---
## How it works

Event specifications (also referred to as &#34;event specs&#34;) represent your [data layer]() for events. Event specifications allow the data quality of your events to be validated in real-time using the [live events chart]() or event specification detail view.

Event specifications contain a set of definitions, which consist of:

* The `tealium_event` attribute, which represents the name of the event and the specification associated with it. For example, if the `tealium_event` attribute has a value of `video_complete`, the system looks for an event specification with the name `video_complete` to validate the incoming event against. This allows you to categorize and manage your events based on their purpose and expected data structure.
* A list of attributes that describe the data expected for that event. Attributes are individual pieces of information, such as `video_id`, `video_length`, or `video_platform`. By defining these attributes, you create a clear expectation of the data your system should receive. This helps teams maintain consistent data structures, reduce errors, and simplify troubleshooting.
* Their expected data types, such as string, number, or boolean. Defining data types helps ensure that each attribute contains the correct kind of information. This reduces errors, improves data consistency, and makes it easier to validate and process events across different systems.
* Whether they are required for a valid event. Required attributes must be present in an event for it to be considered valid. This ensures that critical information is always included, which is essential for accurate analysis and decision-making.

Event specifications do not filter out data. Even if an event is invalid, the system still processes the event.

### Example event specification

For example, a `video_complete` event contains the following attributes and data:

```json
{
    &#34;tealium_event&#34;  : &#34;video_complete&#34;, // name of event and specification
    &#34;video_id&#34;       : &#34;xWlEk2i9r5Q&#34;,
    &#34;video_length&#34;   : 300,
    &#34;video_name&#34;     : &#34;How to track videos in Tealium&#34;,
    &#34;video_platform&#34; : &#34;YouTube&#34;,
}
```

An event specification for this `video_complete` event contains the following:

![](/images/server-side/whiteui-eventspecifications-videocomplete.png)

* The `tealium_event` attribute identifies the event as `video_complete`.
* The **Definitions** table provides contextual information about the event and defines the required attributes, their expected data types, and whether they are required for a valid event.

### Benefits

Event specifications provide two primary benefits for data management:

* To standardize the implementation of events across all platforms.
* To evaluate the data quality of incoming events.

## View event specification statistics

![](/images/server-side/event-health-table.png)

The **Event Health** window displays the total statistics for all event specifications. The table shows the statistics for each individual event specification. You can select a time frame to view the statistics for that period.

The following statistics are displayed:

* **Total Volume**  
The total number of events received in the selected time frame.
* **Valid Events**  
The number of events that satisfy the requirements of an active event specification. This means that the events have a known value for the `tealium_event` attribute and all the required attributes from the specification. The more valid events you see, the better your data quality. This means your installations are sending the data expected in your specifications.
* **Invalid Events**  
The number of events that match an event specification, but do not have the required attributes. This means that the events have a known value for the `tealium_event` attribute, but they are either missing required attributes or the attributes contain unexpected values. These issues can be resolved by fixing the installation code that is sending the events or adjusting the event specification.
* **No Spec**  
The number of events that do not have a matching event specification. This means that the events either do not have the `tealium_event` attribute or the value does not have a corresponding event specification.

The **Defined Events** table lists all existing event specifications and these statistics for each event specification.

## View event specification details

Click any event specification in the **Defined Events** table to view its details.

Statistics about the event specification are displayed at the top of the page, including the total volume of events matching the specification, the percentage of valid events, and the percentage of invalid events.

The **Definitions** table provides contextual information about the event and defines the required attributes, their expected data types, and whether they are required for a valid event.

### Code sample  

From the event specification details window, click **Code** and select the data source you are using to display the base code and examples to use for this event specification.

The following code sample demonstrates the tracking code for the `video_complete` event for a data source named `My iOS App`:

![](/images/server-side/whiteui-eventstream-eventspecifications-viewcode.png)

## Event specifications in live events

Once an event specification is created and the tracking code is implemented, use the live events chart to view incoming events in real-time to evaluate their data quality.

For more information, see [Live events]().