---
title: About CloudStream
description: This article provides information about CloudStream.
url: https://docs.tealium.com/server-side/cloudstream/about/
---
CloudStream is a segment builder that activates customer data directly from your data cloud, without storing or loading data into Tealium. Designed primarily for batch marketing lists and warehouse activation, CloudStream lets you create and manage segments from your data cloud and activate them using supported connectors.

This reduces overhead in the following ways:

* No cost to replicate or synchronize data.
* Eliminate errors from data replication and synchronization.
* Simpler data governance.
* Reduce data management burden.

## Requirements

* Access to a data source (accounts and table permissions required).
* Credentials for activation destinations (email, SMS, ads platforms, etc.).
* Review data movement and compliance policies.
    * Ensure compliance with regulatory guidelines for data transfer, processing, and protection in CloudStream. Review policies to maintain privacy and security when activating data through platforms like Databricks or Snowflake.

## How it works

CloudStream connects directly to your data cloud, letting you activate customer data without moving or storing it in Tealium.

![](/images/early-access/cloudstream/cloudstream_workflow.png)

In a dedicated server-side profile, you define a data source to connect to a table or view in your data cloud, then map its columns to cloud attributes. You can add enrichments to further process the data in attributes, or enrich additional cloud attributes with averages or other calculations. Using these attributes, you build segments — groups of users or entities that meet specific criteria. Finally, you activate these segments by sending them to your chosen destinations through connectors.

CloudStream uses a dedicated CloudStream profile, keeping your workflow organized and separate from other Tealium products.

### Dedicated profile

CloudStream uses its own dedicated server-side profile, separate from other platform profiles. This separation lets you manage attributes, segments, rules, and connectors for large datasets and complex segments without impacting your AudienceStream or EventStream workflows.

 To create a dedicated CloudStream profile, contact Tealium Support.

### Data supply chain dashboard

![](/images/early-access/cloudstream/cloudstream_profile_dashboard.png)

The CloudStream data supply chain dashboard lists the following information:

* The number of cloud data sources configured.
* The number of data records received.
* The number of enrichments applied.
* The number of active segments.
* The number of functions and connector actions triggered.
* The number of connectors configured.

Tables list the cloud data sources, segments, and destinations (connectors and functions) configured in the profile.

### Data sources

Data sources are defined connections to your data cloud, such as Snowflake or Databricks. CloudStream connects to these data sources to retrieve and activate segments without storing the data in Tealium. This lets you work with large datasets directly from the cloud, leveraging the power of your existing data infrastructure.

![](/images/early-access/cloudstream/cloudstream_datasource_summary.png)

 You can connect to up to 10 data sources in a profile. 

CloudStream data sources are designed to work directly with data stored in a data cloud. Data remains in the data cloud and is only temporarily imported for activation through connectors, without being stored in Tealium.

Tealium data sources support two configurations to process data: basic and advanced. 

* Basic: Your data is imported using the default schema you specify in the data source configuration. You can process data from only one table or view.
* Advanced: You can select one or more tables to join using an advanced SQL editor. The tables can be from multiple schemas. 

 CloudStream only supports cloud data sources. 

For more information about cloud data sources, refer to the following articles:

*   
General information about data source features, such as supported data types, limits, SQL queries, query modes, processing information, and data mapping.
*    
Information about creating a data source connection, configuration, and mapping as well as instructions on how to test your configuration.

### Cloud attributes

Cloud attributes are defined when you create a data source in CloudStream. As you connect to a table in your data cloud, CloudStream analyzes the table’s columns, determines their data types, and generates corresponding cloud attributes. You can review and adjust these attribute mappings during the data source setup process to ensure they align with your activation needs.

![](/images/early-access/cloudstream/cloud_attributes.png)

Cloud attributes are identical to event attributes in structure and behavior, except that they cannot be marked as [restricted data]() and CloudStream does not contain [preloaded attributes]().

 If you need more than 500 attributes in a profile, contact your Customer Success Manager. 

For more information, see .

### Segments

Segments are groups of users or entities that meet a set of conditions based on the cloud attributes defined in your data source. Segments in CloudStream are not persisted in the system and are only dynamically evaluated in real time while data is imported from your data cloud and activated through connectors.

![](/images/early-access/cloudstream/cloudstream_segment_details.png)

For more information, see .

#### Segments with multiple data sources

You cannot directly join multiple data sources within CloudStream. However, you might want to combine multiple data sources into a segment that has a shared purpose, such as identifying high value customers or high potential prospects.

For example, suppose you want to create a single segment to find high potential prospects for buying a car from a prospects table and from a table of people who have taken a test drive. First, create a segment that includes each of these data sources. Then, set a filter for the prospects, use an OR condition, and set another filter for the test drive participants.

![](/images/early-access/cloudstream/cloudstream_combined_segment_details.png)

### Activations

Activations are the process of delivering segments to your marketing, analytics, and advertising platforms. You can set activations through connector actions or functions. For more information, see  and .

![](/images/early-access/cloudstream/cloudstream_segment_path.png)

You can output a segment to multiple connector actions or functions. However, each configured activation can only use data from the selected data source. If you want to activate data from additional data sources through an activation, configure a separate action or function for each data source.

 To enable CloudStream connectors and functions, go to **Admin menu** &gt; **Server-Side Settings** &gt; **CloudStream Connectors**, set **Activate CloudStream Connectors** to `On`, and click **Save**.  

## Comparison

The key differences between CloudStream, EventStream, and AudienceStream are:

| Feature               | CloudStream                | EventStream / AudienceStream         |
|-----------------------|----------------------------------|--------------------------------------|
| Data Source           | Data cloud (Snowflake, Databricks)      | Data cloud, web, mobile, server, API events      |
| Data Storage          | No data stored in Tealium        | Data loaded and stored in Tealium (Visitor profiles and DataAccess)    |
| Segment Persistence   | Dynamic, not persisted           | Persisted in visitor profiles        |
| Activations           | AudienceStream connectors and functions  | AudienceStream and EventStream connectors and functions                            |
| Connector Actions     | Separate for each data source    | Multiple data sources per action.   |
| Primary Use Case      | Batch/warehouse activation       | Real-time processing and activation    |