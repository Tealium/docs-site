---
title: Omnichannel File Status API Objects
description: The Omnichannel File Status API provides detailed status information for your Omnichannel files. The Omnichannel File Status API returns a File Status that details when the files imported, how they were processed, and any processing errors.
url: https://docs.tealium.com/api-v1/omnichannel-file-status/data-objects/
---
This is an older version of the [current Tealium Omnichannel File Status API](https://docs.tealium.com/about-omnichannel-file-status-api/).


The API returns a _File Status_ that details when the files imported and how they were processed, including any processing errors. A File Status is represented as a JSON object containing the following keys:

|Name| Type| Description|
|---| ---| ---|
|account| string| Name of the AudienceStream account|
|profile| string| Name of the profile (in the account) where your files are uploaded and processed |
|created at| UTC timestamp| date and time when the file status was created (expressed in [UTC format with the designator 'Z'](https://www.w3.org/TR/NOTE-datetime))|
|file.name| string| Name of the file in question|
|file.size| integer| File size in bytes|
|file.source-type| string| Service used for uploading the file: SFTP, Tealium S3, and S3|
|file.source-host| string| Name of the service<br> * Hosting account for SFTP<br> * Bucket name for S3/Tealium S3 |
|line\_count| integer| Number of rows in the file|
|status.state| string| Indicates the processing action on the file. Possible values are: **DOWNLOADING**, **DOWNLOADED**, **PROCESSING**, or **PROCESSED**.|
|status.timestamp| UTC timestamp| date and time when the [status-state] was recorded (expressed in [UTC format with the designator 'Z'](https://www.w3.org/TR/NOTE-datetime))|
|lines\_successfully\_processed| integer| Number of rows parsed successfully|
|lines\_skipped| integer| Number of rows that could not be parsed due to missing data|
|lines\_failed\_processing| integer| Number of rows that could not be parsed due to bad data or incorrect formatting|
|last\_failure| string| Error due to which the row/file could not be processed (Refer to Error Glossary and Troubleshooting link\_here)|

## Sample File Status

```json
{
    "account": "company_xyz",
    "created_at": {
      "$date": "2016-04-04T22:27:56.993Z"
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

