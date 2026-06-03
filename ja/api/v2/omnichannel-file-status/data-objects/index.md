---
title: オムニチャネルファイルステータスAPIデータオブジェクト
description: ファイルインポートAPIは、ファイルステータスをJSONオブジェクトとして返します。
url: https://docs.tealium.com/ja/api/v2/omnichannel-file-status/data-objects/
---
## 利用可能なフィールド

| パラメータ | タイプ | 説明 |
|---|---|---|
| `account` | string | Tealium AudienceStream CDPアカウントの名前。 |
| `profile` | string | ファイルがアップロードされ、処理されるアカウント内のプロファイルの名前。 |
| `created at` | UTC timestamp | ファイルステータスが作成された日時。[UTC形式のデザイネータ&#39;Z&#39;で表現](https://www.w3.org/TR/NOTE-datetime)。 |
| `file.name` | string | ファイルの名前。 |
| `file.size` | number | ファイルサイズ（バイト単位）。 |
| `file.source-type` | string | ファイルのアップロードに使用されたサービス：FTP、SFTP、Tealium S3、またはS3。 |
| `file.source-host` | string | サービスの名前。&lt;/br&gt;     * FTP/SFTPのホスティングアカウント &lt;/br&gt;   * S3/Tealium S3のバケット名 |
| `line_count` | number | ファイル内の行数。 |
| `status.state` | string | ファイルに対する処理アクションを示します。可能な値は次のとおりです。&lt;/br&gt; * `DOWNLOADING`&lt;/br&gt; * `DOWNLOADED`&lt;/br&gt;   * `PROCESSING`&lt;/br&gt;   * `PROCESSED`&lt;/br&gt; |
| `status.timestamp` | UTC timestamp | `[status-state]`が記録された日時。[UTC形式のデザイネータ&#39;Z&#39;で表現](https://www.w3.org/TR/NOTE-datetime)。 |
| `lines_successfully_processed` | number | 正常に解析された行数。 |
| `lines_skipped` | number | データが欠落しているために解析できなかった行数。 |
| `lines_failed_processing` | number | データが不良または形式が正しくないために解析できなかった行数。 |
| `last_failure` | string | 処理できなかった行またはファイルによるエラー。 |




## ファイルステータスレスポンスの例

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
