---
title: HTTP API - 高度なインカミングウェブフック構成ガイド
description: この記事では、HTTP API - 高度なデータソースの使用方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/webhooks/setup-guides/http-api-advanced/
---
## 仕組み

HTTP API - 高度なデータソースは、条件によって受信リクエストボディを解析できる汎用的なデータソースです。このデータソースは、HTTPエンドポイントを提供し、複雑なオブジェクトのフラット化とバッチイベントのサポートを備えた単一のHTTP呼び出しでリアルタイムのイベントデータを収集することができます。エンドポイントは柔軟で、ウェブページのトラッキングピクセルやカスタムアプリケーションのJSON APIとして実装することができます。

このデータソースは、HTTP APIデータソースと似ていますが、複雑なJSONオブジェクトとバッチ処理の追加サポートがあります。

HTTP POSTを使用して複雑なJSONオブジェクトを送信すると、以下のようにフラット化されます：

* イベント属性名は、オブジェクトのプロパティを小文字にしてアンダースコア("\_")で結合して作成されます。例えば：  
元のデータ: `"alpha" : { "beta" : true }`  
フラット化されたイベント属性: `"alpha_beta" : true`
* 配列内の数値、ブーリアン、文字列は保持されます。
* 配列内のオブジェクトと配列は文字列化されます。

リアルタイムでデータを送信する必要があり、リクエストを標準のTealium Collectエンドポイントの形式要件に合わせて変更することができない場合、このデータソースタイプを使用します。

### 要件

* Tealium EventStreamまたはTealium AudienceStream

### バッチイベント

HTTP API - 高度なデータソースのHTTPエンドポイントは、単一のリクエストで複数のイベントをサポートします。これらのイベントはバッチイベントと呼ばれます。バッチイベントでは、すべてのレコードのステータスに基づいて一つのレスポンスコードを受け取ります。単一のレコード/イベントが失敗した場合、そのイベントのみが失敗し、残りは処理されます。

### レート制限

HTTP API - 高度なデータソースは、最大レート制限として100イベント/秒をサポートしています。

例えば、以下のように送信する場合：

* 1回の呼び出しにつき1イベントを送信する場合、1秒あたり100回の呼び出しが可能です。
* 1回の呼び出しにつき10イベントを送信する場合、1秒あたり10回の呼び出しが可能です。
* 1回の呼び出しにつき100イベントを送信する場合、1秒あたり1回の呼び出しが可能です。

レート制限を超えると、TealiumはHTTP 429レスポンスを送信し、リクエストが多すぎることを示します。


<blockquote>
ビジネスのニーズが高いイベント制限を必要とする場合は、Tealiumのアカウントマネージャーに連絡してください。
</blockquote>


## POSTメソッド

