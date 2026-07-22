---
title: オムニチャネルファイルステータスAPIオブジェクト
description: オムニチャネルファイルステータスAPIは、オムニチャネルファイルの詳細なステータス情報を提供します。オムニチャネルファイルステータスAPIは、ファイルがインポートされた時期、処理方法、および処理エラーの詳細を示すファイルステータスを返します。
url: https://docs.tealium.com/ja/api-v1/omnichannel-file-status/data-objects/
---
これは、[現行のTealium Omnichannel File Status API](https://docs.tealium.com/about-omnichannel-file-status-api/)の古いバージョンです。

APIは、ファイルがインポートされ、どのように処理されたか、処理エラーを含む詳細を示す_File Status_を返します。ファイルステータスは、次のキーを含むJSONオブジェクトとして表されます：

|名前| タイプ| 説明|
|---| ---| ---|
|account| string| AudienceStreamアカウントの名前|
|profile| string| ファイルがアップロードされ、処理されるプロファイル（アカウント内）の名前 |
|created at| UTC timestamp| ファイルステータスが作成された日時（[UTC形式のデザイネータ'Z'で表現](https://www.w3.org/TR/NOTE-datetime)）|
|file.name| string| 対象のファイル名|
|file.size| integer| ファイルサイズ（バイト単位）|
|file.source-type| string| ファイルのアップロードに使用されたサービス：SFTP、Tealium S3、およびS3|
|file.source-host| string| サービスの名前<br> * SFTPのホスティングアカウント<br> * S3/Tealium S3のバケット名 |
|line\_count| integer| ファイル内の行数|
|status.state| string| ファイルに対する処理アクションを示します。可能な値は：**DOWNLOADING**、**DOWNLOADED**、**PROCESSING**、または**PROCESSED**。|
|status.timestamp| UTC timestamp| [status-state]が記録された日時（[UTC形式のデザイネータ'Z'で表現](https://www.w3.org/TR/NOTE-datetime)）|
|lines\_successfully\_processed| integer| 正常に解析された行数|
|lines\_skipped| integer| データが欠落しているために解析できなかった行数|
|lines\_failed\_processing| integer| データが不良または形式が正しくないために解析できなかった行数|
|last\_failure| string| 行/ファイルが処理できなかった原因となるエラー（エラーグロッサリーとトラブルシューティングリンク\_hereを参照）|

## ファイルステータスのサンプル

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
