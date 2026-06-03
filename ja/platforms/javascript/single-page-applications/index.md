---
title: シングルページアプリケーション
description: シングルページアプリケーションのリンクとイベントの追跡方法を学びます。
url: https://docs.tealium.com/ja/platforms/javascript/single-page-applications/
---
 [イベントシステム]()は、JQuery拡張などの以前のイベント追跡ソリューションを置き換えます。[ブラウザ履歴変更]()、[ページロード]()、[ハッシュ変更]()イベントリスナーは、シングルページアプリケーションに特に有用です。

## セットアップ

シングルページアプリケーション（SPA）では、ページが訪問ごとに `utag.js` を一度だけロードするため、自動的なページビュートラッキングの呼び出しを抑制し、アプリケーションがこれらの呼び出しを直接行うことができます。

自動的なページトラッキングをオーバーライドするには、 `utag.js` をロードする前にページに以下の行を追加します：  
```javascript
window.utag_cfg_ovrd = window.utag_cfg_ovrd || {};
window.utag_cfg_ovrd.noview = true
```

アプリケーションがロードされ（そして `utag.js `がロードされたら）、ページコード内で `utag.view()` トラッキング呼び出しをトリガーします。これらの呼び出しは通常、DOM-readyイベントやコンテンツビューのリフレッシュを引き起こすイベントでトリガーされます。 `utag.js` の動作を調整するための利用可能な構成については、[こちら](/ja/platforms/javascript/settings/)をご覧ください。

初期ページ着陸時に宣言された `utag_data` オブジェクトは、これらの呼び出しで再利用されません。初期ページ着陸からのデータを使用するには、それを再宣言し、関数呼び出しで再度渡す必要があります。

グローバルおよびタグスコープの拡張は、これらの呼び出し中に実行されます。プリローダーとDOM Ready拡張は、これらの呼び出し中には実行されません。


## ビューの追跡

シングルページアプリケーションでのビューの追跡は、[`utag.view()`](/ja/platforms/javascript/api/tracking-functions/#utag-view)関数を使用して行います。

以下の `utag.view()` 関数呼び出しは、キー値ペアを使用してデータを渡す方法を示しています：  
```javascript
utag.view({ variable1:&#34;VARIABLE1 VALUE&#34;, variable2:&#34;VARIABLE2 VALUE&#34;, variable3:&#34;VARIABLE3 VALUE&#34; });
```

### 例

以下は、訪問が &#34;政治&#34; を検索したコンテンツサイトの例です：  
```javascript
utag.view({tealium_event:&#34;search&#34;, search_keyword:&#34;politics&#34;, search_results: 42});
```

以下の例は、ビューの追跡方法を示しています：  
```javascript
utag.view({
    &#34;demo_site&#34; : &#34;Tealium React Demo&#34;,
    &#34;demo_event&#34; : &#34;View &#34; &#43; name
})
```

## イベントの追跡

シングルページアプリケーションでのリンクとイベントの追跡は、[`utag.link()`](/ja/platforms/javascript/api/tracking-functions/#utag-view)関数を使用して行います。

jQueryがインストールされている場合、[jQuery onHandler]()拡張を使用するオプションがあります。この拡張は、 `utag.link()` および `utag.view()` 関数をトリガーする特定のイベントバインディングに対して構成可能です。これにより、トラッキングロジックをサイドコードにハードコーディングすることを避けることができます。

以下の `utag.link()` 関数呼び出しは、キー値ペアを使用してデータを渡す方法を示しています：  
```javascript
utag.link({ variable1:&#39;VARIABLE1 VALUE&#39;, variable2:&#39;VARIABLE2 VALUE&#39; });
```

### 早期トラッキングイベントのためのキュー

バージョン4.52以降では、キューシステムがSPAsの早期トラッキングイベントを処理します。これにより、 `utag.view`、 `utag.link`、および `utag.track` 関数がページロード時にすぐに利用可能になり、これらの関数が `utag.js` が完全にロードされる前に呼び出されたときのエラーや失われたイベントを防ぎます。この機能を有効にする方法についての詳細は、[早期トラッキングイベントのためのキュー](/ja/platforms/javascript/version-4-52/#queue-for-early-tracking-events)を参照してください。

### 例

以下は、ソーシャルメディアの共有アクションの追跡のコンテンツサイトの例です：

```javascript
utag.link({
    &#34;content_id&#34;         : &#34;38121&#34;,
    &#34;page_friendly_url&#34; : &#34;/travel/national_parks&#34;,
    &#34;page_name&#34;          : &#34;Travel: National Parks&#34;,
    &#34;social_network&#34;     : &#34;facebook&#34;,
    &#34;tealium_event&#34;      : &#34;social_share&#34;
})
```

以下のReactJSの例は、[Tealiumデモアプリケーション](http://react.tealiumdemo.com/)からのもので、追加、編集、保存、削除機能のイベント追跡方法を示しています。各関数呼び出しは `utag.link()` 関数をトリガーします。  
```javascript
add(text) {
    utag.link({
        &#34;page_type&#34;: &#34;react&#34;,
        &#34;view_name&#34;: &#34;board&#34;,
        &#34;event_type&#34;: &#34;click&#34;,
        &#34;event_name&#34;: &#34;add_note&#34;,
        &#34;tealium_event&#34;: &#34;add_note&#34;
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
        &#34;page_type&#34;: &#34;react&#34;,
        &#34;view_name&#34;: &#34;board&#34;,
        &#34;event_type&#34;: &#34;click&#34;,
        &#34;event_name&#34;: &#34;edit_note&#34;,
        &#34;tealium_event&#34;: &#34;edit_note&#34;
    })
    this.setState({editing: true});
}
save() {
    utag.link({
        &#34;page_type&#34;: &#34;react&#34;,
        &#34;view_name&#34;: &#34;board&#34;,
        &#34;event_type&#34;: &#34;click&#34;,
        &#34;event_name&#34;: &#34;save_note&#34;,
        &#34;tealium_event&#34;: &#34;save_note&#34;
    })
    this.props.onChange(this.refs.newText.value, this.props.id)
    this.setState({editing: false});
}
remove() {
    utag.link({
        &#34;page_type&#34;: &#34;react&#34;,
        &#34;view_name&#34;: &#34;board&#34;,
        &#34;event_type&#34;: &#34;click&#34;,
        &#34;event_name&#34;: &#34;remove_note&#34;,
        &#34;tealium_event&#34;: &#34;remove_note&#34;
    })

    this.props.onRemove(this.props.id)
}
```
