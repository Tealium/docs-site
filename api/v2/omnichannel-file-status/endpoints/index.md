---
title: Omnichannel file status API endpoints
description: Use the File Import Status GET request to retreive detailed status information for your files.
url: https://docs.tealium.com/api/v2/omnichannel-file-status/endpoints/
---## GET file count
File Count returns a count of uploaded files and only applies to files with the same file prefix. 

Use the following GET command to obtain a file count:

```bash
GET /v2/omnichannel/accounts/{account}/profiles/{profile}/files/count
```

### File count operation parameters

File Count uses the following query parameters:

| Parameter | Type | Description |
|---|---|---|
| `filePrefix` | string | The file prefix matching the Omnichannel file definition, such as `sales_transactions`. |
| `startDate` | date | The start date of a range of files to query, for example `2017-01-01T12:34Z`. |
| `endDate` | date | The end date of a range of files to query, for example  `2017-01-08T12:34Z`. |

### Example cURL request

Use the following cURL command for File Count:

```bash
curl -H &#39;Authorization: Bearer {token}&#39; \
https://api.tealiumiq.com/v2/omnichannel/accounts/{account}/profiles/{profile}/files/count?filePrefix={file prefix}&amp;amp;startDate={startDate}&amp;amp;endDate={endDate}
```

If the file count exceeds 50, narrow the date range parameters to reduce the number of returns.

### Example response

The following example shows a typical response generated from the cURL command:

```
{
    &#34;count&#34; : 42
}
```

### Error messages

Potential error messages for this task are:

|Error Code| Error Message|
|---| ---|
|400 Bad request|  * File Definition prefix exceeds 150 characters&lt;/br&gt; * File Definition prefix, start date, or end date is not supplied&lt;/br&gt; * Start or End date format is invalid&lt;/br&gt; * End date is before Start date |

## GET single file status

Use the following GET command to retrieve the status of a single file:

```bash
GET /v2/omnichannel/accounts/{account}/profiles/{profile}/files/{filename}
```

### Example cURL request

Use the following cURL command to retrieve the status of a single file:

```bash
curl -H &#39;Authorization: Bearer {token}&#39; \
&#39;https://api.tealiumiq.com/v2/omnichannel/accounts/{account}/profiles/{profile}/files/{filename}.csv&#39;
-o {filename}.txt
```

Designated .csv filenames should not be similar and must be distinctly different.

### Example response

The following example shows a typical response generated from the cURL command:

```json
{
    &#34;_id&#34;: {
      &#34;$oid&#34;: &#34;5702ea6db993f8f8cbea334c&#34;
    },
    &#34;account&#34;: &#34;acme&#34;,
    &#34;created_at&#34;: {
      &#34;$date&#34;: &#34;2016-04-04T22:27:56.993Z&#34;
    },
    &#34;file&#34;: {
      &#34;name&#34;: &#34;sales-transaction_2016feb4v50.csv&#34;,
      &#34;size&#34;: 2744,
      &#34;checksum&#34;: &#34;44b12d35ea9fffdeeb69f98b03004f22&#34;,
      &#34;source&#34;: {
        &#34;type&#34;: &#34;s3&#34;,
        &#34;host&#34;: &#34;johndoe:&#34;
      },
      &#34;line_count&#34;: 35
    },
    &#34;node_id&#34;: &#34;bulk_downloader_i-cd504b49&#34;,
    &#34;profile&#34;: &#34;main&#34;,
    &#34;status&#34;: [
      {
        &#34;state&#34;: &#34;DOWNLOADING&#34;,
        &#34;timestamp&#34;: {
          &#34;$date&#34;: &#34;2016-04-04T22:27:57.285Z&#34;
        }
      },
      {
        &#34;state&#34;: &#34;DOWNLOADED&#34;,
        &#34;timestamp&#34;: {
          &#34;$date&#34;: &#34;2016-04-04T22:27:57.722Z&#34;
        }
      },
      {
        &#34;state&#34;: &#34;PROCESSING&#34;,
        &#34;timestamp&#34;: {
          &#34;$date&#34;: &#34;2016-04-04T22:27:57.780Z&#34;
        },
        &#34;lines_skipped&#34;: 34
      },
      {
        &#34;state&#34;: &#34;PROCESSED&#34;,
        &#34;timestamp&#34;: {
          &#34;$date&#34;: &#34;2016-04-04T22:27:58.797Z&#34;
        }
      }
    ]
  }
```

