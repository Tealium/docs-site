---
title: Omnichannel File Status API endpoints
description: Use the File Import Status GET request to retreive detailed status information for your files.
url: https://docs.tealium.com/api-v1/omnichannel-file-status/endpoints/
---
This is an older version of the [current Tealium Omnichannel File Status API](https://docs.tealium.com/about-file-import/).


## File count

Returns the count of uploaded files. Only applies to files with the same file prefix.

The following query parameters are used:

* **filePrefix** - the file prefix matching the Omnichannel file definition, for example `sales_transactions`.
* **startDate** - the start date of a range of files to query, for example `2017-01-01T12:34Z`.
* **endDate** - the end date of a range of files to query, for example `2017-01-08T12:34Z`.

```
GET /v1/omnichannel/accounts/{account}/profiles/{profile}/files/count?utk={utk token}&filePrefix={file prefix}&startDate={start date}&endDate={end date}
```

### cURL request

```bash
cURL -i -b JSESSIONID={session_id} \
  https://api.tealiumiq.com/v1/omnichannel/accounts/{account}/profiles/{profile}/files/count?utk={token}&filePrefix={filePrefix}&startDate={startDate}&endDate={endDate}
```


<blockquote>
If the file count exceeds 50, try narrowing the date range parameters.
</blockquote>


### Example response

```json
{
    "count" : 42
}
```

### Error messages

|Error Type| Description|
|---| ---|
|400 Bad request|  * File Definition prefix exceeds 150 chars<br> * File Definition prefix, start date, or end date not supplied<br> * Start/End date format is invalid<br> * End date is before Start date |

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
    "_id": {
      "$oid": "5702ea6db993f8f8cbea334c"
    },
    "account": "acme",
    "created_at": {
      "$date": "2016-04-04T22:27:56.993Z"
    },
    "file": {
      "name": "sales-transaction_2016feb4v50.csv",
      "size": 2744,
      "checksum": "44b12d35ea9fffdeeb69f98b03004f22",
      "source": {
        "type": "s3",
        "host": "johndoe:"
      },
      "line_count": 35
    },
    "node_id": "bulk_downloader_i-cd504b49",
    "profile": "main",
    "status": [
      {
        "state": "DOWNLOADING",
        "timestamp": {
          "$date": "2016-04-04T22:27:57.285Z"
        }
      },
      {
        "state": "DOWNLOADED",
        "timestamp": {
          "$date": "2016-04-04T22:27:57.722Z"
        }
      },
      {
        "state": "PROCESSING",
        "timestamp": {
          "$date": "2016-04-04T22:27:57.780Z"
        },
        "lines_skipped": 34
      },
      {
        "state": "PROCESSED",
        "timestamp": {
          "$date": "2016-04-04T22:27:58.797Z"
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
GET /v1/omnichannel/accounts/{account}/profiles/{profile}/files/search?utk={utk token}&filePrefix={filePrefix}&startDate={startDate}&endDate={endDate}
```

### cURL request

```bash
cURL -i -b JSESSIONID={session_id} \
  https://api.tealiumiq.com/v1/omnichannel/accounts/{account}/profiles/{profile}/files/search?utk={token}&filePrefix={filePrefix}&startDate={startDate}&endDate={endDate} \
  -o {filename}.txt
```

### Example response

Below is a sample file status for three files that are all prefixed by `sales-transaction`. Each file prefix is followed by `_` and a unique date identifier. Each file entry contains information about the file size, line count, and number of lines processed (including any processing errors).

```json
[
  {
    "_id": {
      "$oid": "5702ea6db993f8f8cbea334c"
    },
    "account": "acme",
    "created_at": {
      "$date": "2016-04-04T22:27:56.993Z"
    },
    "file": {
      "name": "sales-transaction_2016feb4v50.csv",
      "size": 2744,
      "checksum": "44b12d35ea9fffdeeb69f98b03004f22",
      "source": {
        "type": "s3",
        "host": "johndoe:"
      },
      "line_count": 35
    },
    "node_id": "bulk_downloader_i-cd504b49",
    "profile": "main",
    "status": [
      {
        "state": "DOWNLOADING",
        "timestamp": {
          "$date": "2016-04-04T22:27:57.285Z"
        }
      },
      {
        "state": "DOWNLOADED",
        "timestamp": {
          "$date": "2016-04-04T22:27:57.722Z"
        }
      },
      {
        "state": "PROCESSING",
        "timestamp": {
          "$date": "2016-04-04T22:27:57.780Z"
        },
        "lines_skipped": 34
      },
      {
        "state": "PROCESSED",
        "timestamp": {
          "$date": "2016-04-04T22:27:58.797Z"
        }
      }
    ]
  },
  {
    "_id": {
      "$oid": "5702ea6bb993f8f8cbea334b"
    },
    "account": "acme",
    "created_at": {
      "$date": "2016-04-04T22:27:55.562Z"
    },
    "file": {
      "name": "sales-transaction_2016feb4v49.csv",
      "size": 2744,
      "checksum": "7b8f92474e220c275bf9931c0337abf3",
      "source": {
        "type": "s3",
        "host": "johndoe:"
      },
      "line_count": 35
    },
    "node_id": "bulk_downloader_i-cd504b49",
    "profile": "main",
    "status": [
      {
        "state": "DOWNLOADING",
        "timestamp": {
          "$date": "2016-04-04T22:27:55.601Z"
        }
      },
      {
        "state": "DOWNLOADED",
        "timestamp": {
          "$date": "2016-04-04T22:27:55.887Z"
        }
      },
      {
        "state": "PROCESSING",
        "timestamp": {
          "$date": "2016-04-04T22:27:56.045Z"
        },
        "lines_skipped": 34
      },
      {
        "state": "PROCESSED",
        "timestamp": {
          "$date": "2016-04-04T22:27:56.669Z"
        }
      }
    ]
  },
  {
    "_id": {
      "$oid": "5702ea69b993f8f8cbea3349"
    },
    "account": "acme",
    "created_at": {
      "$date": "2016-04-04T22:27:53.276Z"
    },
    "file": {
      "name": "sales-transaction_2016feb4v53.csv",
      "size": 2744,
      "checksum": "44b12d35ea9fffdeeb69f98b03004f22",
      "source": {
        "type": "s3",
        "host": "johndoe:"
      },
      "line_count": 35
    },
    "node_id": "bulk_downloader_i-cd504b49",
    "profile": "profile",
    "status": [
      {
        "state": "DOWNLOADING",
        "timestamp": {
          "$date": "2016-04-04T22:27:53.307Z"
        }
      },
      {
        "state": "DOWNLOADED",
        "timestamp": {
          "$date": "2016-04-04T22:27:54.249Z"
        }
      },
      {
        "state": "PROCESSING",
        "timestamp": {
          "$date": "2016-04-04T22:27:54.289Z"
        },
        "lines_skipped": 34
      },
      {
        "state": "PROCESSED",
        "timestamp": {
          "$date": "2016-04-04T22:27:55.480Z"
        }
      }
    ]
  },

```

### Error messages

|Error Type| Description|
|---| ---|
|400 Bad request|  * File Definition prefix exceeds 150 chars<br> * File Definition prefix, start date, or end date not supplied<br> * Start/End date format is invalid<br> * End date is before Start date |

## Omnichannel file errors

File processing can fail for many reasons: invalid service credentials, missing row data, internal server error, etc. In the File Status, these specific errors are logged in the value of the `last_failure` key.

Here's a truncated sample of a file status:

```json
    ...
    {
        "state": "PROCESSING",
        "timestamp": {
            "$date": "2016-10-05T18:09:54.014Z"
        },
        "lines_failed_processing": 1,
        "last_failure": "Failed to find attribute for column with id"
    },
    ...
```


<blockquote>
Below listed errors are specific to Omnichannel Files; they are different from the API endpoint errors.
</blockquote>


### Processing and download errors

|Error message| What does it mean| How to resolve|
|---| ---| ---|
|Unknown file prefix, unable to parse file| File for the supplied prefix (name) could not be found. Either the file doesn't exist or there is a typographical error in the prefix.| Re-upload the file and double check the file prefix in the Omnichannel Definitions tab. If the error persists, please contact your Tealium Account Manager.|
|DBObject of size `{###}`` is over Max BSON size `{###}`| File is too large to be processed| Split up your file data into multiple file definitions|
|Failed to download (SFTP, S3) file| File could not be downloaded due to errors in your service credentials (see [File Import Service Configuration](https://docs.tealium.com/configure-file-import/)).|  * For SFTP, double check the Host name, user name, and password<br> * For S3/Tealium S3, double check the Access/Secret keys and Bucket/prefix |
|Invalid connection type<br> **OR**<br> Could not find required (SFTP, S3) configuration parameters for definition| Your service credentials (under [File Import Service Configuration](https://docs.tealium.com/configure-file-import/)) could not be authenticated.|  * For SFTP, double check the Host name, user name, and password<br> * For S3/Tealium S3, double check the Access/Secret keys and Bucket/prefix |

### Configuration and definition errors

These errors are caused by incorrect column mappings in the [Column Mapping screen](https://docs.tealium.com/configure-file-import/).

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
* `Can't connect to new replica set master [##.#.#.###:###], err: couldn't connect to server [##.#.#.###:###], error querying server`
* `DBClientBase::findN: transport error`
* `socket exception [SEND_ERROR]`

**Resolution**: Re-upload your file(s).
