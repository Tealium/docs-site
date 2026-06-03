---
title: Tealium iQとの統合
description: この記事では、Tealiumプラットフォームのサーバーサイドでの公開プロセスについて説明します。
url: https://docs.tealium.com/ja/server-side/save-publish/with-tealium-iq/
---
## データレイヤー変数のインポート

Customer Data HubはTealium iQの変数を使用できます。これを行うには、Tealium iQプロファイルをProd環境に公開して、これらの変数がCustomer Data Hub内の属性として表示されるようにする必要があります。

## データレイヤーのエンリッチメント

Tealium iQは、[データレイヤーエンリッチメント]()という機能を通じてAudienceStreamの属性を利用できます。Tealium iQで訪問の属性を利用可能にするためには、サーバーサイドの構成を公開する必要があります。これらの属性は他のデータレイヤー変数と同様に使用できます。

デフォルトでは、Tealium iQプロファイルは対応するサーバーサイドプロファイルから訪問の属性をインポートしようとします。例えば、Tealium iQプロファイル `tealium/main` はサーバーサイドプロファイル `tealium/main` から読み取ります。

しかし、異なるサーバーサイドプロファイルから訪問の属性をインポートすることも可能です。

異なるサーバーサイドプロファイルから訪問の属性をインポートするには：

1. 管理メニューで **Configure Publish Settings** をクリックします。**Publish Configuration** ダイアログが表示されます。
* **Implementation** セクションで、**Data Layer Enrichment Profile** リストからサーバーサイドプロファイルを選択します。

![](/images/server-side/no-title-1711i6d0b9fae5a4e3679.png)