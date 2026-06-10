---
title: オムニチャネルファイルステータスAPIオブジェクト
description: オムニチャネルファイルステータスAPIは、オムニチャネルファイルの詳細なステータス情報を提供します。オムニチャネルファイルステータスAPIは、ファイルがインポートされた時期、処理方法、および処理エラーの詳細を示すファイルステータスを返します。
url: https://docs.tealium.com/ja/api-v1/omnichannel-file-status/data-objects/
---
これは、[現行のTealium Omnichannel File Status API]()の古いバージョンです。

APIは、ファイルがインポートされ、どのように処理されたか、処理エラーを含む詳細を示す_File Status_を返します。ファイルステータスは、次のキーを含むJSONオブジェクトとして表されます：

|名前| タイプ| 説明|
|---| ---| ---|
|account| string| AudienceStreamアカウントの名前|
|profile| string| ファイルがアップロードされ、処理されるプロファイル（アカウント内）の名前 |
|created at| UTC timestamp| ファイルステータスが作成された日時（[UTC形式のデザイネータ&#39;Z&#39;で表現](https://www.w3.org/TR/NOTE-datetime)）|
|file.name| string| 対象のファイル名|
|file.size| integer| ファイルサイズ（バイト単位）|
|file.source-type| string| ファイルのアップロードに使用されたサービス：SFTP、Tealium S3、およびS3|
|file.source-host| string| サービスの名前&lt;br&gt; * SFTPのホスティングアカウント&lt;br&gt; * S3/Tealium S3のバケット名 |
|line\_count| integer| ファイル内の行数|
|status.state| string| ファイルに対する処理アクションを示します。可能な値は：**DOWNLOADING**、**DOWNLOADED**、**PROCESSING**、または**PROCESSED**。|
|status.timestamp| UTC timestamp| [status-state]が記録された日時（[UTC形式のデザイネータ&#39;Z&#39;で表現](https://www.w3.org/TR/NOTE-datetime)）|
|lines\_successfully\_processed| integer| 正常に解析された行数|
|lines\_skipped| integer| データが欠落しているために解析できなかった行数|
|lines\_failed\_processing| integer| データが不良または形式が正しくないために解析できなかった行数|
|last\_failure| string| 行/ファイルが処理できなかった原因となるエラー（エラーグロッサリーとトラブルシューティングリンク\_hereを参照）|

## ファイルステータスのサンプル

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
