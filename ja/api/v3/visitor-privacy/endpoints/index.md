---
title: ビジタープライバシーAPIエンドポイント
description: ビジタープライバシーAPIを使用すると、特定のビジターに関する既知のデータを取得したり、ビジターレコードを削除したり、削除リクエストのステータスを確認したりすることができます。
url: https://docs.tealium.com/ja/api/v3/visitor-privacy/endpoints/
---
## GET Visitor

この呼び出しには、認証APIで返された地域固有のホストを使用する必要があります。詳細については、[認証]()を参照してください。

以下のGETコマンドを使用して、ビジターレコードを取得します：

```bash
GET /v3/privacy/visitor/accounts/{account}/profiles/{profile}?attributeId={attributeId}&amp;attributeValue={attributeValue}&amp;prettyName={prettyName}
```

このコマンドは以下のパラメータを使用します：

* `attributeId`
  * アカウントからの[ビジターID属性]()を表す数値ID。
* `attributeValue`
  * 検索する値。
  * 特殊文字を含む値はURLエンコードする必要があります。
* `prettyName`
  * 属性キーがレスポンスにどのように表示されるかを示すブール値：
    * **True** – 属性はユーザーフレンドリーな名前、例えば &#34;Lifetime Order Value&#34; として表示されます。
    * **False** – 属性は数値ID、例えば &#34;28471&#34; として表示されます。

### 権限要件

* サーバーサイドのリーダー、エディター、またはパブリッシャーのレガシー権限、または
* 最小限の **View** ビジタールックアッププラットフォーム権限

### 例：cURLリクエスト

```bash
curl -H &#39;Authorization: Bearer {token}&#39; \
 -G \
&#39;https://us-east-1-platform.tealiumapis.com/v3/privacy/visitor/accounts/my_account/profiles/main&#39; \
 --data-urlencode &#39;attributeId=86&#39; \
 --data-urlencode &#39;attributeValue=user@example.com&#39; \
 --data &#39;prettyName=true&#39;
```

### 例：レスポンス

レスポンスの形式については、例のビジターオブジェクトを参照してください。

### エラーメッセージ

このタスクの可能性のあるエラーメッセージは以下の通りです：

|エラーメッセージ| 説明|
|---| ---|
|400|  `{ &#34;message&#34;: &#34;属性IDまたは属性値が欠落しています&#34;}` |
|401|  `{ &#34;message&#34;: &#34;認証されていません&#34;}` |
| 404 | `システム内にビジターが見つかりません {  &#34;transactionId&#34;: {transactionId}  }` |
|429| `{ &#34;message&#34;: &#34;リクエストが多すぎます&#34;}` |
| 500 |`{ &#34;message&#34;: &#34;内部サーバーエラー&#34;}` |

## DELETE visitor

この呼び出しには、認証APIで返された地域固有のホストを使用する必要があります。詳細については、[認証]()を参照してください。

ビジターレコードを1つ以上削除する前に、以下の点を考慮してください：

* ビジターレコードの削除リクエストは、ビジターID値に関連するすべてのデータの削除を引き起こします。これには、ステッチされたビジターレコードも含まれます。
* 削除リクエストは処理のためにキューに入れられ、完了までに最大30日かかる場合があります。
* ビジターが他のビジターに置き換えられた場合、または他のビジターに置き換えられた場合、ステッチされたすべてのビジターが削除されます。
* DELETEコマンドへのパラメータは、クエリストリングパラメータではなく、コンテンツタイプ &#34; `application/x-www-form-urlencoded`&#34; を使用してURLエンコードされたフォームフィールドとして渡す必要があります。

以下のDELETEコマンドを使用して、ビジターレコードを削除します：

```bash
DELETE /v3/privacy/visitor/accounts/{account}/profiles/{profile}?attributeID={value}&amp;attributeValue={value}
```

このコマンドは以下のパラメータを使用します：

* `attributeId`  
アカウントからの[ビジターID属性]()を表す数値ID。
* `attributeValue`  
検索する値。

### 権限要件

* サーバーサイドのパブリッシャーレガシー権限、または
* **View, Edit, &amp; Delete** ビジタールックアッププラットフォーム権限

### 例：cURLリクエスト

```bash
curl -H &#39;Authorization: Bearer {token}&#39; \
-X DELETE \
&#39;https://us-east1-platform.tealiumapis.com/v3/privacy/visitor/accounts/my_account/profiles/main&#39; \
--data-urlencode &#34;attributeId=86&#34;
--data-urlencode &#34;attributeValue=user@example.com&#34;
```

### 例：レスポンス

