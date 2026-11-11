---
title: About Data Cloud Activation
description: This article provides information about Data Cloud Activation.
url: https://docs.tealium.com/server-side/data-cloud-activation/about/
---
Data Cloud Activation is a feature that lets you create and manage segments directly from your data cloud, without storing or loading data into Tealium. Designed primarily for batch marketing lists and warehouse activation, Data Cloud Activation lets you create and manage segments from your data cloud and activate them using supported connectors.

This reduces overhead in the following ways:

* No cost to replicate or synchronize data.
* Eliminate errors from data replication and synchronization.
* Simpler data governance.
* Reduce data management burden.

## Requirements

* Access to a data source (accounts and table permissions required).
* Credentials for activation destinations (email, SMS, ads platforms, etc.).
* Review data movement and compliance policies.
    * Ensure compliance with regulatory guidelines for data transfer, processing, and protection in Data Cloud Activation. Review policies to maintain privacy and security when activating data through platforms like Databricks or Snowflake.

## How it works

Data Cloud Activation connects directly to your data cloud, letting you activate customer data without moving or storing it in Tealium.

![](https://docs.tealium.com/images/early-access/cloudstream/cloudstream_workflow.png)

In a dedicated server-side profile, you define a data source to connect to a table or view in your data cloud, then map its columns to cloud attributes. You can add enrichments to further process the data in attributes, or enrich additional cloud attributes with averages or other calculations. Using these attributes, you build segments — groups of users or entities that meet specific criteria. Finally, you activate these segments by sending them to your chosen destinations through connectors.

Data Cloud Activation uses a dedicated Data Cloud Activation profile, keeping your workflow organized and separate from other Tealium products.

### Dedicated profile

Data Cloud Activation uses its own dedicated server-side profile, separate from other platform profiles. This separation lets you manage attributes, segments, rules, and connectors for large datasets and complex segments without impacting your Customer Data Platform (CDP) or Event Streaming workflows.


<blockquote>
To create a dedicated Data Cloud Activation profile, contact Tealium Support.
</blockquote>


### Data supply chain dashboard

![](https://docs.tealium.com/images/early-access/cloudstream/cloudstream_profile_dashboard.png)

The Data Cloud Activation data supply chain dashboard lists the following information:

* The number of cloud data sources configured.
* The number of data records received.
* The number of enrichments applied.
* The number of active segments.
* The number of functions and connector actions triggered.
* The number of connectors configured.

Tables list the cloud data sources, segments, and destinations (connectors and functions) configured in the profile.

### Data sources

Data sources are defined connections to your data cloud, such as Snowflake or Databricks. Data Cloud Activation connects to these data sources to retrieve and activate segments without storing the data in Tealium. This lets you work with large datasets directly from the cloud, leveraging the power of your existing data infrastructure.

![](https://docs.tealium.com/images/early-access/cloudstream/cloudstream_datasource_summary.png)


<blockquote>
You can connect to up to 10 data sources in a profile.
</blockquote>


Data Cloud Activation data sources are designed to work directly with data stored in a data cloud. Data remains in the data cloud and is only temporarily imported for activation through connectors, without being stored in Tealium.

Tealium data sources support two configurations to process data: basic and advanced. 

* Basic: Your data is imported using the default schema you specify in the data source configuration. You can process data from only one table or view.
* Advanced: You can select one or more tables to join using an advanced SQL editor. The tables can be from multiple schemas. 


<blockquote>
Data Cloud Activation only supports cloud data sources.
</blockquote>


For more information about cloud data sources, refer to the following articles:

* [about-cloud-data-sources](https://docs.tealium.com/about-cloud-data-sources/)  
General information about data source features, such as supported data types, limits, SQL queries, query modes, processing information, and data mapping.
* [manage-cloud-data-source](https://docs.tealium.com/manage-cloud-data-source/)   
Information about creating a data source connection, configuration, and mapping as well as instructions on how to test your configuration.

### Cloud attributes

Cloud attributes are defined when you create a data source in Data Cloud Activation. As you connect to a table in your data cloud, Data Cloud Activation analyzes the table’s columns, determines their data types, and generates corresponding cloud attributes. You can review and adjust these attribute mappings during the data source setup process to ensure they align with your activation needs.

![](https://docs.tealium.com/images/early-access/cloudstream/cloud_attributes.png)

Cloud attributes are identical to event attributes in structure and behavior, except that they cannot be marked as [restricted data](https://docs.tealium.com/about-restricted-data/) and Data Cloud Activation does not contain [preloaded attributes](https://docs.tealium.com/preloaded-attributes/).


<blockquote>
If you need more than 500 attributes in a profile, [contact support](https://docs.tealium.com/support/).
</blockquote>


For more information, see [manage-data-cloud-activation-attributes](https://docs.tealium.com/manage-data-cloud-activation-attributes/).

### Segments

Segments are groups of users or entities that meet a set of conditions based on the cloud attributes defined in your data source. Segments in Data Cloud Activation are not persisted in the system and are only dynamically evaluated in real time while data is imported from your data cloud and activated through connectors.

![](https://docs.tealium.com/images/early-access/cloudstream/cloudstream_segment_details.png)

For more information, see [manage-data-cloud-activation-segments](https://docs.tealium.com/manage-data-cloud-activation-segments/).

#### Segments with multiple data sources

You cannot directly join multiple data sources within Data Cloud Activation. However, you might want to combine multiple data sources into a segment that has a shared purpose, such as identifying high value customers or high potential prospects.

For example, suppose you want to create a single segment to find high potential prospects for buying a car from a prospects table and from a table of people who have taken a test drive. First, create a segment that includes each of these data sources. Then, set a filter for the prospects, use an OR condition, and set another filter for the test drive participants.

![](https://docs.tealium.com/images/early-access/cloudstream/cloudstream_combined_segment_details.png)

### Activations

Activations are the process of delivering segments to your marketing, analytics, and advertising platforms. You can set activations through connector actions or functions. For more information, see [add-connector](https://docs.tealium.com/add-connector/) and [about-data-record-functions](https://docs.tealium.com/about-data-record-functions/).

![](https://docs.tealium.com/images/early-access/cloudstream/cloudstream_segment_path.png)

You can output a segment to multiple connector actions or functions. However, each configured activation can only use data from the selected data source. If you want to activate data from additional data sources through an activation, configure a separate action or function for each data source.


<blockquote>
To enable Data Cloud Activation connectors and functions, go to **Admin menu** > **Server-Side Settings** > **CloudStream Connectors**, set **Activate CloudStream Connectors** to `On`, and click **Save**.
</blockquote>


## Comparison

The key differences between Data Cloud Activation, Event Streaming, and CDP are:

| Feature               | Data Cloud Activation                | Event Streaming / CDP         |
|-----------------------|----------------------------------|--------------------------------------|
| Data Source           | Data cloud (Snowflake, Databricks)      | Data cloud, web, mobile, server, API events      |
| Data Storage          | No data stored in Tealium        | Data loaded and stored in Tealium (Visitor profiles and DataAccess)    |
| Segment Persistence   | Dynamic, not persisted           | Persisted in visitor profiles        |
| Activations           | CDP connectors and functions  | CDP and Event Streaming connectors and functions                            |
| Connector Actions     | Separate for each data source    | Multiple data sources per action.   |
| Primary Use Case      | Batch/warehouse activation       | Real-time processing and activation    |