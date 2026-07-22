---
title: ページパフォーマンス
description: ページパフォーマンスは、Webページがブラウザでどれだけ速くロードされ、レンダリングされるかを測定します。ページパフォーマンスの主な目的は、ユーザーエクスペリエンスを最適化することです。
url: https://docs.tealium.com/ja/iq-tag-management/troubleshooting/page-performance/
---
[秘密ではありません](https://www.nngroup.com/articles/website-response-times/)が、ロードが遅いページは訪問を失う原因となるため、ページパフォーマンスを最大化することは一般的に価値ある取り組みとされています。

ページパフォーマンスを評価し始めると、ロード速度に影響を与えるさまざまな要因があることが明らかになります：

* ネットワーク遅延
* ファイル圧縮
* ブラウザキャッシング
* CSS
* フォント
* インラインJavaScript

タグ付け（JavaScriptファイルのロード）は、この複雑なプロセスの要因の一つに過ぎませんが、この記事の焦点となります。より具体的には、認識されるページパフォーマンスに寄与する要因と、iQタグ管理コンソール内で使用できるコントロールについて探求します。特に、タグ付けとパフォーマンスに最も関連する二つの概念に焦点を当てます：

* 非同期JavaScript
* DOM-Readyイベント

## 認識されるロード時間と実際のロード時間

始める前に、認識されるロード時間と実際のロード時間の違いについて触れておく価値があります。実際のロード時間は、ブラウザがWebページのすべてのアセットが処理されたことを示す従来の測定です。一方、認識されるロード時間は、より重要とされるもので、Webページが視覚的にレンダリングされ、ユーザーに利用可能になる時点の測定です。

この測定については非常に技術的であり、[WebPagetest](https://sites.google.com/a/webpagetest.org/docs/using-webpagetest/metrics/speed-index)、Googleの[PageSpeed Tools](https://developers.google.com/speed/pagespeed/)、Yahooの[YSlow](http://yslow.org/)などの業界専門ホームによって研究されています。


<blockquote>
iQタグ管理JavaScriptライブラリ（`utag.js`）は、ページの認識されるロード時間にほとんどまたは全く影響を与えないように設計されています。
</blockquote>


## Tealiumファイルとサードパーティファイル

Tealiumソリューションの基盤には、ファイル提供フレームワークがあります。このグローバルかつリアルタイムのソリューションは、Tealiumのファイルが可能な限り迅速に訪問のブラウザに配信されることを保証します。JavaScriptローダー（またはラッパー）ファイルには、iQタグ管理アカウントからのロジックと構成が含まれており、ブラウザのネットワークコンソールで`utag.js`および`utag.#.js`という名前で識別できます。これらは`tags.tiqcdn.com`ドメインからTealiumによって提供されるファイルです。

Tealiumファイルのブラウザネットワークログの例：

![](https://docs.tealium.com/images/iq-tag-management/tealium-network-utag-files.jpg)

ブラウザがこれらのTealiumファイルをロードする際、タグベンダーに必要な追加のファイルリクエストが発生する場合があります。これらのファイルは、`tags.tiqcdn.com`以外のドメインから来ており、`utag`以外の名前で識別されることがあります。


<blockquote>
Tealiumはサードパーティファイルのパフォーマンスをホストまたは制御していません。
</blockquote>


## ブラウザファイルキャッシュ

ブラウザにはページパフォーマンスを最適化するための独自の方法があり、最も広く知られているのはファイルキャッシングです。ブラウザはファイルのコピーを保存し、同じコンテンツを何度もネットワーク経由でリクエストする必要がなくなります。これにより、ネットワークトラフィックが減少し、ブラウザに初期アセットがキャッシュされている場合、サイトページのロードがより迅速になります。

詳細については、[Tealiumファイルのキャッシュ方法]()を参照してください。

## 非同期JavaScript

非同期JavaScriptは、非本質的な要素のロードを遅らせて、ページのレンダリングをユーザーに優先させる方法です。非同期リクエストをページ内の「To Do」リストと考えることができます。ブラウザが他の優先度の高い要素をレンダリングする必要がない場合、非同期「To Do」リストの項目を処理します。対照的に、同期JavaScriptを使用すると、「Must Do」リストのような効果が得られます。ブラウザはページのレンダリングをブロックして、同期「Must Do」リストの項目を処理する必要があります。

すべての現代のタグベンダーは非同期方法に切り替えており、これはページロード速度を向上させる最も一般的な方法の一つです。

iQタグ管理では、`utag.js`ローダーファイルとその後にロードされるすべてのタグファイルが非同期方法を使用しています。

詳細については、以下を読んでください：

* [同期対非同期JavaScript](https://support.tealiumiq.com/en/support/solutions/articles/36000363409-synchronous-vs-asynchronous-javascript-sync-vs-async-)
* [JavaScriptの最適化](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/page-speed-rules-and-recommendations#optimize_javascript_use)

## DOM-readyイベント

DOM-readyイベント（`DOMContentLoaded`とも呼ばれる）は、ブラウザがページの主要コンテンツのロードを完了したことを示す方法です。このイベントは一般的に、ページができるだけ早くレンダリングされるように、非本質的な要素のロードのトリガーとして使用されます。これにより、認識されるロード時間が改善されます。

iQタグ管理では、ページのレンダリングへの影響を最小限に抑えるために、DOM-Readyイベントまでベンダートラッキングが遅延されます。

詳細については、以下を参照してください：

* [操作の順序の理解]()
* [DOMContentLoaded - イベントリファレンス | Mozilla Developer Network]()

## iQタグ管理の構成とベストプラクティス

iQタグ管理には、ページ上でJavaScriptがロードされる方法を制御するためのいくつかのオプションがあります。すべてのウェブサイトが異なるため、すべての人にとって最適な単一のソリューションはありません。iQのデフォルト構成は、認識されるロード時間に最小限の影響を与え、最大数のベンダータグとの互換性を提供するようにバランスが取られています。

### コード配置

コード配置は、HTMLドキュメント内で`utag.js`コードスニペットが表示される場所を指します。HTML内でJavaScriptをロードする主な場所は二つあります：`<head>`タグ内と`<body>`タグ内です。Tealiumの`utag.js`ファイルは`<body>`タグ内にロードする必要があります。

基本的なHTML構造：

```html
<html>
<head>
    <!-- ここにスクリプトファイル -->
</head>
<body>
    <!-- ここにTealium utag.js非同期スクリプト -->
    ....
</body>
</html>
```

ベストプラクティスは、`utag.js`コードスニペットを`<body>`の先頭に配置することです。この位置では、タグ管理構成が非同期でロードされるため、ページが引き続きレンダリングされ、DOM-Readyイベントでタグが発火する準備が整います。`utag.js`ファイルは`<body>`内の下部に配置することも可能です。一般的に、これによりタグのロードが遅れたり、認識されるロード時間がわずかに速くなったりします。

詳細については、[utag.jsコード配置](https://docs.tealium.com/ja/platforms/javascript/install)を参照してください。

### Ready Waitフラグ

Ready Waitフラグは[**公開構成**エリア]()で見つけることができます。これは`utag.js`が実行を開始するタイミングを制御します。デフォルトでは、このフラグは**オフ**であり、`utag.js`はページにロードされるとすぐに実行を開始します。このフラグを**オン**に構成すると、`utag.js`はDOM-Readyイベントまで実行を待機します。このフラグをオンにすることで、ページロード時間の可能な改善を優先してタグを後回しにすることができます。


<blockquote>
**Ready Waitフラグ**を**オン**に構成すると、タグがロードされる前に訪問がページから離れるため、トラッキングが失われる可能性があります。常に新しい構成をライブサイトにリリースする前に徹底的なテストを行ってください。
</blockquote>


### ファイルの圧縮と最小化

Tealiumのサーバーから送信されるファイルは、ほとんどのブラウザーで業界標準のBrotliを使用して圧縮されます。（Brotliを処理できない古いブラウザーは、代わりにGzip圧縮を使用します。）これにより、JavaScriptファイル（テキストファイル）がブラウザーに配信される際に可能な限り小さくなります。この動作は変更できません。これらのJavaScriptファイル内のコードもデフォルトで最小化されています。最小化は、コメント行と空白を削除することで、コードファイルをその本質的なテキストのみに圧縮する別のステップを追加します。デバッグが必要な場合は、この構成をオフにすることができます。

詳細については、[Minify Tag Templates setting]()を参照してください。

### バンドリング

バンドリングにより、ベンダータグコードをメインの`utag.js`ファイルに含めることができ、ページからの追加のHTTPリクエストを排除します。デフォルトでは、iQタグ管理で構成されたベンダータグは別々のファイル（例えば、`utag.4.js`）としてページにロードされます。これは、メインの`utag.js`ファイルにコードエラーを導入するリスクを最小限に抑えるためです（例えば、あるファイルのエラーが他のファイルに影響を与えない）。しかし、別々のファイルを使用すると、タグをロードするためにページが行うHTTPリクエストの数が増えます。これらのファイルの配信はTealiumのサーバーとブラウザキャッシュを介して最適化されていますが、さらに最適化が必要な場合はバンドリングが検討すべきオプションです。

ここに、Tealiumからのファイルのロード時間が80％改善されたバンドリングタグの簡単な例を示します。

#### バンドルされていない2つのベンダータグ

* **ファイル数:** 3 (utag.js, utag.1.js, utag.21.js)
* **合計サイズ:** 18.2 KB (9.1 + 5.0 + 4.1)
* **合計時間:** 100 ms (54 + 23 + 23)

![](https://docs.tealium.com/images/iq-tag-management/tlc-network-utag.jpg)

#### バンドルされた2つのベンダータグ

* **ファイル数:** 1 (utag.js)
* **合計サイズ:** 17 KB
* **合計時間:** 19 ms

![](https://docs.tealium.com/images/iq-tag-management/tlc-network-utag-bundle.jpg)

詳細については、[Bundling individual tags](https://docs.tealium.com/tag-advanced-settings/#bundle-flag)または[Bundling any tag using the **All Pages** load rule](https://docs.tealium.com/publish-configuration/#performance-optimization)を参照してください。

### タグのタイミング (tags)

前述のように、`utag.js`のデフォルトの動作は、DOM-Readyイベントを待ってからベンダータグを発火させることです。**Tag Timing**構成は、個々のタグのこのロジックを制御するタグレベルの構成です。デフォルト構成は**DOM Ready (default)**で、これは「DOM-Readyを待つ」という意味です。このフラグが**Prioritized**に構成されている場合、個々のタグは可能な限り早く（通常はDOM-Ready前に）実行されます。

詳細については、[Tag timing for tags](https://docs.tealium.com/tag-advanced-settings/#tag-timing)を参照してください。

### タグの順序

構成されたタグは、iQタグ管理コンソールに表示される順序でページにロードされます。タグをロードしたい順序にドラッグアンドドロップできます。Tealiumのベストプラクティスは、分析タグや他の優先度の高いタグをリストのトップに置き、それらが最初にロードされるようにすることです。

詳細については、[Tag ordering](https://docs.tealium.com/manage-tags/#load-order)を参照してください。
