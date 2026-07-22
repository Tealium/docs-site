---
title: データレイヤー変数の種類
description: この記事では、Tealium iQタグ管理で利用可能なさまざまなデータレイヤー変数の種類の使用方法について説明します。
url: https://docs.tealium.com/ja/iq-tag-management/data-layer/data-layer-variables/
---
データレイヤー画面では、変数をタイプ別に整理しています。これらのタイプはデータの出所に基づいています。

サポートされているタイプは以下の通りです：

* **UDO変数**: ユニバーサルデータオブジェクト（`utag_data`）からの変数。
* **クエリ文字列パラメータ**: URLクエリ文字列からの変数。
* **ファーストパーティクッキー**: クッキーとして保存される変数。
* **JavaScript変数**: あなたのサイトコードに既に存在する変数。
* **メタデータ要素**: `<meta>`タグからの変数。
* **DOM変数**: 組み込みのDOM変数。
* **ローカル保存変数**: セッション間でローカルに保存されるデータ。
* **セッション保存変数**: セッション間で期限切れになるローカルに保存されるデータ。
* **AudienceStream属性**: AudienceStreamから[データレイヤーエンリッチメント](https://docs.tealium.com/about-data-layer-enrichment/)によってインポートされる変数。この変数タイプはAudienceStreamを持つ顧客のみ利用可能です。

![](https://docs.tealium.com/images/iq-tag-management/whiteui-tiq-datalayervariables-filter.png)


<blockquote>
これらのデータレイヤー変数は、あなたのTealium iQ構成で使用するためのものです。サイトのデータレイヤーコードを作成する方法の詳細については、[データレイヤー](https://docs.tealium.com/quick-start-web/#data-layer)および[ユニバーサルデータオブジェクト]()を参照してください。
</blockquote>


## UDO変数

UDOタイプは、[ユニバーサルデータオブジェクト](https://docs.tealium.com/ja/platforms/javascript/about-utag-data/)（`utag_data`とも呼ばれる）で定義された変数用です。UDOはあなたのサイトまたはアプリのコードに実装されます。ほとんどの変数はこのタイプになります。

#### 例

次のJavaScriptスニペットは、ページコードで`language`変数がどのように定義されているかを示しています：

```js
var utag_data = {
  language : "en"
};
```

* 変数名: `language`  
* JavaScript拡張での参照: `b["language"]`

## クエリ文字列パラメータ

クエリ文字列タイプは、URLからのパラメータ用です。クエリ文字列はURLの`?`文字の後に続くものです。クエリ文字列パラメータは`key=value`の形式で、`key`はパラメータ名です。

#### 例

次のURLは、`sortOrder`変数がどのように定義されているかを示しています：

```none
http://example.com/path/page.html?pg=4&sortOrder=price
```

* iQでの変数名: `sortOrder`  
* JavaScript拡張での参照: `b["qp.sortOrder"]`

## ファーストパーティクッキー

ファーストパーティクッキータイプは、あなたのドメインに構成されたクッキー用です。クッキーはファーストパーティクッキーでなければならず、それは使用される同じドメインに構成されていることを意味します。

クッキーにデータを保存するには、ファーストパーティクッキー変数を作成し、その後[Persist Data Value拡張]()を使用して構成します。

ブラウザコンソールを見てクッキーを調べます。たとえば、このドキュメントサイト（`docs.tealium.com`）では、ドメイン`.tealium.com`のクッキーのみがファーストパーティと見なされます。異なるドメインで構成されたクッキーはサードパーティと見なされます。

#### 例

次の構成は、ブラウザクッキーで`_aff`変数がどのように定義されているかを示しています：

![](https://docs.tealium.com/images/iq-tag-management/data-layer/data-layer-variables/first-party-third-party-cookies-marked.png)

* ブラウザクッキー名: `_aff`  
* iQでの変数名: `_aff`  
* JavaScript拡張での参照: `b["cp._aff"]`


<blockquote>
デフォルトでは、`utag.js`はいくつかのクッキーを作成し維持します。これらはあなたの構成で役立つかもしれません。  
詳細については、[Tealium組み込みクッキー](https://docs.tealium.com/tealium-cookies/#built-in-cookies)を参照してください。
</blockquote>


### バージョン4.49以前

`utag.js`のバージョン4.49以前は、いくつかの区切られたキーバリューペアを含む単一のマルチバリュークッキー`utag_main`を作成し維持します。

`utag_main`を使用してカスタムクッキーを作成するには、プレフィックス`utag_main_`（例えば、`utag_main_mycookie`）を持つファーストパーティクッキー変数を作成します。これにより、クッキーがTealiumインストールに関連付けられ、グローバルクッキー名前空間から分離されます。このアプローチは名前の衝突を避け、どのクッキーがタグマネージャーから来たものかを明確にします。

![](https://docs.tealium.com/images/iq-tag-management/whiteui-tiq-tealium-cookies-add-first-party-cookie-variable.jpg)

## JavaScript変数

JavaScriptタイプは、あなたのウェブページ上のJavaScript変数（`utag_data`オブジェクト以外）を参照します。変数名には、文字、数字、アンダースコア、ドル記号、配列ブラケット、ピリオドのみを含めることができます。オブジェクトプロパティを参照するにはドット表記法（`object.propertyName`）を使用します。

#### 例

次のJavaScriptスニペットは、ページコードで`myApp.page.name`変数がどのように定義されているかを示しています：

```js
var myApp = { page : { name : "Home Page" } };
```

* iQでの変数名: `myApp.page.name`  
* JavaScript拡張での参照: `b["js_page.myApp.page.name"]`

## メタデータ要素

メタデータタイプは、ページの`<meta>`タグの内容を参照します。

#### 例

次のメタタグは、ページコードで`author`変数がどのように定義されているかを示しています：

```html
<meta name="author" content="Tealium" />
```

* iQでの変数名: `author`  
* JavaScript拡張での参照: `b["meta.author"]`

## DOM変数

DOMタイプは、`window`および`document`オブジェクトのプロパティを参照します。これらの変数はページ内で自動的に構成されます。

JavaScriptページ変数: `location.hostname`  
JavaScript拡張での参照: `b["dom.hostname"]`

詳細については、[標準ページデータ](https://docs.tealium.com/ja/platforms/javascript/built-in-variables/)を参照してください。

## ローカルおよびセッション保存
（[`utag.js` 4.49](https://docs.tealium.com/ja/release-notes/?filter=tealium-universal-tag#tealium-universal-tag-2022-09-01)で新規）

ローカル保存およびセッション保存タイプは、ブラウザのローカル保存またはセッション保存からのデータを参照します：

* ローカル保存はブラウザセッション間で保存されます。このデータは期限切れになりません。
* セッション保存はページセッションが終了すると期限切れになります。

これらの保存タイプとその使用法の違いについての詳細は、MDN Web Docsの[Window.localStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage)および[Window.sessionStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/sessionStorage)を参照してください。

ローカル保存またはセッション保存に値を構成するには、次のようなカスタムJavaScriptコードを使用して[Advanced JavaScript Code拡張](https://docs.tealium.com/advanced-javascript-code-extension/)を使用します：

```js
localStorage.setItem("key", value);
sessionStorage.setItem("key", value);
```

[Persist Data Value](https://docs.tealium.com/persist-data-value-extension/)または[Set Data Values](https://docs.tealium.com/set-data-values-extension/)拡張を使用して、ローカルまたはセッション保存のブラウザで値を構成することはできません。

セッションおよびローカル保存は、同じサブドメイン内のデータのみにアクセスできます。たとえば、`www.example.com`でアクセスされたデータは`store.example.com`ではアクセスできません。詳細については、[Same Origin Policy](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy#cross-origin_data_storage_access)を参照してください。

拡張でJavaScriptを使用してこれらの変数を参照します：

* ローカル保存: `b["ls.my_local_storage_var"]`
* セッション保存: `b["ss.my_session_storage_var"]`


<blockquote>
2023年3月1日以前に`ls.`または`ss.`プレフィックスでUDOタイプとしてローカル保存またはセッション保存変数を追加した場合、それらの変数は新しいローカル保存およびセッション保存変数タイプに変換されません。
</blockquote>


#### 例

あなたのシステムはローカル保存に`last_category_viewed`変数を保存します：

![](https://docs.tealium.com/images/iq-tag-management/data-layer/data-layer-variables/localandsessionstorage2.png)

この値はページから次のようにアクセスできます：

```js
localStorage.getItem("last_category_viewed").
```---
title: "構成ファイルにこの変数を追加する方法"
linktitle: "構成ファイルに変数を追加"
description: "データレイヤー変数を作成し、ローカル保存変数として構成する方法を説明します。"
---

この変数を構成ファイルに追加するには、**タイプ**を**ローカル保存変数**に構成し、**ソース**を`last_category_viewed`に構成したデータレイヤー変数を作成します：

![](https://docs.tealium.com/images/iq-tag-management/data-layer/data-layer-variables/localandsessionstorage1.png)

値を構成するには、以下のようなカスタムJavaScriptコードを使用して[Advanced JavaScript Code Extension](https://docs.tealium.com/advanced-javascript-code-extension/)を使用します：

```js
localStorage.setItem("last_category_viewed", "Apparel")
```

### バージョン4.48以前

`utag.js`のバージョン4.48以前では、以下の名前形式でローカルまたはセッション保存変数を**UDO**タイプとして手動で追加する必要があります：

* ローカル保存: `ls.VARIABLE_NAME`
* セッション保存: `ss.VARIABLE_NAME`

これらの保存変数を使用するには：

1. **Tag Management > Data Layer > +Add Variable**に進みます。
1. **UDO Variable**を選択します。
1. ソース変数名を入力します。