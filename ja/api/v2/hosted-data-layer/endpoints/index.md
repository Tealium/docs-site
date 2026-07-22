---
title: ホストされたデータレイヤーAPIエンドポイント
description: ホストされたデータレイヤーオブジェクトまたはJSONファイルを使用して、ホストされたデータレイヤーを管理します。
url: https://docs.tealium.com/ja/api/v2/hosted-data-layer/endpoints/
---
## ホストされたデータレイヤーオブジェクトまたはJSONファイルをアップロードする（POST）

ホストされたデータレイヤーオブジェクトをアップロードするには、次のPOSTコマンドを使用します：

```bash
POST /v2/dle/accounts/{account}/profiles/{profile}/datalayers/{datalayer_id}
```

JSONファイルをアップロードするには、次のPOSTコマンドを使用します：

```bash
POST /v2/dle/accounts/{account}/profiles/{profile}/datalayers/{datalayer_id}?file-type=json
```

### cURLリクエストの例

このタスクを実行するためには、次のcURLコマンドを使用します：

```bash
curl -X POST https://api.tealiumiq.com/v2/dle/accounts/{account}/profiles/{profile}/datalayers/{datalayer id}} \
-H 'Authorization: Bearer {token}' \
-H 'Accept: application/json' \
-H 'Content-Type: application/json' \
-d '{ "key1" : "value1", "key2" : "value2" }'
```


<blockquote>
cURLコマンドを使用して`-d`パラメータにファイルを渡す場合、ファイル名は`@`文字で接頭辞を付ける必要があります。
</blockquote>


### レスポンスの例

次の例は、cURLコマンドから生成される典型的なレスポンスを示しています。ネットワークトラフィックに応じて、リクエストのレートは最大で1秒あたり100リクエストまで変動します。Tealiumのサーバーに変更が反映されるまでに最大1時間かかる場合があります。

`Status 200 OK`

### エラーメッセージ

このタスクの潜在的なエラーメッセージを次の表に示します：

|エラーコード|エラーメッセージ|説明|
|---|---|---|
| 400 Bad request |``` {    "returnCode" : 1400,    "message" : "Invalid request submission. Please check supplied parameters or request body." } ```|  このエラーは、次のいずれかが真である場合に発生します：JSONキーにピリオドが含まれている場合、アカウント、プロファイル、および`datalayer_id`の組み合わせが250文字を超える場合、`datalayer_id`に制限された文字が含まれる場合、アカウント/プロファイル名にタイプミスがある場合、リクエストボディが空である場合、不正なJSON、JSONデータが1MBを超える場合、またはfile-typeパラメータに「json」または「javascript」以外の値が含まれる場合。  |
| 401 Unauthorized | ``` {    "returnCode" : 1469,    "message" : "although the user is authenticated, the request is denied because of a lack of proper permissions" }  ```|  このエラーは、ユーザーが適切な権限を持っていないか、アカウント/プロファイル名にタイプミスがある場合に発生します。  |

## ホストされたデータレイヤーオブジェクトまたはJSONファイルを更新する（PUT）

ホストされたデータレイヤーオブジェクトを更新するには、次のPUTコマンドを使用します：

```bash
PUT /v2/dle/accounts/{account}/profiles/{profile}/datalayers/{datalayer_id}
```

JSONファイルを更新するには、次のPUTコマンドを使用します：

```bash
PUT /v2/dle/accounts/{account}/profiles/{profile}/datalayers/{datalayer_id}?file-type=json
```

### cURLリクエストの例

このタスクを実行するためには、次のcURLコマンドを使用します：

```bash
curl -X PUT https://api.tealiumiq.com/v2/dle/accounts/{account}/profiles/{profile}/datalayers/{datalayer id} \
-H 'Authorization: Bearer {token}' \
-H 'Accept: application/json' \
-H 'Content-Type: application/json' \
-d '{ "key1" : "value1", "key2" : "value2" }'
```

### レスポンスの例

