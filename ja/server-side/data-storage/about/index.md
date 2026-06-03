---
title: DataAccessについて
description: この記事ではTealium DataAccessの機能と異なるデータ形式について説明します。
url: https://docs.tealium.com/ja/server-side/data-storage/about/
---
DataAccessをアカウントとプロファイルで有効にするには、アカウントマネージャーに連絡してください。

## 前提条件

DataAccessを使用するには、ユーザーはデータウェアハウス管理者の役割が割り当てられている必要があります。詳細については、[サーバーサイドアカウント構成]()を参照してください。

## 動作原理

Tealium DataAccessは、[Tealium iQタグ管理](/ja/iq-tag-management/)、[Tealium AudienceStream CDP]()、および[Tealium EventStream API Hub]()の機能を拡張し、ウェブやモバイルのタッチポイント、オンラインおよびオフラインチャネル、リアルタイムオーディエンスから収集されたデータの長期保存を提供するエンタープライズデータハブソリューションです。

DataAccessはEventStreamフィードと連携してイベントデータを保存し、AudienceStreamオーディエンスと連携して訪問プロファイルデータを保存します。

DataAccessは以下の製品で構成されています：
* [Tealium EventStore]()
* [Tealium AudienceStore]()
* [Tealium EventDB]()
* [Tealium AudienceDB]()

### データ形式

Amazon RedshiftおよびAmazon S3のエンタープライズクラスのソリューションに基づいて構築されたDataAccessは、構造化データと半構造化データの2つの形式での保存を提供します。

#### 構造化データ

構造化データはAmazon Redshift Spectrumに保存されます。データは固定フィールドを持ち、高度に組織化されているため、アップロード、抽出、ロード、保存、クエリ、およびデータ分析が容易です。構造化データは、サードパーティのビジネスインテリジェンスツールを使用してアクセスできます。

構造化データは以下の製品で使用されます：

* [Tealium EventDB]()
* [Tealium AudienceDB]()

#### 半構造化データ

半構造化データは原始形式でAmazon S3に保存されます。データはインターフェースから直接JSONファイルとしてダウンロードできます。半構造化データには組織が欠けているため、構造を実現するのが難しいです。データを使用するには、Hadoopなどのシステムにデータを抽出、変換、ロード（ETL）する必要があります。

半構造化データは以下の製品で使用されます：

* [Tealium EventStore]()
* [Tealium AudienceStore]()

## 製品機能

|提供名| データ保存| データ抽出| データクエリ| データ分析| データ可視化|
|:-:| :-:| :-:| :-:| :-:| :-:|
|EventStore| ✔| ✔| | ✔| |
|EventDB| ✔| ✔| ✔| ✔| ✔|
|AudienceStore| ✔| ✔| | ✔| |
|AudienceDB| ✔| ✔| ✔| ✔| ✔|
|EventDirect| | ✔| | | |
|Webhook (Event/Audience)| | ✔| | | |

## 製品説明

