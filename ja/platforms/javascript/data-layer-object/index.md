---
title: データレイヤーオブジェクト（b）
description: データレイヤーオブジェクトの変数エイリアスの使用方法について説明します。
url: https://docs.tealium.com/ja/platforms/javascript/data-layer-object/
---
## 仕組み

`b` 変数は、データレイヤーを表す `utag.js` 内のJavaScriptオブジェクトです。ページの読み込み時またはトラッキング呼び出し時に処理されるデータレイヤーオブジェクトを保持します。

タグ管理では通常、ドロップダウンリストを使用してデータレイヤー変数を参照しますが、JavaScriptコード内で `b` 変数を使用して参照することもできます。

たとえば、**Set Data Values** 拡張機能の一般的な用途の1つは、変数に値がまだ構成されていない場合にデフォルト値を構成することです。この拡張機能は、次のようになります。

![](https://docs.tealium.com/images/platforms/javascript/b-object-extension-example.png)

`utag.js` では、この拡張機能は次のようなJavaScriptコードで表されます。

```js
function(a, b) {
  try {
    if (typeof b['page_type'] == 'undefined') {
      b['page_type'] = "generic"
    } catch (e) {
        utag.DB(e);
    }
  }
}
```

`b` 変数はデータレイヤーオブジェクトへのローカル参照であり、`b['page_type']` はUDO変数 `page_type` への参照です。同様に、拡張機能でカスタムJavaScriptを使用する場合、`b` を使用してデータレイヤーオブジェクト内の任意の変数を参照できます。


<blockquote>
`utag.js` バージョン4.39以前では、トラッキング呼び出し時の `b` オブジェクトの内容は `utag.data` の完全なコピーです。この更新の詳細については、[リリース4.40](https://docs.tealium.com/ja/release-notes/?filter=tealium-universal-tag#tealium-universal-tag-2016-04-01)を参照してください。
</blockquote>


### 使用できる場所

`b` オブジェクトは、`utag.js` の特定のセクション内でローカルスコープを持つ変数であり、次の拡張機能スコープで使用できます。

* **Before Load Rules**
* **After Load Rules**
* **Tag Scope**
* **After Tags**

次のスコープでは `b` オブジェクトを参照できません。

* **Pre Loader**  
**Pre Loader** スコープの拡張機能は、`b` オブジェクトが作成される前に実行されるため、`b` オブジェクトを参照できません。
* **DOM Ready**  
**DOM Ready** スコープの拡張機能はメインスコープの外部で実行されるため、`b` オブジェクトを参照できません。

### シナリオ：ページの読み込み

標準的なページ読み込みでは、`b` オブジェクトは、[ユニバーサルデータオブジェクト](https://docs.tealium.com/universal-data-object/)を含む、ページ上のすべてのデータのコレクションです。

たとえば、次の例では、拡張機能内で `b['page_type']` を参照できます。

```html
<script>
var utag_data = {
    page_type: "home"
}
</script>
<script src="//tags.tiqcdn.com/utag/example/main/prod/utag.js"></script>
```

### シナリオ：トラッキング呼び出し

トラッキング呼び出しでは、`b` オブジェクトは、ページ上のすべてのデータ（ユニバーサルデータオブジェクトを除く）と、トラッキング呼び出しに渡されたデータのコレクションです。

たとえば、次のトラッキング呼び出しでは、拡張機能内で `b['tealium_event']` を参照できます。

```js
var tmp = { tealium_event: "link_click" };
utag.link(tmp)

utag.view({ tealium_event: "cart_add" })
```

この例では、`b['page_type']` は（`utag_data` で定義されている場合でも）定義されない点に注意してください。これは、トラッキング呼び出しで渡されるデータオブジェクトに含まれていないためです。

ページ上のその他の種類のデータレイヤー変数を参照する方法については、[使用方法](#usage)を参照してください。


<blockquote>
トラッキング呼び出しに `utag_data` の変数を含めるには、[パブリッシュ構成の基本変数構成](https://docs.tealium.com/publish-configuration/)を使用します。
</blockquote>


### タグスコープの拡張機能

特定のタグをスコープとする拡張機能では、`b` オブジェクトはデータレイヤーオブジェクトのローカルコピーです。そのため、他のタグに影響を与えることなく `b` オブジェクトの値を変更できます。

次の例では、JavaScript Code拡張機能を使用して、データレイヤー変数 `order_id` をタグごとにカスタマイズしています。各拡張機能の `b` は、同じ `order_id` の値から始まります。

![](https://docs.tealium.com/images/platforms/javascript/b-object-tag-scope-example-fb.png)

![](https://docs.tealium.com/images/platforms/javascript/b-object-tag-scope-example-ga.png)


## 使用方法

タグテンプレートまたは拡張機能で `b` オブジェクトの変数を参照するには、変数の種類ごとに正しい構文を使用する必要があります。

各変数タイプの構文は次のとおりです。

| 変数タイプ | 構文 |
| --------------------- | ------ |
| ユニバーサルデータオブジェクト | `b['VAR_NAME']` |
| JavaScriptページ | `b['js_page.VAR_NAME']` |
| クエリ文字列 | `b['qp.VAR_NAME']` |
| 標準Cookie | `b['cp.VAR_NAME']` |
| DOM要素 | `b['dom.VAR_NAME']` |
| メタデータ | `b['meta.VAR_NAME']` |
| ローカル保存 | `b['ls.VAR_NAME']` |
| セッション保存 | `b['ss.VAR_NAME']` |

詳細については、[データレイヤー変数のタイプ](https://docs.tealium.com/data-layer-variables/)を参照してください。