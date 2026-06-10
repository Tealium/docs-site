---
title: Omnichannel File Status API endpoints
description: Use the File Import Status GET request to retreive detailed status information for your files.
url: https://docs.tealium.com/api-v1/omnichannel-file-status/endpoints/
---
This is an older version of the [current Tealium Omnichannel File Status API]().


## File count

Returns the count of uploaded files. Only applies to files with the same file prefix.

The following query parameters are used:

* **filePrefix** - the file prefix matching the Omnichannel file definition, for example `sales_transactions`.
* **startDate** - the start date of a range of files to query, for example `2017-01-01T12:34Z`.
* **endDate** - the end date of a range of files to query, for example `2017-01-08T12:34Z`.

```
GET /v1/omnichannel/accounts/{account}/profiles/{profile}/files/count?utk={utk token}&amp;filePrefix={file prefix}&amp;startDate={start date}&amp;endDate={end date}
```

### cURL request

```bash
cURL -i -b JSESSIONID={session_id} \
  https://api.tealiumiq.com/v1/omnichannel/accounts/{account}/profiles/{profile}/files/count?utk={token}&amp;filePrefix={filePrefix}&amp;startDate={startDate}&amp;endDate={endDate}
```

If the file count exceeds 50, try narrowing the date range parameters.

### Example response

```json
{
    &#34;count&#34; : 42
}
```

### Error messages

|Error Type| Description|
|---| ---|
|400 Bad request|  * File Definition prefix exceeds 150 chars&lt;br&gt; * File Definition prefix, start date, or end date not supplied&lt;br&gt; * Start/End date format is invalid&lt;br&gt; * End date is before Start date |

## Single file status

```
GET /v1/omnichannel/accounts/{account}/profiles/{profile}/files/{fileName}?utk={utk token}
```

### cURL request

```bash
cURL -i -b JSESSIONID={session_id} \
  https://api.tealiumiq.com/v1/omnichannel/accounts/{account}/profiles/{profile}/files/{filename}.csv?utk={utk token} \
  -o {filename}.txt

```

### Example response

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

|Error Type| Description|
|---| ---|
|404 Not Found| Supplied file name not found|
|400 Bad request| File name exceeds 150 chars|

## Multiple file statuses

Returns an array of file statuses within the specified date range. Only applies to files with the same file prefix.

```
GET /v1/omnichannel/accounts/{account}/profiles/{profile}/files/search?utk={utk token}&amp;filePrefix={filePrefix}&amp;startDate={startDate}&amp;endDate={endDate}
```

### cURL request

```bash
cURL -i -b JSESSIONID={session_id} \
  https://api.tealiumiq.com/v1/omnichannel/accounts/{account}/profiles/{profile}/files/search?utk={token}&amp;filePrefix={filePrefix}&amp;startDate={startDate}&amp;endDate={endDate} \
  -o {filename}.txt
```

### Example response

Below is a sample file status for three files that are all prefixed by `sales-transaction`. Each file prefix is followed by `_` and a unique date identifier. Each file entry contains information about the file size, line count, and number of lines processed (including any processing errors).

```json
[
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
  },
  {
    &#34;_id&#34;: {
      &#34;$oid&#34;: &#34;5702ea6bb993f8f8cbea334b&#34;
    },
    &#34;account&#34;: &#34;acme&#34;,
    &#34;created_at&#34;: {
      &#34;$date&#34;: &#34;2016-04-04T22:27:55.562Z&#34;
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
          &#34;$date&#34;: &#34;2016-04-04T22:27:55.601Z&#34;
        }
      },
      {
        &#34;state&#34;: &#34;DOWNLOADED&#34;,
        &#34;timestamp&#34;: {
          &#34;$date&#34;: &#34;2016-04-04T22:27:55.887Z&#34;
        }
      },
      {
        &#34;state&#34;: &#34;PROCESSING&#34;,
        &#34;timestamp&#34;: {
          &#34;$date&#34;: &#34;2016-04-04T22:27:56.045Z&#34;
        },
        &#34;lines_skipped&#34;: 34
      },
      {
        &#34;state&#34;: &#34;PROCESSED&#34;,
        &#34;timestamp&#34;: {
          &#34;$date&#34;: &#34;2016-04-04T22:27:56.669Z&#34;
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
      &#34;$date&#34;: &#34;2016-04-04T22:27:53.276Z&#34;
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
          &#34;$date&#34;: &#34;2016-04-04T22:27:53.307Z&#34;
        }
      },
      {
        &#34;state&#34;: &#34;DOWNLOADED&#34;,
        &#34;timestamp&#34;: {
          &#34;$date&#34;: &#34;2016-04-04T22:27:54.249Z&#34;
        }
      },
      {
        &#34;state&#34;: &#34;PROCESSING&#34;,
        &#34;timestamp&#34;: {
          &#34;$date&#34;: &#34;2016-04-04T22:27:54.289Z&#34;
        },
        &#34;lines_skipped&#34;: 34
      },
      {
        &#34;state&#34;: &#34;PROCESSED&#34;,
        &#34;timestamp&#34;: {
          &#34;$date&#34;: &#34;2016-04-04T22:27:55.480Z&#34;
        }
      }
    ]
  },

```

