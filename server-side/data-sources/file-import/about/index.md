---
title: About file import
description: This article describes how to import CSV files as a data source, allowing you to enrich offline data and make it actionable within the Customer Data Hub.
url: https://docs.tealium.com/server-side/data-sources/file-import/about/
---
## Prerequisites 

* Tealium AudienceStream CDP **OR**
* Tealium EventStream API Hub


<blockquote>
To be successfully imported, you must format your CSV files correctly. For information on file and data formats, see [Prepare a CSV file for import](https://docs.tealium.com/prepare-a-csv-file-for-import/).
</blockquote>


## How it works

Use the Tealium server to connect to a file service (such as an Amazon S3 bucket), read the file, and import the data. Each imported row is processed as an event. After importing, the data can then be enriched, stitched to existing visitor profiles, and sent to other vendors.

### Processing rate

File import is a batched ingestion process for historical data and is not intended for real-time event data. 
File rows are processed at a variable rate based on the regional load in our multi-tenant environment, but most files are processed within 24 hours. 

For real-time processing of large volumes of event data, use any of the following:
* [HTTP API](https://docs.tealium.com/endpoint-spec/)
* [Advanced HTTP API](https://docs.tealium.com/http-api-advanced-incoming-webhook-setup-guide/)

### Events

In the default Tealium [data collection order of operations](https://docs.tealium.com/server-side-order-of-operations/), events from a file import data source are processed before the _Event received_ step and do not change the order of operations.

File import events are sent to EventStream and AudienceStream in the same way as events from other data sources with the following important exceptions:

* **Browser-specific attributes**: Browser-specific attributes, such as user agent, are not populated.
* **Enrichments**: Enrichments on pre-loaded attributes in AudienceStream are not run, except the **First Visit** pre-loaded attribute.
* **Functions**: Data transformation functions are not run.
* **Single-page visits**: Incoming events are exempt from the single-page visit/visitors criteria. Single-page visits and visitors from other data sources are not persisted in AudienceStream. For more information about single-page visits/visitors, see [How are single-page visits processed in AudienceStream?](https://docs.tealium.com/single-event-visitor/) (requires Tealium login).
* **Visit length**: A visit started by a file import event lasts for 60 seconds.
* **Visitor ID mapping**: If you map an AudienceStream visitor ID attribute in your file import data source configuration, the visitor ID is set directly to the value of the column you choose.

Additionally, you can use the following event attributes with incoming data from a file import data source:

* `_source_file` (String) - The name of the file associated with the event.
* `_file_line_num` (Integer) - The line of the file associated with the event.


## Set up a file import data source

There are two steps in setting up a file import as a data source:

1. **Column mapping and file transfer service configuration**  
To set up a file import data source, map columns from your CSV file to event attributes in Tealium and select a file transfer service. 
<blockquote>
To assist with column mapping, upload a sample CSV file with your column labels and up to 1,000 rows of data.
</blockquote>

1. **Upload files to your file transfer service**  
After you set up your data source, upload your CSV files to your file service. File uploading is done outside of Tealium.

## Step 1: CSV column mapping and file transfer service configuration

### Column mapping

The column mapping configuration determines the event attributes that correspond to each column in the CSV file. The column names are often different from the attribute names in the Customer Data Hub, so this mapping ensures that the data is imported properly. For example, a CSV file might have a column named `postalCode`, but the matching event attribute is named `customer_zip`, so you need to map these columns to associate them.

Mappings can be configured based on an existing event specification or as a custom event.

#### Event specification mapping

Each row of the CSV file is processed as an event. When you select an event specification mapping, event attributes are pre-selected in the **Column Mapping** table. Each row is processed as an event of the selected specification, for example `tealium_event = "purchase"`.

#### Custom mapping

If you select a custom event mapping, specify the event attribute that corresponds to each CSV column. Each row is processed as an event with the following event identifier:

`tealium_event = "imported"`

#### Visitor ID mapping

To ensure your imported data is stitched with other sources, such as web, mobile, or HTTP API, ensure that every row in a file import source file has a column with a unique visitor ID. You can then map the visitor ID column and corresponding event attribute to a visitor ID attribute (a unique attribute type for visitor identification in AudienceStream). The value in the mapped event attribute is assigned to the `tealium_visitor_id` attribute and matched directly to any existing visitor profiles.

For more information about Visitor ID Mapping in AudienceStream, see [Visitor Identification using Tealium Data Sources](https://docs.tealium.com/visitor-identification-data-sources/).

### File transfer service

The file transfer service is a secure location where you upload the files to be imported. Tealium supports the following file transfer services:

* Amazon S3
  * [AWS S3 bucket](https://docs.tealium.com/aws-s3/)
  * [Tealium S3 bucket](https://docs.tealium.com/tealium-s3/)  
* [Microsoft Azure File/Blob Storage](https://docs.tealium.com/azure/)
* [SFTP](https://docs.tealium.com/sftp/)

#### Tealium S3 file retention

By using the Tealium S3 bucket in your file import configuration, you agree to the following file retention policy:

* **1-3 years** - One year after uploading files to the Tealium S3 bucket, the files will be moved to a repository for long-term storage. Files will be accessible for up to three years. Retrieving files from long-term storage will incur a minimal to moderate service charge depending on the size and number of items requested. To retrieve any file, contact Tealium Support.
* **3 years or more** - Three years after uploading files to the Tealium S3 bucket, files will be deleted permanently. If your business case requires storage for longer than three years, a longer data retention time must be explicitly stated in the customer contract. To request a longer retention policy, contact Tealium Support.

## Step 2: Upload your files to a file transfer service

After you complete your file import data source configuration, upload files to the file service you have selected.

Tealium uses the following order of operations to import files:
1. **Check for new files**  
The system checks the file transfer service for new files every 10 minutes.
1. **Copy new files**  
When a new file is detected, it is copied from the file transfer location and processed in the Customer Data Hub.
1. **Match Filename Prefix to File Import data source**  
The prefix of the filename is used to identify which file import data source to use when importing the data in the file.
1. **Process files**  
The header line is read to identify the attributes being imported. After reading the header line, the following processing is performed:
    1. **Visitor lookup** — The visitor ID is used to look up the visitor record in AudienceStream. If an existing visitor record is not found, a new one is created. 
<blockquote>
Grouping rows with the same visitor ID decreases the import time.
</blockquote>

    1. **Attribute enrichment** - The visitor record is enriched according to the attributes imported and the existing enrichments in your account.
