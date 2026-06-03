---
title: Google Cloud Storage Connector Setup Guide
description: This article describes how to set up the Google Cloud Storage connector.
url: https://docs.tealium.com/server-side-connectors/google-cloud-storage-connector/
---
## API information

This connector uses the following vendor API:

* API Name: Google Cloud Storage API
* API Version: v1
* API Endpoint: `https://storage.googleapis.com/`
* Documentation: [Google Cloud Storage API](https://cloud.google.com/storage/docs/json_api)

## Batch limits

This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see Batched Actions. Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 100,000
* Max time since oldest request: 10 minutes
* Max size of requests: 100 MB

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **Project ID**: Select the project ID to connect to.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Entire Event Data | ✗ | ✓ |
| Send Custom Event Data | ✗ | ✓ |
| Send Entire Visitor Data | ✓ | ✗ |
| Send Custom Visitor Data | ✓ | ✗ |
| Send Log Event | ✗ | ✓ |
| Send Entire Log Event | ✗ | ✓ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Send Entire Event Data

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Bucket | Select the bucket where you want to create the objects. |
| Object Path | Specify the path to the object where you want the data to be appended. |
| Object Path Suffix | Select an attribute to append to the file path as a dynamic suffix (for example, a timestamp). If multiple suffix values are provided, they are separated by an underscore character. |
| Record Suffix | &lt;ul&gt;&lt;li&gt;A suffix to add on the end of each record as a delimiter.&lt;/li&gt;&lt;li&gt;The default is `Newline`. &lt;/li&gt;&lt;li&gt;Available options are `Newline` and `No Delimiter`.&lt;/li&gt;&lt;/ul&gt; |
| Overwrite Existing Object | If the object already exists, overwrite it with the current data. If unchecked, the data is appended instead. When appending the data, each block consists of an array of a single object containing the payload with the data being forwarded from Tealium. |
| Print Attribute Names | By default, the attribute keys are used. If you want to use the attribute names as keys instead, enable this checkbox. Consider that the payload names will reflect the update if the attribute names are updated. |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60` minutes. The default value is `10` minutes. |

### Send Custom Event Data

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Bucket | Select the bucket where you want to create the objects. |
| Object Path | Specify the path to the object where you want the data to be appended. |

#### Message Data

| **Parameter** | **Description** |
| --- | --- |
| Event Attribute | Define custom mappings between event attributes and vendor parameters. |
| Object Path Suffix | Select an attribute to append to the file path as a dynamic suffix (for example, a timestamp). If multiple suffix values are provided, they are separated by an underscore character. |
| Record Suffix | &lt;ul&gt;&lt;li&gt;A suffix to add on the end of each record as a delimiter.&lt;/li&gt;&lt;li&gt;The default is `Newline`. &lt;/li&gt;&lt;li&gt;Available options are `Newline` and `No Delimiter`.&lt;/li&gt;&lt;/ul&gt; |
| Overwrite Existing Object | If the object already exists, overwrite it with the current data. If unchecked, the data is appended instead. When appending the data, each block will consist of an array of a single object containing the payload with the data being forwarded from Tealium. |
| Template Variables | &lt;ul&gt;&lt;li&gt;Provide template variables as data input for **Templates**. For more information and usage examples, see .&lt;/li&gt;&lt;li&gt;Name nested template variables with the dot notation. Example: `items.name.`&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes.&lt;/li&gt;&lt;/ul&gt; |
| Templates | &lt;ul&gt;&lt;li&gt;Provide templates to be referenced in the Message Data. For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected by name with double curly braces into supported fields, For example, `{{SomeTemplateName}}`.&lt;/li&gt;&lt;/ul&gt;|
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60` minutes. The default value is `10` minutes. |

### Send Entire Visitor Data

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Bucket | Select the bucket where you want to create the objects. |
| Object Path | Specify the path to the object where you want the data to be appended. |
| Object Path Suffix | Select an attribute to append to the file path as a dynamic suffix (for example, a timestamp). If multiple suffix values are provided, they are separated by an underscore character. |
| Record Suffix | &lt;ul&gt;&lt;li&gt;A suffix to add on the end of each record as a delimiter.&lt;/li&gt;&lt;li&gt;The default is `Newline`. &lt;/li&gt;&lt;li&gt;Available options are `Newline` and `No Delimiter`.&lt;/li&gt;&lt;/ul&gt; |
| Overwrite Existing Object | If the object already exists, overwrite it with the current data. If unchecked, the data is appended instead. When appending the data, each block consists of an array of a single object containing the payload with the data being forwarded from Tealium. |
| Print Attribute Names | By default, the attribute keys are used. If you want to use the attribute names as keys instead, enable this checkbox. Consider that the payload names will reflect the update if the attribute names are updated. |
| Include Current Visit Data with Visitor Data | Select this option to include current visit data with visitor data. |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60` minutes. The default value is `10` minutes. |

### Send Custom Visitor Data

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Bucket | Select the bucket where you want to create the objects. |
| Object Path | Specify the path to the object where you want the data to be appended. |

#### Message Data

| **Parameter** | **Description** |
| --- | --- |
| Object Path Suffix | Select an attribute to append to the file path as a dynamic suffix (for example, a timestamp). If multiple suffix values are provided, they are separated by an underscore character. |
| Record Suffix | &lt;ul&gt;&lt;li&gt;A suffix to add on the end of each record as a delimiter.&lt;/li&gt;&lt;li&gt;The default is `Newline`. &lt;/li&gt;&lt;li&gt;Available options are `Newline` and `No Delimiter`.&lt;/li&gt;&lt;/ul&gt; |
| Overwrite Existing Object | If the object already exists, overwrite it with the current data. If unchecked, the data will be appended instead. When appending the data, each block will consist of an array of a single object containing the payload with the data being forwarded from Tealium. |
| Template Variables | &lt;ul&gt;&lt;li&gt;Provide template variables as data input for **Templates**. For more information and usage examples, see .&lt;/li&gt;&lt;li&gt;Name nested template variables with the dot notation. Example: `items.name.`&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes.&lt;/li&gt;&lt;/ul&gt; |
| Templates | &lt;ul&gt;&lt;li&gt;Provide templates to be referenced in the Message Data. For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected by name with double curly braces into supported fields, For example, `{{SomeTemplateName}}`.&lt;/li&gt;&lt;/ul&gt;|
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60` minutes. The default value is `10` minutes. |

### Send Log Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Bucket | Select the bucket where you want to create the objects. |
| Object Path | Specify the path to the object where you want the data to be appended. |

#### Message Data

| **Parameter** | **Description** |
| --- | --- |
| Event Attribute | Define custom mappings between event attributes and vendor parameters. |
| Object Path Suffix | Select an attribute to append to the file path as a dynamic suffix (for example, a timestamp). If multiple suffix values are provided, they are separated by an underscore character. |
| Record Suffix | &lt;ul&gt;&lt;li&gt;A suffix to add on the end of each record as a delimiter.&lt;/li&gt;&lt;li&gt;The default is `Newline`. &lt;/li&gt;&lt;li&gt;Available options are `Newline` and `No Delimiter`.&lt;/li&gt;&lt;/ul&gt; |
| Overwrite Existing Object | If the object already exists, overwrite it with the current data. If unchecked, the data is appended instead. When appending the data, each block will consist of an array of a single object containing the payload with the data being forwarded from Tealium. |
| Template Variables | &lt;ul&gt;&lt;li&gt;Provide template variables as data input for **Templates**. For more information and usage examples, see .&lt;/li&gt;&lt;li&gt;Name nested template variables with the dot notation. Example: `items.name.`&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes.&lt;/li&gt;&lt;/ul&gt; |
| Templates | &lt;ul&gt;&lt;li&gt;Provide templates to be referenced in the Message Data. For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected by name with double curly braces into supported fields, For example, `{{SomeTemplateName}}`.&lt;/li&gt;&lt;/ul&gt;|
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60` minutes. The default value is `10` minutes. |

### Send Entire Log Event

Send connector error logs to this vendor. For more information, see .

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Bucket | Select the bucket where you want to create the objects. |
| Object Path | Specify the path to the object where you want the data to be appended. |
| Object Path Suffix | Select an attribute to append to the file path as a dynamic suffix (for example, a timestamp). If multiple suffix values are provided, they are separated by an underscore character. |
| Record Suffix | Suffix added to the end of each record to be used as a delimiter. Select either a newline (`\n`) or no delimiter. |