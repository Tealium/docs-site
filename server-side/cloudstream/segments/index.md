---
title: Manage CloudStream segments
description: This article provides information about how to manage CloudStream segments.
url: https://docs.tealium.com/server-side/cloudstream/segments/
---
## How it works

A CloudStream segment defines a set of records from a connected data cloud, such as Snowflake or Databricks, based on configurable conditions applied to attributes in that data source.

When activated, the segment queries the data cloud and retrieves only those records matching the defined criteria. Segment data is not persisted or stored in Tealium systems. After retrieving the data and sending it to configured connectors, Tealium discards it.

## View segments

Go to **CloudStream &gt; Segments** to view the **Segments Overview** page.

![](/images/early-access/cloudstream/cloudstream_segments_overview.png)

The **Segments Overview** table lists the following information about each segment:

* Name
* Total Processed: The total number of incoming data records that match the segment conditions, where at least one activation is configured and enabled.
* Date Modified
* Labels
* Activations
* Status: An active segment requires at least one working chain, with an active data source and an activation.

The more actions button lets you add labels to each segment or delete the segment.

Select checkboxes next to each activation and perform bulk actions to edit the labels on the segments or delete them.

## Add a segment

Use one of two methods to build a segment:

* Follow the steps in the [Segment Builder](#segment-builder).
* [Manually build the segment](#manual-builder).

If you see the error, `Segment creation requires Cloud Stream Connectors to be enabled in Settings`, use the following steps to enable connectors on your profile:

1. Go to **Admin menu** &gt; **Server-Side Settings** &gt; **CloudStream Connectors**.
1. Toggle on **Activate CloudStream Connectors**.
1. Click **Save**.

### Segment Builder

Click **Segment Builder**. The **Data Source Configuration** step appears.

#### Data source configuration

![](/images/early-access/cloudstream/cloudstream_data_source_selection.png)

Select a cloud data source for the segment.

If you do not have any data sources configured, click **&#43; Add Cloud Data Source**. For more information about configuring a cloud data source, see .

To duplicate a data source, select the data source and click **Duplicate**. Then enter a name for the new copy of the data source.

Each data source can connect to a single view or table at a time.

* If you need to connect to multiple tables or views from a data cloud, configure a separate data source for each table or view.
* If you want to combine data from multiple tables into data records that CloudStream can read in a segment, you need to join the tables or views at the data cloud into a single table or view and then use that joined table as the segment data source.

When you have finished setting up your data sources, click **Next**.

#### Segment configuration

![](/images/early-access/cloudstream/cloudstream_segment_configuration.png)

Use the following steps to configure the segment:

1. Enter a **Name** for the segment.
1. To add a condition, select an attribute, an operator, and a value.  
For operators that specify a time frame, select a value and the time frame.
1. To add another condition, click **&#43; Add Condition**.
1. If you want to add labels or enter any notes about the segment, click **More Options** and make your changes.

#### Segment activations

You can activate a segment through a connector or a function.

![](/images/early-access/cloudstream/cloudstream_segment_activation.png)

* To activate a segment through a connector, see .
* To activate a segment through a function, see .

The **Segment Activations** table lists the actions that you have configured.

Click **Next**.

#### Summary

The **Summary** page shows a diagram with the flow of data from the data sources to the segment you build and into the activations.

![](/images/early-access/cloudstream/cloudstream_segment_summary.png)

Click the more arrow to see the individual actions and functions for each activation.

Click **Save**, and then save and publish your profile.

### Manual builder

To build a segment manually:

1. Click **&#43; New Segment** to manually build a segment.
1. Enter a **Name** for the segment.
1. To add a condition, select an attribute, an operator, and a value.  
For operators that specify a time frame, select a value and the time frame.
1. To add another condition, click **&#43; Add Condition**.
1. If you want to add labels or enter any notes about the segment, click **More Options** and make your changes.
1. Click **Done**.

You will need to manually add a data source, configure it, add an activation, and configure the action or function.

## Manage segments

Click a segment to manage it.

![](/images/early-access/cloudstream/cloudstream_segment_details.png)

The **Segment Details** page lists the following information:

* **Created**: Who created the segment and when.
* **Modified**: Who last modified the segment and when.
* **Labels**: Any labels on the segment.

Click on any of the following tabs:

### Overview

The **Overview** window displays a data flow diagram which lists the data sources, the segments, and the activations. Click a data source to view the path from that data source through the segment to its connected activations:

![](/images/early-access/cloudstream/cloudstream_segment_path.png)

#### Manage data sources and activations

You can add or edit data sources for the segment, and you can add or edit activations on the segment.

1. After you add and configure a new data source, it appears as an **Unused Data Source**.
1. Click **Configuration** to add conditions to the segment to query the new data source attributes.
1. Click **Add Activation** to add an activation for the connector.
1. Select and configure the action or function.  
Be sure to select the data source you want the segment to use from the **Data Source** list.
1. The data flow diagram updates to include the new data source and activations.

Use the toggle in an activation to enable and disable it, or use the toggle next to the segment name to enable and disable all of its activations.

### Configuration

The **Configuration** window lets you edit the configuration of the segment. Update the conditions for the segment and click **Done**.

### Insights

The **Insights** window displays a summary and chart of the connector activations for the time range that you select:

* **Matched**: The number of imported records from any data source meeting the segment conditions, regardless of segment activity.
* **Processed**: The number of imported records from any data source meeting the active segment conditions and triggering an enabled activation.