---
title: Omnichannel File Status API Objects
description: The Omnichannel File Status API provides detailed status information for your Omnichannel files. The Omnichannel File Status API returns a File Status that details when the files imported, how they were processed, and any processing errors.
url: https://docs.tealium.com/api-v1/omnichannel-file-status/data-objects/
---
This is an older version of the [current Tealium Omnichannel File Status API]().


The API returns a _File Status_ that details when the files imported and how they were processed, including any processing errors. A File Status is represented as a JSON object containing the following keys:

|Name| Type| Description|
|---| ---| ---|
|account| string| Name of the AudienceStream account|
|profile| string| Name of the profile (in the account) where your files are uploaded and processed |
|created at| UTC timestamp| date and time when the file status was created (expressed in [UTC format with the designator &#39;Z&#39;](https://www.w3.org/TR/NOTE-datetime))|
|file.name| string| Name of the file in question|
|file.size| integer| File size in bytes|
|file.source-type| string| Service used for uploading the file: SFTP, Tealium S3, and S3|
|file.source-host| string| Name of the service&lt;br&gt; * Hosting account for SFTP&lt;br&gt; * Bucket name for S3/Tealium S3 |
|line\_count| integer| Number of rows in the file|
|status.state| string| Indicates the processing action on the file. Possible values are: **DOWNLOADING**, **DOWNLOADED**, **PROCESSING**, or **PROCESSED**.|
|status.timestamp| UTC timestamp| date and time when the [status-state] was recorded (expressed in [UTC format with the designator &#39;Z&#39;](https://www.w3.org/TR/NOTE-datetime))|
|lines\_successfully\_processed| integer| Number of rows parsed successfully|
|lines\_skipped| integer| Number of rows that could not be parsed due to missing data|
|lines\_failed\_processing| integer| Number of rows that could not be parsed due to bad data or incorrect formatting|
|last\_failure| string| Error due to which the row/file could not be processed (Refer to Error Glossary and Troubleshooting link\_here)|

## Sample File Status

```json
{
    &#34;account&#34;: &#34;company_xyz&#34;,
    &#34;created_at&#34;: {
      &#34;$date&#34;: &#34;2016-04-04T22:27:56.993Z&#34;
    },
    &#34;file&#34;: {
      &#34;name&#34;: &#34;sales-transaction_2016feb4v50.csv&#34;,
      &#34;size&#34;: 2744,
      &#34;checksum&#34;: &#34;44b12d35ea9fffdeeb69f98b03004f22&#34;,
      &#34;source&#34;: {
        &#34;type&#34;: &#34;s3&#34;,
        &#34;host&#34;: &#34;companyxyz:&#34;
      },
      &#34;line_count&#34;: 35
    },
    &#34;node_id&#34;: &#34;bulk_downloader_i-cd504b49&#34;,
    &#34;profile&#34;: &#34;omnichannelv2&#34;,
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

