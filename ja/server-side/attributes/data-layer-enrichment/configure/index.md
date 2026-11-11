---
title: タグ管理でのデータレイヤーエンリッチメントの構成
description: タグ管理でデータレイヤーエンリッチメントに属性を提供する顧客データプラットフォーム（CDP）プロファイルを構成します。
url: https://docs.tealium.com/ja/server-side/attributes/data-layer-enrichment/configure/
---
タグ管理の公開構成を使用して、データレイヤーに訪問属性と訪問属性を提供する顧客データプラットフォーム（CDP）プロファイルを選択します。公開構成の詳細については、[公開構成](https://docs.tealium.com/publish-configuration/)を参照してください。


<blockquote>
この構成では、サーバーサイドのデータレイヤーエンリッチメントを有効または無効にすることはできません。Data Layer Enrichment APIおよびProfile Definition APIへのアクセスを制御する方法については、[サーバーサイドのデータレイヤーエンリッチメントを有効にする](https://docs.tealium.com/enable-data-layer-enrichment/)を参照してください。
</blockquote>


## 仕組み

タグ管理のデータレイヤーエンリッチメントでは、iQプロファイルをCDPプロファイルにリンクします。選択したCDPプロファイルから提供される訪問属性と訪問属性が、タグ管理によってデータレイヤーにインポートされます。

デフォルトでは、タグ管理は`main`という名前のCDPプロファイルを使用します。公開構成で別のプロファイルを選択できます。

## CDPプロファイルの選択

1. 管理メニューで、**Configure Publish Settings**をクリックします。**Publish Configuration**ダイアログが表示されます。
1. **General Publishing**タブで、**Implementation**セクションの一番下までスクロールします。
1. **Data Layer Enrichment Profile**からCDPプロファイルを選択します。
1. **Apply**をクリックします。
1. 変更内容を保存し、**Prod**環境に公開します。

![](https://docs.tealium.com/images/server-side/whiteui-datalayerenrichment-selectdatalayerenrichmentprofile.png)