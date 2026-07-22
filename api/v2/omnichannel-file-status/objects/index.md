---
title: Omnichannel file status API data objects
description: The File Import API returns a file status as a JSON object.
url: https://docs.tealium.com/api/v2/omnichannel-file-status/objects/
---
## Available fields

| Parameter | Type | Description |
|---|---|---|
| `account` | string | The name of the Tealium AudienceStream CDP account. |
| `profile` | string | The name of the profile in the account where your files are uploaded and processed. |
| `created at` | UTC timestamp | The date and time when the file status was created, expressed in [UTC format with the designator 'Z'](https://www.w3.org/TR/NOTE-datetime). |
| `file.name` | string | The name of the file. |
| `file.size` | number | The file size, in bytes. |
| `file.source-type` | string | The service used for uploading the file: SFTP, Tealium S3, or S3. |
| `file.source-host` | string | The name of the service.</br>     * Hosting account for SFTP </br>   * Bucket name for S3/Tealium S3 |
| `line_count` | number | The number of rows in the file. |
| `status.state` | string | Indicates the processing action on the file. Possible values are:</br> * `DOWNLOADING`</br> * `DOWNLOADED`</br>   * `PROCESSING`</br>   * `PROCESSED`</br> |
| `status.timestamp` | UTC timestamp | The date and time when the `[status-state]` was recorded, expressed in [UTC format with the designator 'Z'](https://www.w3.org/TR/NOTE-datetime). |
| `lines_successfully_processed` | number | The number of rows successfully parsed. |
| `lines_skipped` | number | The number of rows that could not be parsed due to missing data. |
| `lines_failed_processing` | number | The number of rows that could not be parsed due to bad data or incorrect formatting. |
| `last_failure` | string | Error due to a row or file that could not be processed. |




## Example file status response

```json
{
    "account": "company_xyz",
    "created_at": {
      "$date": "2017-04-04T22:27:56.993Z"
    },
    "file": {
      "name": "sales-transaction_2016feb4v50.csv",
      "size": 2744,
      "checksum": "44b12d35ea9fffdeeb69f98b03004f22",
      "source": {
        "type": "s3",
        "host": "companyxyz:"
      },
      "line_count": 35
    },
    "node_id": "bulk_downloader_i-cd504b49",
    "profile": "omnichannelv2",
    "status": [
      {
        "state": "DOWNLOADING",
        "timestamp": {
          "$date": "2017-04-04T22:27:57.285Z"
        }
      },
      {
        "state": "DOWNLOADED",
        "timestamp": {
          "$date": "2017-04-04T22:27:57.722Z"
        }
      },
      {
        "state": "PROCESSING",
        "timestamp": {
          "$date": "2017-04-04T22:27:57.780Z"
        },
        "lines_skipped": 34

      },
      {
        "state": "PROCESSED",
        "timestamp": {
          "$date": "2017-04-04T22:27:58.797Z"
        }
      }
    ]
}
```
