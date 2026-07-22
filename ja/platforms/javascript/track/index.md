---
title: トラッキング
description: ユーザー活動を追跡するための機能について学びます。
url: https://docs.tealium.com/ja/platforms/javascript/track/
---
## ビューの追跡

[`utag.view()`](https://docs.tealium.com/ja/platforms/javascript/api/tracking-functions/#utag-view) 関数は、ページビュー、仮想ページビュー、およびAjaxページフローを追跡します。この関数を呼び出すと、構成されたベンダータグ内の対応するページ追跡機能がトリガーされます。`utag.js`は、ページがロードされるたびに自動的にこの関数をトリガーします。

`utag.view()`は、ユーザーがサイトをナビゲートする際にURLがリフレッシュされないAjaxページフローで一般的に使用されます。例えば、シングルページチェックアウトやシングルページアプリケーションなどです。

最初のページロード時に宣言されたユニバーサルデータオブジェクト（UDO）、`utag_data`は、これらの呼び出しで再利用されません。新しいデータオブジェクトをこの関数に明示的に渡す必要があります。


<blockquote>
重要なページビューイベントを識別するために変数[`tealium_event`](#tealium-event)を使用し、ページテンプレートを一意に識別するために`page_type`を使用することがベストプラクティスです。
</blockquote>


以下の例では、「商品クイックビュー」ビューを追跡します：

```javascript
utag.view({
    "tealium_event": "product_view",
    "page_type"    : "product_quick_view",
    "page_name"    : "Quick View: Shirts: Lucky Shirt",
    "product_id"   : ["12345"],
    "product_name" : ["Lucky Shirt"]
});
```

## イベントの追跡

[`utag.link()`](https://docs.tealium.com/ja/platforms/javascript/api/tracking-functions/#utag-link) 関数は、ページビュー以外のイベント、ページ内のインタラクション、その他の動的ページイベントを追跡します。イベント追跡は、訪問のページ内でのインタラクションに関する情報を収集します。ページビュー追跡が訪問のナビゲーションパスに関する情報を収集するのに対し、イベント追跡はナビゲーションステップの間に訪問が行うことを監視します。

以下の例では、「カートに追加」イベントを追跡します：

```javascript
utag.link({
    "tealium_event"    : "cart_add",
    "product_id"       : ["12345"],
    "product_name"     : ["Lucky Shirt"],
    "product_quantity" : ["2"],
    "product_price"    : ["12.99"]
});
```

## `tealium_event`

追跡される各タイプのインタラクションを一意に識別するために、予約変数`tealium_event`を使用します。この変数は、Tealium iQ全体でロードルール、拡張機能、およびデータマッピングを構成するために参照されます。他のすべてのイベントデータには、お好みの追加変数名を使用します。

`tealium_event`の値の提案には、以下が含まれますが、これに限定されません：

| `tealium_event`の値 | イベントの説明 |
| --- | --- |
| `page_view` | ページビュー |
| `product_view` | 商品詳細ページビュー |
| `search` | 内部検索 |
| `cart_add` | ショッピングカートに追加 |
| `cart_remove` | ショッピングカートから削除 |
| `cart_view` | ショッピングカートを表示 |
| `purchase` | 購入完了 |
| `user_register` | ユーザー登録完了 |
| `user_login` | ユーザーログイン |
| `email_signup` | ニュースレターのメール登録 |
| `social_share` | ソーシャルサイトでリンクを共有 |

以下の例では、追跡コールに関連する追加情報を追加します：

```javascript
utag.link({
    "tealium_event"  : "social_share",
    "social_network" : "LinkedIn",
    "shared_link"    : "https://tealium.com/"
});
```

[データレイヤーとTealiumイベントについての詳細](https://docs.tealium.com/an-introduction-to-the-data-layer/)を学びましょう。

## 実装オプション

ページビュー追跡が追跡されるページについてのコンテキストを提供するデータレイヤーオブジェクトを必要とするように、イベント追跡も追跡コールに含まれるデータレイヤーオブジェクトが必要です。追跡コールのデータオブジェクトにイベントに関連する変数を含めます。

次のセクションでは、Tealiumのイベント追跡をウェブサイトに実装する方法について説明します。

### jQueryとHTML5

[ジェイクエリ拡張](https://docs.tealium.com/jquery-onhandler-extension/)を使用して、クリック、展開、選択などのページ内の基本的なインタラクションを追跡します。追跡される要素の情報プロパティを実装するためにHTML5 [データ属性](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Using_data_attributes)を使用します。[セマンティックHTML](https://en.wikipedia.org/wiki/Semantic_HTML)を使用したウェブページが必要です。

* リンククリック、ボタンクリック、フォームフィールドのインタラクションに最適です。
* Ajaxページフローやフォーム送信には推奨されません。

データ属性を持つ要素は、ページコードで次のように表示されるかもしれません：

```html
<a href="/logout" data-click_name="Sign Out" data-click_category="header">Log out</a> 
```

このリンクをクリックして追跡し、関連するイベントデータを構成するために、ジェイクエリ拡張でこれらの属性を参照します。

*   特定のデータ属性を持つ要素を識別するためにセレクタを使用します。例えば、`a[data-click_name]`。
*   "JS Code"オプションを使用して、クリックされた要素のデータ属性を参照する変数を構成します。例えば、`$(this).data('click_name')`。

### ページコード

ページコードは、動的ページコンテンツのリフレッシュ、Ajaxページ、モーダルフォームの送信、またはクライアントのウェブサーバーにラウンドトリップリクエスト/レスポンスを必要とするイベントを追跡するために使用されます。

* モーダルフォーム、商品クイックビュー、シングルページウェブサイト、非商品ページからのカート追加に最適です。
* リンク追跡には推奨されません。

### ビデオ追跡

ビデオ追跡は、ビデオプラットフォームAPIの仕様に合わせたカスタムソリューションコーディングをしばしば必要とします。

Tealiumの現在のソリューションについては、[YouTubeビデオ追跡セットアップガイド](https://docs.tealium.com/youtube-event/)で詳しく学びましょう。

### シングルページアプリケーション

[シングルページアプリケーション](https://docs.tealium.com/ja/platforms/javascript/single-page-applications/)のビューとイベントの追跡について学びましょう。