### Error messages

|Error Type| Description|
|---| ---|
|400 Bad request|  * File Definition prefix exceeds 150 chars&lt;br&gt; * File Definition prefix, start date, or end date not supplied&lt;br&gt; * Start/End date format is invalid&lt;br&gt; * End date is before Start date |

## Omnichannel file errors

File processing can fail for many reasons: invalid service credentials, missing row data, internal server error, etc. In the File Status, these specific errors are logged in the value of the `last_failure` key.

Here&#39;s a truncated sample of a file status:

```json
    ...
    {
        &#34;state&#34;: &#34;PROCESSING&#34;,
        &#34;timestamp&#34;: {
            &#34;$date&#34;: &#34;2016-10-05T18:09:54.014Z&#34;
        },
        &#34;lines_failed_processing&#34;: 1,
        &#34;last_failure&#34;: &#34;Failed to find attribute for column with id&#34;
    },
    ...
```

Below listed errors are specific to Omnichannel Files; they are different from the API endpoint errors.

### Processing and download errors

|Error message| What does it mean| How to resolve|
|---| ---| ---|
|Unknown file prefix, unable to parse file| File for the supplied prefix (name) could not be found. Either the file doesn&#39;t exist or there is a typographical error in the prefix.| Re-upload the file and double check the file prefix in the Omnichannel Definitions tab. If the error persists, please contact your Tealium Account Manager.|
|DBObject of size `{###}`` is over Max BSON size `{###}`| File is too large to be processed| Split up your file data into multiple file definitions|
|Failed to download (SFTP, S3) file| File could not be downloaded due to errors in your service credentials (see [File Import Service Configuration]()).|  * For SFTP, double check the Host name, user name, and password&lt;br&gt; * For S3/Tealium S3, double check the Access/Secret keys and Bucket/prefix |
|Invalid connection type&lt;br&gt; **OR**&lt;br&gt; Could not find required (SFTP, S3) configuration parameters for definition| Your service credentials (under [File Import Service Configuration]()) could not be authenticated.|  * For SFTP, double check the Host name, user name, and password&lt;br&gt; * For S3/Tealium S3, double check the Access/Secret keys and Bucket/prefix |

### Configuration and definition errors

These errors are caused by incorrect column mappings in the [Column Mapping screen]().

|Error Message| What does it mean| How to resolve|
|---| ---| ---|
|Failed to find attribute for column with id| AudienceStream could not generate an Omnichannel Attribute for the column name you mapped.| Replace the offending column header with a fresh instance and re-upload the file|
|Exception thrown while processing file| Unable to parse the value of your mapped column header into the Omnichannel Attribute| Replace the offending column value and re-upload the file.|
|Secondary visitor ID column= `{column_name_here}` does not exist in the file, unable to continue| The column header you mapped to the Visitor ID field does not exist in your file. This could be due to a typo or the header is not defined.| Make sure the column header you supplied matches what is in the file|
|`{date_format_here}` could not be parsed as a Date| The date format you specified for the mapped column name does not exist in your file.| Make sure the date format you supplied matches what is in the file|
|The number of columns to be processed `{##}` must match the number of CellProcessors `{##}`: check that the number of CellProcessors you have defined matches the expected number of columns being read/written| The column names you mapped under Omnichannel Attributes do not exist in your file. This could be due to a typo or the header is not defined.| Make sure the column header you supplied matches what is in the file|

### Internal server errors

These errors occur when the different servers processing your files are unable to communicate with each other.

* `Connection is already closed due to connection error; cause: com.rabbitmq.client.MissedHeartbeatException`
* `Can&#39;t connect to new replica set master [##.#.#.###:###], err: couldn&#39;t connect to server [##.#.#.###:###], error querying server`
* `DBClientBase::findN: transport error`
* `socket exception [SEND_ERROR]`

**Resolution**: Re-upload your file(s).
