---
title: 利用レポートの理解
description: この記事では、利用レポートとそのアクセス方法について説明します。
url: https://docs.tealium.com/ja/server-side/administration/understanding-the-usage-report/
---
## 仕組み

利用レポートは、アカウントやプロファイルに関連するデータの量と操作の数を示します。これらのレポートを使用して、データサプライチェーンの各ポイントを通じて流れるデータの量を分析し、各機能の請求コストを見積もります。

レポートは、アカウント内のすべてのプロファイルまたは特定のプロファイルに対して利用可能です。レポートデータは特定の日付範囲に調整することができます。

## 請求の見積もり

Tealium EventStream、Tealium EventDB、Tealium EventStore、およびEDFとCDHバンドルを持つ顧客の利用コストは、[**Total Inbound Events**](#data-collection-reports)レポートに基づいて計算されます。このレポートは、アカウントに流れ込むイベントの総量を表しています。

Tealium AudienceStream、Tealium AudienceDB、Tealium AudienceStore、およびTealium Predictの利用コストは、**AudienceStream Filtered Events**レポートに基づいて計算されます。

すべてのイベントは、Tealium Customer Data Hubに入る時点で総量にカウントされ、等しく課金されます。

利用レポートは請求や価格情報を提供しません。最終的な利用コストは、イベントの量、契約条件、および実装構成の組み合わせによって決定されます。請求と価格に関するすべての問い合わせは、アカウントマネージャーにお問い合わせください。

## グラフ形式

レポートは折れ線グラフとして表示されます。日付範囲は水平軸にプロットされ、メトリックは垂直軸にプロットされ、ドットでマークされます。ドットの上にマウスを置くと、集計されたメトリックの値とそれが集計された日が表示されます。

![](/images/server-side/whiteui-data-access-usage-reports-click-dot-to-display-metrics.jpg)

## 利用可能なレポート

以下のリストは、利用可能なレポートタイプを説明しています。

* **すべての利用レポート**  
レポートダッシュボードですべてのレポートを順番に表示します。これがデフォルトのビューです。

### コネクタレポート

コネクタレポートは、コネクタによるイベントの利用状況に対応し、以下のレポートを返します：

* **Total Connector Calls**  
EventStreamとAudienceStreamのコネクタアクションをトリガーするために行われたサーバーリクエストの合計数。
* **Connector Calls - EventStream**  
EventStreamコネクタアクションによって行われたサーバーリクエストの数。EventStreamと契約したコネクタ呼び出しの数は、このレポートに基づいています。
* **Connector Calls - AudienceStream**  
AudienceStreamコネクタアクションによって行われたサーバーリクエストの数。

### DataAccessレポート

DataAccessレポートは、AudienceStore、EventStore、AudienceDB、およびEventDBに格納されたレコードの数を示します：

* **Total DataAccess Records Inserted**  
すべてのDataAccess製品に格納されたイベントと訪問のレコードの数。
* **Total EventDB Events Inserted**  
EventDBに挿入されたイベントレコードの数。
* **Total EventStore Events Inserted**  
EventStoreに格納されたイベントレコードの数。
* **Total AudienceDB Visitors Inserted**  
AudienceDBに挿入された訪問レコードの数。
* **Total AudienceStore visitors Inserted**  
AudienceStoreに格納された訪問レコードの数。

### データ収集レポート

データ収集レポートは、リアルタイムおよびオフラインのイベントがCustomer Data Hubプロファイルに流れ込むことに対応し、以下のレポートを返します：

* **Total Inbound Events**  
リアルタイムイベントとファイルインポートイベントの合計。EventStreamのデータ使用コストは、**Total Inbound Events**レポートに基づいて計算されます。
* **Total Real-time Events**  
指定された日付範囲内であなたのウェブサイトまたはモバイルアプリから[Tealium Collect]()タグによってキャプチャされたイベントの数。詳細については、[Live Events and Feeds]()を参照してください。
* **Total File Import Events**  
AudienceStreamにインポートされた[file import]()の行またはラインの数。
* **Total Omnichannel Events**  
レガシーのOmnichannel機能のユーザー向け。AudienceStreamにインポートされたOmnichannelの行またはラインの数。
* **Total AudienceStream Events**  
AudienceStreamが受け取ったイベントの総数。AudienceStreamイベントフィルタが有効になっている場合、このレポートにはフィルタリングされたAudienceStreamイベントのみが含まれます。
* **Real-time AudienceStream Events**  
AudienceStreamが受け取ったリアルタイムイベントの数。このグラフにはOmnichannel、File Import、またはData Connectイベントは含まれません。AudienceStreamイベントフィルタが有効になっている場合、このレポートにはフィルタリングされたAudienceStreamイベントのみが含まれます。
* **Bulk AudienceStream Events**  
AudienceStreamが受け取ったオフラインおよびバルクイベントの数。このグラフにはOmnichannelおよびFile Importイベントが含まれます。AudienceStreamイベントフィルタが有効になっている場合、このレポートにはフィルタリングされたAudienceStreamイベントのみが含まれます。

#### Total Real-time Events vs. Total AudienceStream Events

リアルタイムイベントの数とAudienceStreamイベントの数が一致しない場合があります。これは以下の予想される理由によるものです：

* **フィルタリングされたイベント**  
[AudienceStreamイベントフィルタ]()が構成されている場合、フィルタに一致するイベントのみが処理されます。
* **同意**  
同意が使用されている場合、訪問がCDP同意カテゴリにオプトインしない限り、AudienceStreamはイベントを処理しません。詳細については、を参照してください。
* **データサイズ制限を超える**  
プラットフォームの安定性を確保するため、指定されたサイズ制限を超えるイベントまたは訪問データは処理されない場合があります。これらの措置は、すべての顧客に最適なパフォーマンスを維持するために、システムの過負荷を防ぐためのものです。詳細については、を参照してください。

AudienceStreamのデータ使用コストは、**Total AudienceStream Events**レポートに基づいて計算されます。

### Data Connectレポート

* **Total DataConnect Records**  
格納されたレコードの数。
* **Total DataConnect Kb**  
すべてのレコードの保存サイズ（キロバイト単位）。
* **Total DataConnect Workato Tasks**  
実行されたWorkatoタスクの数。

### Data Layer Enrichmentレポート

Data Layer Enrichmentレポートは、[AudienceStream Data Layer Enrichment]()サービスに対応します。このレポートは、Tealium Collectタグが最新の訪問プロファイルを取得するためにAudienceStreamデータレイヤーにリクエストを行った回数を返します。

### Functionsレポート

[Functions]()レポートは、トリガーされた関数の数と関数タイプごとの関数の合計実行時間を示します。

* **Total Invocations Custom Actions**  
トリガーされたイベントと訪問関数の総数。
* **Total Invocations Transformations**  
トリガーされたデータ変換関数の総数。
* **Total Execution Time Custom Actions, hours**  
すべてのイベントと訪問関数の合計実行時間。
* **Total Execution Time Transformations, hours**  
すべてのデータ変換関数の合計実行時間。

### Insightsレポート

* **Insights Spice**  
使用中のSPICEメモリ容量（メガバイト単位）。
* **Insights Authors**  
Insightsアカウントに割り当てられた著者ロールの数。
* **Insight Readers**  
Insightsアカウントに割り当てられたリーダーロールの数。

### Predict Enrichments

Predict enrichmentsレポートは、デプロイされたモデルが関連する属性に予測出力値を構成する回数を示します。

### View-Through Trackingレポート

* **Total View-Through Tracking Writes**  
view-through trackingサービスによって実行された書き込みの数。
* **Total View-Through Tracking Reads**  
view-through trackingサービスによって実行された読み取りの数。

詳細については、を参照してください。

## レポートの表示
利用レポートを表示するには、**Data Supply Chain &gt; Usage Reports**に移動します。デフォルトの表示はすべてのプロファイルとすべての製品機能に対してです。

![](/images/server-side/usage-reports.png)

特定のプロファイル、機能、または日付範囲のレポートを表示するには：

1. ドロップダウンリストからプロファイルと機能タイプを選択します。    
      ![](/images/server-side/usage-reports-report-selector.png)
1. レポートの日付範囲を調整するために開始日または終了日をクリックします。  
デフォルトの日付範囲は現在の年の1月1日から現在の日付までに構成されています。デフォルトを変更するには、アカウント管理者に連絡してください。
1. **Get Report**をクリックします。

## FAQ

**なぜ私のレポートに今日のデータが表示されないのですか？**

利用レポートは完全に処理し更新するのに最大48時間かかることがあります。日付範囲が過去24-48時間だけである場合、レポートにデータが表示されない場合があります。現在の日付より3日以上前の開始日を選択してください。

**なぜ2016年4月1日以前の日付を選択できないのですか？**

利用レポートは、リリース時から最大1年間のデータを提供します。この方法は、ほとんどのアカウントが年間請求サイクルを評価するために必要なデータを提供します。