### Error messages

Potential error messages for this task are:

|Error Code| Error Message|
|---| ---|
|404 Not Found| Supplied file name not found|
|400 Bad request|  File name exceeds 150 characters|

## Multiple file statuses

Returns an array of file statuses within the specified date range. Multiple File Statuses only applies to files with the same file prefix.

Use the following GET command to retrieve the status of multiple files for a specific date range.  For startDate and endDate, specify the date and time in this format - 2016-07-31T13:45-0700

```bash
GET /v2/omnichannel/accounts/{account}/profiles/{profile}/files/search?filePrefix={filePrefix}&amp;amp;startDate={startDate}&amp;amp;endDate={endDate}
```

### Example cURL request

Use the following cURL command to retrieve the status of multiple files for a specific date range:

```bash
curl -H &#39;Authorization: Bearer {token}&#39; \
&#39;https://api.tealiumiq.com/v2/omnichannel/accounts/{account}/profiles/{profile}/files/search?filePrefix={filePrefix}&amp;amp;startDate={startDate}&amp;amp;endDate={endDate}&#39; \
-o {filename}.txt
```

### Example response

The following sample file status shows three files with the following criteria:

* Each file is prefixed by `sales-transaction`
* Each file prefix is followed by `&#34;_&#34;`, and a unique date identifier
* Each file entry contains information about the file size, line count (number of rows), and number of lines processed (including any processing errors)