|提供名| 説明| 構造タイプ| 使用技術|
|---| ---| ---| ---|
|EventStore|  &lt;ul&gt;&lt;li&gt;EventStoreは、ウェブ、モバイル、IoT、オフラインチャネルからの生のイベントデータを収集します。&lt;/li&gt;&lt;li&gt;データは[JavaScript Object Notation (JSON)](http://www.json.org/)の半構造化データ形式でAmazon Simple Storage Service S3バケットに保存されます。&lt;/li&gt;&lt;/ul&gt; | 半構造化| Amazon S3|
|EventDB|  &lt;ul&gt;&lt;li&gt;EventDBはEventStoreの機能を拡張し、生のイベントデータを構造化されたAmazon Redshiftデータベースインスタンスに整理します。&lt;/li&gt;&lt;li&gt;このデータには、Postgres対応プラットフォームからアクセスでき、ユーザーはデータベースに直接SQLを実行できます。&lt;/li&gt;&lt;li&gt;構造化データは、SplunkやTableauなどのビジネスインテリジェンス（BI）ツールやデータ可視化ツールによって使用できます。&lt;/li&gt;&lt;/ul&gt; | 構造化| Amazon Redshift Spectrum|
|EventDirect|  &lt;ul&gt;&lt;li&gt;EventDirectは、次のようなイベントデータをお客様の選択したエンタープライズデータウェアハウス（EDW）に直接送信します：&lt;ul&gt;&lt;li&gt;メタデータ&lt;/li&gt;&lt;li&gt;クエリ文字列パラメータ&lt;/li&gt;&lt;li&gt;ウェブクッキーデータ&lt;/li&gt;&lt;li&gt;コンテンツ内イベント&lt;/li&gt;&lt;li&gt;JavaScript変数&lt;/li&gt;&lt;li&gt;マーケティングソース&lt;/li&gt;&lt;li&gt;URLパラメータ&lt;/li&gt;&lt;li&gt;データ操作 / Tealium iQ拡張データ - プライバシー、ルックアップテーブル、帰属)&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; &lt;ul&gt;&lt;li&gt;データはHTTP POST形式で送信されます。&lt;/li&gt;&lt;/ul&gt; | お客様の選択| お客様のホスト|
|AudienceStore|  &lt;ul&gt;&lt;li&gt;AudienceStoreは、AudienceStreamから収集されたオーディエンスデータと属性の生の保存を提供します。&lt;/li&gt;&lt;li&gt;EventStoreと同様に、データはAmazon S3インスタンス上の半構造化形式で保存されます。&lt;/li&gt;&lt;li&gt;[JavaScript Object Notation (JSON)](http://www.json.org/)またはカンマ区切り値(.csv)がこのファイルの作成に使用されます。&lt;/li&gt;&lt;li&gt;データはAmazon S3バケットを通じてダウンロード可能です。&lt;/li&gt;&lt;/ul&gt; | 半構造化| Amazon S3|
|AudienceDB|  &lt;ul&gt;&lt;li&gt;AudienceDBはAudienceStoreの機能を拡張し、AudienceStreamから収集されたオーディエンスデータと属性を構造化形式で保存します。&lt;/li&gt;&lt;li&gt;このデータには、Postgres対応プラットフォームからアクセスでき、ユーザーはデータベースに直接SQLを実行できます。&lt;/li&gt;&lt;li&gt;構造化データは、後日BIツール（例：Splunk）やデータ可視化ツール（例：Tableau）による歴史分析や可視化に利用できます。&lt;/li&gt;&lt;/ul&gt; | 構造化| Amazon Redshift|
|Webhook (Event/Audience)|  &lt;ul&gt;&lt;li&gt;Webhook (Event/Audience)は、オーディエンスデータ（属性/プロファイル、バッジ、オムニチャネル/オフラインデータ）をお客様の選択したEDWに直接送信します。&lt;/li&gt;&lt;/ul&gt; | お客様の選択| お客様のホスト|

DataAccess製品は有効になっている間のみデータを収集します。

## ロギング

DataAccessへのすべてのクエリはログに記録され、「DataAccessクエリ履歴」データセットに保存されます。

このデータセットは、すべてのDataAccess顧客に対して読み取り専用モードで利用可能です。次の方法でアクセスできます：

* **DataAccessテーブル**：認証資格情報が必要です。詳細については、を参照してください。
* **インサイトダッシュボード**：**Insights &gt; Dashboards &gt; Analyses**の下で利用可能です。詳細については、を参照してください。

クエリ履歴データセットを使用して、次のことができます：

* 不正アクセスや通常と異なるクエリパターンを特定し、セキュリティ脅威を示す可能性があります。
* 規制要件をサポートするためにユーザーアクティビティの監査証跡を維持します。
* DataAccessのパフォーマンスに影響を与える可能性のある非効率的なクエリを検出します。

![](/images/server-side/data-access/data-access-queries-history.png)
