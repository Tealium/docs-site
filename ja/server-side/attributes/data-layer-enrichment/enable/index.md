---
title: データレイヤーエンリッチメントを有効にする
description: この記事では、データレイヤーエンリッチメントを有効にする方法について説明します。
url: https://docs.tealium.com/ja/server-side/attributes/data-layer-enrichment/enable/
---
データレイヤーエンリッチメントを有効にするには、属性をインポートするAudienceStreamプロファイルを選択する必要があります。デフォルトでは、Tealium iQはメインのAudienceStreamプロファイルから属性をロードしますが、Tealium iQのPublish Configurationエリアで別のプロファイルを構成することができます。

データレイヤーエンリッチメントに使用するAudienceStreamプロファイルを構成するには：

1. 管理メニューで、**Configure Publish Settings**をクリックします。**Publish Configuration**ダイアログが表示されます。
1. **General Publishing**タブで、**Implementation**セクションの最下部までスクロールします。
1. 適切な**Data Layer Enrichment Profile**を選択します。
1. **Apply**をクリックし、変更を**Prod**環境に保存して公開を続けます。

![](/images/server-side/whiteui-datalayerenrichment-selectdatalayerenrichmentprofile.png)
