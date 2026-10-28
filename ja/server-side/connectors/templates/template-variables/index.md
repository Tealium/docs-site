---
title: コネクターテンプレート変数
description: テンプレート変数を使用して高度なコネクターリクエストを作成する方法について説明します。
url: https://docs.tealium.com/ja/server-side/connectors/templates/template-variables/
---
## 概要

コネクターテンプレートとテンプレート変数を使用すると、コネクター用のカスタムAPIリクエストを作成できます。これらを使用して、JSONやXMLなど、ベンダーのエンドポイントで必要とされる形式のペイロードを動的に生成できます。

テンプレートはAPIリクエストの構造を定義し、テンプレート変数は動的な値を提供します。

詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。

## 予約変数

予約変数は、テンプレートに対応するすべてのWebhookコネクターアクションで自動的に使用できます。使用するために変数マッピングを作成する必要はありません。

| 変数 | 説明 |
|---|---|
| `tealium_event_payload` | `account`、`profile`、`env`、`data`（`udo`、`dom`、`firstparty_tealium_cookies`）、`post_time`、`useragent`、`event_id`、`visitor_id`を含む、現在のイベント全体。 |
| `tealium_visitor_payload` | 属性、現在の訪問データ、セカンダリIDを含む、訪問プロファイル全体。構造は、**HTTPリクエストによる訪問データの送信**のペイロードと一致します。 |

予約変数から単一の値にアクセスするには、ドット記法を使用します。

```json
{
    "eventId": "{{tealium_event_payload.event_id}}",
    "email": "{{tealium_event_payload.data.udo.email}}"
}
```

オブジェクト全体またはネストされたオブジェクトをJSON文字列としてシリアル化するには、`.toJson`を使用します。

```json
{
    "event": {{tealium_event_payload.toJson}},
    "udo": {{tealium_event_payload.data.udo.toJson}}
}
```

## 仕組み

テンプレート変数は、テンプレートに動的データを提供する属性マッピングです。

たとえば、動的な注文ID値をテンプレートに含めるには、属性`order_id`を`orderID`という名前のテンプレート変数にマッピングします。次に、テンプレート内で注文ID値を表示する箇所に`{{orderID}}`を指定します。

テンプレート変数を追加するには、コネクターアクションに移動して**テンプレート**タブをクリックし、属性を変数名にマッピングします。

