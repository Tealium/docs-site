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
    &#34;purchases&#34;: [
        {
            &#34;item&#34;: &#34;Golden gadget&#34;,
            &#34;price&#34;: 25.50,
            &#34;transaction_id&#34;: &#34;f029342&#34;
        },
        {
            &#34;item&#34;: &#34;Different gadget&#34;,
            &#34;price&#34;: 17.75,
            &#34;transaction_id&#34;: &#34;f029342&#34;
        }
    ],
    &#34;transactions&#34;: [
        {
            &#34;id&#34;: &#34;f029342&#34;,
            &#34;items&#34;: 2,
            &#34;total&#34;: 43.25
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

&#34;Body&#34;オプションを選択し、テンプレート参照を提供します。

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

変数は内部的にJSONに変換され、すべてのテンプレートで利用可能になります。

#### 結果のJSON構造:

```json
{
  &#34;purchases&#34;: [
    {
      &#34;price&#34;: &#34;17.75&#34;,
      &#34;item&#34;: &#34;Different gadget&#34;
    },
    {
      &#34;price&#34;: &#34;25.50&#34;,
      &#34;item&#34;: &#34;Golden gadget&#34;
    }
  ],
  &#34;apiVersion&#34;: &#34;3.0&#34;,
  &#34;transactionId&#34;: &#34;f029342&#34;,
  &#34;transactionItemCount&#34;: &#34;2&#34;,
  &#34;transactionTotalPrice&#34;: &#34;43.25&#34;,
  &#34;projectId&#34;: &#34;98765&#34;
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
    &#34;purchases&#34;: [
        {{#purchases}}
        {
            &#34;item&#34;: &#34;{{item}}&#34;,
            &#34;price&#34;: {{price}},
            &#34;transaction_id&#34;: &#34;{{transactionId}}&#34;
        }{{#iter.hasNext}}, {{/iter.hasNext}}
        {{/purchases}}
    ],
    &#34;transactions&#34;: [
        {
            &#34;id&#34;: &#34;{{transactionId}}&#34;,
            &#34;items&#34;: {{transactionItemCount}},
            &#34;total&#34;: {{transactionTotalPrice}}
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
    &#34;purchases&#34;: [
        {
            &#34;item&#34;: &#34;Different gadget&#34;,
            &#34;price&#34;: 17.75,
            &#34;transaction_id&#34;: &#34;f029342&#34;
        },
        {
            &#34;item&#34;: &#34;Golden gadget&#34;,
            &#34;price&#34;: 25.50,
            &#34;transaction_id&#34;: &#34;f029342&#34;
        }
    ],
    &#34;transactions&#34;: [
        {
            &#34;id&#34;: &#34;f029342&#34;,
            &#34;items&#34;: 2,
            &#34;total&#34;: 43.25
        }
    ]
}
```


## アクション構成のスクリーンショット

![](/images/server-side/example)