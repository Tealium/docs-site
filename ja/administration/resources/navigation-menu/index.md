---
title: ナビゲーションメニュー
description: ユーザーのワークフローを効率化し、アクセシビリティを向上させ、将来の製品拡張に対応できるよう、刷新・統合されたナビゲーションメニューを導入しました。
url: https://docs.tealium.com/ja/administration/resources/navigation-menu/
---
## 概要

ナビゲーションメニューは、製品名ではなくアクション別に構成されています。カテゴリーは、さまざまなユーザーロールに共通する作業ごとにグループ化されています。

![](https://docs.tealium.com/images/administration/navigation-menu-after.png) 

* **タグ管理**  
クライアント側のタグ、ルール、イベント、同意を管理します。
* **接続**  
データ収集やコネクターなど、受信および送信データの統合を管理します。
* **ガバナンス**  
同意オーケストレーションや訪問検索など、データ品質、プライバシー、同意を管理します。
* **変換**  
データ属性を管理し、ルール、関数、予測スコアリングなどのエンリッチメントを使用してデータアセットを作成します。
* **アクティベート**  
オーディエンスの作成、オーディエンスジョブ、Context APIを使用した訪問プロファイルのアクティベーションなど、データのアクティベーションを管理します。
* **検証**  
トレース、ライブイベント、ライブ訪問（旧称「訪問プロファイルサンプラー」）、イベント仕様などのツールを使用して、本番環境でユースケースをテストおよび検証します。
* **保存**  
データベース保存製品を一元管理します。以前はDataAccessに含まれていた機能が、こちらに追加されました。
* **分析**  
レポートおよび分析ツールを使用して、パフォーマンスの監視、インサイトの生成、データとオーディエンス全体の結果測定を行います。

### フィードバックの提供

新しいナビゲーションの使用感をお聞かせください。フィードバックを送信するには、**リソースセンター > 新しいナビゲーションに関するフィードバック**に移動します。

## 新機能

### 変更前と変更後

| 変更前 | 変更後 |
|--------|-------|
| ![](https://docs.tealium.com/images/administration/navigation-menu-before.png) | ![](https://docs.tealium.com/images/administration/navigation-menu-after.png) |
{.vtop}

### 名前が変更された項目

以前のナビゲーションメニューにあった次の項目は、名前が変更されました。以前の名前を基に目的の項目を探すには、この表を使用してください。

| 以前の項目 | 新しい項目 |
| -------- | -------- |
| タグ管理 | タグ管理 |
| サーバー側ツール > ルールを管理 | 変換 > ルール |
| サーバー側ツール > 訪問プロファイルサンプラー | 検証 > ライブ訪問 |
| サーバー側ツール > 訪問検索 | ガバナンス > 訪問検索 |
| データサプライチェーン > 使用状況レポート | 分析 > 使用状況 |
| インサイト > ユーザーを管理 | 分析 > インサイト > QuickSightユーザー |

### 新しいナビゲーションメニューの階層

ナビゲーションメニュー項目の完全な一覧です。

* [タグ管理](https://docs.tealium.com/tag-management/) 
  * ダッシュボード 
  * [データレイヤー](https://docs.tealium.com/about-the-data-layer/) 
  * [読み込みルール](https://docs.tealium.com/about-load-rules/) 
  * [イベント](https://docs.tealium.com/about-events/) 
  * [タグ](https://docs.tealium.com/about-tags/) 
  * [拡張機能](https://docs.tealium.com/about-extensions/) 
  * [同意統合](https://docs.tealium.com/about-consent-integrations/) 
  * クライアント側ツール
    * [ブラウザーツール](https://docs.tealium.com/ja/tools/tealium-tools/) 
    * [タグレポート](https://docs.tealium.com/tag-reporting/) 
    * [同意管理](https://docs.tealium.com/about-consent-management/) 
  * [クライアント側バージョン](https://docs.tealium.com/client-side-versions/) 
* 接続 
  * [データサプライチェーン](https://docs.tealium.com/data-supply-chain-dashboard/) 
  * [データソース](https://docs.tealium.com/about-data-sources/) 
  * [コネクター](https://docs.tealium.com/about-connectors/) 
  * イベントコネクター 
  * オーディエンスコネクター 
  * マーケットプレイス 
  * [Data Connect](https://docs.tealium.com/about-data-connect/) 
    * [統合](https://docs.tealium.com/about-data-connect-integrations/) 
    * [ダッシュボード](https://docs.tealium.com/data-connect-dashboard/) 
* ガバナンス 
  * [同意オーケストレーション](https://docs.tealium.com/about-consent-orchestration/) 
  * [訪問検索](https://docs.tealium.com/visitor-search/) 
* 変換 
  * [イベント属性](https://docs.tealium.com/about-attributes/) 
  * [訪問／訪問属性](https://docs.tealium.com/about-attributes/) 
  * [ルール](https://docs.tealium.com/rule-condition-definitions/) 
  * [関数](https://docs.tealium.com/about-functions/) 
  * [Predict](https://docs.tealium.com/about-predict/) 
* アクティベート 
  * [オーディエンス](https://docs.tealium.com/about-audiences/) 
  * オーディエンスジョブ 
  * [Discover](https://docs.tealium.com/audience-discovery/) 
  * [Context API](https://docs.tealium.com/about-context-api/) 
* 検証 
  * [トレース](https://docs.tealium.com/about-trace/) 
  * [ライブイベント](https://docs.tealium.com/about-live-events/) 
  * [ライブ訪問](https://docs.tealium.com/visitor-profile-sampler/) 
  * [イベント仕様](https://docs.tealium.com/about-event-specifications/) 
* 保存 
  * [EventStore](https://docs.tealium.com/audiencestore-and-eventstore/) 
  * [AudienceStore](https://docs.tealium.com/audiencestore-and-eventstore/) 
  * [EventDB / AudienceDB](https://docs.tealium.com/audiencedb-and-eventdb/) 
  * [EventStore Legacy](https://docs.tealium.com/audiencedb-and-eventdb/) 
* 分析 
  * [使用状況](https://docs.tealium.com/understanding-the-usage-report/) 
  * [オーディエンスダッシュボード](https://docs.tealium.com/cdp-dashboard/) 
  * [インサイト](https://docs.tealium.com/about-data-insights/)
    * [ダッシュボード](https://docs.tealium.com/manage-dashboards/) 
    * [テンプレート](https://docs.tealium.com/data-insights-templates/) 
    * [QuickSightユーザー](https://docs.tealium.com/about-data-insights/)

## 機能の対応関係

従来のナビゲーションにあった機能が、新しいナビゲーションのどこに配置されているかを確認するには、この表を使用してください。

### タグ管理

| 以前の場所 | 新しい場所 |
| ------------ | ------------ |
| タグ管理 > ダッシュボード | タグ管理 > ダッシュボード |
| タグ管理 > データレイヤー | タグ管理 > データレイヤー |
| タグ管理 > 読み込みルール | タグ管理 > 読み込みルール |
| タグ管理 > イベント | タグ管理 > イベント |
| タグ管理 > タグ | タグ管理 > タグ |
| タグ管理 > 拡張機能 | タグ管理 > 拡張機能 |
| タグ管理 > 同意統合 | タグ管理 > 同意統合 |
| タグ管理 > クライアント側ツール > ブラウザーツール | クライアント側ツール > ブラウザーツール |
| タグ管理 > クライアント側ツール > タグレポート | クライアント側ツール > タグレポート |
| タグ管理 > クライアント側ツール > 同意管理 | クライアント側ツール > 同意管理 |
| タグ管理 > クライアント側ツール > クライアント側バージョン | クライアント側バージョン |

### データサプライチェーン

| 以前の場所 | 新しい場所 |
| ------------ | ------------ |
| データサプライチェーン > 概要 | 接続 > データサプライチェーン |
| データサプライチェーン > 使用状況レポート | 分析 > 使用状況 |

### ソース

| 以前の場所 | 新しい場所 |
| ------------ | ------------ |
| ソース > データソース | 接続 > データソース |

### イベントストリーミング

| 以前の場所 | 新しい場所 |
| ------------ | ------------ |
| イベントストリーミング > ライブイベント | 検証 > ライブイベント |
| イベントストリーミング > イベント仕様 | 検証 > イベント仕様 |
| イベントストリーミング > イベント属性 | 変換 > イベント属性 |

### カスタマーデータプラットフォーム（CDP）

| 以前の場所 | 新しい場所 |
| ------------ | ------------ |
| CDP > ダッシュボード | 分析 > オーディエンスダッシュボード |
| CDP > Discover | アクティベート > Discover |
| CDP > 訪問／訪問属性 | 変換 > 訪問／訪問属性 |
| CDP > オーディエンス | アクティベート > オーディエンス |
| CDP > オーディエンスジョブ | アクティベート > オーディエンスジョブ |
| CDP > Context API（旧称Moments API） | アクティベート > Context API |

### コネクター

| 以前の場所 | 新しい場所 |
| ------------ | ------------ |
| コネクター > 概要 | 接続 > コネクター |
| コネクター > マーケットプレイス | 接続 > マーケットプレイス |

### DataAccess

| 以前の場所 | 新しい場所 |
| ------------ | ------------ |
| DataAccess > EventStore | 保存 > EventStore |
| DataAccess > AudienceStore | 保存 > AudienceStore |
| DataAccess > EventDB / AudienceDB | 保存 > EventDB / AudienceDB |

### インサイト

| 以前の場所 | 新しい場所 |
| ------------ | ------------ |
| インサイト > ダッシュボード | 分析 > インサイト > ダッシュボード |
| インサイト > ユーザーを管理 | 分析 > インサイト > QuickSightユーザー |
| インサイト > テンプレート | 分析 > インサイト > テンプレート |
### Data Connect

| 以前の場所 | 新しい場所 |
| ------------ | ------------ |
| Data Connect > Integrations | Connect > Data Connect > Integrations |
| Data Connect > Dashboard | Connect > Data Connect > Dashboard |

### Predict

| 以前の場所 | 新しい場所 |
| ------------ | ------------ |
| Predict | Transform > Predict |

### Functions

| 以前の場所 | 新しい場所 |
| ------------ | ------------ |
| Functions > Overview | Transform > Functions |

### Consent Orchestration

| 以前の場所 | 新しい場所 |
| ------------ | ------------ |
| Consent Orchestration | Govern > Consent Orchestration |

### Trace

| 以前の場所 | 新しい場所 |
| ------------ | ------------ |
| Trace | Validate > Trace |

### サーバーサイドツール

| 以前の場所 | 新しい場所 |
| ------------ | ------------ |
| Server-Side Tools > Visitor Profile Sampler | Validate > Live Visitors |
| Server-Side Tools > Manage Rules | Transform > Rules |
| Server-Side Tools > Visitor Lookup | Govern > Visitor Search |

### サーバーサイドバージョン

| 以前の場所 | 新しい場所 |
| ------------ | ------------ |
| Server-Side Versions | Server-Side Versions |