---
title: JSONオブジェクトのフラット化拡張機能
description: ネストされたデータレイヤーオブジェクトをキーと値のペアが1層のみの新しいオブジェクトに変換するために、JSONオブジェクトのフラット化拡張機能を使用します。
url: https://docs.tealium.com/ja/iq-tag-management/extensions/extensions-list/flatten-json-objects-extension/
---
データレイヤーを変換するためのより高度なオプションについては、[Data Layer Converter]()を参照してください。

### 前提条件

* [拡張機能について]()を参照してください。

### 要件

* utag v4.38以降。`utag.js`テンプレートを更新する方法については、ナレッジベースの記事[utag.jsの最新バージョンへの更新のベストプラクティス](https://support.tealiumiq.com/en/support/solutions/articles/36000363470)を参照してください。

### 動作原理

以下は、JSONオブジェクトのフラット化拡張機能がどのように機能するかを示すいくつかの例です：

* `parent -&gt; child`のようなオブジェクトは`parent.child`としてフラット化されます。
* `parent -&gt; array -&gt; [obj1,objN]`のような配列オブジェクトは`parent.array0.obj1key`および`parent.arrayN.objNkey`としてフラット化されます。
* 配列の場合、追加の`parent.array.array-size`値が自動的に構成されます。

## 拡張機能の使用

拡張機能が追加されると、以下の構成オプションが利用可能になります：

* **JSONオブジェクト**：フラット化するJSONオブジェクト変数。
* **出力オブジェクト**：結果を含む出力オブジェクト変数。

## 例

以下は、親子関係と配列を含むJSONオブジェクトの例です：

![](/images/iq-tag-management/no-title-1265i9f0146e131a9389e.png)

```
var person_object = {
  &#34;firstName&#34; : &#34;John&#34;,
  &#34;lastName&#34; : &#34;Doe&#34;,
  &#34;age&#34; : 25,
  &#34;address&#34; : {
    &#34;streetAddress&#34; : &#34;1234 Main St&#34;,
    &#34;city&#34; : &#34;Los Angeles&#34;,
    &#34;state&#34; : &#34;CA&#34;,
    &#34;postalCode&#34; : &#34;90010&#34;
  },
  &#34;phoneNumber&#34; : [
    {
      &#34;type&#34; : &#34;home&#34;,
      &#34;number&#34; : &#34;310-555-1234&#34;
    },
    {
      &#34;type&#34; : &#34;fax&#34;,
      &#34;number&#34; : &#34;310-555-5678&#34;
    }
  ]
};

```

フラット化されたとき、オブジェクトは以下のようになります：

```
var person_flatobject = {
    &#34;address.city&#34; : &#34;Los Angeles&#34;,
    &#34;address.postalCode&#34; : &#34;90010&#34;
    &#34;address.state&#34; : &#34;CA&#34;,
    &#34;address.streetAddress&#34;: &#34;1234 Main St&#34;,
    &#34;age&#34; : 25,
    &#34;firstName&#34; : &#34;John&#34;,
    &#34;lastName&#34; : &#34;Doe&#34;,
    &#34;phoneNumber.array-size&#34; : 2
    &#34;phoneNumber0.number&#34; : &#34;310-555-1234&#34;
    &#34;phoneNumber0.type&#34;  : &#34;home&#34;,
    &#34;phoneNumber1.number&#34; : &#34;310-555-5678&#34;
    &#34;phoneNumber1.type&#34;  : &#34;fax&#34;
};

```

新しいオブジェクトからデータレイヤー変数として項目を参照する必要がある場合、`person_flatobject`で述べられている表記法を使用します。たとえば、アドレスの`state`データにアクセスするには`person_flatobject.address.state`を使用します。

![](/images/iq-tag-management/no-title-1266i4a38c24e66920d3e.png)