削除リクエストへのレスポンスには、`transaction_id`とステータスが含まれます。`transaction_id`は、以前のリクエストのステータスを確認するためのGETトランザクション呼び出しで使用されます。次のステータス文字列が可能です：**PENDING**、**SUCCESS**、または**FAILED**。

成功したレスポンスは、`transactionId`値を持つ202 Acceptedメッセージを表示します。同じ`account`、`profile`、`attributeId`、および`attributeValue`を持つリクエストが既に存在し、そのトランザクションステータスが**PENDING**である場合、既存のトランザクションIDが返されます。以下のようになります：

```json
{
&#34;transactionId&#34; : &#34;{transactionId1}&#34;
}
```

### エラーメッセージ

このタスクの可能性のあるエラーメッセージは以下の通りです：

|エラーメッセージ| 説明|
|---| ---|
|400|  `{ &#34;message&#34;: &#34;属性IDまたは属性値が欠落しています&#34;}` |
|401|  `{ &#34;message&#34;: &#34;認証されていません&#34;}` |
|404|  `システム内にビジターが見つかりません {  &#34;transactionId&#34;: {transactionId}  }` |
|429| `{ &#34;message&#34;: &#34;リクエストが多すぎます&#34;}` |

## GET transaction

この呼び出しには、認証APIで返された地域固有のホストを使用する必要があります。詳細については、[認証]()を参照してください。

トランザクションとは、任意のDELETEビジターリクエストを指します。DELETEビジターリクエストは後で処理するためにキューに入れられます。これにより、`transaction_id`がそのリクエストの一意のレコードとなり、処理ステータスを確認するためのIDとして使用されます。

以下のGETコマンドを使用して、トランザクションのステータスを確認します：

```bash
GET /v3/privacy/visitor/accounts/{account}/profiles/{profile}/transactions/{transaction_id}
```

### 権限要件

* サーバーサイドのリーダー、エディター、またはパブリッシャーのレガシー権限、または
* 最小限の **View** ビジタールックアッププラットフォーム権限

### 例：cURLリクエスト

APIキーからベアラートークンを生成する方法については、[認証]()を参照してください。ベアラートークンはAPIキーではなく、API呼び出しで使用されます。

```bash
curl -H &#39;Authorization: Bearer {token}&#39; \
https://us-east-1-platform.tealiumapis.com/v3/privacy/visitor/accounts/my_account/profiles/main/transactions/0123456789
```

### 例：レスポンス

レスポンスには、キーが`transaction_id`で値が次のステータス文字列のいずれかであるキー-値ペアを含むオブジェクトが含まれます：**PENDING**、**SUCCESS**、または**FAILED**。

```json
{
  &#34;0123456789&#34; : &#34;SUCCESS&#34;
}
```

### エラーメッセージ

このタスクの可能性のあるエラーメッセージは以下の通りです：

|エラーメッセージ| 説明|
|---| ---|
|401|  `{ &#34;message&#34;: &#34;認証されていません&#34;}` |
|404|  `システム内にビジターが見つかりません {  &#34;transactionId&#34;: {transactionId}  }` |
|429| `{ &#34;message&#34;: &#34;リクエストが多すぎます&#34;}` |

## GET Visitor ID Attributes

以下のGETコマンドを使用して、アカウントで利用可能なビジターID属性のリストを取得します：

```bash
GET /v3/privacy/visitor/accounts/{account}/profiles/{profile}/ids
```

### 権限要件

* サーバーサイドのリーダー、エディター、またはパブリッシャーのレガシー権限、または
* 最小限の **View** ビジタールックアッププラットフォーム権限

### 例：cURLリクエスト

```bash
curl -H &#39;Authorization: Bearer {token}&#39; \
https://platform.tealiumapis.com/v3/privacy/visitor/accounts/my_account/profiles/main/ids
```

### 例：レスポンス

このコマンドのレスポンスは、ビジターID属性の数値IDと名前を表すキー-値ペアのオブジェクトです。

```json
{
  &#34;43&#34; : &#34;Email Address&#34;,
  &#34;57&#34; : &#34;Tax ID Number&#34;
}
```

### エラーメッセージ

このタスクの可能性のあるエラーメッセージは以下の通りです：

|エラーメッセージ| 説明|
|---| ---|
|401|  `{ &#34;message&#34;: &#34;認証されていません&#34;}` |
|404|  `{ &#34;message&#34; : &#34;アカウントとプロファイルにビジターIDが見つかりませんでした&#34;}` |
|429| `{ &#34;message&#34;: &#34;リクエストが多すぎます&#34;}` |
|500|  `{ &#34;message&#34; : &#34;内部サーバーエラー&#34;}` |