```json
[
  {
    &#34;_id&#34;: {
    &#34;$oid&#34;: &#34;5702ea6db993f8f8cbea334c&#34;
    },
    &#34;account&#34;: &#34;acme&#34;,
    &#34;created_at&#34;: {
      &#34;$date&#34;: &#34;2017-04-04T22:27:56.993Z&#34;
    },
    &#34;file&#34;: {
      &#34;name&#34;: &#34;sales-transaction_2016feb4v50.csv&#34;,
      &#34;size&#34;: 2744,
      &#34;checksum&#34;: &#34;44b12d35ea9fffdeeb69f98b03004f22&#34;,
      &#34;source&#34;: {
        &#34;type&#34;: &#34;s3&#34;,
        &#34;host&#34;: &#34;johndoe:&#34;
      },
      &#34;line_count&#34;: 35
    },
    &#34;node_id&#34;: &#34;bulk_downloader_i-cd504b49&#34;,
    &#34;profile&#34;: &#34;main&#34;,
    &#34;status&#34;: [
      {
        &#34;state&#34;: &#34;DOWNLOADING&#34;,
        &#34;timestamp&#34;: {
          &#34;$date&#34;: &#34;2017-04-04T22:27:57.285Z&#34;
        }
      },
      {
        &#34;state&#34;: &#34;DOWNLOADED&#34;,
        &#34;timestamp&#34;: {
          &#34;$date&#34;: &#34;2017-04-04T22:27:57.722Z&#34;
        }
      },
      {
        &#34;state&#34;: &#34;PROCESSING&#34;,
        &#34;timestamp&#34;: {
          &#34;$date&#34;: &#34;2017-04-04T22:27:57.780Z&#34;
        },
        &#34;lines_skipped&#34;: 34
      },
      {
        &#34;state&#34;: &#34;PROCESSED&#34;,
        &#34;timestamp&#34;: {
          &#34;$date&#34;: &#34;2016-04-04T22:27:58.797Z&#34;
        }
      }
    ]
  },
  {
    &#34;_id&#34;: {
      &#34;$oid&#34;: &#34;5702ea6bb993f8f8cbea334b&#34;
    },
    &#34;account&#34;: &#34;acme&#34;,
    &#34;created_at&#34;: {
      &#34;$date&#34;: &#34;2017-04-04T22:27:55.562Z&#34;
    },
    &#34;file&#34;: {
      &#34;name&#34;: &#34;sales-transaction_2016feb4v49.csv&#34;,
      &#34;size&#34;: 2744,
      &#34;checksum&#34;: &#34;7b8f92474e220c275bf9931c0337abf3&#34;,
      &#34;source&#34;: {
        &#34;type&#34;: &#34;s3&#34;,
        &#34;host&#34;: &#34;johndoe:&#34;
      },
      &#34;line_count&#34;: 35
    },
    &#34;node_id&#34;: &#34;bulk_downloader_i-cd504b49&#34;,
    &#34;profile&#34;: &#34;main&#34;,
    &#34;status&#34;: [
      {
        &#34;state&#34;: &#34;DOWNLOADING&#34;,
        &#34;timestamp&#34;: {
          &#34;$date&#34;: &#34;2017-04-04T22:27:55.601Z&#34;
        }
      },
      {
        &#34;state&#34;: &#34;DOWNLOADED&#34;,
        &#34;timestamp&#34;: {
          &#34;$date&#34;: &#34;2017-04-04T22:27:55.887Z&#34;
        }
      },
      {
        &#34;state&#34;: &#34;PROCESSING&#34;,
        &#34;timestamp&#34;: {
          &#34;$date&#34;: &#34;2017-04-04T22:27:56.045Z&#34;
        },
        &#34;lines_skipped&#34;: 34
      },
      {
        &#34;state&#34;: &#34;PROCESSED&#34;,
        &#34;timestamp&#34;: {
          &#34;$date&#34;: &#34;2017-04-04T22:27:56.669Z&#34;
        }
      }
    ]
  },
  {
    &#34;_id&#34;: {
      &#34;$oid&#34;: &#34;5702ea69b993f8f8cbea3349&#34;
    },
    &#34;account&#34;: &#34;acme&#34;,
    &#34;created_at&#34;: {
      &#34;$date&#34;: &#34;2017-04-04T22:27:53.276Z&#34;
    },
    &#34;file&#34;: {
      &#34;name&#34;: &#34;sales-transaction_2016feb4v53.csv&#34;,
      &#34;size&#34;: 2744,
      &#34;checksum&#34;: &#34;44b12d35ea9fffdeeb69f98b03004f22&#34;,
      &#34;source&#34;: {
        &#34;type&#34;: &#34;s3&#34;,
        &#34;host&#34;: &#34;johndoe:&#34;
      },
      &#34;line_count&#34;: 35
    },
    &#34;node_id&#34;: &#34;bulk_downloader_i-cd504b49&#34;,
    &#34;profile&#34;: &#34;profile&#34;,
    &#34;status&#34;: [
      {
        &#34;state&#34;: &#34;DOWNLOADING&#34;,
        &#34;timestamp&#34;: {
          &#34;$date&#34;: &#34;2017-04-04T22:27:53.307Z&#34;
        }
      },
      {
        &#34;state&#34;: &#34;DOWNLOADED&#34;,
        &#34;timestamp&#34;: {
          &#34;$date&#34;: &#34;2017-04-04T22:27:54.249Z&#34;
        }
      },
      {
        &#34;state&#34;: &#34;PROCESSING&#34;,
        &#34;timestamp&#34;: {
          &#34;$date&#34;: &#34;2017-04-04T22:27:54.289Z&#34;
        },
        &#34;lines_skipped&#34;: 34
      },
      {
        &#34;state&#34;: &#34;PROCESSED&#34;,
        &#34;timestamp&#34;: {
          &#34;$date&#34;: &#34;2017-04-04T22:27:55.480Z&#34;
        }
      }
    ]
  }
]
``` 

### Error messages

Potential error messages for this task are:

