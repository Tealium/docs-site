---
title: Tealium iQでデータレイヤーエンリッチメントを構成する
description: Tealium iQでデータレイヤーエンリッチメントに必要な属性を提供するAudienceStreamプロファイルを構成します。
url: https://docs.tealium.com/ja/server-side/attributes/data-layer-enrichment/configure/
---
Tealium iQの公開構成を使用して、データレイヤーに訪問と訪問属性を提供するAudienceStreamプロファイルを選択します。公開構成の詳細については、[公開構成](https://docs.tealium.com/publish-configuration/)を参照してください。


<blockquote>
この構成はサーバーサイドのデータレイヤーエンリッチメントを有効または無効にするものではありません。データレイヤーエンリッチメントAPIおよびプロファイル定義APIへのアクセスを制御するには、[サーバーサイドのデータレイヤーエンリッチメントを有効にする](https://docs.tealium.com/enable-data-layer-enrichment/)を参照してください。
</blockquote>


## 仕組み

Tealium iQでのデータレイヤーエンリッチメントは、iQプロファイルをAudienceStreamプロファイルにリンクします。選択したAudienceStreamプロファイルは、Tealium iQがデータレイヤーにインポートする訪問と訪問属性を提供します。

デフォルトでは、Tealium iQは`main`という名前のAudienceStreamプロファイルを使用します。公開構成で異なるプロファイルを選択できます。

## AudienceStreamプロファイルを選択

1. 管理メニューで**公開構成の構成**をクリックします。**公開構成**ダイアログが表示されます。
1. **一般公開**タブで、**実装**セクションの最下部までスクロールします。
1. **データレイヤーエンリッチメントプロファイル**からAudienceStreamプロファイルを選択します。
1. **適用**をクリックします。
1. 変更を**Prod**環境に保存して公開します。

![](https://docs.tealium.com/images/server-side/whiteui-datalayerenrichment-selectdatalayerenrichmentprofile.png)