HTTP API - 高度なデータソースはPOSTメソッドをサポートしています。GETメソッドのリクエストについては、[HTTP API](https://docs.tealium.com/platforms/http-api/endpoint-spec/)を使用してください。

HTTP API - 高度なデータソースにアクセスするための次のエンドポイントを使用します：

```
https://collect.tealiumiq.com/integration/event/ACCOUNT/PROFILE/DATA_SOURCE_KEY
```

オプションの`tealium_trace_id`クエリパラメータ(`tealium_trace_id=TRACEID`)を使用して、Traceツールを使用したデバッグをサポートします。トレースの使用についての詳細は、[About Trace](https://docs.tealium.com/about-trace/)を参照してください。


<blockquote>
データソースキーを見つけるには、**Data Sources**ダッシュボードに移動し、使用したいデータソースをクリックし、**Data Source Key**フィールドからキーをコピーします。
</blockquote>


## 訪問識別子

AudienceStreamは以下の組み合わせで訪問を追跡します：

* **匿名ID**：通常、訪問を匿名で追跡するために使用されるID（例えば、デバイスやブラウザから）。[既知の訪問](#known-visitors-server-to-server)の場合、ユーザー識別子に基づく値を使用できます。
* **ユーザー識別子**：訪問が既知であることが確認された後に送信されます。特定のデバイスではなく、ユーザーを識別する値に基づいています。

### 匿名ID

匿名IDは、AudienceStreamがイベントと訪問の間で訪問を関連付けるために使用する匿名識別子です。この値はGUIDであることと、訪問に対して一貫性があることを確認してください。また、この値は各サーバーサイドプロファイルごとに一意である必要があります。

匿名IDのキー名は`tealium_visitor_id`です。

ビジネスケースに応じて、匿名値または既知のユーザー識別子に基づく値を使用できます。

#### 匿名値

|AudienceStream| EventStream|
|---| ---|
| 必須 | N/A |

Tealium iQタグ管理を使用し、API呼び出しをサーバー間で送信して匿名訪問プロファイルをエンリッチする場合、`tealium_visitor_id`の値は`utag_main_v_id`クッキーの値と一致する必要があります。utag.jsからの組み込み変数についての詳細は、[JavaScript (Web) > Data Layer](https://docs.tealium.com/platforms/javascript/data-layer/)を参照してください。


<blockquote>
Adobe LaunchまたはGoogle Tag Managerを使用している場合、値は**TEAL**クッキーの`v`部分と一致する必要があります。
</blockquote>


#### 既知の訪問サーバー間

|AudienceStream| EventStream|
|---| ---|
| 必須 | 推奨 |

既知の訪問のデータを送信する場合（`email_address`などの訪問ID属性に値が存在する場合）、以下のものを連結して含めます：

* アカウント
* プロファイル  
プロファイル名を含めることで、`tealium_visitor_id`が各サーバーサイドプロファイルごとに一意になり、同じ訪問プロファイルが一つの地域内の複数のサーバーサイドプロファイルに送信される場合に必要となります。
* 訪問ID属性IDと値 
<blockquote>
訪問ID属性IDは、属性リストの属性名の隣や詳細を展開した中にあります。詳細については、[About Attributes](https://docs.tealium.com/about-attributes/#attribute-ids)を参照してください。
</blockquote>

* `tealium_visitor_id`パラメータの値

例えば、以下の値の場合：

* アカウント名：`my-account`
* プロファイル：`main`
* 訪問ID属性ID：`7688`
* 伝えたい顧客番号の値：`45653454`

これらの値を以下のように連結します：

```
tealium_visitor_id":"__my-account_main__7688_45653454__"
```


<blockquote>
`tealium_visitor_id`が正しくフォーマットされていることを確認してから進めてください。フォーマットが正しくないパラメータはAudienceStreamでエラーを引き起こし、正しく追跡されない可能性があります。
</blockquote>


JSONの例：

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
匿名訪問を使用するか既知の訪問を使用するかに関わらず、API呼び出しに一貫した`tealium_visitor_id`が含まれていない場合、各イベントは新しい訪問を生成し、訪問のスティッチングは不可能になります。
</blockquote>


### ユーザー識別子

AudienceStreamを使用する場合、トラッキング呼び出しに既知のユーザー識別子を渡すことができます。例えば、`email_address`や`login_id`などです。

ユーザー識別子は、EventStreamを使用していてベンダーコネクタにIDを提供する必要がある場合にも必要です。

AudienceStreamでは、これらのユーザー識別子は[訪問ID属性](https://docs.tealium.com/visitor-id-attribute/)をエンリッチするために使用されます。

## データソースの追加

このセクションでは、HTTP API - 高度なデータソースを追加し、ウェブフックを作成する方法について説明します。

HTTP API - 高度なデータソースを追加してから進め、生成されたエンドポイントを外部システムで使用するためにコピーします。


<blockquote>
HTTP API - 高度なエンドポイントは、データソースを追加し、プロファイルを公開するまでアクティブになりません。
</blockquote>


関連：[データソースの追加方法](https://docs.tealium.com/about-data-sources/)

## レスポンスコード

|レスポンスコード| 説明|
|---| ---|
| HTTP 204 | リクエスト成功|
| HTTP 400 | JSONリクエストの形式が不正|
| HTTP 404 |

## 例

HTTP API - 高度なインカミングウェブフックは、JavaScript、bashスクリプト、またはcurlを使用してHTTP API高度な呼び出しを送信したい場合に便利です。

### JSON配列をペイロードとして

JSON配列を全体のペイロードとして渡すと、それは複数のイベント（バッチング）として扱われます。

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
このペイロードは、いくつかのイベントに変換されます：

```json
// 最初のイベント
  {
    "tealium_visitor_id": "503126878d17fcd6bde7df320ff6eb7c278a1c42f",
    "my_string": "12345a",
    "detail_name":  "イベントA"
  }

  // 二番目のイベント
  {
    "tealium_visitor_id": "e0f7e1bb7c5efa1afeba05fc4ddf93aa86caee629",
    "my_string": "12345b",
    "detail_name":  "イベントB"
  }
```

### ペイロードのキー値としてのJSON配列

ペイロードのキーの値として配列を渡すと、その配列は文字列の配列にフラット化されます。

例えば、以下の配列：

```json
{
   "tealium_visitor_id": "503126878d17fcd6bde7df320ff6eb7c278a1c42f",
   "my_string": "12345a",
   "detail_name": "イベントA",
   "events": [
       {
           "id": "1",
           "name": "イベントA"
       },
       {
           "id": "2",
           "name": "イベントB"
       },
       {
           "id": "3",
           "name": "イベントC"
       }
   ]
}

```

は、以下の文字列の配列にフラット化されます：

```json
{
   "tealium_visitor_id": "503126878d17fcd6bde7df320ff6eb7c278a1c42f",
   "my_string": "12345a",
   "detail_name": "イベントA",
       "events": [
        "{\"id\":\"1\",\"name\":\"イベントA\"}",
        "{\"id\":\"2\",\"name\":\"イベントB\"}",
        "{\"id\":\"3\",\"name\":\"イベントC\"}"
    ]
}

```

複雑なビジネスケースや要件に対しては、HTTP API - Advancedエンドポイントに加えて、または代わりに、[Tealiumイベント変換関数](https://docs.tealium.com/about-data-transformation-functions/)を使用することを検討してください。

## 複雑なオブジェクト

このセクションでは、複雑なオブジェクトの入力コードと結果の（フラット化された）出力の例を提供します。

### フラット化前

以下の購入イベントの例は、複雑なオブジェクトを持つクライアントサイドのeコマースイベントがどのようにフラット化されるかを示しています。

```json
{
   "tealium_visitor_id": "503126878d17fcd6bde7df320ff6eb7c278a1c42f",
   "my_string": "12345a",
   "detail_name": "イベントA",
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

フラット化後、購入イベントは次のようになります：

```json
{
   "tealium_visitor_id": "503126878d17fcd6bde7df320ff6eb7c278a1c42f",
   "my_string": "12345a",
   "detail_name": "イベントA",
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

* 最大ペイロードサイズは3.5 MBです。
* リクエストごとに処理できるレコードの数は、ペイロードサイズによって制限されます。