|Error Code| Error Message|
|---| ---|
|400 Bad request|  * File Definition prefix exceeds 150 characters&lt;/br&gt; * File Definition prefix, start date, or end date is not supplied&lt;/br&gt; * Start or End date format is invalid&lt;/br&gt; * End date is before Start date |

## Omnichannel file errors

File processing can fail for many reasons, such as invalid service credentials, missing row data, or an internal server error. In the File Status, specific errors are logged in the value of the `last_failure` key.

The following truncated sample shows the last failure for a file status:

```
   ...
    {
        &#34;state&#34;: &#34;PROCESSING&#34;,
        &#34;timestamp&#34;: {
            &#34;$date&#34;: &#34;2017-12-05T18:09:54.014Z&#34;
        },
        &#34;lines_failed_processing&#34;: 1,
        &#34;last_failure&#34;: &#34;Failed to find attribute for column with id&#34;
    },
    ...
```

The errors listed in the following sections below are specific to Omnichannel Files. These errors are different from API endpoint errors.

### Processing and download errors

The following table describes errors specific to processing and downloading and provides an explanation of the meaning and a resolution.

|Error message| Meaning| Resolution|
|---| ---| ---|
|`Unknown file prefix, unable to parse file`| File for the supplied prefix ( `name`) could not be found. Either the file does not exist or there is a typographical error in the prefix.| Re-upload the file and double check the file prefix in the [File Import Service Configuration](). If the error persists, contact your Tealium Account Manager.|
|`DBObject of size {###} is over Max BSON size {###}`| File is too large to be processed| Split your file data into multiple file definitions|
|`Failed to download (FTP, SFTP, S3) file`|  File could not be downloaded due to errors in your service credentials. See [File Import Service Configuration](). |  For FTP/SFTP, double check the host name, user name, and password. For S3/Tealium S3, double check the Access/Secret keys and Bucket/prefix |
| `Invalid connection type`&lt;br&gt; – **OR** – &lt;br&gt; `Could not find required (FTP, SFTP, S3) configuration parameters for definition`| Your service credentials under the [File Import Service Configuration]() could not be authenticated|  For FTP/SFTP, double check the host name, user name, and password. For S3/Tealium S3, double check the Access/Secret keys and Bucket/prefix |

### Configuration and definition errors

The following table describes errors are caused by incorrect column mappings in the File Import [Column Mapping screen]() and provides an explanation of the meaning and a resolution.

|Error Message| Meaning| Resolution|
|---| ---| ---|
|`Failed to find attribute for column with id`| AudienceStream could not generate an Omnichannel attribute for the mapped column name| Replace the offending column header with a fresh instance and re-upload the file|
|`Exception thrown while processing file`| Unable to parse the value of your mapped column header into the Omnichannel attribute| Replace the offending column value and re-upload the file|
|`Secondary visitor ID column= {column_name_here} does not exist in the file, unable to continue`| The column header mapped to the Visitor ID field does not exist in your file. This could be due to a typographical error or the header is not defined.| Ensure that the column header  supplied matches the column header in the file|
|`{date_format_here} could not be parsed as a Date`| The date format specified for the mapped column name does not exist in your file| Ensure that the date format you supplied matches the date format in the file|
|`The number of columns to be processed {##} must match the number of CellProcessors {##}: check that the number of CellProcessors you have defined matches the expected number of columns being read/written`| The column names mapped under Omnichannel attributes do not exist in your file. This could be due to a typographical error or the header is not defined.| Ensure that the column header  supplied matches the column header in the file|

### Internal server errors

The following errors occur when the different servers processing your files are unable to communicate with each other. To resolve these errors, re-upload your files.

* `Connection is already closed due to connection error; cause: com.rabbitmq.client.MissedHeartbeatException`

* `Can&#39;t connect to new replica set master [##.#.#.###:###], err: couldn&#39;t connect to server [##.#.#.###:###], error querying server`

*  `DBCClientBase::findN: transport error`

*  `socket exception [SEND_ERROR]`
