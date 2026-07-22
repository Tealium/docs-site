---
title: Webhook - Keen.io API
description: Keen.io API用の高度なWebhook - テンプレート変数を使用したカスタムリクエストアクションの構成方法
url: https://docs.tealium.com/ja/server-side/connectors/webhook-connectors/vendor-examples/webhook-keenio-api/
---

## 概要

Keen.ioにhttpリクエストを送信し、単一のトランザクションに対して複数の購入イベントを記録します。リクエストボディ全体はJSONメッセージです。

## ベンダーの要件

ドキュメンテーション: [Keen IO Data Collection API](https://keen.io/docs/data-collection/)

リクエストURL

```
https://api.keen.io/API_VERSION/projects/PROJECT_ID/events

```

### APIリクエストボディの例:

```json
{
    "purchases": [
        {
            "item": "Golden gadget",
            "price": 25.50,
            "transaction_id": "f029342"
        },
        {
            "item": "Different gadget",
            "price": 17.75,
            "transaction_id": "f029342"
        }
    ],
    "transactions": [
        {
            "id": "f029342",
            "items": 2,
            "total": 43.25
        }
    ]
}

```

## アクションの実装

### メソッドフィールド

`POST`に構成します。

### URLフィールド

`{{url_template}}`に構成します。

URLはハードコーディング（組み込みのAPIバージョンとプロジェクトID付き）でも、テンプレートベースでも構いません。後者のアプローチは、データレイヤー属性の柔軟性を高めるために採用されています。以下のテンプレートセクションを参照してください。

### ボディコンテンツタイプ

`application/json`を選択します。

### ボディデータ

"Body"オプションを選択し、テンプレート参照を提供します。

|名前| 値|
|---| ---|
|Body| `{{json_template}}`|

### テンプレート変数

テンプレートで参照され、置換される名前と値のペアを構成します。変数の値はこの例ではカスタム値ですが、動的なデータレイヤー属性として簡単に提供することができます。

|名前| 値| ノート|
|---| ---| ---|
|`transactionId`| `f029342`|
|`transactionItemCount`| `2`|
|`transactionTotalPrice`| `43.25`|
|`purchases.item`| Keen.io Purchase Items| 文字列のセット属性|
|`purchases.price`| Keen.io Purchase Prices| 文字列のセット属性|
|`apiVersion`| `3.0`|
|`projectId`| `987.65`|


<blockquote>
変数は内部的にJSONに変換され、すべてのテンプレートで利用可能になります。
</blockquote>


#### 結果のJSON構造:

```json
{
  "purchases": [
    {
      "price": "17.75",
      "item": "Different gadget"
    },
    {
      "price": "25.50",
      "item": "Golden gadget"
    }
  ],
  "apiVersion": "3.0",
  "transactionId": "f029342",
  "transactionItemCount": "2",
  "transactionTotalPrice": "43.25",
  "projectId": "98765"
}

```

### テンプレート

`url_template`

```
https://api.keen.io/{{apiVersion}}/projects/{{projectId}}/events
```

`json_template`   

```json
{
    "purchases": [
        {{#purchases}}
        {
            "item": "{{item}}",
            "price": {{price}},
            "transaction_id": "{{transactionId}}"
        }{{#iter.hasNext}}, {{/iter.hasNext}}
        {{/purchases}}
    ],
    "transactions": [
        {
            "id": "{{transactionId}}",
            "items": {{transactionItemCount}},
            "total": {{transactionTotalPrice}}
        }
    ]
}
 ```


### レンダリングされたテンプレート

内部的にテンプレートがレンダリングされ（下記参照）、参照された場所にその内容が注入されます。例えば、URLフィールドやBodyなど。

`url_template`

```
https://api.keen.io/3.0/projects/98765/events
```

`json_template`

```json
{
    "purchases": [
        {
            "item": "Different gadget",
            "price": 17.75,
            "transaction_id": "f029342"
        },
        {
            "item": "Golden gadget",
            "price": 25.50,
            "transaction_id": "f029342"
        }
    ],
    "transactions": [
        {
            "id": "f029342",
            "items": 2,
            "total": 43.25
        }
    ]
}
```


## アクション構成のスクリーンショット

![](https://docs.tealium.com/images/server-side/example)