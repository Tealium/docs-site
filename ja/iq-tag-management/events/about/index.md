---
title: イベントについて
description: この記事では、私たちのイベントシステムの紹介を行います。
url: https://docs.tealium.com/ja/iq-tag-management/events/about/
---
## 仕組み


<blockquote>
イベントシステムは、JQuery拡張などの以前のイベントトラッキングソリューションを置き換えます。
</blockquote>


イベントリスナー、別名 _イベント_ は、ページ上の特定の訪問のアクションを追跡する構成可能なJavaScriptリスナーです。

イベントリスナーは、訪問がページ上で特定のアクションを実行したとき、例えば要素をクリックしたり、ページをスクロールしたり、ビデオプレーヤーを使用したりするときに追跡します。訪問がアクションを実行すると、イベントリスナーの変数を含むトラッキングコールがトリガーされます。

コードなしのイベントリスナーを使用すると、以下のことができます：

* 自分のユニークなニーズに合わせてイベントリスナーを構成します。
* イベントリスナーがページ上でロードされるタイミングを決定するさまざまなスコープから選択します。
* イベントリスナーをロードするページを決定するための高度なルールロジックを構成します。
* トラッキングニーズに基づいて構成できるユニークなイベントトリガーを構成します。
* イベントリスナーでページ上の特定の要素をターゲットにします。
* アクションが発生したときに送信されるデータペイロードを構成します。


## イベントの種類と変数

以下の種類のイベントがこの機能を通じて利用可能です：

* [**クリック**](https://docs.tealium.com/click-event/) - 訪問がページ上でマウスをクリックしたとき。
* [**マウスオーバー**](https://docs.tealium.com/mouseover-event/) - 訪問がページ上の特定の要素にマウスをホバーしたとき。
* [**フォーム送信**](https://docs.tealium.com/form-submission-event/) - 訪問がページ上のフォームを送信したとき。
* [**YouTube**](https://docs.tealium.com/youtube-event/) - 訪問がページ上の埋め込まれたYouTubeビデオを操作したとき。
* [**Vimeo**](https://docs.tealium.com/vimeo-event/) - 訪問がページ上の埋め込まれたVimeoビデオを操作したとき。
* [**HTML5ビデオ**](https://docs.tealium.com/html5-video-event/) - 訪問がページ上の埋め込まれたHTML5ビデオを操作したとき。
* [**ページロード**](https://docs.tealium.com/page-load-event/) - 訪問がページをロードしたとき。
* [**スクロール**](https://docs.tealium.com/scroll-event/) - 訪問がページを縦または横にスクロールしたとき。
* [**要素の可視性**](https://docs.tealium.com/element-visibility-event/) - ページが訪問にスクリーン要素を表示したとき。
* [**ブラウザ履歴の変更**](https://docs.tealium.com/browser-history-change-event/) - 訪問がシングルページアプリケーション（SPA）をナビゲートしたとき。
* [**ハッシュ変更**](https://docs.tealium.com/hash-change-event/) - ページのURLのハッシュ記号（`#`）の後のアンカー部分が変更されたとき。

これらのイベントのそれぞれは、そのイベントに特有の`tealium_event`値（例えば、スクロールイベントの場合は`scroll`）で事前に構成されています。これらのイベントタイプの一部には、デフォルトで追加のイベント変数が含まれており、必要に応じてイベント変数をカスタマイズまたは追加できます。

詳細については、[ベストプラクティス - イベントトラッキング](https://docs.tealium.com/best-practices-for-iq/#event-tracking)を参照してください。