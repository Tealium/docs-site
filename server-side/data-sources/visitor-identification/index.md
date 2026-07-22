---
title: Visitor identification using Tealium data sources
description: This article describes how visitor identification works for data you upload using a Tealium data source.
url: https://docs.tealium.com/server-side/data-sources/visitor-identification/
---

<blockquote>
Disabling Visitor ID Mapping in AudienceStream may cause errors in visitor stitching. For optimal visitor stitching results, keep visitor ID mapping enabled.
</blockquote>



## How it works

When you upload your offline customer data using the file import or Snowflake data sources, each imported row is processed as an event. To stitch your imported data with other sources such as web, mobile, or HTTP API, ensure that every row in your data source has a column with a unique visitor ID that associates the data to a customer.  


<blockquote>
For more information, see [About Visitor Stitching](https://docs.tealium.com/about-visitor-stitching/).
</blockquote>


Using visitor ID mapping, you can assign one or more visitor ID attributes values to visitor identification columns in your data. The value in the visitor ID column is assigned to `tealium_visitor_id` and matched to any existing visitor profiles. If no value is available for any column mapped to a visitor ID attribute, a random `tealium_visitor_id` value is generated.

The following example shows how the `tealium_visitor_id` for each row/event is constructed:

`__acme_main__1234_100120394__`

With the following parameters:
* `acme` - The account name.
* `main` - The Tealium Customer Data Hub profile name.
* `1234` - The numeric ID of the visitor ID attribute in AudienceStream.
* `100120394` - The value from the CSV file that is being set to the visitor ID attribute.

For more information about visitor IDs, see [Anonymous IDs, User Identifiers, and Visitor ID Attributes](https://docs.tealium.com/anonymous-user-visitor-id-attributes/).

## When to disable visitor ID mapping 

There are specific use cases when you do not need to have Visitor ID Mapping in AudienceStream enabled during your file import or Snowflake data source configurations:

* The Tealium profile does not have AudienceStream enabled.
* You are importing data that is based on the same anonymous visitor ID that AudienceStream has used to identify a user on the web or in an app. In this case, disable Visitor ID Mapping in AudienceStream and instead map the column containing this visitor ID directly to the event attribute `tealium_visitor_id`.

## When to use attribute enrichment (File Import only)

In the following cases, for optimal visitor stitching results, change the source data in your CSV file. If it is not possible to edit the CSV file data, use manual visitor ID attribute enrichment.

* The uploaded file may have incorrect values in the visitor identification columns. If you cannot filter data to ensure incorrect values are removed prior to uploading to Tealium, disable Visitor ID Mapping in AudienceStream and set up visitor ID enrichments manually. 
<blockquote>
If your files contain incorrect visitor ID values and visitor ID mapping is enabled, it will not be possible to validate the visitor ID values and may cause errors in visitor stitching.
</blockquote>

* You need to transform the data uploaded through file import before assigning it to a visitor ID. For example, you need to concatenate, lowercase, or apply a prefix or suffix to column values. We recommend including the required transformation as a column in the source CSV file when possible.  If you cannot include the transformation in the file itself, disable Visitor ID Mapping in AudienceStream and set up visitor ID enrichments manually. 