![](https://docs.tealium.com/images/server-side/connectors/connector-templates-variables-mapping.png)

## データ型

コネクターテンプレートを効果的に使用するには、テンプレートのレンダリングに使用されるデータの構造を理解することが重要です。

このセクションでは、さまざまなデータ型のテンプレート変数をテンプレートで使用する方法について説明します。値の直接参照、`.toJson`などのヘルパーメソッドの使用、複数の値に対する反復処理などが含まれます。

以下の例は、次のテンプレート変数マッピングに基づいています。

![](https://docs.tealium.com/images/server-side/connectors/connector-template-variables-mapping-sample.png)

### バッジ

バッジ属性にマッピングされた変数は、割り当てられている場合は`true`、割り当てられていない場合は空の値になります。バッジ変数が`false`になることはないため、空の値を避けるには、セクションと反転セクションを使用して、値を強制的に`true`または`false`にします。

**テンプレート変数の値：**
```js
unbadgedBadge =
didSearchBadge = true
```

**テンプレート：**
```json
{
    "badge1": "{{unbadgedBadge}}",
    "badge2": {{didSearchBadge}},
    "badge1SectionInvert": {{#unbadgedBadge}}true{{/unbadgedBadge}}{{^unbadgedBadge}}false{{/unbadgedBadge}},
    "badge2SectionInvert": {{#didSearchBadge}}true{{/didSearchBadge}}{{^didSearchBadge}}false{{/didSearchBadge}}
}
```

**レンダリングされたテンプレート：**
```json
{
    "badge1": "",
    "badge2": true,
    "badge1SectionInvert": false,
    "badge2SectionInvert": true
}
```

### ブール値

ブール値にマッピングされた変数は、`true`、`false`、または未割り当てのいずれかです。値を直接レンダリングするか、セクションまたは反転セクションのロジックで使用します。ブール値は引用符で囲みません。

**テンプレート変数の値：**
```js
returningVisitorBoolean = false
```

**テンプレート：**
```json
{
    "boolean": {{returningVisitorBoolean}},
    "booleanSectionTrue": {{#returningVisitorBoolean}}true{{/returningVisitorBoolean}},
    "booleanSectionInvert": {{^returningVisitorBoolean}}false{{/returningVisitorBoolean}}
}
```

**レンダリングされたテンプレート：**
```json
{
  "boolean": false, 
  "booleanSectionTrue": , 
  "booleanSectionInvert": false
}
```

ブール値が構成されていない場合があることに注意してください。テンプレートでこの状況を処理するには、セクションと反転セクションのロジックを使用して、値を強制的にレンダリングします。

**テンプレートロジック：**
```json
{
    "boolean": {{#returningVisitorBoolean}}true{{/returningVisitorBoolean}}{{^returningVisitorBoolean}}false{{/returningVisitorBoolean}}
}
```

### 日付

日付属性にマッピングされた変数は、テンプレートデータではタイムスタンプ（数値）として表され、出力ではISO 8601文字列としてレンダリングされます。

ヘルパー関数：[formatDate](https://docs.tealium.com/connector-template-helper-functions/#formatDate)、[toTimestamp](https://docs.tealium.com/connector-template-helper-functions/#toTimestamp)、[toTimestampMs](https://docs.tealium.com/connector-template-helper-functions/#toTimestampMs)、[unixTimestamp](https://docs.tealium.com/connector-template-helper-functions/#unixTimestamp)、[unixTimestampMs](https://docs.tealium.com/connector-template-helper-functions/#unixTimestampMs)。

**テンプレート変数の値：**
```js
firstVisitDate = 1749081326718
```

**テンプレート：**
```json
{
    "date": "{{firstVisitDate}}"
}
```

**レンダリングされたテンプレート：**
```json
{
    "date": "2025-06-04T23:55:26.718Z"
}
```

### 数値

数値属性にマッピングされた変数は、直接レンダリングするか、`.toInteger`を使用して整数に変換できます。

**テンプレート変数の値：**
```js
lifetimeVisitCountNumber = 1.0
```

**テンプレート：**
```json
{
    "number": {{lifetimeVisitCountNumber}},
    "numberToInteger": {{lifetimeVisitCountNumber.toInteger}}
}
```

**レンダリングされたテンプレート：**
```json
{
    "number": 1.0,
    "numberToInteger": 1
}
```

### 文字列

文字列属性にマッピングされた変数は、直接参照できます。JSONテンプレートを作成する場合は、`.toJson`を使用して、引用符で囲むことができるエスケープ済み文字列を生成します。

ヘルパー関数：[hash](https://docs.tealium.com/connector-template-helper-functions/#hash)、[md5](https://docs.tealium.com/connector-template-helper-functions/#md5)、[sha1](https://docs.tealium.com/connector-template-helper-functions/#sha1)、[sha256](https://docs.tealium.com/connector-template-helper-functions/#sha256)、[substring](https://docs.tealium.com/connector-template-helper-functions/#substring)。

**テンプレート変数の値：**
```json
activeBrowserTypeString = "Chrome"
```

**テンプレート：**
```json
{
    "string": "{{activeBrowserTypeString.toJson}}"
}
```

**レンダリングされたテンプレート：**
```json
{
    "string": "Chrome"
}
```

### 文字列セット

文字列セット属性にマッピングされた変数は配列に似ていますが、順序が保持されない場合があります。文字列セット変数を配列としてレンダリングするには、`.toJson`を使用します。より高度なケースでは、反復処理を使用して各エントリにカスタム形式を適用します。

ヘルパー関数：[sum](https://docs.tealium.com/connector-template-helper-functions/#sum)。

**テンプレート変数の値：**
```json
activeBrowserTypesSetOfStrings = ["Chrome", "Safari"]
```

**テンプレート：**
```json
{
    "setOfStrings": {{activeBrowserTypesSetOfStrings}},
    "setOfStringsToJson": {{activeBrowserTypesSetOfStrings.toJson}},
    "setOfStringsIter": [
    {{#activeBrowserTypesSetOfStrings}}
        "-- {{.}} --"{{#iter.hasNext}},{{/iter.hasNext}}
    {{/activeBrowserTypesSetOfStrings}}
    ]
}
```


<blockquote>
文字列セット変数を`.toJson`や反復処理を使用せずに直接参照すると、引用符で囲まれていない値がレンダリングされます。
</blockquote>


**レンダリングされたテンプレート：**
```json
{
    "setOfStrings": [Chrome,Safari], 
    "setOfStringsToJson": ["Chrome", "Safari"],
    "setOfStringsIter": [
        "-- Chrome --",
        "-- Safari --"
    ]
}
```
### 配列

配列属性にマッピングされた変数は、`.toJson` を使用して参照する必要があります。より高度なケースでは、反復処理を使用して各エントリにカスタム形式を適用します。

ヘルパー関数：[sum](https://docs.tealium.com/connector-template-helper-functions/#sum)。


<blockquote>
配列変数を直接参照すると、引用符で囲まれていない値がレンダリングされます。
</blockquote>


**テンプレート変数の値：**
```json
browsersArray = ["Chrome", "Safari"]
```

**テンプレート：**
```json
{
    "array": {{browsersArray}},
    "arrayToJson": {{browsersArray.toJson}},
    "arrayIter": [
    {{#browsersArray}}
        "-- ({{iter.index}}) {{.}} --"{{#iter.hasNext}},{{/iter.hasNext}}
    {{/browsersArray}}
    ],
}
```

**レンダリングされたテンプレート：**
```json
{
    "array": [Chrome,Safari], 
    "arrayToJson": ["Chrome", "Safari"], 
    "arrayIter": [
        "-- (1) Chrome --",
        "-- (2) Safari --"
    ] 
}
```

### 集計

集計属性にマッピングされた変数は、キーと数値の対応を表すマップです。引用符で囲まれたキーを含む集計全体をレンダリングするには、`.toJson` を使用します。集計を反復処理するには `.entrySet` を使用し、キーと値のペアを参照するには `key` と `value` を使用します。


<blockquote>
集計を直接参照すると、引用符で囲まれていない値がレンダリングされます。
</blockquote>


**テンプレート変数の値：**
```js
categoriesTally = { 
    "Shirts" : 1, 
    "Blazers" : 2,  
    "Electronics" : 4, 
    "Eyewear" : 1 
}
```

**テンプレート：**
```json
{
    "tally": {{categoriesTally}},
    "tallyToJson": {{categoriesTally.toJson}},
    "tallyIter": {
        {{#each categoriesTally.entrySet}}
        "{{key}}": "{{value.toInteger}}"{{#iter.hasNext}},{{/iter.hasNext}}
        {{/each}}
    }
}
```

**レンダリングされたテンプレート：**
```json
{
    "tally": {Shirts=1, Blazers=2, Electronics=4, Eyewear=1},
    "tallyToJson": {
        "Shirts":1,
        "Blazers":2,
        "Electronics":4,
        "Eyewear":1
    }, 
    "tallyIter": { 
        "Shirts": "1",  
        "Blazers": "2", 
        "Electronics": "4",
        "Eyewear": "1" 
  }
}
```