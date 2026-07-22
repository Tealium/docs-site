---
title: Omnichannel File Status APIエンドポイント
description: ファイルの詳細なステータス情報を取得するために、ファイルインポートステータスGETリクエストを使用します。
url: https://docs.tealium.com/ja/api-v1/omnichannel-file-status/endpoints/
---
これは[現在のTealium Omnichannel File Status API](https://docs.tealium.com/about-file-import/)の古いバージョンです。


## ファイル数

アップロードされたファイルの数を返します。同じファイルプレフィックスを持つファイルにのみ適用されます。

以下のクエリパラメータが使用されます：

* **filePrefix** - Omnichannelファイル定義に一致するファイルプレフィックス、例：`sales_transactions`。
* **startDate** - クエリするファイルの範囲の開始日、例：`2017-01-01T12:34Z`。
* **endDate** - クエリするファイルの範囲の終了日、例：`2017-01-08T12:34Z`。

```
GET /v1/omnichannel/accounts/{account}/profiles/{profile}/files/count?utk={utk token}&filePrefix={file prefix}&startDate={start date}&endDate={end date}
```

### cURLリクエスト

```bash
cURL -i -b JSESSIONID={session_id} \
  https://api.tealiumiq.com/v1/omnichannel/accounts/{account}/profiles/{profile}/files/count?utk={token}&filePrefix={filePrefix}&startDate={startDate}&endDate={endDate}
```


<blockquote>
ファイル数が50を超える場合は、日付範囲パラメータを絞り込んでください。
</blockquote>


### レスポンス例

```json
{
    "count" : 42
}
```

### エラーメッセージ

|エラータイプ| 説明|
|---| ---|
|400 Bad request|  * ファイル定義のプレフィックスが150文字を超えています<br> * ファイル定義のプレフィックス、開始日、または終了日が指定されていません<br> * 開始/終了日の形式が無効です<br> * 終了日が開始日よりも前です |

## 単一ファイルのステータス

```
GET /v1/omnichannel/accounts/{account}/profiles/{profile}/files/{fileName}?utk={utk token}
```

### cURLリクエスト

```bash
cURL -i -b JSESSIONID={session_id} \
  https://api.tealiumiq.com/v1/omnichannel/accounts/{account}/profiles/{profile}/files/{filename}.csv?utk={utk token} \
  -o {filename}.txt

```

### レスポンス例

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

|エラータイプ| 説明|
|---| ---|
|404 Not Found| 指定されたファイル名が見つかりません|
|400 Bad request| ファイル名が150文字を超えています|

## 複数のファイルステータス

指定された日付範囲内のファイルステータスの配列を返します。同じファイルプレフィックスを持つファイルにのみ適用されます。

```
GET /v1/omnichannel/accounts/{account}/profiles/{profile}/files/search?utk={utk token}&filePrefix={filePrefix}&startDate={startDate}&endDate={endDate}
```

### cURLリクエスト

```bash
cURL -i -b JSESSIONID={session_id} \
  https://api.tealiumiq.com/v1/omnichannel/accounts/{account}/profiles/{profile}/files/search?utk={token}&filePrefix={filePrefix}&startDate={startDate}&endDate={endDate} \
  -o {filename}.txt
```

### レスポンス例

以下は、すべてが `sales-transaction` で始まる3つのファイルのサンプルファイルステータスです。各ファイルプレフィックスの後には `_` と一意の日付識別子が続きます。各ファイルエントリには、ファイルサイズ、行数、および処理された行数（処理エラーを含む）に関する情報が含まれています。

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

### エラーメッセージ

|エラータイプ| 説明|
|---| ---|
|400 Bad request|  * ファイル定義のプレフィックスが150文字を超えています<br> * ファイル定義のプレフィックス、開始日、または終了日が指定されていません<br> * 開始/終了日の形式が無効です<br> * 終了日が開始日よりも前です |

## Omnichannelファイルエラー

ファイル処理は、無効なサービス資格情報、行データの欠落、内部サーバーエラーなどの理由で失敗する場合があります。ファイルステータスでは、これらの特定のエラーは `last_failure` キーの値に記録されます。

以下は、ファイルステータスの一部のサンプルです（一部省略）：

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
以下にリストされているエラーは、Omnichannelファイル固有のものであり、APIエンドポイントのエラーとは異なります。
</blockquote>


### 処理およびダウンロードエラー

|エラーメッセージ| その意味| 解決方法|
|---| ---| ---|
|Unknown file prefix, unable to parse file| 指定されたプレフィックス（名前）のファイルが見つかりませんでした。ファイルが存在しないか、プレフィックスにタイプミスがある可能性があります。| ファイルを再アップロードし、Omnichannel Definitionsタブでファイルプレフィックスをダブルチェックしてください。エラーが解消しない場合は、Tealiumのアカウントマネージャにお問い合わせください。|
|DBObject of size `{###}`` is over Max BSON size `{###}`| ファイルが処理できるサイズを超えています| ファイルデータを複数のファイル定義に分割してください|
|Failed to download (SFTP, S3) file| サービス資格情報にエラーがあるため、ファイルをダウンロードできませんでした（[File Import Service Configuration](https://docs.tealium.com/configure-file-import/)を参照）。|  * SFTPの場合、ホスト名、ユーザー名、パスワードをダブルチェックしてください<br> * S3/Tealium S3の場合、アクセスキー/シークレットキーとバケット/プレフィックスをダブルチェックしてください |
|Invalid connection type<br> **OR**<br> Could not find required (SFTP, S3) configuration parameters for definition| サービス資格情報（[File Import Service Configuration](https://docs.tealium.com/configure-file-import/)）が認証できませんでした。|  * SFTPの場合、ホスト名、ユーザー名、パスワードをダブルチェックしてください<br> * S3/Tealium S3の場合、アクセスキー/シークレットキーとバケット/プレフィックスをダブルチェックしてください |

### 構成および定義エラー

これらのエラーは、[Column Mapping screen](https://docs.tealium.com/configure-file-import/)での不正な列マッピングによって引き起こされます。

|エラーメッセージ| その意味| 解決方法|
|---| ---| ---|
|Failed to find attribute for column with id| AudienceStreamは、マッピングした列名のためのOmnichannel属性を生成できませんでした。| 問題のある列ヘッダーを新しいものに置き換え、ファイルを再アップロードしてください|
|Exception thrown while processing file| マッピングした列ヘッダーの値をOmnichannel属性にパースできませんでした。| 問題のある列値を置き換え、ファイルを再アップロードしてください。|
|Secondary visitor ID column= `{column_name_here}` does not exist in the file, unable to continue| ビジターIDフィールドにマッピングした列ヘッダーがファイルに存在しません。これは、タイプミスまたはヘッダーが定義されていないことが原因です。| 提供した列ヘッダーがファイルと一致していることを確認してください|
|`{date_format_here}` could not be parsed as a Date| マッピングした列名の日付形式がファイルに存在しません。| 提供した日付形式がファイルと一致していることを確認してください|
|The number of columns to be processed `{##}` must match the number of CellProcessors `{##}`: check that the number of CellProcessors you have defined matches the expected number of columns being read/written| Omnichannel属性の下にマッピングした列名がファイルに存在しません。これは、タイプミスまたはヘッダーが定義されていないことが原因です。| 提供した列ヘッダーがファイルと一致していることを確認してください|

### 内部サーバーエラー

これらのエラーは、ファイルを処理するさまざまなサーバー間で通信できない場合に発生します。

* `Connection is already closed due to connection error; cause: com.rabbitmq.client.MissedHeartbeatException`
* `Can't connect to new replica set master [##.#.#.###:###], err: couldn't connect to server [##.#.#.###:###], error querying server`
* `DBClientBase::findN: transport error`
* `socket exception [SEND_ERROR]`

**解決方法**: ファイルを再アップロードしてください。