次の例は、cURLコマンドから生成される典型的なレスポンスを示しています：

`Status 200 OK`


<blockquote>
Tealiumのサーバーに変更が反映されるまでに最大1時間かかる場合があります。
</blockquote>


### エラーメッセージ

このタスクの潜在的なエラーメッセージを次の表に示します：

|エラーコード|エラーメッセージ|説明|
|---| ---| ---|
|400 Bad request| ``` {    "returnCode" : 1400,    "message" : "Invalid request submission. Please check supplied parameters or request body." } ```|  このエラーは、次のいずれかが真である場合に発生します：JSONキーにピリオドが含まれている場合、アカウント、プロファイル、および`datalayer_id`の組み合わせが250文字を超える場合、`datalayer_id`に制限された文字が含まれる場合、アカウント/プロファイル名にタイプミスがある場合、リクエストボディが空である場合、不正なJSON、JSONデータが1MBを超える場合、file-typeパラメータに「json」または「javascript」以外の値が含まれる場合。  |

## ホストされたデータレイヤーオブジェクトまたはJSONファイルを削除する（DELETE）

ホストされたデータレイヤーオブジェクトを削除するには、次のコマンドを使用します：

```bash
DELETE /v2/dle/accounts/{account}/profiles/{profile}/datalayers/{datalayer_id}
```

JSONファイルを削除するには、次のコマンドを使用します：

```bash
DELETE /v2/dle/accounts/{account}/profiles/{profile}/datalayers/{datalayer_id}?file-type=json
```

### cURLリクエストの例

このタスクを実行するためには、次のcURLコマンドを使用します：

```bash
curl -X DELETE https://api.tealiumiq.com/v2/dle/accounts/{account}/profiles/{profile}/datalayers/{datalayer id} \
-H 'Authorization: Bearer {token}' \
-H 'Accept: application/json'
```

### レスポンスの例

次の例は、cURLコマンドから生成される典型的なレスポンスを示しています。ネットワークトラフィックに応じて、リクエストのレートは最大で1秒あたり100リクエストまで変動します。Tealiumのサーバーに変更が反映されるまでに最大1時間かかる場合があります。

`Status 200 OK`

### エラーメッセージ

このタスクの潜在的なエラーメッセージを次の表に示します：

|エラーコード|エラーメッセージ|説明|
|---|--- | ---|
| 400 Bad request | ``` {    "returnCode" : 1400,    "message" : "Invalid request submission. Please check supplied parameters or request body." } ```|  このエラーは、次のいずれかが真である場合に発生します：アカウント、プロファイル、および`datalayer_id`の組み合わせが250文字を超える場合、`datalayer_id`に制限された文字が含まれる場合、アカウント/プロファイル名にタイプミスがある場合、file-typeパラメータに「json」または「javascript」以外の値が含まれる場合。  |
| 401 Unauthorized | ``` {    "returnCode" : 1469,    "message" : "although the user is authenticated, the request is denied because of a lack of proper permissions" } ```|  このエラーは、適切な権限がないか、アカウント/プロファイル名にタイプミスがある場合に発生します。  |

## ファイルのメタデータを取得する（GET）

ファイルをアップロードした後、このGETメソッドを使用してファイルのメタデータを取得できます。

* リターンオブジェクトが含まれる200のレスポンスは、ファイルが正常にアップロードされたことを検証します。
* 何度か試してもファイルの404レスポンスが返される場合は、`failed-uploads`呼び出しを使用して返されたリストからファイルを探します。
* 失敗したアップロードは、ファイル転送プロセスに問題がある可能性を示しています。
* アップロードを再試行してください。

ホストされたデータレイヤーオブジェクトのファイル情報を取得するには、次のGETコマンドを使用します：

```bash
GET /v2/dle/accounts/{account}/profiles/{profile}/datalayers/{datalayer_id}
```

JSONファイルの情報を取得するには、次のGETコマンドを使用します：

