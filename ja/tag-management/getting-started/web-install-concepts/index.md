---
title: Webインストールの概念
description: Webインストールの基本について説明します。
url: https://docs.tealium.com/ja/tag-management/getting-started/web-install-concepts/
---
## データレイヤー

Webページ用のTealiumデータレイヤーは、JavaScriptオブジェクトの`utag_data`（Universal Data Objectとも呼ばれます）です。これは、デジタルプロパティ上で追跡するアクティビティを、ベンダーに依存しない使いやすい形式で表したものです。

Universal Data Objectには、読み込まれたページに関する基本情報を収集する組み込み変数が含まれています。これらの変数には、`utag.js`によって作成されたCookie、ページの標準DOM変数、および読み込まれた構成に関するTealium固有の変数が含まれます。

`utag.js`によって生成されるUniversal Data Objectの一部である[データレイヤー変数](https://docs.tealium.com/ja/platforms/javascript/data-layer/)の詳細をご覧ください。

## イベント名

イベント名では、追跡する各インタラクションの種類を一意に識別するために、予約変数`tealium_event`を使用します。この変数は、ロードルール、拡張機能、およびデータマッピングを構成するためにTealium全体で参照されます。その他のすべてのイベントデータには、任意の名前を付けた追加の変数を使用します。

[イベントのトラッキングとイベント名](https://docs.tealium.com/ja/platforms/javascript/track/)の詳細をご覧ください。


## シングルページアプリケーション（SPA）

1回の訪問につき`utag.js`を一度だけ読み込むシングルページアプリケーション（SPA）では、自動ページビュー追跡呼び出しを抑制し、アプリケーションが`utag.view()`を使用してこれらの呼び出しを直接行えるようにします。

[シングルページアプリケーション](https://docs.tealium.com/ja/platforms/javascript/single-page-applications/)の詳細をご覧ください。