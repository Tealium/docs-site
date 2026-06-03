---
title: About data sources
description: This article describes the different types of data sources that you can use to send data to Tealium.
url: https://docs.tealium.com/server-side/data-sources/about-data-sources/
---
A data source represents a digital property that sends data to the Customer Data Hub. These systems include including websites, mobile apps, cloud data warehouses, offline data in the form of a CSV file, or any custom application that generates visitor event data. 

Examples of data source platforms:

* iQ Tag Management (websites)
* iOS (native mobile)
* Android (native mobile)
* HTTP API
* Apple TV
* Roku
* Python
* Java
* File import
* Cloud data warehouse (For example, Snowflake)

## How it works

Data sources are used to identify and keep track of the applications that send data to your Tealium account. Before you install Tealium in a new application or website, create a data source for it.

After you configure a data source, use Live Events to inspect and validate events coming into that data source.

A maximum of 10 cloud data warehouse data sources per profile can be enabled at a time.

### Platforms and APIs

When you create a platform or API data source, a unique value called a _data source key_ is generated. You will use the data source key in the installation code to match to the data source in your account. 

## Import offline data

Tealium supports several methods to import offline data into Tealium for enrichment and activation. Depending on your business case, your development support, and your import needs, you can select one of the following:

* **[File Import]()**  
For customers that have development support to compile offline data into CSVs.
* **[Data Connect]()**  
For customers that want a low-code solution to ingest data.
* **Tealium Collect API endpoint**   
For customers that have resources for development. Tealium Support recommended.

The following table summarizes the basic differences between the three import options.

| | **File Import**| **Data Connect**| **Collect API**|
|:---|:---|:---|:---|
|**Use case** |_For customers that have support to compile offline data into CSVs._ | _For customers that want a low-code solution to ingest data._ | _For customers that have resources for development. Tealium Support recommended._|
|**AudienceStream and EventStream**|&lt;ul&gt;&lt;li&gt;Included&lt;/li&gt;&lt;li&gt;Imported events count towards account usage&lt;/li&gt;&lt;/ul&gt;|&lt;ul&gt;&lt;li&gt;Not included&lt;/li&gt;&lt;li&gt;Imported events count towards account usage&lt;/li&gt;&lt;/ul&gt;|&lt;ul&gt;&lt;li&gt;Included&lt;/li&gt;&lt;li&gt;Imported events count towards account usage&lt;/li&gt;&lt;/ul&gt;|
|**Data import** | &lt;ul&gt;&lt;li&gt;Polls service configuration every 10 minutes&lt;/li&gt;&lt;/ul&gt; | &lt;ul&gt;&lt;li&gt;Closer to real-time&lt;/li&gt;&lt;/ul&gt; | &lt;ul&gt;&lt;li&gt;Real-time&lt;/li&gt;&lt;/ul&gt;|
|**Data sources**| &lt;ul&gt;&lt;li&gt;For large amounts of data, sometimes used to seed the platform&lt;/li&gt;&lt;li&gt;Have a file service provider, or can use Tealium S3&lt;/li&gt;&lt;/ul&gt;|&lt;ul&gt;&lt;li&gt;Need a connection to an outside system such as Snowflake, Hubspot, Salesforce, etc.&lt;/li&gt;&lt;li&gt;If needed, set schedule for importing&lt;/li&gt;&lt;/ul&gt;|&lt;ul&gt;&lt;li&gt;Higher volume of data&lt;/li&gt;&lt;li&gt;Need a programmatic way to interact with the platform&lt;/li&gt;&lt;/ul&gt;| 

