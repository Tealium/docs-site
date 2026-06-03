---
title: コネクターテンプレート変数
description: テンプレート変数を使用して高度なコネクターリクエストを構築する方法を学びます。
url: https://docs.tealium.com/ja/server-side/connectors/templates/template-variables/
---
## 概要

コネクターテンプレートとテンプレート変数を使用して、コネクターのカスタムAPIリクエストを構築できます。これらを使用して、ベンダーのエンドポイントが要求する形式（JSONやXMLなど）でペイロードを動的に生成します。

テンプレートはAPIリクエストの構造を定義し、テンプレート変数は動的な値を提供します。

詳細については、を参照してください。

## 動作原理

テンプレート変数は、テンプレートの動的データを提供する属性マッピングです。

例えば、テンプレートに動的な注文ID値を含めるには、属性`order_id`を`orderID`というテンプレート変数にマッピングします。その後、テンプレートで注文ID値が表示されるべき場所に`{{orderID}}`を参照します。

テンプレート変数を追加するには、コネクターアクションに移動し、**テンプレート**タブをクリックして、属性を変数名にマッピングします。

![](/images/server-side/connectors/connector-templates-variables-mapping.png)

## データタイプ

コネクターテンプレートを効果的に使用するには、テンプレートのレンダリングに使用されるデータの構造を理解することが重要です。

このセクションでは、テンプレートで異なるデータタイプのテンプレート変数を使用する方法について説明します。これには、値を直接参照する方法、`.toJson`のようなヘルパーメソッドの使用方法、複数の値を反復処理する方法が含まれます。

これらの例は、以下のテンプレート変数マッピングに基づいています：

