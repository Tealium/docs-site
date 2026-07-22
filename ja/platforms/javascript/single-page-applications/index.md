---
title: シングルページアプリケーション
description: シングルページアプリケーションのリンクとイベントの追跡方法を学びます。
url: https://docs.tealium.com/ja/platforms/javascript/single-page-applications/
---

<blockquote>
[イベントシステム](https://docs.tealium.com/about-events/)は、JQuery拡張などの以前のイベント追跡ソリューションを置き換えます。[ブラウザ履歴変更](https://docs.tealium.com/browser-history-change-event/)、[ページロード](https://docs.tealium.com/page-load-event/)、[ハッシュ変更](https://docs.tealium.com/hash-change-event/)イベントリスナーは、シングルページアプリケーションに特に有用です。
</blockquote>


## セットアップ

シングルページアプリケーション（SPA）では、ページが訪問ごとに `utag.js` を一度だけロードするため、自動的なページビュートラッキングの呼び出しを抑制し、アプリケーションがこれらの呼び出しを直接行うことができます。

自動的なページトラッキングをオーバーライドするには、 `utag.js` をロードする前にページに以下の行を追加します：  
```javascript
window.utag_cfg_ovrd = window.utag_cfg_ovrd || {};
window.utag_cfg_ovrd.noview = true
```

アプリケーションがロードされ（そして `utag.js `がロードされたら）、ページコード内で `utag.view()` トラッキング呼び出しをトリガーします。これらの呼び出しは通常、DOM-readyイベントやコンテンツビューのリフレッシュを引き起こすイベントでトリガーされます。 `utag.js` の動作を調整するための利用可能な構成については、[こちら](https://docs.tealium.com/ja/platforms/javascript/settings/)をご覧ください。

初期ページ着陸時に宣言された `utag_data` オブジェクトは、これらの呼び出しで再利用されません。初期ページ着陸からのデータを使用するには、それを再宣言し、関数呼び出しで再度渡す必要があります。

グローバルおよびタグスコープの拡張は、これらの呼び出し中に実行されます。プリローダーとDOM Ready拡張は、これらの呼び出し中には実行されません。


## ビューの追跡

シングルページアプリケーションでのビューの追跡は、[`utag.view()`](https://docs.tealium.com/ja/platforms/javascript/api/tracking-functions/#utag-view)関数を使用して行います。

以下の `utag.view()` 関数呼び出しは、キー値ペアを使用してデータを渡す方法を示しています：  
```javascript
utag.view({ variable1:"VARIABLE1 VALUE", variable2:"VARIABLE2 VALUE", variable3:"VARIABLE3 VALUE" });
```

### 例

以下は、訪問が "政治" を検索したコンテンツサイトの例です：  
```javascript
utag.view({tealium_event:"search", search_keyword:"politics", search_results: 42});
```

以下の例は、ビューの追跡方法を示しています：  
```javascript
utag.view({
    "demo_site" : "Tealium React Demo",
    "demo_event" : "View " + name
})
```

## イベントの追跡

シングルページアプリケーションでのリンクとイベントの追跡は、[`utag.link()`](https://docs.tealium.com/ja/platforms/javascript/api/tracking-functions/#utag-view)関数を使用して行います。


<blockquote>
jQueryがインストールされている場合、[jQuery onHandler](https://docs.tealium.com/jquery-onhandler-extension/)拡張を使用するオプションがあります。この拡張は、 `utag.link()` および `utag.view()` 関数をトリガーする特定のイベントバインディングに対して構成可能です。これにより、トラッキングロジックをサイドコードにハードコーディングすることを避けることができます。
</blockquote>


以下の `utag.link()` 関数呼び出しは、キー値ペアを使用してデータを渡す方法を示しています：  
```javascript
utag.link({ variable1:'VARIABLE1 VALUE', variable2:'VARIABLE2 VALUE' });
```

### 早期トラッキングイベントのためのキュー

バージョン4.52以降では、キューシステムがSPAsの早期トラッキングイベントを処理します。これにより、 `utag.view`、 `utag.link`、および `utag.track` 関数がページロード時にすぐに利用可能になり、これらの関数が `utag.js` が完全にロードされる前に呼び出されたときのエラーや失われたイベントを防ぎます。この機能を有効にする方法についての詳細は、[早期トラッキングイベントのためのキュー](https://docs.tealium.com/ja/platforms/javascript/version-4-52/#queue-for-early-tracking-events)を参照してください。

### 例

以下は、ソーシャルメディアの共有アクションの追跡のコンテンツサイトの例です：

```javascript
utag.link({
    "content_id"         : "38121",
    "page_friendly_url" : "/travel/national_parks",
    "page_name"          : "Travel: National Parks",
    "social_network"     : "facebook",
    "tealium_event"      : "social_share"
})
```

以下のReactJSの例は、[Tealiumデモアプリケーション](http://react.tealiumdemo.com/)からのもので、追加、編集、保存、削除機能のイベント追跡方法を示しています。各関数呼び出しは `utag.link()` 関数をトリガーします。  
```javascript
add(text) {
    utag.link({
        "page_type": "react",
        "view_name": "board",
        "event_type": "click",
        "event_name": "add_note",
        "tealium_event": "add_note"
    })
    var notes = [
        ...this.state.notes,
        {
            id: this.nextId(),
            note: text
        }
    ]
    this.setState({notes})
}

edit() {
    utag.link({
        "page_type": "react",
        "view_name": "board",
        "event_type": "click",
        "event_name": "edit_note",
        "tealium_event": "edit_note"
    })
    this.setState({editing: true});
}
save() {
    utag.link({
        "page_type": "react",
        "view_name": "board",
        "event_type": "click",
        "event_name": "save_note",
        "tealium_event": "save_note"
    })
    this.props.onChange(this.refs.newText.value, this.props.id)
    this.setState({editing: false});
}
remove() {
    utag.link({
        "page_type": "react",
        "view_name": "board",
        "event_type": "click",
        "event_name": "remove_note",
        "tealium_event": "remove_note"
    })

    this.props.onRemove(this.props.id)
}
```
