---
title: OmnichannelファイルステータスAPIエンドポイント
description: ファイルの詳細なステータス情報を取得するために、ファイルインポートステータスGETリクエストを使用します。
url: https://docs.tealium.com/ja/api/v2/omnichannel-file-status/endpoints/
---## ファイル数を取得する
ファイル数は、アップロードされたファイルの数を返します。ファイル数は、同じファイルプレフィックスを持つファイルにのみ適用されます。

次のGETコマンドを使用して、ファイル数を取得します：

```bash
GET /v2/omnichannel/accounts/{account}/profiles/{profile}/files/count
```

### ファイル数の操作パラメータ

ファイル数は、次のクエリパラメータを使用します：

| パラメータ | タイプ | 説明 |
|---|---|---|
| `filePrefix` | string | Omnichannelファイル定義に一致するファイルプレフィックス（例：`sales_transactions`）です。 |
| `startDate` | date | クエリするファイルの範囲の開始日（例：`2017-01-01T12:34Z`）です。 |
| `endDate` | date | クエリするファイルの範囲の終了日（例：`2017-01-08T12:34Z`）です。 |

### cURLリクエストの例

ファイル数のために、次のcURLコマンドを使用します：

```bash
curl -H 'Authorization: Bearer {token}' \
https://api.tealiumiq.com/v2/omnichannel/accounts/{account}/profiles/{profile}/files/count?filePrefix={file prefix}&amp;startDate={startDate}&amp;endDate={endDate}
```


<blockquote>
ファイル数が50を超える場合は、返される数を減らすために日付範囲パラメータを狭めてください。
</blockquote>


### レスポンスの例

次の例は、cURLコマンドから生成される典型的なレスポンスを示しています：

```
{
    "count" : 42
}
```

### エラーメッセージ

このタスクの潜在的なエラーメッセージは次のとおりです：

|エラーコード|エラーメッセージ|
|---| ---|
|400 Bad request|  * ファイル定義のプレフィックスが150文字を超えています</br> * ファイル定義のプレフィックス、開始日、または終了日が指定されていません</br> * 開始日または終了日の形式が無効です</br> * 終了日が開始日よりも前です |

## 単一ファイルのステータスを取得する

単一ファイルのステータスを取得するには、次のGETコマンドを使用します：

```bash
GET /v2/omnichannel/accounts/{account}/profiles/{profile}/files/{filename}
```

### cURLリクエストの例

単一ファイルのステータスを取得するには、次のcURLコマンドを使用します：

```bash
curl -H 'Authorization: Bearer {token}' \
'https://api.tealiumiq.com/v2/omnichannel/accounts/{account}/profiles/{profile}/files/{filename}.csv'
-o {filename}.txt
```


<blockquote>
指定された.csvファイル名は類似していてはならず、明確に異なるものである必要があります。
</blockquote>


### レスポンスの例

次の例は、cURLコマンドから生成される典型的なレスポンスを示しています：

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

### エラーメッセージ

このタスクの潜在的なエラーメッセージは次のとおりです：

|エラーコード|エラーメッセージ|
|---| ---|
|404 Not Found| 指定されたファイル名が見つかりません|
|400 Bad request|  ファイル名が150文字を超えています|

## 複数のファイルステータス

指定された日付範囲内のファイルステータスの配列を返します。複数のファイルステータスは、同じファイルプレフィックスを持つファイルにのみ適用されます。

次のGETコマンドを使用して、指定された日付範囲の複数のファイルのステータスを取得します。startDateとendDateには、次の形式で日付と時刻を指定します- 2016-07-31T13:45-0700

```bash
GET /v2/omnichannel/accounts/{account}/profiles/{profile}/files/search?filePrefix={filePrefix}&amp;startDate={startDate}&amp;endDate={endDate}
```

### cURLリクエストの例

指定された日付範囲の複数のファイルのステータスを取得するには、次のcURLコマンドを使用します：

```bash
curl -H 'Authorization: Bearer {token}' \
'https://api.tealiumiq.com/v2/omnichannel/accounts/{account}/profiles/{profile}/files/search?filePrefix={filePrefix}&amp;startDate={startDate}&amp;endDate={endDate}' \
-o {filename}.txt
```

### レスポンスの例

次のサンプルファイルステータスは、次の条件を持つ3つのファイルを示しています：

* 各ファイルは`sales-transaction`で始まります
* 各ファイルプレフィックスの後には`"_"`と一意の日付識別子が続きます
* 各ファイルエントリには、ファイルサイズ、行数（行の数）、および処理された行数（処理エラーを含む）の情報が含まれています

```json
[
  {
    "_id": {
    "$oid": "5702ea6db993f8f8cbea334c"
    },
    "account": "acme",
    "created_at": {
      "$date": "2017-04-04T22:27:56.993Z"
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
      "$date": "2017-04-04T22:27:55.562Z"
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
          "$date": "2017-04-04T22:27:55.601Z"
        }
      },
      {
        "state": "DOWNLOADED",
        "timestamp": {
          "$date": "2017-04-04T22:27:55.887Z"
        }
      },
      {
        "state": "PROCESSING",
        "timestamp": {
          "$date": "2017-04-04T22:27:56.045Z"
        },
        "lines_skipped": 34
      },
      {
        "state": "PROCESSED",
        "timestamp": {
          "$date": "2017-04-04T22:27:56.669Z"
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
      "$date": "2017-04-04T22:27:53.276Z"
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
          "$date": "2017-04-04T22:27:53.307Z"
        }
      },
      {
        "state": "DOWNLOADED",
        "timestamp": {
          "$date": "2017-04-04T22:27:54.249Z"
        }
      },
      {
        "state": "PROCESSING",
        "timestamp": {
          "$date": "2017-04-04T22:27:54.289Z"
        },
        "lines_skipped": 34
      },
      {
        "state": "PROCESSED",
        "timestamp": {
          "$date": "2017-04-04T22:27:55.480Z"
        }
      }
    ]
  }
]
``` 

