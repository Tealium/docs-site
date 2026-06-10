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
| `created at` | UTC timestamp | The date and time when the file status was created, expressed in [UTC format with the designator &#39;Z&#39;](https://www.w3.org/TR/NOTE-datetime). |
| `file.name` | string | The name of the file. |
| `file.size` | number | The file size, in bytes. |
| `file.source-type` | string | The service used for uploading the file: SFTP, Tealium S3, or S3. |
| `file.source-host` | string | The name of the service.&lt;/br&gt;     * Hosting account for SFTP &lt;/br&gt;   * Bucket name for S3/Tealium S3 |
| `line_count` | number | The number of rows in the file. |
| `status.state` | string | Indicates the processing action on the file. Possible values are:&lt;/br&gt; * `DOWNLOADING`&lt;/br&gt; * `DOWNLOADED`&lt;/br&gt;   * `PROCESSING`&lt;/br&gt;   * `PROCESSED`&lt;/br&gt; |
| `status.timestamp` | UTC timestamp | The date and time when the `[status-state]` was recorded, expressed in [UTC format with the designator &#39;Z&#39;](https://www.w3.org/TR/NOTE-datetime). |
| `lines_successfully_processed` | number | The number of rows successfully parsed. |
| `lines_skipped` | number | The number of rows that could not be parsed due to missing data. |
| `lines_failed_processing` | number | The number of rows that could not be parsed due to bad data or incorrect formatting. |
| `last_failure` | string | Error due to a row or file that could not be processed. |




## Example file status response

```json
{
    &#34;account&#34;: &#34;company_xyz&#34;,
    &#34;created_at&#34;: {
      &#34;$date&#34;: &#34;2017-04-04T22:27:56.993Z&#34;
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
          &#34;$date&#34;: &#34;2017-04-04T22:27:58.797Z&#34;
        }
      }
    ]
}
```
