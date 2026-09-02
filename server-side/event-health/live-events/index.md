---
title: Live events
description: The Live Events chart is used to inspect real-time incoming data. This article shows how to inspect and evaluate data quality.
url: https://docs.tealium.com/server-side/event-health/live-events/
---
## How it works

The live events chart displays events in real time coming from all data sources and all event feeds. Each bar in the chart has a height to indicate the volume of events detected. If you have active [event specifications](), the chart reflects the quality of the incoming data with color-coded segments: green for valid events, yellow for warn events, red for invalid events, and blue for events with no specification.

## Use live events

Access live events by going to **Validate > Live Events**.

![](https://docs.tealium.com/images/server-side/whiteui-eventstream-liveeventfeed.png)
<!-- GAP: replace whiteui-eventstream-liveeventfeed.png with a screenshot of the live events chart showing all four status segments including Warn (yellow) in the Event Specification Filters legend -->

You control which events are displayed in the chart using the **Data Sources** and **Event Feeds** lists. The default selections are **All Data Sources** and **All Events**. Adjusting these menus refreshes the chart and displays the event activity for the selected combination.

![](https://docs.tealium.com/images/server-side/whiteui-eventstream-liveevents-filter-drop-down-lists.png)

If you select a specific event for an event feed, the chart displays data for that event only. To compare an event feed to all event data, click **Compare against All Events**. For example, you can create event feeds for specific countries or regions, then compare a country or region event feed to all events.

## Use a trace ID

Use a trace ID to filter out all incoming events except for the ones you trigger. A trace ID is a temporary, unique identifier to be inserted into your event tracking code so that only specific events are displayed in the live events chart. For more information, see [About Trace](https://docs.tealium.com/about-trace/).

To set up a trace:

1. Click **Trace ID**.  
The trace options modal is displayed.
1. Click **Start Trace** and follow the instructions.
1. Copy the generated trace ID and click **Continue**.
1. Open a new Chrome browser window with the page to test.
1. Open **Tealium Tools > Trace** and enter the trace ID.  

The live events chart now shows only events triggered during your traced session. You can start a new trace or rejoin an existing trace following the same steps.

## Filter by specification status

If you have [event specifications]() defined, Live Events displays the quality of your incoming data. Each bar in the chart is segmented according to the status of the event specifications applied. The following filters can be toggled on or off to adjust the display of the chart:

![](https://docs.tealium.com/images/server-side/whiteui-eventstream-liveeventsandfeeds-event-specification-filters.png)
<!-- GAP: replace whiteui-eventstream-liveeventsandfeeds-event-specification-filters.png with a screenshot showing the filter legend with all four statuses: Valid (green), Warn (yellow), Invalid (red), and No Spec (blue) -->

* **Valid Events**  
These events satisfy the requirements of an active event specification. Valid events have a known value for the `tealium_event` attribute and all the required attributes from the specification. The more valid events you see the better, as higher counts indicate your installations are sending the data expected in your specifications.
* **Warn Events**  
These events match an event specification and all required attributes pass validation, but one or more optional attributes are missing, have the wrong data type, or don't match a configured data value rule.
* **Invalid Events**  
These events match an event specification, but have at least one required attribute that is missing, has the wrong data type, or doesn't match a configured data value rule. These issues can be resolved by fixing the installation code that is sending the events or, in some cases, adjusting the event specification.
* **No Spec**  
These events do not have a matching event specification. No Spec events either do not have the `tealium_event` attribute or do not have a corresponding event specification.


<blockquote>
Event specifications do not filter out data. Even if an event is invalid, the system still processes the event.
</blockquote>


## View event details

Click a bar in the chart to view the event details from an incoming data sample. The data sample is limited to 10 events per bar in the chart. Events are primarily identified by the `tealium_event` attribute. The detected value of this attribute is displayed in the heading of the event detail. If `tealium_event` has a corresponding event specification, the event is displayed as valid, warn, or invalid according to the requirements in the specification. The heading also displays the data source from which the event originated.

For example, a valid `cart_empty` event:

![](https://docs.tealium.com/images/server-side/whiteui-eventstream-live-events-and-feeds-valid-events-details.png)
<!-- GAP: replace whiteui-eventstream-live-events-and-feeds-valid-events-details.png with a screenshot of a valid event's detail view showing the green header and per-attribute spec validation results -->

The event attribute details are organized into the following attribute types: Universal Variable, JavaScript Page Variable, HTML Metadata, First-party Cookie, Query String Parameter, and Tealium-provided.

An invalid `cart_empty` event resembles the following:

![](https://docs.tealium.com/images/server-side/whiteui-eventstream-eventspecifications-invalid-event.png)
<!-- GAP: replace whiteui-eventstream-eventspecifications-invalid-event.png with a screenshot of an invalid cart_empty event detail view showing the red header with per-attribute validation results and failure reasons (missing required attribute or wrong data type) highlighted inline -->

The details view highlights each attribute's validation status inline and shows the reason for each failure, such as a missing required attribute or an incorrect data type.

## Define unknown attributes

An unknown attribute is an attribute detected in the incoming event that has not yet been created in your account as an event attribute with a data type (for example: string, number, boolean, etc.) Before you can use an attribute in your account, it must be created as an event attribute.

In the event details view, unknown attributes are indicated in the **Data Type** column as `Unknown`.

![](https://docs.tealium.com/images/server-side/whiteui-eventstream-liveeventsandfeeds-add-unknown-attribute.png)

Unknown attributes can be defined directly from this screen by using the **Quick Add** action, as follows:

1. Next to an unknown attribute, click the more options icon and then click **Quick Add**.
1. Select the data type.
1. Click **Define**.

The attribute now displays its new data type.

## Create an event specification

Events with a custom value for `tealium_event` are displayed as `Unknown` in the event details view if they do not have an associated event specification. When this occurs, create a custom event specification directly from the event details view based on the detected value of `tealium_event` and the attributes of the event.


<blockquote>
We recommend that you define unknown attributes before you create an event specification from a live event. For more information, see [Define unknown attributes](#define-unknown-attributes).
</blockquote>


For more information, see [Manage event specifications](https://docs.tealium.com/manage-event-specifications/#create-an event-specification).