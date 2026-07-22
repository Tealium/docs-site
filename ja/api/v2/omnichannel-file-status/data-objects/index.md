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
| `created at` | UTC timestamp | ファイルステータスが作成された日時。[UTC形式のデザイネータ'Z'で表現](https://www.w3.org/TR/NOTE-datetime)。 |
| `file.name` | string | ファイルの名前。 |
| `file.size` | number | ファイルサイズ（バイト単位）。 |
| `file.source-type` | string | ファイルのアップロードに使用されたサービス：SFTP、Tealium S3、またはS3。 |
| `file.source-host` | string | サービスの名前。</br>     * SFTPのホスティングアカウント </br>   * S3/Tealium S3のバケット名 |
| `line_count` | number | ファイル内の行数。 |
| `status.state` | string | ファイルに対する処理アクションを示します。可能な値は次のとおりです。</br> * `DOWNLOADING`</br> * `DOWNLOADED`</br>   * `PROCESSING`</br>   * `PROCESSED`</br> |
| `status.timestamp` | UTC timestamp | `[status-state]`が記録された日時。[UTC形式のデザイネータ'Z'で表現](https://www.w3.org/TR/NOTE-datetime)。 |
| `lines_successfully_processed` | number | 正常に解析された行数。 |
| `lines_skipped` | number | データが欠落しているために解析できなかった行数。 |
| `lines_failed_processing` | number | データが不良または形式が正しくないために解析できなかった行数。 |
| `last_failure` | string | 処理できなかった行またはファイルによるエラー。 |




## ファイルステータスレスポンスの例

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
