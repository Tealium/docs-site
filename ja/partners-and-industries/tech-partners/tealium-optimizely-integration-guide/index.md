---
title: Tealium + Optimizely 統合ガイド
description: この記事では、TealiumとOptimizelyを最大限に活用し、TealiumのオーディエンスとオーディエンスバッジをOptimizelyに送信する方法について説明します。
url: https://docs.tealium.com/ja/partners-and-industries/tech-partners/tealium-optimizely-integration-guide/
---## 仕組み

Optimizelyプラットフォームには、フィーチャーフラグ、大規模なA/Bテスト、AIによるパーソナライゼーション、ストリーミング分析など、現代のソフトウェア開発のための技術が含まれています。Optimizelyプラットフォームで実験とフィーチャーフラグを実行することで、何がうまくいき、何がうまくいかないかを理解し、推測を排除します。

### クライアントサイドの統合

以下の表は、Optimizelyタグのクライアントサイド統合の説明と前提条件を一覧表示し、詳細なセットアップドキュメンテーションへのリンクを提供します：

|統合タイプ| この統合から期待できること| 製品要件| セットアップガイド|
|---| ---| ---| ---|
| **Optimizelyタグ** &lt;ul&gt;&lt;li&gt;非同期&lt;/li&gt;&lt;li&gt;同期&lt;/li&gt;&lt;/ul&gt; | Tealium Optimizelyの非同期および同期タグ統合により、Tealium iQタグ管理でOptimizelyを構成することで、OptimizelyのWebプロジェクトを迅速かつ簡単にデプロイできます。非同期タグは同時にロードされ、同期タグは順番にロードされます。|  **Tealium** &lt;ul&gt;&lt;li&gt;Tealium iQタグ管理（必須）&lt;/li&gt;&lt;/ul&gt; **Optimizely** &lt;ul&gt;&lt;li&gt;Optimizelyアカウント（必須）&lt;/li&gt;&lt;/ul&gt; |  以下のセットアップガイドを参照してください： &lt;ul&gt;&lt;li&gt;[非同期]()&lt;/li&gt;&lt;li&gt;[同期]()&lt;/li&gt;&lt;/ul&gt; |

### サーバーサイドの統合

以下の表は、サーバーサイドのOptimizely統合タイプの説明と前提条件を一覧表示し、詳細なセットアップドキュメンテーションへのリンクを提供します。

|統合タイプ| この統合から期待できること| 製品要件| セットアップガイド|
|---| ---| ---| ---|
| **Optimizelyイベント** | Tealium Optimizelyイベントとの統合により、Tealium EventStreamを通じてオンラインおよびオフラインのイベントデータをOptimizelyに送信できます。この方法は、顧客の包括的なビューを提供することで、すべてのOptimizely製品に利益をもたらし、コンバージョンとキャンペーン分析の改善につながる洞察を提供します。これは、顧客ライフサイクル全体の体験を向上させるために使用できます。|  **Tealium** &lt;ul&gt;&lt;li&gt;EventStreamおよび/またはAudienceStream（必須）&lt;/li&gt;&lt;/ul&gt; **Optimizely** &lt;ul&gt;&lt;li&gt;Optimizely WebまたはFull Stack（必須）&lt;/li&gt;&lt;/ul&gt; |  以下のセットアップガイドを参照してください： &lt;ul&gt;&lt;li&gt;[Optimizelyイベントコネクタセットアップガイド（BETA）]()&lt;/li&gt;&lt;/ul&gt; |
| **Optimizelyダイナミックカスタマープロファイル** &lt;br&gt; | Optimizelyダイナミックカスタマープロファイルとの統合により、オンラインおよびオフラインのファーストパーティデータを提供することで、顧客の単一で行動可能なビューを作成します。Tealium AudienceStream Customer Data Platform（CDP）を活用することで、Optimizelyおよび他のチャネルがアクションを起こすことができるTealium内でプロファイルとオーディエンスを作成できます。この統合により、TealiumとOptimizelyの共同顧客は、最も価値のある顧客に対して一貫したパーソナライズされたWebおよびモバイル体験を提供し、その結果の体験の影響を測定することができます。|  **Tealium** &lt;ul&gt;&lt;li&gt;EventStreamおよび/またはAudienceStream（必須）&lt;/li&gt;&lt;/ul&gt; **Optimizely** &lt;ul&gt;&lt;li&gt;Optimizely WebまたはFull Stack（必須）&lt;/li&gt;&lt;/ul&gt; |  以下のセットアップガイドを参照してください： &lt;ul&gt;&lt;li&gt;[Optimizely DCPコネクタセットアップガイド]()&lt;/li&gt;&lt;/ul&gt; |

## 追加のリソース

* [OptimizelyイベントAPI：はじめに](https://docs.developers.optimizely.com/web/docs/getting-started-event-api)
* [Optimizely：ダイナミックカスタマープロファイルを使用したオーディエンスの作成](https://help.optimizely.com/Target_Your_Visitors/Personalization%3A_Create_Audiences_with_Dynamic_Customer_Profiles)
* [OptimizelyとTealium AudienceStreamの統合]()
* [AudienceStreamとOptimizely Full Stackの統合]()
* [Tealiumツール：Optimizelyヘルパー]()