```bash
GET /v2/dle/accounts/{account}/profiles/{profile}/datalayers/{datalayer_id}?file-type=json
```

### cURLリクエストの例

このタスクを実行するためには、次のcURLコマンドを使用します：

```bash
curl -X GET https://api.tealiumiq.com/v2/dle/accounts/{account}/profiles/{profile}/datalayers/{datalayer id} \
-H 'Authorization: Bearer {token}' \
-H 'Accept: application/json'
```

### レスポンスの例

次の例は、cURLコマンドから生成される典型的なレスポンスを示しています：

```json
{
  "file": "dle/tealium/main/datalayer1.js",
  "lastModified": "2017-04-07T02:41:24+0000",
  "size": 70
}
```

### エラーメッセージ

このタスクの潜在的なエラーメッセージを次の表に示します：

|エラーコード|エラーメッセージ|説明|
|---|---| ---|
| 404 Not Found | ``` {   "returnCode" : 1404,   "message" : "Could not locate data layer identified by {datalayer_id}" } ```|  このエラーは、指定された`datalayer_id`が存在しない場合に発生します。  |
| 400 Bad request | ``` {    "returnCode" : 1400,    "message" : "Invalid request submission. Please check supplied parameters or request body." } ```|  このエラーは、次のいずれかが真である場合に発生します：アカウント、プロファイル、および`datalayer_id`の組み合わせが250文字を超える場合、`datalayer_id`に制限された文字が含まれる場合、アカウント/プロファイル名にタイプミスがある場合、file-typeパラメータに「json」または「javascript」以外の値が含まれる場合。  |
| 401 Unauthorized | ``` {    "returnCode" : 1469,    "message" : "although the user is authenticated, the request is denied because of a lack of proper permissions" } ```|  適切な権限がないか、アカウント/プロファイル名にタイプミスがある場合にこのエラーが発生します。  |

## データレイヤーオブジェクトとJSONファイルのリストを取得する（GET）

次のコマンドのいずれかを使用して、最大1,000のホストされたデータレイヤーオブジェクトとJSONファイルのリストを返すことができます。レスポンスで継続トークンが受け取られた場合、継続トークンクエリパラメータを使用して1,000を超えるリストを取得できます。

```bash
GET /v2/dle/accounts/{account}/profiles/{profile}/datalayers
```

### 継続トークンの有無によるcURLリクエストの例

このタスクを実行するためには、次のcURLコマンドのいずれかを使用します：

#### 継続トークンなしのcURLリクエストの例

```bash
curl -X GET 'https://api.tealiumiq.com/v2/dle/accounts/{account}/profiles/{profile}/datalayers' \
-H 'Authorization: Bearer {token}' \
-H 'Accept: application/json'
```

#### 継続トークンありのcURLリクエストの例

```bash
curl -X GET 'https://api.tealiumiq.com/v2/dle/accounts/{account}/profiles/{profile}/datalayers?continuationToken={continuation_token}' \
-H 'Authorization: Bearer {token}' \
-H 'Accept: application/json'
```

### レスポンスの例

次の例は、cURLコマンドから生成される典型的なレスポンスを示しています：

#### 継続トークンなしのレスポンスの例

```json
{
  "isTruncated": false,
  "fileStatuses": [
    {
      "file": "dle/tealium/main/datalayer1.js",
      "lastModified": "2017-04-07T02:41:24+0000",
      "size": 70
    },
    {
      "file": "dle/tealium/main/datalayer2.js",
      "lastModified": "2017-04-06T23:37:17+0000",
      "size": 69
    },
    {
      "file": "dle/tealium/main/datalayer3.json",
      "lastModified": "2017-04-07T02:40:30+0000",
      "size": 86
    },
    ...
  ]
}
```

#### 継続トークンありのレスポンスの例

