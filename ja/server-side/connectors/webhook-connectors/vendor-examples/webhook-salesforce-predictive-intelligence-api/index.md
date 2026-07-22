---
title: Webhook Salesforce Predictive Intelligence APIの構成
description: Salesforce Predictive Intelligence APIのための高度なWebhook - テンプレート変数を使用したカスタムリクエストアクションの構成方法
url: https://docs.tealium.com/ja/server-side/connectors/webhook-connectors/vendor-examples/webhook-salesforce-predictive-intelligence-api/
---

## 概要

Salesforce Predictive Intelligence（旧iGoDigital）にHTTPリクエストを送信し、ユーザーのショッピングカートの変更を記録します。ショッピングカートはJSON URLパラメータとして表現されます。

## ベンダーの要件

### APIリクエストの例:

```
https://nova.collect.igodigital.com/c2/6391707/track_conversion?payload={.......}]
```

URLパラメータ `payload` の値はJSONです:

```json
{
    "cart": [
        {
            "item": "2890-17738",
            "quantity": "1",
            "price": "94.00",
            "unique_id": "1233388"
        },
        {
            "item": "2890-60773",
            "quantity": "2",
            "price": "133.00",
            "unique_id": "7113048"
        },
        {
            "item": "3414-301727",
            "quantity": "3",
            "price": "1.99",
            "unique_id": "7107457"
        }
    ],
    "order_number": "830100487001",
    "discount": "89.99",
    "shipping": "0.00",
    "user_info": {
        "email": "abc.xxx@tealium.com",
        "details": {}
    }
}

```

## アクションの実装

### メソッドフィールド

"GET"に構成します。

### URLフィールド

`{{url_template}}`に構成します。

URLはハードコーディング（組み込みのプロジェクトID付き）でも、テンプレートベースでも構いません。後者のアプローチは、データレイヤー属性の柔軟性を高めるために採用されています。以下のテンプレートセクションを参照してください。

### URLパラメータ

|名前| 値|
|---| ---|
|`payload`| `{{json_template}}`|

### テンプレート変数

テンプレートで参照され、置換される名前と値のペアを構成します。変数の値はこの例ではカスタム値ですが、動的なデータレイヤー属性として簡単に提供することができます。

|名前| 値| ノート|
|---| ---| ---|
|`projectId`| `6391707`|
|`cart.item`| PredictIntel Cart Items| [Set of Strings attribute]()|
|`cart.quantity`| PredictIntel Cart Quantities| Set of Strings attribute|
|`cart.price`| PredictIntel Cart Prices| Set of Strings attribute|
|`cart.id`| PredictIntel Cart IDs| Set of Strings attribute|
|`orderNumber`| `830100487001`|
|`discount`| `89.99`|
|`shipping`| `0.00`|
|`userEmail`| `abc.xxx@tealium.com`|


<blockquote>
変数は内部的にJSONに変換され、すべてのテンプレートで利用可能になります。
</blockquote>


#### 結果として得られるJSON構造:

```json
{

  "shipping": "0.00",
  "orderNumber": "830100487001",
  "userEmail": "abc.xxx@tealium.com",
  "cart": [
    {
      "id": "7113048",
      "price": "1.99",
      "item": "3414-301727",
      "quantity": "3"
    },
    {
      "id": "7107457",
      "price": "133.00",
      "item": "2890-60773",
      "quantity": "2"
    },
    {
      "id": "1233388",
      "price": "94.00",
      "item": "2890-17738",
      "quantity": "1"
    }
  ],
  "projectId": "6391707",
  "discount": "89.99"

}

```

### テンプレート

`url_template` 

```
https://nova.collect.igodigital.com/c2/{{projectId}}/track_conversion
```

`json_template` 

```json
{
    "cart": [
        {{#cart}}
        {
            "item": "{{item}}",
            "quantity": "{{quantity}}",
            "price": "{{price}}",
            "unique_id": "{{id}}"
        }{{#iter.hasNext}}, {{/iter.hasNext}}
        {{/cart}}
    ],
    "order_number": "{{orderNumber}}",
    "discount": "{{discount}}",
    "shipping": "{{shipping}}",
    "user_info": {
        "email": "{{userEmail}}",
        "details": {}
    }
}
```

### レンダリングされたテンプレート

内部的にテンプレートがレンダリングされ（下記参照）、参照された場所にその内容が注入されます。例えば、URLフィールドやURLパラメータなどです。

`url_template` 

```
https://nova.collect.igodigital.com/c2/6391707/track_conversion
```

`json_template` 

```json
{
    "cart": [
        {
            "item": "3414-301727",
            "quantity": "3",
            "price": "1.99",
            "unique_id": "7113048"
        },
        {
            "item": "2890-60773",
            "quantity": "2",
            "price": "133.00",
            "unique_id": "7107457"
        },
        {
            "item": "2890-17738",
            "quantity": "1",
            "price": "94.00",
            "unique_id": "1233388"
        }
    ],
    "order_number": "830100487001",
    "discount": "89.99",
    "shipping": "0.00",
    "user_info": {
        "email": "abc.xxx@tealium.com",
        "details": {}
    }
}
```


## アクション構成のスクリーンショット

![](https://docs.tealium.com/images/server-side/example)