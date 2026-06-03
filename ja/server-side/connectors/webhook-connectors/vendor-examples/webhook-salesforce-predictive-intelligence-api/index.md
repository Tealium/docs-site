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
    &#34;cart&#34;: [
        {
            &#34;item&#34;: &#34;2890-17738&#34;,
            &#34;quantity&#34;: &#34;1&#34;,
            &#34;price&#34;: &#34;94.00&#34;,
            &#34;unique_id&#34;: &#34;1233388&#34;
        },
        {
            &#34;item&#34;: &#34;2890-60773&#34;,
            &#34;quantity&#34;: &#34;2&#34;,
            &#34;price&#34;: &#34;133.00&#34;,
            &#34;unique_id&#34;: &#34;7113048&#34;
        },
        {
            &#34;item&#34;: &#34;3414-301727&#34;,
            &#34;quantity&#34;: &#34;3&#34;,
            &#34;price&#34;: &#34;1.99&#34;,
            &#34;unique_id&#34;: &#34;7107457&#34;
        }
    ],
    &#34;order_number&#34;: &#34;830100487001&#34;,
    &#34;discount&#34;: &#34;89.99&#34;,
    &#34;shipping&#34;: &#34;0.00&#34;,
    &#34;user_info&#34;: {
        &#34;email&#34;: &#34;abc.xxx@tealium.com&#34;,
        &#34;details&#34;: {}
    }
}

```

## アクションの実装

### メソッドフィールド

&#34;GET&#34;に構成します。

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

変数は内部的にJSONに変換され、すべてのテンプレートで利用可能になります。

#### 結果として得られるJSON構造:

```json
{

  &#34;shipping&#34;: &#34;0.00&#34;,
  &#34;orderNumber&#34;: &#34;830100487001&#34;,
  &#34;userEmail&#34;: &#34;abc.xxx@tealium.com&#34;,
  &#34;cart&#34;: [
    {
      &#34;id&#34;: &#34;7113048&#34;,
      &#34;price&#34;: &#34;1.99&#34;,
      &#34;item&#34;: &#34;3414-301727&#34;,
      &#34;quantity&#34;: &#34;3&#34;
    },
    {
      &#34;id&#34;: &#34;7107457&#34;,
      &#34;price&#34;: &#34;133.00&#34;,
      &#34;item&#34;: &#34;2890-60773&#34;,
      &#34;quantity&#34;: &#34;2&#34;
    },
    {
      &#34;id&#34;: &#34;1233388&#34;,
      &#34;price&#34;: &#34;94.00&#34;,
      &#34;item&#34;: &#34;2890-17738&#34;,
      &#34;quantity&#34;: &#34;1&#34;
    }
  ],
  &#34;projectId&#34;: &#34;6391707&#34;,
  &#34;discount&#34;: &#34;89.99&#34;

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
    &#34;cart&#34;: [
        {{#cart}}
        {
            &#34;item&#34;: &#34;{{item}}&#34;,
            &#34;quantity&#34;: &#34;{{quantity}}&#34;,
            &#34;price&#34;: &#34;{{price}}&#34;,
            &#34;unique_id&#34;: &#34;{{id}}&#34;
        }{{#iter.hasNext}}, {{/iter.hasNext}}
        {{/cart}}
    ],
    &#34;order_number&#34;: &#34;{{orderNumber}}&#34;,
    &#34;discount&#34;: &#34;{{discount}}&#34;,
    &#34;shipping&#34;: &#34;{{shipping}}&#34;,
    &#34;user_info&#34;: {
        &#34;email&#34;: &#34;{{userEmail}}&#34;,
        &#34;details&#34;: {}
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
    &#34;cart&#34;: [
        {
            &#34;item&#34;: &#34;3414-301727&#34;,
            &#34;quantity&#34;: &#34;3&#34;,
            &#34;price&#34;: &#34;1.99&#34;,
            &#34;unique_id&#34;: &#34;7113048&#34;
        },
        {
            &#34;item&#34;: &#34;2890-60773&#34;,
            &#34;quantity&#34;: &#34;2&#34;,
            &#34;price&#34;: &#34;133.00&#34;,
            &#34;unique_id&#34;: &#34;7107457&#34;
        },
        {
            &#34;item&#34;: &#34;2890-17738&#34;,
            &#34;quantity&#34;: &#34;1&#34;,
            &#34;price&#34;: &#34;94.00&#34;,
            &#34;unique_id&#34;: &#34;1233388&#34;
        }
    ],
    &#34;order_number&#34;: &#34;830100487001&#34;,
    &#34;discount&#34;: &#34;89.99&#34;,
    &#34;shipping&#34;: &#34;0.00&#34;,
    &#34;user_info&#34;: {
        &#34;email&#34;: &#34;abc.xxx@tealium.com&#34;,
        &#34;details&#34;: {}
    }
}
```


## アクション構成のスクリーンショット

![](/images/server-side/example)