```json
{
 "isTruncated": true,
 "continuationToken":"1bQZQPYomjLBOQxhZhMazJVoPcrW9iEtOcPhcRQVlMZWx9IssfpisOKt0Kb85bVlRDbkR7NR%2BZd3eUgB0vnx5eomAoz5KX0K2qgcNMOwiJXdbN5CtD4A%2B%2FLK%2B%2Fj0AJ1eYXEu2l%2F9Z%2FGk%3D",
 "fileStatuses": [
   {
     "file": "dle/tealium/main/datalayer1.js",
     "lastModified": "2017-04-07T02:41:24+0000",
     "size": 70
   },
   {
     "file": "dle/tealium/main/datalayer2.js",
     "lastModified": "2017-04-06T23:37:17+0000",
     "size": 69
   },
   {
     "file": "dle/tealium/main/datalayer3.json",
     "lastModified": "2017-04-07T02:40:30+0000",
     "size": 86
   },
   ...
 ]
}
```

### エラーメッセージ

このタスクの潜在的なエラーメッセージを次の表に示します：

|エラーコード|エラーメッセージ|説明|
|---|---| ---|
| 400 Bad request | ``` {   "returnCode" : 1400,   "message" : "Invalid request submission. Please check supplied parameters or request body." } ```|  アカウント/プロファイル名にタイプミスがある場合にこのエラーが発生します。  |
| 401 Unauthorized | ``` {    "returnCode" : 1469,    "message" : "although the user is authenticated, the request is denied because of a lack of proper permissions" } ```|  適切な権限がないか、アカウント/プロファイル名にタイプミスがある場合にこのエラーが発生します。  |

## 失敗したアップロードを取得する（GET）

次のコマンドを使用して、失敗したアップロードをクエリできます：

```bash
GET /v2/dle/accounts/{account}/profiles/{profile}/failed-uploads?start-date={start_date}&amp;end-date={end_date}
```

* 返される結果には最大5,000件のレコードが含まれ、ページングされません。
* 失敗したアップロードは、ファイル転送プロセスに問題がある可能性を示しています。
* アップロードを再試行してください。

次の日付範囲パラメータを使用して結果をフィルタリングできます。日付の形式は`YYYY-MM-DDTHH:MM:SSTZ`です。例：`2017-03-31T13:45:33-0700`

* **start-date**
    * オプションです。
    * この値以上の日付を持つ失敗したアップロードのみが返されます。
* **end-date**
    * オプションです。
    * この値以下の日付を持つ失敗したアップロードのみが返されます。

### cURLリクエストの例

このタスクを実行するためには、次のcURLコマンドを使用します：

```bash
curl -X GET 'https://api.tealiumiq.com/v2/dle/accounts/{account}/profiles/{profile}/failed-uploads?start-date={YYYY-MM-DDThh:mm:ssZ}&amp;end-date={YYYY-MM-DDThh:mm:ssZ}' \
-H 'Authorization: Bearer {token}' \
-H 'Accept: application/json'
```

### レスポンスの例

次の例は、cURLコマンドから生成される典型的なレスポンスを示しています：

```json
Status 200 OK
{
  "account": "your_account",
  "profile": "main",
  "count": 2,
  "failedUploads": [
    {
      "file": "/dle/your_account/main/forremoval2.js",
      "date": "2017-05-20T17:22:00+0000"
    },
    {
      "file": "/dle/your_account/main/forremoval.js",
      "date": "2017-05-20T17:22:00+0000"
    }
  ]
}
```

### エラーメッセージ

このタスクの潜在的なエラーメッセージを次の表に示します：

|エラーコード|エラーメッセージ|説明|
|---|---| ---|
| 400 Bad request | ``` {   "returnCode" : 1400,   "message" : "Invalid request submission. Please check supplied parameters or request body." } ```|  アカウント/プロファイル名にタイプミスがある場合にこのエラーが発生します。  |
| 401 Unauthorized | ``` {   "returnCode" : 1469,   "message" : "although the user is authenticated, the request is denied because of a lack of proper permissions" } ```|  適切な権限がないか、アカウント/プロファイル名にタイプミスがある場合にこのエラーが発生します。  |