### エラーメッセージ

このタスクの潜在的なエラーメッセージは次のとおりです：

|エラーコード|エラーメッセージ|
|---| ---|
|400 Bad request|  * ファイル定義のプレフィックスが150文字を超えています</br> * ファイル定義のプレフィックス、開始日、または終了日が指定されていません</br> * 開始日または終了日の形式が無効です</br> * 終了日が開始日よりも前です |

## Omnichannelファイルエラー

ファイル処理は、無効なサービス資格情報、欠落した行データ、または内部サーバーエラーなど、さまざまな理由で失敗する場合があります。ファイルステータスでは、特定のエラーは`last_failure`キーの値に記録されます。

次の切り詰められたサンプルは、ファイルステータスの最後のエラーを示しています：

```
   ...
    {
        "state": "PROCESSING",
        "timestamp": {
            "$date": "2017-12-05T18:09:54.014Z"
        },
        "lines_failed_processing": 1,
        "last_failure": "Failed to find attribute for column with id"
    },
    ...
```


<blockquote>
以下のセクションにリストされているエラーは、Omnichannelファイル固有のものです。これらのエラーはAPIエンドポイントのエラーとは異なります。
</blockquote>


### 処理およびダウンロードエラー

次の表は、処理およびダウンロードに固有のエラーを説明し、その意味と解決策を提供しています。

|エラーメッセージ|意味|解決策|
|---| ---| ---|
|`Unknown file prefix, unable to parse file`|指定されたプレフィックス（`name`）のファイルが見つかりませんでした。ファイルが存在しないか、プレフィックスに誤字がある可能性があります。|ファイルを再アップロードし、[ファイルインポートサービスの構成](https://docs.tealium.com/configure-file-import/)でファイルプレフィックスをダブルチェックしてください。エラーが解消しない場合は、Tealiumのアカウントマネージャに連絡してください。|
|`DBObject of size {###} is over Max BSON size {###}`|ファイルが処理できるサイズを超えています|ファイルデータを複数のファイル定義に分割してください|
|`Failed to download (SFTP, S3) file`|サービス資格情報にエラーがあるため、ファイルをダウンロードできませんでした。[ファイルインポートサービスの構成](https://docs.tealium.com/configure-file-import/)を参照してください。|SFTPの場合は、ホスト名、ユーザー名、パスワードをダブルチェックしてください。S3/Tealium S3の場合は、アクセス/シークレットキーとバケット/プレフィックスをダブルチェックしてください。|
|`Invalid connection type`<br> – **または** – <br> `Could not find required (SFTP, S3) configuration parameters for definition`| [ファイルインポートサービスの構成](https://docs.tealium.com/configure-file-import/)のサービス資格情報が認証できませんでした|SFTPの場合は、ホスト名、ユーザー名、パスワードをダブルチェックしてください。S3/Tealium S3の場合は、アクセス/シークレットキーとバケット/プレフィックスをダブルチェックしてください。|

### 構成および定義エラー

次の表は、ファイルインポートの[列マッピング画面](https://docs.tealium.com/configure-file-import/)での不正な列マッピングによるエラーを説明し、その意味と解決策を提供しています。

|エラーメッセージ|意味|解決策|
|---| ---| ---|
|`Failed to find attribute for column with id`|AudienceStreamは、マップされた列名のためのOmnichannel属性を生成できませんでした。|問題のある列ヘッダーを新しいものに置き換え、ファイルを再アップロードしてください。|
|`Exception thrown while processing file`|マップされた列ヘッダーの値をOmnichannel属性にパースできませんでした。|問題のある列値を置き換え、ファイルを再アップロードしてください。|
|`Secondary visitor ID column= {column_name_here} does not exist in the file, unable to continue`|訪問IDフィールドにマップされた列ヘッダーがファイルに存在しません。これは、誤字の可能性があるか、ヘッダーが定義されていないためです。|提供された列ヘッダーがファイルの列ヘッダーと一致することを確認してください。|
|`{date_format_here} could not be parsed as a Date`|マップされた列名のために指定された日付形式がファイルに存在しません。|提供された日付形式がファイルの日付形式と一致することを確認してください。|
|`The number of columns to be processed {##} must match the number of CellProcessors {##}: check that the number of CellProcessors you have defined matches the expected number of columns being read/written`|Omnichannel属性の下にマップされた列名がファイルに存在しません。これは、誤字の可能性があるか、ヘッダーが定義されていないためです。|提供された列ヘッダーがファイルの列ヘッダーと一致することを確認してください。|

### 内部サーバーエラー

次のエラーは、ファイルを処理するさまざまなサーバー間で通信できない場合に発生します。これらのエラーを解決するには、ファイルを再アップロードしてください。

* `Connection is already closed due to connection error; cause: com.rabbitmq.client.MissedHeartbeatException`

* `Can't connect to new replica set master [##.#.#.###:###], err: couldn't connect to server [##.#.#.###:###], error querying server`

*  `DBCClientBase::findN: transport error`

*  `socket exception [SEND_ERROR]`
