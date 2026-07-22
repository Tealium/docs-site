---
title: Microsoft Azure Blob Storage Connector Setup Guide
description: This article describes how to set up the Microsoft Azure Blob Storage connector.
url: https://docs.tealium.com/server-side-connectors/microsoft-azure-blob-storage-connector/
---
## Batch Limits
This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see Batched Actions. Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 100,000
* Max time since oldest request: 60 minutes
* Max size of requests: 100 MB

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **Tenant ID**: The unique identifier for your Azure Active Directory instance, representing your organization.
* **Authentication type**: Select the authentication type. Available options are: Client credentials, Authorization Code flow (SSO), and Shared Access Signature (SAS).
* **Client ID**: The unique identifier assigned to your application registered in Azure Active Directory.
* **Client Secret**: The string that acts like a password, used by the application to authenticate with Azure Active Directory.
* **Shared Access Signature**: Provide the special set of query parameters that indicate how the resources may be accessed by Tealium.
* **Storage account name**: The unique name of your Azure Storage account, used to access storage services like Blob, File, Queue, and Table storage.
* **API version**: The API version compatible with your Azure Storage instance. By default: 2025-01-05.

## Actions

| Action Name | AudienceStream | EventStream |
| ----------- | :------------: | :---------: |
| Send Entire Event Data | ✗ | ✓ |
| Send Custom Event Data | ✗ | ✓ |
| Send Entire Visitor Data | ✓ | ✗ |
| Send Custom Visitor Data | ✓ | ✗ |
| Send Entire Log Event | ✗ | ✓ |
| Send Log Event | ✗ | ✓ |

### Send Entire Event Data

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Container | Select the container where you want to create the objects. This container represents the top-level storage unit within an account that organizes a set of blobs, similar to folders in a file system. |
| Blob Path | Specify the path to the Blob object where you want the data to be appended. |
| File Blob Suffix | If you want to dynamically add a suffix to the filename, for example, an attribute with the current timestamp, select it here. If multiple suffix values are provided, they are separated by an underscore character. |
| Record Suffix | <ul><li>A suffix to add on the end of each record as a delimiter.</li><li>The default is `Newline`. </li><li>Available options are `Newline` and `No Delimiter`.</li></ul> |
| Overwrite Existing Blob | If the Blob object already exists, overwrite it with the current data. If unchecked, the data is appended instead. When appending the data, each block consists of a group of `JSON` objects containing the payload with the data being forwarded from Tealium. |
| Print Attribute Names | By default, the attribute keys are used. If you want to use the attribute names as keys instead, enable this checkbox. Consider that the payload names reflect any updates to attribute names. |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60` minutes. The default value is `10` minutes. |

### Send Custom Event Data

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Container | Select the container where you want to create the objects. This container represents the top-level storage unit within an account that organizes a set of blobs, similar to folders in a file system. |
| Blob Path |  Specify the path to the Blob object where you want the data to be appended. |
| File Blob Suffix | If you want to dynamically add a suffix to the filename, for example, an attribute with the current timestamp, select it here. If multiple suffix values are provided, they are separated by an underscore character. |
| Record Suffix | <ul><li>A suffix to add on the end of each record as a delimiter.</li><li>The default is `Newline`. </li><li>Available options are `Newline` and `No Delimiter`.</li></ul> |
| Overwrite Existing Blob | If the Blob object already exists, overwrite it with the current data. If unchecked, the data is appended instead. When appending the data, each block consists of a group of `JSON` objects containing the payload with the data being forwarded from Tealium. |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60` minutes. The default value is `10` minutes. |

#### Message Data

| **Parameter** | **Description** |
| --- | --- |
| Template Variables | <ul><li>Provide template variables as data input for **Templates**. For more information and usage examples, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Name nested template variables with the dot notation. Example: `items.name.`</li><li>Nested template variables are typically built from data layer list attributes.</li></ul> |
| Templates | <ul><li>Provide templates to be referenced in the Message Data. For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).</li><li>Templates are injected by name with double curly braces into supported fields, For example, `{{SomeTemplateName}}`.</li></ul>|

### Send Entire Visitor Data

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Container | Select the container where you want to create the objects. This container represents the top-level storage unit within an account that organizes a set of blobs, similar to folders in a file system. |
| Blob Path |  Specify the path to the Blob object where you want the data to be appended. |
| File Blob Suffix | If you want to dynamically add a suffix to the filename, for example, an attribute with the current timestamp, select it here. If multiple suffix values are provided, they are separated by an underscore character. |
| Record Suffix | <ul><li>A suffix to add on the end of each record as a delimiter.</li><li>The default is `Newline`. </li><li>Available options are `Newline` and `No Delimiter`.</li></ul> |
| Overwrite Existing Blob | If the Blob object already exists, overwrite it with the current data. If unchecked, the data is appended instead. When appending the data, each block consists of a group of `JSON` objects containing the payload with the data being forwarded from Tealium. |
| Print Attribute Names | By default, the attribute keys are used. If you want to use the attribute names as keys instead, enable this checkbox. Consider that the payload names reflect any updates to attribute names. |
| Include Current Visit Data with Visitor Data | Select this option to include current visit data with visitor data. |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60` minutes. The default value is `10` minutes. |

### Send Custom Visitor Data

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Container | Select the container where you want to create the objects. This container represents the top-level storage unit within an account that organizes a set of blobs, similar to folders in a file system. |
| Blob Path |  Specify the path to the Blob object where you want the data to be appended. |
| File Blob Suffix | If you want to dynamically add a suffix to the filename, for example, an attribute with the current timestamp, select it here. If multiple suffix values are provided, they will be separated by an underscore character. |
| Record Suffix | <ul><li>A suffix to add on the end of each record as a delimiter.</li><li>The default is `Newline`. </li><li>Available options are `Newline` and `No Delimiter`.</li></ul> |
| Overwrite Existing Blob | If the Blob object already exists, overwrite it with the current data. If unchecked, the data is appended instead. When appending the data, each block consists of a group of `JSON` objects containing the payload with the data being forwarded from Tealium. |
| Message Data | <ul><li>Provide values to construct message data.</li><li>Template Support: reference template name to generate message data from the template. If using a template, map it to Custom Message Definition. Any other key-value pairs are ignored if the template is used.</li></ul> |
| Template Variables | <ul><li>Provide template variables as data input for **Templates**. For more information and usage examples, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Name nested template variables with the dot notation. Example: `items.name.`</li><li>Nested template variables are typically built from data layer list attributes.</li></ul> |
| Templates | <ul><li>Provide templates to be referenced in the Message Data. For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).</li><li>Templates are injected by name with double curly braces into supported fields, For example, `{{SomeTemplateName}}`.</li></ul>|
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60` minutes. The default value is `10` minutes. |

### Send Entire Log Event

Send connector error logs to this vendor. For more information, see [connector-error-logging](https://docs.tealium.com/connector-error-logging/).

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Container | Select the container where you want to create the objects. This container represents the top-level storage unit within an account that organizes a set of blobs, similar to folders in a file system. |
| Blob Path | Specify the path to the Blob object where you want the data to be appended. |
| Record Suffix | Suffix added to the end of each record to be used as a delimiter. Default: Comma with newline (`,\n`). Newline (`\n`). No Delimiter. |

### Send Log Event

See [Send Entire Log Event](#send-entire-log_event) for shared mapping options.

For information about resource, HTTP, result, and other log event attributes, see .