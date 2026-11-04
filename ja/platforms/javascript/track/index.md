---
title: トラッキング
description: ユーザーアクティビティをトラッキングするための関数について説明します。
url: https://docs.tealium.com/ja/platforms/javascript/track/
---
## ビューのトラッキング

[`utag.view()`](https://docs.tealium.com/ja/platforms/javascript/api/tracking-functions/#utag-view) 関数は、ページビュー、仮想ページビュー、Ajax ページフローをトラッキングします。この関数を呼び出すと、構成済みのベンダータグ内で、対応するページトラッキング機能がトリガーされます。`utag.js` は、ページが読み込まれるたびにこの関数を自動的にトリガーします。

`utag.view()` は一般に、ユーザーがサイト内を移動しても URL が更新されない Ajax ページフローで使用されます。たとえば、単一ページのチェックアウトやシングルページアプリケーションなどです。

最初のページ読み込み時に宣言されたユニバーサルデータオブジェクト（UDO）である `utag_data` は、これらの呼び出しでは再利用されません。この関数には、新しいデータオブジェクトを明示的に渡す必要があります。


<blockquote>
重要なページビューイベントを識別するには変数 [`tealium_event`](#tealium-event) を使用し、ページテンプレートを一意に識別するには `page_type` を使用することを推奨します。
</blockquote>


次の例では、「Product Quick View」ビューをトラッキングします。

```javascript
utag.view({
    "tealium_event": "product_view",
    "page_type"    : "product_quick_view",
    "page_name"    : "Quick View: Shirts: Lucky Shirt",
    "product_id"   : ["12345"],
    "product_name" : ["Lucky Shirt"]
});
```

## イベントのトラッキング

[`utag.link()`](https://docs.tealium.com/ja/platforms/javascript/api/tracking-functions/#utag-link) 関数は、ページビュー以外のアクション、ページ上の操作、その他の動的なページイベントなどをトラッキングします。イベントトラッキングでは、ページ_内_での訪問の操作に関する情報を収集します。ページビュートラッキングが訪問の移動経路に関する情報を収集するのに対し、イベントトラッキングは移動ステップの間に訪問が行う操作を監視します。

次の例では、「Add to Cart」イベントをトラッキングします。

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

トラッキングする各操作の種類を一意に識別するには、予約変数 `tealium_event` を使用します。この変数は、タグ管理全体で、ロードルール、拡張機能、データマッピングを構成するために参照されます。その他のすべてのイベントデータには、任意の名前を付けた追加の変数を使用してください。

推奨される `tealium_event` の値には、次のものがありますが、これらに限定されません。

| `tealium_event` の値 | イベントの説明 |
| --- | --- |
| `page_view` | ページビュー |
| `product_view` | 商品詳細ページの表示 |
| `search` | 内部検索 |
| `cart_add` | ショッピングカートへの追加 |
| `cart_remove` | ショッピングカートからの削除 |
| `cart_view` | ショッピングカートの表示 |
| `purchase` | 購入の完了 |
| `user_register` | ユーザー登録の完了 |
| `user_login` | ユーザーログイン |
| `email_signup` | メールニュースレターへの登録 |
| `social_share` | ソーシャルサイトでのリンク共有 |

次の例では、トラッキング呼び出しにイベント関連の追加情報を加えています。

```javascript
utag.link({
    "tealium_event"  : "social_share",
    "social_network" : "LinkedIn",
    "shared_link"    : "https://tealium.com/"
});
```

[データレイヤーと Tealium イベント](https://docs.tealium.com/an-introduction-to-the-data-layer/)について詳しく説明します。

## 実装オプション

ページビュートラッキングで、トラッキング対象のページに関するコンテキストを提供するためにデータレイヤーオブジェクトが必要なのと同様に、イベントトラッキングでも、トラッキング呼び出しにデータレイヤーオブジェクトを含める必要があります。トラッキング呼び出しのデータオブジェクトには、イベントに関連する変数を含めてください。

以降のセクションでは、Tealium のイベントトラッキングをウェブサイトに実装する方法について説明します。

### jQuery と HTML5

ページ内でのクリック、展開、選択などの基本的な操作をトラッキングするには、[jQuery 拡張機能](https://docs.tealium.com/jquery-onhandler-extension/)を使用します。トラッキング対象要素の情報プロパティを実装するには、HTML5 の[データ属性](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Using_data_attributes)を使用します。[セマンティック HTML](https://en.wikipedia.org/wiki/Semantic_HTML) を使用したウェブページが必要です。

* リンクのクリック、ボタンのクリック、フォームフィールドの操作に最適です。
* Ajax ページフローやフォーム送信には推奨されません。

データ属性を持つ要素は、ページコード内では次のようになります。

```html
<a href="/logout" data-click_name="Sign Out" data-click_category="header">Log out</a> 
```

jQuery 拡張機能でこれらの属性を参照し、このリンクのクリックをトラッキングするとともに、「JS Code」オプションを使用して関連するイベントデータを構成します。

*   特定のデータ属性を持つ要素を識別するには、セレクターを使用します。例：`a[data-click_name]`
*   クリックされた要素のデータ属性を参照するには、「JS Code」オプションを使用して変数を構成します。例：`$(this).data('click_name')`

### ページコード

ページコードは、動的なページコンテンツの更新、Ajax ページ、モーダルフォームの送信、またはページ上にまだ存在しない追加データを取得するためにクライアントのウェブサーバーとのリクエスト／レスポンスの往復を必要とするイベントをトラッキングする場合に使用します。

* モーダルフォーム、商品のクイックビュー、単一ページのウェブサイト、商品ページ以外からのカートへの追加に最適です。
* リンクのトラッキングには推奨されません。

### 動画のトラッキング

動画のトラッキングでは、多くの場合、動画プラットフォーム API の仕様に従ってコーディングしたカスタムソリューションが必要です。

Tealium の現在のソリューションについて詳しくは、[YouTube 動画トラッキング構成ガイド](https://docs.tealium.com/youtube-event/)を参照してください。

### シングルページアプリケーション

[シングルページアプリケーション](https://docs.tealium.com/ja/platforms/javascript/single-page-applications/)でのビューとイベントのトラッキングについて説明します。