---
title: Work with your data cloud
description: Learn how Tealium works with your data cloud to import data as events, send data to the data cloud, and activate data in place without copying it.
url: https://docs.tealium.com/get-started/work-with-your-data-cloud/
---
A data cloud is a platform for storing and querying large datasets, such as Snowflake, Databricks, or Google BigQuery. Choose how Tealium works with your data cloud for each use case, based on whether the data needs to reach real-time visitor profiles.

## Import data from your data cloud as events

Cloud data sources read rows from a table or view in your data cloud. Tealium processes each row as an event, with columns mapped to event attributes. Tealium copies the imported data, so the data updates visitor profiles and triggers connectors like any other event.

Imports run at a frequency that you set, from near real time to weekly. Common imports include model scores, customer relationship management (CRM) attributes, and offline purchases.


![](https://docs.tealium.com/images/icons/icon-cloud-down.svg)

#### Cloud data sources

Import rows from your data cloud as events.


## Send data to your data cloud

Connectors stream event and visitor data to your data cloud. Tealium data storage also keeps copies of event and visitor data in raw and structured formats. Common uses include analysis, reporting, and model training.


![](https://docs.tealium.com/images/icons/icon-cloud-up.svg)

#### Snowflake streaming

Stream event and visitor data into Snowflake tables.



![](https://docs.tealium.com/images/icons/icon-database.svg)

#### Data storage

Store event and visitor data in raw and structured formats.


## Activate data in your data cloud

Warehouse activation (activation directly from your data cloud) reads rows from your data cloud, groups them into segments, and sends the segments to connectors without storing the data in Tealium. A segment is a group of rows that meet a set of conditions. Because warehouse activation is zero-copy, your data cloud stays the system of record.

Warehouse activation follows four stages:

1. A cloud data source connects to a table or view in your data cloud.
1. Tealium maps the table columns to attributes.
1. Conditions on those attributes define each segment.
1. Connectors send the segments to your destinations.

Warehouse activation runs in a separate server-side profile, and its data never reaches visitor profiles. Tealium evaluates segments each time it reads the table and does not store the segments. Common uses include batch marketing lists and suppression lists.


![](https://docs.tealium.com/images/icons/icon-cloud-up.svg)

#### Warehouse activation

Activate segments from your data cloud without storing data in Tealium.


## Choose a flow

The flows differ in whether Tealium copies the data and whether the data reaches visitor profiles:

| Flow | Copies data into Tealium | Updates visitor profiles | Common uses |
|---|---|---|---|
| Import as events | Yes | Yes | Model scores, CRM attributes, offline purchases |
| Send to your data cloud | Not applicable | No | Analysis, reporting, model training |
| Activate in place | No | No | Batch marketing lists, suppression lists |

To combine data cloud data with real-time behavior and identity, import the data as events, because only imported data updates visitor profiles. To analyze Tealium data or train models, send the data to your data cloud. To activate data cloud segments without copying data, activate the data in place.
