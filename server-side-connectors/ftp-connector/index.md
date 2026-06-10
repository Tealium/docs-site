---
title: File Transfer Protocol (SFTP, FTPS) Connector Setup Guide
description: This article describes how to set up the File Transfer Protocol connector.
url: https://docs.tealium.com/server-side-connectors/ftp-connector/
---
## Batch Limits

This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 100,000
* Max time since oldest request: 60 minutes
* Max size of requests: 200 MB

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:
* **Connection type**: (Required) Specify the connection type.
  * SFTP
  * FTPS
* **Host**: (Required) Specify the remote host.
* **Username**: (Required) Specify the username.
* **Password**: (Required) Specify the user password.
* **Port**: (Optional) Specify the port. If no port is specified, the following default ports will be used:
    * SFTP: 22
    * FTPS: 990

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Entire Event Data | ✗ | ✓ |
| Send Custom Event Data | ✗ | ✓ |
| Send Entire Visitor Data | ✓ | ✗ |
| Send Custom Visitor Data | ✓ | ✗ |
| Send Log Event  | ✗ | ✓ |
| Send Entire Log Event | ✗ | ✓ |

Enter a name for the action and select the action type .

The following section describes how to set up parameters and options for each action.

### Send Entire Event Data

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| File Type | Specify the file type. Possible values: `CSV` or `JSON`. |
| File Path | Specify the path to the file where data is appended. |
| File Path Suffix | Map a value to dynamically add a suffix to the file path. If multiple suffix values are provided, they are separated by an underscore character. |
| Overwrite Existing File | If the file already exists, overwrite it with the current data. If unchecked, the data is appended instead. When appending the data, each block consists of an array of a single JSON object or CSV line containing the payload with the data sent from Tealium. |
| Record Suffix | Suffix added to the end of each record to be used as a delimiter. Default: Newline (`\n`). Applicable only for files with JSON format. |
| Compress File | Set this to compress files using gzip. This option is ignored if **Overwrite existing file** is set to `false`. |

#### Batch Configuration

| **Parameter** | **Description** |
| --- | --- |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60`. Default: `15`. |
| Maximum file size | Maximum uncompressed file size in MB. Set a value between `1` and `200`. The default value is `90`. |
| Print Attribute Names | By default, attribute IDs are used as keys in the object data. Select this option to use the attribute names as keys instead. Note that if you rename attributes, the keys in the saved data may differ across files, potentially leading to inconsistencies. |

### Send Custom Event Data

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| File Type | Specify the file type. Possible values: `CSV` or `JSON`. |
| File Path | Specify the path to the file where data is appended. |

#### Message data

| **Parameter** | **Description** |
| --- | --- |
| Event Attribute | Define custom mappings between event attributes and vendor parameters. |
| File Path Suffix | Map a value to dynamically add a suffix to the file path. If multiple suffix values are provided, they are separated by an underscore character. |
| Overwrite Existing File | If the file already exists, overwrite it with the current data. If unchecked, the data is appended instead. When appending the data, each block consists of an array of a single JSON object or CSV line containing the payload with the data sent from Tealium. |
| Record Suffix | Suffix added to the end of each record to be used as a delimiter. Default: Newline (`\n`). Applicable only for files with JSON format. |
| Compress File | Set this to compress files using gzip. This option is ignored if **Overwrite existing file** is set to `false`. |

#### Batch Configuration

| **Parameter** | **Description** |
| --- | --- |
| Batch Time To Live |Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60`. Default: `15`. |
| Maximum file size | Maximum uncompressed file size in MB. Set a value between `1` and `200`. The default value is `90`. |
| Template Variables | Provide template variables as data input for **Templates**.&lt;br&gt;For usage examples, see [Template Variables Guide](/server-side/connectors/templates/template-variables/).&lt;br&gt;Name nested template variables with the dot notation. Example: `items.name`.&lt;br&gt;Nested template variables are typically built from data layer list attributes. |
| Templates | Provide templates to be referenced in Message Data. For more information, see: [Templates Guide](/server-side/connectors/templates/about/).&lt;br&gt;Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`. |

### Send Entire Visitor Data

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| File Type | Specify the file type. Possible values: `CSV` or `JSON`. |
| File Path | Specify the path to the file where data is appended. |
| File Path Suffix | Map a value to dynamically add a suffix to the file path. If multiple suffix values are provided, they are separated by an underscore character. |
| Overwrite Existing File | If the file already exists, overwrite it with the current data. If unchecked, the data is appended instead. When appending the data, each block consists of an array of a single JSON object or CSV line containing the payload with the data sent from Tealium. |
| Record Suffix | Suffix added to the end of each record to be used as a delimiter. Default: Newline (`\n`). Applicable only for files with JSON format. |
| Compress File | Set this to compress files using gzip. This option is ignored if **Overwrite existing file** is set to `false`. |

#### Batch Configuration

| **Parameter** | **Description** |
| --- | --- |
| Batch Time To Live |Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60`. Default: `15`. |
| Maximum file size | Maximum uncompressed file size in MB. Set a value between `1` and `200`. The default value is `90`. |
| Print Attribute Names | By default, attribute IDs are used as keys in the object data. Select this option to use the attribute names as keys instead. Note that if you rename attributes, the keys in the saved data may differ across files, potentially leading to inconsistencies. |
| Include Current Visit Data | Include the current visit data with the visitor data. |

