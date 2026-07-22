---
title: Cloud attributes
description: This article provides an overview of how cloud attributes are used and steps to add, duplicate, or remove an attribute.
url: https://docs.tealium.com/server-side/cloudstream/attributes/
---
![](https://docs.tealium.com/images/early-access/cloudstream/cloud_attributes.png)

Cloud attributes are the foundational data elements used within CloudStream. They are defined when you create a data source in CloudStream. As you connect to a table in your data cloud, CloudStream analyzes the table’s columns, determines their data types, and generates corresponding cloud attributes. 

![](https://docs.tealium.com/images/early-access/cloudstream/datasource_cloud_attribute_mapping.png)

The cloud data source supports all data types. Review and adjust attribute mappings during the data source setup process to ensure that each attribute's data type is correct and matches the requirements for data activation, such as segmentation or audience targeting.

In general, use the following data type mappings to ensure data is imported correctly:

| Cloud data       | Tealium                            |
|------------------|------------------------------------|
| Numeric          | Number attributes                  |
| String           | String attributes                  |
| Logical          | Boolean attributes                 |
| Date and time    | Date attributes                    |
| Arrays           | Array of strings, array of numbers, or array of booleans |
| Other            | String attributes                  |

For more information about data types, see [About cloud data sources > Data types](https://docs.tealium.com/about-cloud-data-sources/#data-types).

You can also select an existing cloud attribute in a mapping to reuse it across different data sources and segments within CloudStream.


<blockquote>
You can see your current cloud attribute total on the **Attributes** screen. If you need more than 500 attributes in a profile, [contact support](https://docs.tealium.com/support/).
</blockquote>


Cloud attributes are identical to event attributes in structure and behavior, except that they cannot be marked as restricted data and CloudStream does not contain preloaded attributes.

For more information, see [about-attributes](https://docs.tealium.com/about-attributes/).