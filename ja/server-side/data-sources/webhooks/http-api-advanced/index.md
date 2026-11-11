---
title: HTTP API - 高度な受信 Webhook セットアップガイド
description: この記事では、HTTP API - Advanced データソースの使用方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/webhooks/http-api-advanced/
---
## 仕組み

HTTP API - Advanced データソースは、受信したリクエスト本文を条件に応じて解析できる汎用データソースです。このデータソースは、複雑なオブジェクトのフラット化とイベントのバッチ処理をサポートし、1 回の HTTP 呼び出しでリアルタイムのイベントデータを収集できる HTTP エンドポイントを提供します。このエンドポイントは柔軟性が高く、Web ページのトラッキングピクセルとして、またはカスタムアプリケーションの JSON API として実装できます。

このデータソースは HTTP API データソースと似ていますが、複雑な JSON オブジェクトとバッチ処理もサポートしています。

複雑な JSON オブジェクトを使用して HTTP POST で送信されたイベントは、次のようにフラット化されます。

* イベント属性名は、オブジェクトのプロパティを小文字に変換し、アンダースコア（「\_」）で結合して作成されます。例：  
ソースデータ：`"alpha" : { "beta" : true }`  
フラット化されたイベント属性：`"alpha_beta" : true`
* 配列内の数値、ブール値、文字列は保持されます。
* 配列内のオブジェクトと配列は文字列化されます。

リアルタイムでデータを送信する必要があり、標準の Tealium Collect エンドポイントの形式要件を満たすようにリクエストを変更できない場合は、このデータソースタイプを使用します。

### 要件

* Event Streaming または Customer Data Platform（CDP）

### バッチイベント

HTTP API - Advanced データソースの HTTP エンドポイントは、1 回のリクエストで複数のイベントをサポートします。これらのイベントをバッチイベントと呼びます。バッチイベントでは、すべてのレコードのステータスに基づく 1 つのレスポンスコードを受信します。1 つのレコードまたはイベントが失敗しても、そのイベントのみが失敗し、残りは処理されます。

### レート制限

HTTP API - Advanced データソースでは、最大レートが 100 イベント/秒に制限されています。

たとえば、次のように送信できます。

* 1 回の呼び出しにつき 1 イベントの場合、1 秒あたり 100 回呼び出せます。
* 1 回の呼び出しにつき 10 イベントの場合、1 秒あたり 10 回呼び出せます。
* 1 回の呼び出しにつき 100 イベントの場合、1 秒あたり 1 回呼び出せます。

レート制限を超えると、リクエストが多すぎることを示す HTTP 429 レスポンスが Tealium から送信されます。


<blockquote>
ビジネス上、より高いイベント上限が必要な場合は、Tealium のアカウントマネージャーにお問い合わせください。
</blockquote>


## POST メソッド

