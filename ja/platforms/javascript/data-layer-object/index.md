---
title: データレイヤーオブジェクト (b)
description: データレイヤーオブジェクトへの変数エイリアスの使用方法を学びます。
url: https://docs.tealium.com/ja/platforms/javascript/data-layer-object/
---
## 仕組み

`b`変数は、データレイヤーを表す`utag.js`内のJavaScriptオブジェクトです。ページの読み込みやトラッキング呼び出し中に処理されるデータレイヤーオブジェクトを保持しています。

Tealium iQでは、データレイヤー変数は通常、ドロップダウンリストを使用して参照されますが、`b`変数を使用してJavaScriptコード内で参照することもできます。

例えば、**Set Data Values**拡張の一般的な使用法は、変数がまだ構成されていない場合にデフォルト値を構成することです。拡張は次のようになるかもしれません：

![](/images/platforms/javascript/b-object-extension-example.png)

`utag.js`では、この拡張は次のようにJavaScriptコードで表されます：

```js
function(a, b) {
  try {
    if (typeof b[&#39;page_type&#39;] == &#39;undefined&#39;) {
      b[&#39;page_type&#39;] = &#34;generic&#34;
    } catch (e) {
        utag.DB(e);
    }
  }
}
```

`b`変数はデータレイヤーオブジェクトへのローカル参照であり、`b[&#39;page_type&#39;]`はUDO変数`page_type`への参照です。同様に、拡張機能でカスタムJavaScriptを使用するときは、`b`を使用してデータレイヤーオブジェクト内の任意の変数を参照できます。

`utag.js`バージョン4.39以前では、トラッキング呼び出し中の`b`オブジェクトの内容は`utag.data`の完全なコピーです。この更新については[リリース4.40](/ja/release-notes/?filter=tealium-universal-tag#tealium-universal-tag-2016-04-01)で詳しく説明しています。

### 使用場所

`b`オブジェクトは`utag.js`の特定のセクション内のローカルスコープ変数であり、以下の拡張スコープで利用可能です：

* **Before Load Rules**
* **After Load Rules**
* **Tag Scope**
* **After Tags** 

`b`オブジェクトは以下のスコープでは参照できません：

* **Pre Loader**  
**Pre Loader**にスコープされた拡張は、`b`オブジェクトが作成される前に実行されるため、`b`オブジェクトを参照できません。
* **DOM Ready**  
**DOM Ready**にスコープされた拡張は、メインスコープの外部で実行されるため、`b`オブジェクトを参照できません。

### シナリオ：ページの読み込み

標準的なページの読み込みでは、`b`オブジェクトはページ上のすべてのデータ、[ユニバーサルデータオブジェクト]()を含むコレクションです。

例えば、次の例では、拡張機能で`b[&#39;page_type&#39;]`を参照できます：

```html
&lt;script&gt;
var utag_data = {
    page_type: &#34;home&#34;
}
&lt;/script&gt;
&lt;script src=&#34;//tags.tiqcdn.com/utag/example/main/prod/utag.js&#34;&gt;&lt;/script&gt;
```

### シナリオ：トラッキング呼び出し

トラッキング呼び出しでは、`b`オブジェクトはページ上のすべてのデータ（ユニバーサルデータオブジェクトを除く）と、トラッキング呼び出しに渡されたデータのコレクションです。

例えば、これらのトラッキング呼び出しでは、拡張機能で`b[&#39;tealium_event&#39;]`を参照できます：

```js
var tmp = { tealium_event: &#34;link_click&#34; };
utag.link(tmp)

utag.view({ tealium_event: &#34;cart_add&#34; })
```

この例では、`b[&#39;page_type&#39;]`が定義されていないことに注意が必要です（`utag_data`で定義されていても）これは、トラッキング呼び出しで渡されたデータオブジェクトの一部ではないからです。

ページから他のタイプのデータレイヤー変数を参照するには、[使用法](#usage)を参照してください。

トラッキング呼び出しで`utag_data`から変数を含めるには、[公開構成の基本変数構成]()を使用してください。

### タグスコープの拡張

特定のタグにスコープされた拡張では、`b`オブジェクトはデータレイヤーオブジェクトのローカルコピーです。これは、`b`オブジェクトの値を他のタグに影響を与えずに変更できることを意味します。

これらの例では、データレイヤー変数`order_id`がJavaScript Code拡張を使用して各タグでカスタマイズされています。各拡張では、`b`は`order_id`の同じ値から始まります：

![](/images/platforms/javascript/b-object-tag-scope-example-fb.png)

![](/images/platforms/javascript/b-object-tag-scope-example-ga.png)


## 使用法

タグテンプレートや拡張で`b`オブジェクト変数を参照するには、各変数タイプの正しい構文を使用する必要があります。

各変数タイプの構文は次のとおりです：

| 変数タイプ         | 構文 |
| --------------------- | ------ |
| ユニバーサルデータオブジェクト | `b[&#39;VAR_NAME&#39;]` |
| JavaScriptページ       | `b[&#39;js_page.VAR_NAME&#39;]` |
| クエリストリング          | `b[&#39;qp.VAR_NAME&#39;]` |
| 標準クッキー       | `b[&#39;cp.VAR_NAME&#39;]` |
| DOM要素           | `b[&#39;dom.VAR_NAME&#39;]` |
| メタデータ             | `b[&#39;meta.VAR_NAME&#39;]` |
| ローカル保存         | `b[&#39;ls.VAR_NAME&#39;]` |
| セッション保存       | `b[&#39;ss.VAR_NAME&#39;]` |

詳細については、[データレイヤー変数タイプ]()を参照してください。