---
title: Connector Insights: Amazon Ads Data Manager
description: Access Amazon Ads Data Manager insights to review audience dataset metrics.
url: https://docs.tealium.com/server-side-connectors/connector-insights-amazon-ads-data-manager/
---
## Overview

The Amazon Ads Data Manager connector insights is an integration with Amazon Ads that brings audience dataset metrics into Tealium.

## Access

To access connector insights, go to **AudienceStream &gt; Connectors**, find the Amazon Ads Data Manager connector action, and click **Insights**.

![](/images/server-side-connectors/connector-insights-btn.png)

## Metrics

The insights summary displays the following dataset metrics:

* **Upload Count**: The total number of records in this dataset. This includes all uploaded records, including audience remove requests, records without identity, and malformed records.
* **Accepted Count**: The number of records accepted in this dataset.
* **Records Resolved**: The number of records matched to recognized users in this dataset, including duplicates. If you uploaded multiple records for the same user, each user record resolved to an identity is counted.
* **Records with Identity**: The number of records received with an identifier in this dataset.
* **Invalid Records**: The number of records in the dataset rejected due to malformed data (for example, using a string in a number field) or that do not comply with the hashing standards. For more information, see [Amazon DSP: Format audience file for hashing](https://advertising.amazon.com/help/GCCXMZYCK4RXWS6C).
* **Match Records Percentage**: The percentage of records successfully matched in the dataset. The match rate is calculated by dividing **Records Resolved** by **Records with Identity**.