![](/images/server-side/connectors/connector-template-variables-mapping-sample.png)

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
    &#34;badge1&#34;: &#34;{{unbadgedBadge}}&#34;,
    &#34;badge2&#34;: {{didSearchBadge}},
    &#34;badge1SectionInvert&#34;: {{#unbadgedBadge}}true{{/unbadgedBadge}}{{^unbadgedBadge}}false{{/unbadgedBadge}},
    &#34;badge2SectionInvert&#34;: {{#didSearchBadge}}true{{/didSearchBadge}}{{^didSearchBadge}}false{{/didSearchBadge}}
}
```

**レンダリングされたテンプレート:**
```json
{
    &#34;badge1&#34;: &#34;&#34;,
    &#34;badge2&#34;: true,
    &#34;badge1SectionInvert&#34;: false,
    &#34;badge2SectionInvert&#34;: true
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
    &#34;boolean&#34;: {{returningVisitorBoolean}},
    &#34;booleanSectionTrue&#34;: {{#returningVisitorBoolean}}true{{/returningVisitorBoolean}},
    &#34;booleanSectionInvert&#34;: {{^returningVisitorBoolean}}false{{/returningVisitorBoolean}}
}
```

**レンダリングされたテンプレート:**
```json
{
  &#34;boolean&#34;: false, 
  &#34;booleanSectionTrue&#34;: , 
  &#34;booleanSectionInvert&#34;: false
}
```

ブール値が構成されていない場合を考慮して、テンプレートでセクションと逆セクションロジックを使用して値がレンダリングされるようにします。

**テンプレートロジック:**
```json
{
    &#34;boolean&#34;: {{#returningVisitorBoolean}}true{{/returningVisitorBoolean}}{{^returningVisitorBoolean}}false{{/returningVisitorBoolean}}
}
```

### 日付

日付属性にマッピングされた変数は、テンプレートデータ内でタイムスタンプ（数字）として表され、出力ではISO 8601文字列としてレンダリングされます。

ヘルパー関数: [formatDate](), [toTimestamp](), [toTimestampMs](), [unixTimestamp](), [unixTimestampMs]().

**テンプレート変数の値:**
```js
firstVisitDate = 1749081326718
```

**テンプレート:**
```json
{
    &#34;date&#34;: &#34;{{firstVisitDate}}&#34;
}
```

**レンダリングされたテンプレート:**
```json
{
    &#34;date&#34;: &#34;2025-06-04T23:55:26.718Z&#34;
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
    &#34;number&#34;: {{lifetimeVisitCountNumber}},
    &#34;numberToInteger&#34;: {{lifetimeVisitCountNumber.toInteger}}
}
```

**レンダリングされたテンプレート:**
```json
{
    &#34;number&#34;: 1.0,
    &#34;numberToInteger&#34;: 1
}
```

### 文字列

文字列属性にマッピングされた変数は、直接参照できます。JSONテンプレートを構築する場合は、`.toJson`を使用してエスケープされた文字列を引用符で囲むことを確実にします。

ヘルパー関数: [hash](), [md5](), [sha1](), [sha256](), [substring]().

**テンプレート変数の値:**
```json
activeBrowserTypeString = &#34;Chrome&#34;
```

**テンプレート:**
```json
{
    &#34;string&#34;: &#34;{{activeBrowserTypeString.toJson}}&#34;
}
```

**レンダリングされたテンプレート:**
```json
{
    &#34;string&#34;: &#34;Chrome&#34;
}
```

### 文字列のセット

文字列のセット属性にマッピングされた変数は、配列に似ていますが、順序を保持しない場合があります。文字列のセット変数を配列としてレンダリングするには、`.toJson`を使用します。より高度なケースでは、カスタム形式を各エントリに適用するために反復処理を使用します。

ヘルパー関数: [sum]().

**テンプレート変数の値:**
```json
activeBrowserTypesSetOfStrings = [&#34;Chrome&#34;, &#34;Safari&#34;]
```

**テンプレート:**
```json
{
    &#34;setOfStrings&#34;: {{activeBrowserTypesSetOfStrings}},
    &#34;setOfStringsToJson&#34;: {{activeBrowserTypesSetOfStrings.toJson}},
    &#34;setOfStringsIter&#34;: [
    {{#activeBrowserTypesSetOfStrings}}
        &#34;-- {{.}} --&#34;{{#iter.hasNext}},{{/iter.hasNext}}
    {{/activeBrowserTypesSetOfStrings}}
    ]
}
```

文字列のセット変数を直接参照すると、`.toJson`や反復処理を使用せずに引用符なしの値がレンダリングされます。

**レンダリングされたテンプレート:**
```json
{
    &#34;setOfStrings&#34;: [Chrome,Safari], 
    &#34;setOfStringsToJson&#34;: [&#34;Chrome&#34;, &#34;Safari&#34;],
    &#34;setOfStringsIter&#34;: [
        &#34;-- Chrome --&#34;,
        &#34;-- Safari --&#34;
    ]
}
```

### 配列

配列属性にマッピングされた変数は、`.toJson`で参照する必要があります。より高度なケースでは、カスタム形式を各エントリに適用するために反復処理を使用します。

ヘルパー関数: [sum]().

配列変数を直接参照すると、引用符なしの値がレンダリングされます。

**テンプレート変数の値:**
```json
browsersArray = [&#34;Chrome&#34;, &#34;Safari&#34;]
```

**テンプレート:**
```json
{
    &#34;array&#34;: {{browsersArray}},
    &#34;arrayToJson&#34;: {{browsersArray.toJson}},
    &#34;arrayIter&#34;: [
    {{#browsersArray}}
        &#34;-- ({{iter.index}}) {{.}} --&#34;{{#iter.hasNext}},{{/iter.hasNext}}
    {{/browsersArray}}
    ],
}
```

**レンダリングされたテンプレート:**
```json
{
    &#34;array&#34;: [Chrome,Safari], 
    &#34;arrayToJson&#34;: [&#34;Chrome&#34;, &#34;Safari&#34;], 
    &#34;arrayIter&#34;: [
        &#34;-- (1) Chrome --&#34;,
        &#34;-- (2) Safari --&#34;
    ] 
}
```
### 集計

集計属性にマップされた変数は、キーと数値のマップです。`.toJson`を使用して、引用符付きキーで完全な集計をレンダリングします。`.entrySet`を使用して集計を反復処理し、`key`と`value`を使用してキーと値のペアを参照します。

集計を直接参照すると、引用符なしの値がレンダリングされます。

**テンプレート変数の値:**
```js
categoriesTally = { 
    &#34;Shirts&#34; : 1, 
    &#34;Blazers&#34; : 2,  
    &#34;Electronics&#34; : 4, 
    &#34;Eyewear&#34; : 1 
}
```

**テンプレート:**
```json
{
    &#34;tally&#34;: {{categoriesTally}},
    &#34;tallyToJson&#34;: {{categoriesTally.toJson}},
    &#34;tallyIter&#34;: {
        {{#each categoriesTally.entrySet}}
        &#34;{{key}}&#34;: &#34;{{value.toInteger}}&#34;{{#iter.hasNext}},{{/iter.hasNext}}
        {{/each}}
    }
}
```

**レンダリングされたテンプレート:**
```json
{
    &#34;tally&#34;: {Shirts=1, Blazers=2, Electronics=4, Eyewear=1},
    &#34;tallyToJson&#34;: {
        &#34;Shirts&#34;:1,
        &#34;Blazers&#34;:2,
        &#34;Electronics&#34;:4,
        &#34;Eyewear&#34;:1
    }, 
    &#34;tallyIter&#34;: { 
        &#34;Shirts&#34;: &#34;1&#34;,  
        &#34;Blazers&#34;: &#34;2&#34;, 
        &#34;Electronics&#34;: &#34;4&#34;,
        &#34;Eyewear&#34;: &#34;1&#34; 
  }
}
```