### Send Custom Visitor Data

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| File Type | Specify the file type. Possible values: `CSV` or `JSON`. |
| File Path | Specify the path to the file where data is appended. |

#### Message data

| **Parameter** | **Description** |
| --- | --- |
| File Path Suffix | Map a value to dynamically add a suffix to the file path. If multiple suffix values are provided, they are separated by an underscore character. |
| Overwrite Existing File | If the file already exists, overwrite it with the current data. If unchecked, the data is appended instead. When appending the data, each block consists of an array of a single JSON object or CSV line containing the payload with the data sent from Tealium. |
| Record Suffix | Suffix added to the end of each record to be used as a delimiter. Default: Newline (`\n`). Applicable only for files with JSON format. |
| Compress File | Set this to compress files using gzip. This option is ignored if **Overwrite existing file** is set to `false`. |

#### Batch Configuration

| **Parameter** | **Description** |
| --- | --- |
| Batch Time To Live |Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60`. Default: `15`. |
| Maximum file size | Maximum uncompressed file size in `MB`. Set a value between `1` and `200`. The default value is `90`. |
| Template Variables | Provide template variables as data input for **Templates**.&lt;br&gt;For usage examples, see [Template Variables Guide](/server-side/connectors/templates/template-variables/).&lt;br&gt;Name nested template variables with the dot notation. Example: `items.name`.&lt;br&gt;Nested template variables are typically built from data layer list attributes. |
| Templates | Provide templates to be referenced in Message Data. For more information, see: [Templates Guide](/server-side/connectors/templates/about/).&lt;br&gt;Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`. |

### Send Log Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| File Type | Specify the file type. Possible values: `CSV` or `JSON`. |
| File Path | Specify the path to the file where data is appended. |

#### Message data

| **Parameter** | **Description** |
| --- | --- |
| Event Attribute | Define custom mappings between event attributes and vendor parameters. |
| File Path Suffix | Map a value to dynamically add a suffix to the file path. If multiple suffix values are provided, they are separated by an underscore character. |
| Overwrite Existing File | If the file already exists, overwrite it with the current data. If unchecked, the data is appended instead. When appending the data, each block consists of an array of a single JSON object or CSV line containing the payload with the data sent from Tealium. |
| Record Suffix | Suffix added to the end of each record to be used as a delimiter. Default: Newline (`\n`). Applicable only for files with JSON format. |
| Compress File | Set this to compress files using gzip. This option is ignored if **Overwrite existing file** is set to `false`. |

### Send Entire Log Event 

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| File Type | Specify the file type. Possible values: `CSV` or `JSON`. |
| File Path | Specify the path to the file where data is appended. |
| Record Suffix | Suffix added to the end of each record to be used as a delimiter. Default: Newline (`\n`). Applicable only for files with JSON format. |
| Compress File | Set this to compress files using gzip. This option is ignored if **Overwrite existing file** is set to `false`. |