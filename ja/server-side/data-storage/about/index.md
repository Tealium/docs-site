---
title: DataAccess について
description: この記事では、Tealium DataAccess、その機能、およびさまざまなデータ形式について説明します。
url: https://docs.tealium.com/ja/server-side/data-storage/about/
---

<blockquote>
アカウントとプロファイルで DataAccess を有効にするには、アカウントマネージャーにお問い合わせください。
</blockquote>


## 前提条件

DataAccess を使用するには、ユーザーに Data Warehouse Admin ロールが割り当てられている必要があります。詳細については、[サーバーサイドのアカウント構成]()を参照してください。

## 仕組み

Tealium DataAccess は、Web およびモバイルのタッチポイント、オンラインおよびオフラインチャネル、リアルタイムオーディエンスから収集されたデータを長期保存することで、[タグ管理](https://docs.tealium.com/ja/tag-management/)、[顧客データプラットフォーム（CDP）](https://docs.tealium.com/server-side/getting-started/tutorials/visitor-profile-management/introduction/)、および[イベントストリーミング API ハブ](https://docs.tealium.com/server-side/getting-started/tutorials/event-data-activation/introduction/)の機能を拡張する、エンタープライズデータハブソリューションです。

DataAccess は、イベントストリーミングフィードと連携してイベントデータを保存し、顧客データプラットフォーム（CDP）のオーディエンスと連携して訪問プロファイルデータを保存します。

DataAccess は、以下の製品で構成されています。

* [Tealium EventStore]()
* [Tealium AudienceStore]()
* [Tealium EventDB]()
* [Tealium AudienceDB]()

### データ形式

エンタープライズクラスのソリューションである Amazon Redshift と Amazon S3 を基盤とする DataAccess は、構造化データと半構造化データの 2 つの保存形式を提供します。

#### 構造化データ

構造化データは Amazon Redshift に保存されます。このデータには固定フィールドがあり、高度に整理されているため、データのアップロード、抽出、読み込み、保存、クエリ、分析を容易に行えます。構造化データには、サードパーティーのビジネスインテリジェンスツールを使用してアクセスできます。

構造化データは、以下の製品で使用されます。

* [Tealium EventDB]()
* [Tealium AudienceDB]()

#### 半構造化データ

半構造化データは、Amazon S3 に保存される未加工の形式です。データは、インターフェイスから JSON ファイルとして直接ダウンロードできます。半構造化データは整理されていないため、構造化がより困難です。データを使用するには、Hadoop などのシステムへの抽出、変換、読み込み（ETL）が必要です。

半構造化データは、以下の製品で使用されます。

* [Tealium EventStore]()
* [Tealium AudienceStore]()

## 製品機能

|製品名|データの保存|データの抽出|データのクエリ|データの分析|データの可視化|
|:-:| :-:| :-:| :-:| :-:| :-:|
|EventStore| ✔| ✔| | ✔| |
|EventDB| ✔| ✔| ✔| ✔| ✔|
|AudienceStore| ✔| ✔| | ✔| |
|AudienceDB| ✔| ✔| ✔| ✔| ✔|
|EventDirect| | ✔| | | |
|Webhook（イベント／オーディエンス）| | ✔| | | |

## 製品の説明

|製品名|説明|構造タイプ|使用テクノロジー|
|---| ---| ---| ---|
|EventStore|  <ul><li>EventStore は、Web、モバイル、モノのインターネット（IoT）、およびオフラインチャネルから未加工のイベントデータを収集します。</li><li>データは、Amazon Simple Storage Service（S3）バケット上に、[JavaScript Object Notation（JSON）](http://www.json.org/)による半構造化データ形式で保存されます。</li></ul> | 半構造化| Amazon S3|
|EventDB|  <ul><li>EventDB は、未加工のイベントデータを構造化された Amazon Redshift データベースインスタンスに整理することで、EventStore の機能を拡張します。</li><li>Postgres 対応のプラットフォームからこのデータにアクセスでき、ユーザーはデータベースに対して SQL を直接実行できます。</li><li>構造化データは、ビジネスインテリジェンス（BI）ツールおよびデータ可視化ツールで使用できます。</li></ul> | 構造化| Amazon Redshift|
|EventDirect|  <ul><li>EventDirect は、以下のようなイベントデータを、選択したエンタープライズデータウェアハウス（EDW）に直接送信します。<ul><li>メタデータ</li><li>クエリ文字列パラメータ</li><li>Web Cookie データ</li><li>コンテンツ内イベント</li><li>JavaScript 変数</li><li>マーケティングソース</li><li>URL パラメータ</li><li>データ操作／タグ管理拡張機能のデータ（プライバシー、ルックアップテーブル、アトリビューション）</li></ul> </li></ul> <ul><li>データは HTTP POST 形式で送信されます。</li></ul> | 顧客による選択| 顧客のホスト|
|AudienceStore|  <ul><li>AudienceStore は、CDP から収集されたオーディエンスデータと属性を未加工のまま保存します。</li><li>EventStore と同様に、データは Amazon S3 インスタンス上に半構造化形式で保存されます。</li><li>このファイルの作成には、[JavaScript Object Notation（JSON）](http://www.json.org/)またはカンマ区切り値（.csv）が使用されます。</li><li>データは、Amazon S3 バケットを通じてダウンロードできます。</li></ul> | 半構造化| Amazon S3|
|AudienceDB|  <ul><li>EventDB と同様に、AudienceDB は AudienceStore の機能を拡張し、CDP から収集されたオーディエンスデータと属性を構造化形式で保存します。</li><li>Postgres 対応のプラットフォームからこのデータにアクセスでき、ユーザーはデータベースに対して SQL を直接実行できます。</li><li>構造化データは、後からビジネスインテリジェンス（BI）ツールやデータ可視化ツールで利用し、履歴分析や可視化に使用できます。</li></ul> | 構造化| Amazon Redshift|
|Webhook（イベント／オーディエンス）|  <ul><li>Webhook（イベント／オーディエンス）は、オーディエンスデータ（属性／プロファイル、バッジ、オムニチャネル／オフラインデータ）を、選択した EDW に直接送信します。</li></ul> | 顧客による選択| 顧客のホスト|


<blockquote>
DataAccess 製品は、有効になっている間のみデータを収集します。
</blockquote>


## ロギング

DataAccess に対するすべてのクエリはログに記録され、**DataAccess クエリ履歴**データセットに保存されます。

このデータセットは、すべての DataAccess ユーザーが読み取り専用モードで利用できます。以下の方法でアクセスできます。

* **DataAccess テーブル**：認証資格情報が必要です。詳細については、[connect-to-databases](https://docs.tealium.com/connect-to-databases/)を参照してください。  
* **Insights ダッシュボード**：**Analyze > Insights > Dashboards > Analyses** から利用できます。詳細については、[manage-analyses](https://docs.tealium.com/manage-analyses/)を参照してください。

クエリ履歴データセットは、以下の目的で使用できます。

* セキュリティ上の脅威を示す可能性のある、不正アクセスや通常とは異なるクエリパターンを特定する。
* 規制要件への対応を支援するため、ユーザーアクティビティの監査証跡を維持する。
* DataAccess のパフォーマンスに影響を与える可能性のある非効率なクエリを検出する。

![](https://docs.tealium.com/images/server-side/data-access/data-access-queries-history.png)