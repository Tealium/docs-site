---
title: コネクターテンプレート変数
description: テンプレート変数を使用して高度なコネクターリクエストを構築する方法を学びます。
url: https://docs.tealium.com/ja/server-side/connectors/templates/template-variables/
---
## 概要

コネクターテンプレートとテンプレート変数を使用して、コネクターのカスタムAPIリクエストを構築できます。これらを使用して、ベンダーのエンドポイントが要求する形式（JSONやXMLなど）でペイロードを動的に生成します。

テンプレートはAPIリクエストの構造を定義し、テンプレート変数は動的な値を提供します。

詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。

## 動作原理

テンプレート変数は、テンプレートの動的データを提供する属性マッピングです。

例えば、テンプレートに動的な注文ID値を含めるには、属性`order_id`を`orderID`というテンプレート変数にマッピングします。その後、テンプレートで注文ID値が表示されるべき場所に`{{orderID}}`を参照します。

テンプレート変数を追加するには、コネクターアクションに移動し、**テンプレート**タブをクリックして、属性を変数名にマッピングします。

![](https://docs.tealium.com/images/server-side/connectors/connector-templates-variables-mapping.png)

## データタイプ

コネクターテンプレートを効果的に使用するには、テンプレートのレンダリングに使用されるデータの構造を理解することが重要です。

このセクションでは、テンプレートで異なるデータタイプのテンプレート変数を使用する方法について説明します。これには、値を直接参照する方法、`.toJson`のようなヘルパーメソッドの使用方法、複数の値を反復処理する方法が含まれます。

これらの例は、以下のテンプレート変数マッピングに基づいています：

![](https://docs.tealium.com/images/server-side/connectors/connector-template-variables-mapping-sample.png)

### バッジ

バッジ属性にマッピングされた変数は、割り当てられている場合は`true`の値を持ち、割り当てられていない場合は空の値を持ちます。バッジ変数は`false`の値を持つことはないため、空白の値を避けるために、セクションと逆セクションを使用して`true`または`false`の値を強制します。

**テンプレート変数の値:**
```js
unbadgedBadge =
didSearchBadge = true
```

**テンプレート:**
```json
{
    "badge1": "{{unbadgedBadge}}",
    "badge2": {{didSearchBadge}},
    "badge1SectionInvert": {{#unbadgedBadge}}true{{/unbadgedBadge}}{{^unbadgedBadge}}false{{/unbadgedBadge}},
    "badge2SectionInvert": {{#didSearchBadge}}true{{/didSearchBadge}}{{^didSearchBadge}}false{{/didSearchBadge}}
}
```

**レンダリングされたテンプレート:**
```json
{
    "badge1": "",
    "badge2": true,
    "badge1SectionInvert": false,
    "badge2SectionInvert": true
}
```

### ブール値

ブール値にマッピングされた変数は、`true`、`false`、または未割り当てです。値を直接レンダリングするか、セクションまたは逆セクションロジックで使用します。ブール値は引用符で囲まれません。

**テンプレート変数の値:**
```js
returningVisitorBoolean = false
```

**テンプレート:**
```json
{
    "boolean": {{returningVisitorBoolean}},
    "booleanSectionTrue": {{#returningVisitorBoolean}}true{{/returningVisitorBoolean}},
    "booleanSectionInvert": {{^returningVisitorBoolean}}false{{/returningVisitorBoolean}}
}
```

**レンダリングされたテンプレート:**
```json
{
  "boolean": false, 
  "booleanSectionTrue": , 
  "booleanSectionInvert": false
}
```

ブール値が構成されていない場合を考慮して、テンプレートでセクションと逆セクションロジックを使用して値がレンダリングされるようにします。

**テンプレートロジック:**
```json
{
    "boolean": {{#returningVisitorBoolean}}true{{/returningVisitorBoolean}}{{^returningVisitorBoolean}}false{{/returningVisitorBoolean}}
}
```

### 日付

日付属性にマッピングされた変数は、テンプレートデータ内でタイムスタンプ（数字）として表され、出力ではISO 8601文字列としてレンダリングされます。

ヘルパー関数: [formatDate](https://docs.tealium.com/connector-template-helper-functions/#formatDate), [toTimestamp](https://docs.tealium.com/connector-template-helper-functions/#toTimestamp), [toTimestampMs](https://docs.tealium.com/connector-template-helper-functions/#toTimestampMs), [unixTimestamp](https://docs.tealium.com/connector-template-helper-functions/#unixTimestamp), [unixTimestampMs](https://docs.tealium.com/connector-template-helper-functions/#unixTimestampMs).

**テンプレート変数の値:**
```js
firstVisitDate = 1749081326718
```

**テンプレート:**
```json
{
    "date": "{{firstVisitDate}}"
}
```

**レンダリングされたテンプレート:**
```json
{
    "date": "2025-06-04T23:55:26.718Z"
}
```

### 数値

数値属性にマッピングされた変数は、直接レンダリングするか、`.toInteger`を使用して整数に変換できます。

**テンプレート変数の値:**
```js
lifetimeVisitCountNumber = 1.0
```

**テンプレート:**
```json
{
    "number": {{lifetimeVisitCountNumber}},
    "numberToInteger": {{lifetimeVisitCountNumber.toInteger}}
}
```

**レンダリングされたテンプレート:**
```json
{
    "number": 1.0,
    "numberToInteger": 1
}
```

### 文字列

文字列属性にマッピングされた変数は、直接参照できます。JSONテンプレートを構築する場合は、`.toJson`を使用してエスケープされた文字列を引用符で囲むことを確実にします。

ヘルパー関数: [hash](https://docs.tealium.com/connector-template-helper-functions/#hash), [md5](https://docs.tealium.com/connector-template-helper-functions/#md5), [sha1](https://docs.tealium.com/connector-template-helper-functions/#sha1), [sha256](https://docs.tealium.com/connector-template-helper-functions/#sha256), [substring](https://docs.tealium.com/connector-template-helper-functions/#substring).

**テンプレート変数の値:**
```json
activeBrowserTypeString = "Chrome"
```

**テンプレート:**
```json
{
    "string": "{{activeBrowserTypeString.toJson}}"
}
```

**レンダリングされたテンプレート:**
```json
{
    "string": "Chrome"
}
```

### 文字列のセット

文字列のセット属性にマッピングされた変数は、配列に似ていますが、順序を保持しない場合があります。文字列のセット変数を配列としてレンダリングするには、`.toJson`を使用します。より高度なケースでは、カスタム形式を各エントリに適用するために反復処理を使用します。

ヘルパー関数: [sum](https://docs.tealium.com/connector-template-helper-functions/#sum).

**テンプレート変数の値:**
```json
activeBrowserTypesSetOfStrings = ["Chrome", "Safari"]
```

**テンプレート:**
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
文字列のセット変数を直接参照すると、`.toJson`や反復処理を使用せずに引用符なしの値がレンダリングされます。
</blockquote>


**レンダリングされたテンプレート:**
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

配列属性にマッピングされた変数は、`.toJson`で参照する必要があります。より高度なケースでは、カスタム形式を各エントリに適用するために反復処理を使用します。

ヘルパー関数: [sum](https://docs.tealium.com/connector-template-helper-functions/#sum).


<blockquote>
配列変数を直接参照すると、引用符なしの値がレンダリングされます。
</blockquote>


**テンプレート変数の値:**
```json
browsersArray = ["Chrome", "Safari"]
```

**テンプレート:**
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

**レンダリングされたテンプレート:**
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

集計属性にマップされた変数は、キーと数値のマップです。`.toJson`を使用して、引用符付きキーで完全な集計をレンダリングします。`.entrySet`を使用して集計を反復処理し、`key`と`value`を使用してキーと値のペアを参照します。


<blockquote>
集計を直接参照すると、引用符なしの値がレンダリングされます。
</blockquote>


**テンプレート変数の値:**
```js
categoriesTally = { 
    "Shirts" : 1, 
    "Blazers" : 2,  
    "Electronics" : 4, 
    "Eyewear" : 1 
}
```

**テンプレート:**
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

**レンダリングされたテンプレート:**
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