HTTP API - Advanced データソースは POST メソッドをサポートしています。GET メソッドのリクエストには、[HTTP API](https://docs.tealium.com/platforms/http-api/endpoint-spec/) を使用してください。

HTTP API - Advanced データソースにアクセスするには、次のエンドポイントを使用します。

```
https://collect.tealiumiq.com/integration/event/ACCOUNT/PROFILE/DATA_SOURCE_KEY
```

Trace ツールによるデバッグをサポートするには、オプションの `tealium_trace_id` クエリパラメータ（`tealium_trace_id=TRACEID`）を使用します。Trace の使用方法について詳しくは、[Trace について](https://docs.tealium.com/about-trace/)を参照してください。


<blockquote>
データソースキーを確認するには、**データソース**ダッシュボードに移動し、使用するデータソースをクリックして、**データソースキー**フィールドからキーをコピーします。
</blockquote>


## 訪問識別子

訪問のトラッキングでは、次の組み合わせを使用します。

* **匿名 ID**：通常、訪問を匿名でトラッキングするために使用する ID（デバイスやブラウザから取得する ID など）です。[既知の訪問](#known-visitors-server-to-server)の場合は、ユーザー識別子に基づく値を使用できます。
* **ユーザー識別子**：訪問が判明した後に送信されます。特定のデバイスではなく、ユーザーを識別する値に基づきます。

### 匿名 ID

匿名 ID は、Customer Data Platform（CDP）がイベントや訪問をまたいで訪問を関連付けるために使用する匿名識別子です。この値が GUID であり、同じ訪問に対して一貫していることを確認してください。また、この値はサーバーサイドプロファイルごとに一意である必要があります。

匿名 ID のキー名は `tealium_visitor_id` です。

ビジネス上のユースケースに応じて、匿名の値または既知のユーザー識別子に基づく値を使用できます。

#### 匿名の値

|CDP| Event Streaming|
|---| ---|
| 必須 | 該当なし |

Tag Management を使用し、匿名訪問プロファイルを拡充するためにサーバー間で API 呼び出しを送信している場合、`tealium_visitor_id` の値は `utag_main_v_id` Cookie の値と一致する必要があります。utag.js の組み込み変数について詳しくは、[JavaScript（Web）> データレイヤー](https://docs.tealium.com/platforms/javascript/data-layer/)を参照してください。


<blockquote>
Adobe Launch または Google Tag Manager を使用している場合、この値は **TEAL** Cookie の `v` 部分と一致する必要があります。
</blockquote>


#### サーバー間通信における既知の訪問

|CDP| Event Streaming|
|---| ---|
| 必須 | 推奨 |

既知の訪問のデータ（`email_address` など、訪問 ID 属性の値が存在する場合）を送信するときは、次の項目を連結した値を含めます。

* アカウント
* プロファイル  
プロファイル名を含めることで、`tealium_visitor_id` がサーバーサイドプロファイルごとに一意になります。これは、同じ訪問プロファイルを同一リージョン内の複数のサーバーサイドプロファイルに送信する場合に不可欠です。
* 訪問 ID 属性の ID と値 
<blockquote>
訪問 ID 属性の ID は、属性リストの属性名の横、または展開した詳細内で確認できます。詳しくは、[属性について](https://docs.tealium.com/about-attributes/#attribute-ids)を参照してください。
</blockquote>

* `tealium_visitor_id` パラメータの値

たとえば、次の値があるとします。

* アカウント名：`my-account`
* プロファイル：`main`
* 訪問 ID 属性の ID：`7688`
* 渡す顧客番号の値：`45653454`

これらの値は、次のように連結します。

```
tealium_visitor_id":"__my-account_main__7688_45653454__"
```


<blockquote>
続行する前に、`tealium_visitor_id` が正しくフォーマットされていることを確認してください。パラメータのフォーマットが正しくない場合、CDP でエラーが発生し、適切にトラッキングされない可能性があります。
</blockquote>


JSON の例：

```json
{
    "tealium_account"    : "my-account",
    "tealium_profile"    : "main",
    "tealium_event"      : "user_login",
    "email_address"      : "user@example.com",
    "customer_number"    : "45653454", 
    "tealium_visitor_id" : "__my-account_main__7688_45653454__"
}
```


<blockquote>
匿名訪問と既知の訪問のどちらを使用する場合でも、API 呼び出しに一貫した `tealium_visitor_id` が含まれていないと、イベントごとに新しい訪問が生成され、訪問のスティッチングができなくなります。
</blockquote>


### ユーザー識別子

CDP を使用する場合、トラッキング呼び出しで既知のユーザー識別子を渡すことができます。たとえば、`email_address` や `login_id` です。

Event Streaming を使用し、ベンダーコネクタに ID を提供する必要がある場合にも、ユーザー識別子が必要です。

CDP では、これらのユーザー識別子を使用して[訪問 ID 属性](https://docs.tealium.com/visitor-id-attribute/)を拡充します。

## データソースの追加

このセクションでは、HTTP API - Advanced データソースを追加し、Webhook を作成する方法について説明します。

続行する前に HTTP API - Advanced データソースを追加し、生成されたエンドポイントをコピーして外部システムで使用します。


<blockquote>
HTTP API - Advanced エンドポイントは、データソースを追加してプロファイルをパブリッシュするまで有効になりません。
</blockquote>


関連項目：[データソースを追加する方法](https://docs.tealium.com/about-data-sources/)

## レスポンスコード

|レスポンスコード| 説明|
|---| ---|
| HTTP 204 | リクエスト成功|
| HTTP 400 | 不正な形式の JSON リクエスト|
| HTTP 404 |

## 例

HTTP API - Advanced Incoming Webhook は、JavaScript、bash スクリプト、または curl を使用して HTTP API Advanced 呼び出しを送信する場合に便利です。
### ペイロードとしての JSON 配列

JSON 配列をペイロード全体として渡すと、複数のイベント（バッチ）として扱われます。

```json
[
  {
    "tealium_visitor_id": "503126878d17fcd6bde7df320ff6eb7c278a1c42f",
    "my_string": "12345a",
    "Detail": {
      "Name": "Event A"
    }
  },
  {
    "tealium_visitor_id": "e0f7e1bb7c5efa1afeba05fc4ddf93aa86caee629",
    "my_string": "12345b",
    "Detail": {
      "Name": "Event B"
    }
  }
]
```

このペイロードは、複数のイベントに変換されます。

```json
// First Event
  {
    "tealium_visitor_id": "503126878d17fcd6bde7df320ff6eb7c278a1c42f",
    "my_string": "12345a",
    "detail_name":  "Event A"
  }

  // Second Event
  {
    "tealium_visitor_id": "e0f7e1bb7c5efa1afeba05fc4ddf93aa86caee629",
    "my_string": "12345b",
    "detail_name":  "Event B"
  }
```

### ペイロード内のキーと値としての JSON 配列

ペイロード内のキーの値として配列を渡すと、その配列は文字列の配列にフラット化されます。

たとえば、次の配列は、

```json
{
   "tealium_visitor_id": "503126878d17fcd6bde7df320ff6eb7c278a1c42f",
   "my_string": "12345a",
   "detail_name": "Event A",
   "events": [
       {
           "id": "1",
           "name": "Event A"
       },
       {
           "id": "2",
           "name": "Event B"
       },
       {
           "id": "3",
           "name": "Event C"
       }
   ]
}

```

次の文字列の配列にフラット化されます。

```json
{
   "tealium_visitor_id": "503126878d17fcd6bde7df320ff6eb7c278a1c42f",
   "my_string": "12345a",
   "detail_name": "Event A",
       "events": [
        "{\"id\":\"1\",\"name\":\"Event A\"}",
        "{\"id\":\"2\",\"name\":\"Event B\"}",
        "{\"id\":\"3\",\"name\":\"Event C\"}"
    ]
}

```

複雑なビジネスユースケースや要件については、HTTP API - Advanced エンドポイントに加えて、またはその代わりに、[Tealium Event Transformation 関数](https://docs.tealium.com/about-data-transformation-functions/)の使用を検討してください。

## 複雑なオブジェクト

このセクションでは、複雑なオブジェクトの入力コードと、その結果生成される（フラット化された）出力の例を示します。

### フラット化前

次の購入イベントの例は、複雑なオブジェクトを含むクライアント側の e コマースイベントがどのようにフラット化されるかを示しています。

```json
{
   "tealium_visitor_id": "503126878d17fcd6bde7df320ff6eb7c278a1c42f",
   "my_string": "12345a",
   "detail_name": "Event A",
  "ecommerce": {
    "event": "purchase",
    "purchase": {
      "customer": {
        "id": "8237572",
        "email": "john.smith@example.com",
        "city": "San Diego",
        "state": "CA",
        "country": "United States"
      },
      "order": {
        "id": "ORD123456",
        "store": "mobile web",
        "subtotal": "2524.00",
        "total": "2549.00"
      },
      "product": {
          "name": ["Product One", "Product Two"],
          "id": ["PROD123","PROD456"],
          "price": ["12.00","1250.00"],
          "brand": ["Ralph Lauren","Lucky"],
          "category": ["Apparel","Apparel"],
          "quantity": [1,1]
        }
    }
  }
}

```

### フラット化後

フラット化すると、購入イベントは次のようになります。

```json
{
   "tealium_visitor_id": "503126878d17fcd6bde7df320ff6eb7c278a1c42f",
   "my_string": "12345a",
   "detail_name": "Event A",
    "ecommerce_event": "purchase",
    "ecommerce_purchase_customer_id": "8237572",
    "ecommerce_purchase_customer_email": "john.smith@example.com",
    "ecommerce_purchase_customer_city": "San Diego",
    "ecommerce_purchase_customer_state": "CA",
    "ecommerce_purchase_customer_country": "United States",
    "ecommerce_purchase_order_id": "ORD123456",
    "ecommerce_purchase_order_store": "mobile web",
    "ecommerce_purchase_order_subtotal": "2524.00",
    "ecommerce_purchase_order_total": "2549.00",
    "ecommerce_purchase_product_name": ["Product One", "Product Two"],
    "ecommerce_purchase_product_id": ["PROD123","PROD456"],
    "ecommerce_purchase_product_price": ["12.00","1250.00"],
    "ecommerce_purchase_product_brand": ["Ralph Lauren","Lucky"],
    "ecommerce_purchase_product_category": ["Apparel","Apparel"],
    "ecommerce_purchase_product_quantity": [1,1]
}

```

## 制限事項

* ペイロードの最大サイズは 3.5 MB です。
* リクエストごとに処理できるレコード数は、ペイロードサイズによって制限されます。