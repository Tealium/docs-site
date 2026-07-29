---
title: 訪問プライバシーAPIエンドポイント
description: 訪問プライバシーAPIを使用して、特定の訪問に関する既知のデータを取得したり、訪問レコードを削除したり、削除リクエストのステータスを確認したりすることができます。
url: https://docs.tealium.com/ja/api/v3/visitor-privacy/endpoints/
---
## GET 訪問


<blockquote>
この呼び出しには、認証APIで返された地域固有のホストを使用する必要があります。詳細については、[認証](https://docs.tealium.com/api/v3/getting-started/authentication/)を参照してください。
</blockquote>


訪問レコードを取得するには、次のGETコマンドを使用します：

```bash
GET /v3/privacy/visitor/accounts/{account}/profiles/{profile}?attributeId={attributeId}&attributeValue={attributeValue}&prettyName={prettyName}
```

このコマンドは以下のパラメータを使用します：

* `attributeId`
  * アカウントからの[訪問ID属性](https://docs.tealium.com/visitor-id-attribute/)を表す数値ID。
* `attributeValue`
  * 検索する値。
  * 特殊文字を含む値はURLエンコードする必要があります。
* `prettyName`
  * 属性キーがレスポンスでどのように表示されるかを示すブール値：
    * **True** – 属性は「Lifetime Order Value」のようなユーザーフレンドリーな名前で表示されます。
    * **False** – 属性は「28471」のような数値IDで表示されます。

### 権限要件

* サーバーサイドのリーダー、エディター、またはパブリッシャーのレガシー権限、または
* 最低限の**閲覧**訪問ルックアッププラットフォーム権限

### cURLリクエストの例

```bash
curl -H 'Authorization: Bearer {token}' \
 -G \
'https://us-east-1-platform.tealiumapis.com/v3/privacy/visitor/accounts/my_account/profiles/main' \
 --data-urlencode 'attributeId=86' \
 --data-urlencode 'attributeValue=user@example.com' \
 --data 'prettyName=true'
```

### レスポンスの例

レスポンスの形式については、訪問オブジェクトの例を参照してください。

### エラーメッセージ

このタスクに関連する可能性のあるエラーメッセージは以下の通りです：

|エラーメッセージ| 説明|
|---| ---|
|400|  `{ "message": "属性IDまたは属性値が不足しています"}` |
|401|  `{ "message": "許可されていません"}` |
| 404 | `システムに訪問が見つかりません {  "transactionId": {transactionId}  }` |
|429| `{ "message": "リクエストが多すぎます"}` |
| 500 |`{ "message": "内部サーバーエラー"}` |

## 訪問の削除


<blockquote>
この呼び出しには、認証APIで返された地域固有のホストを使用する必要があります。詳細については、[認証](https://docs.tealium.com/api/v3/getting-started/authentication/)を参照してください。
</blockquote>


一つまたは複数の訪問レコードを削除する前に、以下の点を考慮してください：

* 訪問レコードの削除リクエストは、訪問ID値に関連付けられたすべてのデータの削除を引き起こします。これには、ステッチされた訪問レコードも含まれます。
* 削除リクエストは処理のためにキューに入れられ、完了までに最大30日かかる場合があります。
* 訪問が別の訪問に置き換えられた場合、または置き換えられた場合、ステッチされたすべての訪問が削除されます。

訪問レコードを削除するには、次のDELETEコマンドを使用します：

```bash
DELETE /v3/privacy/visitor/accounts/{account}/profiles/{profile}?attributeID={value}&attributeValue={value}
```

このコマンドは以下のパラメータを使用します：

* `attributeId`  
アカウントからの[訪問ID属性](https://docs.tealium.com/visitor-id-attribute/)を表す数値ID。
* `attributeValue`  
検索する値。特殊文字を含む値はURLエンコードする必要があります。

### 権限要件

* サーバーサイドのパブリッシャーのレガシー権限、または
* **閲覧、編集、および削除**訪問ルックアッププラットフォーム権限

### cURLリクエストの例

```bash
curl -H 'Authorization: Bearer {token}' \
-X DELETE \
-G \
'https://us-east1-platform.tealiumapis.com/v3/privacy/visitor/accounts/my_account/profiles/main' \
--data-urlencode "attributeId=86" \
--data-urlencode "attributeValue=user@example.com"
```

### レスポンスの例

削除リクエストへのレスポンスには、`transaction_id`とステータスが含まれます。`transaction_id`は、以前のリクエストのステータスを確認するためにGETトランザクションコールで使用されるIDです。可能なステータス文字列には、**PENDING**、**SUCCESS**、または**FAILED**があります。

成功したレスポンスは、`transactionId`値を持つ202 Acceptedメッセージを表示します。同じ`account`、`profile`、`attributeId`、および`attributeValue`を持つリクエストが**PENDING**のトランザクションステータスで既に存在する場合、既存のトランザクションIDが次のように返されます：

```json
{
"transactionId" : "{transactionId1}"
}
```

### エラーメッセージ

このタスクに関連する可能性のあるエラーメッセージは以下の通りです：

|エラーメッセージ| 説明|
|---| ---|
|400|  `{ "message": "属性IDまたは属性値が不足しています"}` |
|401|  `{ "message": "許可されていません"}` |
|404|  `システムに訪問が見つかりません {  "transactionId": {transactionId}  }` |
|429| `{ "message": "リクエストが多すぎます"}` |

## トランザクションの取得


<blockquote>
この呼び出しには、認証APIで返された地域固有のホストを使用する必要があります。詳細については、[認証](https://docs.tealium.com/api/v3/getting-started/authentication/)を参照してください。
</blockquote>


トランザクションは、任意のDELETE訪問リクエストを指します。DELETE訪問リクエストは後で処理されるため、`transaction_id`はそのリクエストとIDのためのユニークなレコードとして使用され、処理ステータスを確認する際に使用されます。

トランザクションのステータスを確認するために、次のGETコマンドを使用します：

```bash
GET /v3/privacy/visitor/accounts/{account}/profiles/{profile}/transactions/{transaction_id}
```

### 権限要件

* サーバーサイドのリーダー、エディター、またはパブリッシャーのレガシー権限、または
* 最低限の**閲覧**訪問ルックアッププラットフォーム権限

### cURLリクエストの例

APIキーからベアラートークンを生成する方法については、[認証](https://docs.tealium.com/api/v3/getting-started/authentication/)を参照してください。APIキーではなく、APIコールでベアラートークンが使用されます。

```bash
curl -H 'Authorization: Bearer {token}' \
https://us-east-1-platform.tealiumapis.com/v3/privacy/visitor/accounts/my_account/profiles/main/transactions/0123456789
```

### レスポンスの例

レスポンスには、キーが`transaction_id`で値が次のいずれかのステータス文字列であるオブジェクトが含まれます：**PENDING**、**SUCCESS**、または**FAILED**。

```json
{
  "0123456789" : "SUCCESS"
}
```

### エラーメッセージ

このタスクに関連する可能性のあるエラーメッセージは以下の通りです：

|エラーメッセージ| 説明|
|---| ---|
|401|  `{ "message": "許可されていません"}` |
|404|  `システムに訪問が見つかりません {  "transactionId": {transactionId}  }` |
|429| `{ "message": "リクエストが多すぎます"}` |

## 訪問ID属性の取得

アカウントで利用可能な訪問ID属性のリストを取得するために、次のGETコマンドを使用します：

```bash
GET /v3/privacy/visitor/accounts/{account}/profiles/{profile}/ids
```

### 権限要件

* サーバーサイドのリーダー、エディター、またはパブリッシャーのレガシー権限、または
* 最低限の**閲覧**訪問ルックアッププラットフォーム権限

### cURLリクエストの例

```bash
curl -H 'Authorization: Bearer {token}' \
https://platform.tealiumapis.com/v3/privacy/visitor/accounts/my_account/profiles/main/ids
```

### レスポンスの例

このコマンドのレスポンスは、訪問ID属性の数値IDと名前を表すキーと値のペアのオブジェクトです。

```json
{
  "43" : "Email Address",
  "57" : "Tax ID Number"
}
```

### エラーメッセージ

このタスクに関連する可能性のあるエラーメッセージは以下の通りです：

|エラーメッセージ| 説明|
|---| ---|
|401|  `{ "message": "許可されていません"}` |
|404|  `{ "message" : "アカウントとプロファイルに訪問IDが見つかりません"}` |
|429| `{ "message": "リクエストが多すぎます"}` |
|500|  `{ "message" : "内部サーバーエラー"}` |