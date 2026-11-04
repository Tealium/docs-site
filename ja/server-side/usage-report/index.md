---
title: 利用状況レポートについて
description: この記事では、利用状況レポートとそのアクセス方法について説明します。
url: https://docs.tealium.com/ja/server-side/usage-report/
---
## 仕組み

利用状況レポートには、アカウントまたはプロファイルに関連付けられたデータ量と操作数が表示されます。これらのレポートを使用して、データサプライチェーンの各ポイントを流れるデータ量を分析し、各機能の請求コストを見積もることができます。

レポートは、アカウント内のすべてのプロファイル、または特定のプロファイルについて利用できます。レポートデータは、特定の日付範囲に調整できます。

## 請求額の見積もり

Tealium Event Streaming、Tealium EventDB、Tealium EventStore、およびTealium CollectとCDHのバンドルをご利用のお客様の利用コストは、[**受信イベント総数**](#data-collection-reports)レポートに基づいて計算されます。このレポートは、アカウントに流入するイベントの総量を表します。

Tealium Customer Data Platform（CDP）、Tealium AudienceDB、Tealium AudienceStore、およびTealium Predictの利用コストは、**リアルタイムCustomer Data Platformイベント総数**レポートに基づいて計算されます。

各イベントは、Tealium Customer Data Hubへの流入時点で総量にカウントされ、すべて同じ基準で課金されます。

利用状況レポートでは、可視性を確保するためにオーディエンスのフィルイベントを追跡しますが、フィルイベントは契約上のイベント量にはカウントされません。詳細については、[オーディエンスのフィル](https://docs.tealium.com/about-audiences/#fill-an-audience)を参照してください。


<blockquote>
利用状況レポートには、請求や価格に関する情報は表示されません。最終的な利用コストは、イベント量、契約条件、および実装構成の組み合わせによって決まります。請求および価格に関するお問い合わせは、アカウントマネージャーにご連絡ください。
</blockquote>


## グラフ形式

レポートは折れ線グラフとして表示されます。日付範囲は横軸に、指標は縦軸にプロットされ、点で示されます。点にカーソルを合わせると、集計された指標値と集計日が表示されます。

![](https://docs.tealium.com/images/server-side/whiteui-data-access-usage-reports-click-dot-to-display-metrics.jpg)

## 利用可能なレポート

以下に、利用可能なレポートタイプを示します。

* **すべての利用状況レポート**  
レポートダッシュボードにすべてのレポートを順番に表示します。これがデフォルトのビューです。

### コネクターレポート

コネクターレポートは、コネクターによるイベント使用量に対応し、以下のレポートを提供します。

* **コネクター呼び出し総数**  
Event StreamingおよびCustomer Data Platformのコネクターアクションをトリガーするために行われたサーバーリクエストの総数。
* **コネクター呼び出し - Event Streaming**  
Event Streamingのコネクターアクションによって行われたサーバーリクエストの数。Event Streamingで契約されるコネクター呼び出し数は、このレポートに基づきます。
* **コネクター呼び出し - Customer Data Platform**  
Customer Data Platformのコネクターアクションによって行われたサーバーリクエストの数。
* **コネクター呼び出し - Data Cloud Activation**  
Data Cloud Activationのコネクターアクションによって行われたサーバーリクエストの数。このレポートは、Data Cloud Activationを使用するアカウントでのみ利用できます。

### DataAccessレポート

DataAccessレポートには、AudienceStore、EventStore、AudienceDB、およびEventDBに保存されたレコード数が表示されます。

* **挿入されたDataAccessレコード総数**  
すべてのDataAccess製品に保存されたイベントレコードと訪問レコードの数。
* **挿入されたEventDBイベント総数**  
EventDBに挿入されたイベントレコードの数。
* **挿入されたEventStoreイベント総数**  
EventStoreに保存されたイベントレコードの数。
* **挿入されたAudienceDB訪問総数**  
AudienceDBに挿入された訪問レコードの数。
* **挿入されたAudienceStore訪問総数**  
AudienceStoreに保存された訪問レコードの数。

### データ収集レポート

データ収集レポートは、Customer Data Hubプロファイルに流入するリアルタイムイベントとオフラインイベントに対応し、以下のレポートを提供します。

* **受信イベント総数**  
リアルタイムイベントとファイルインポートイベントの合計。Event Streamingのデータ利用コストは、**受信イベント総数**レポートに基づいて計算されます。
* **リアルタイムイベント総数**  
指定した日付範囲内で、[Tealium Collect](https://docs.tealium.com/tealium-collect-tag/)タグがWebサイトまたはモバイルアプリから取得したイベントの数。詳細については、[ライブイベントとフィード](https://docs.tealium.com/about-live-events/)を参照してください。
* **ファイルインポートイベント総数**  
Customer Data Platformにインポートされた[ファイルインポート]()の行数。
* **オムニチャネルイベント総数**  
従来のオムニチャネル機能を使用しているユーザー向けです。Customer Data Platformにインポートされたオムニチャネルの行数。
* **Data Cloudイベント総数**  
Data Cloud Activationデータソースからインポートされたイベントの数。
* **Data Cloud Activation：受信したイベント（データレコード）の総数**  
Data Cloud Activationが受信したデータレコードの総数。このレポートは、Data Cloud Activationを使用するアカウントでのみ利用できます。
* **Customer Data Platformイベント総数**  
Customer Data Platformが受信したイベントの総数。AudienceStreamイベントフィルターが有効になっている場合、このレポートにはフィルター処理されたCustomer Data Platformイベントのみが含まれます。
* **リアルタイムCustomer Data Platformイベント総数**  
Customer Data Platformが受信したリアルタイムイベントの数。このグラフには、オムニチャネル、ファイルインポート、またはData Connectのイベントは含まれません。AudienceStreamイベントフィルターが有効になっている場合、このレポートにはフィルター処理されたCustomer Data Platformイベントのみが含まれます。
* **一括Customer Data Platformイベント**  
Customer Data Platformが受信したオフラインイベントと一括イベントの数。このグラフには、オムニチャネルイベントとファイルインポートイベントが含まれます。AudienceStreamイベントフィルターが有効になっている場合、このレポートにはフィルター処理されたCustomer Data Platformイベントのみが含まれます。

#### リアルタイムイベント総数とCustomer Data Platformイベント総数の比較

リアルタイムイベント数とCustomer Data Platformイベント数は、以下の想定される理由により一致しない場合があります。

* **フィルター処理されたイベント**  
[Customer Data Platformイベントフィルター](https://docs.tealium.com/server-side-account-settings/#general-settings)が構成されている場合、フィルターに一致するイベントのみが処理されます。
* **同意**  
同意機能を使用している場合、訪問がCDP同意カテゴリにオプトインしていない限り、Customer Data Platformはイベントを処理しません。詳細については、を参照してください。
* **データサイズ制限の超過**  
プラットフォームの安定性を確保するため、指定されたサイズ制限を超えるイベントデータまたは訪問データは処理されない場合があります。これらの対策によりシステムの過負荷を防ぎ、すべてのお客様に対して最適なパフォーマンスを維持します。詳細については、を参照してください。


<blockquote>
Tealiumでは、**Customer Data Platformイベント総数**レポートに基づいてCustomer Data Platformのデータ利用コストを計算します。
</blockquote>


### Data Connectレポート

* **DataConnectレコード総数**  
保存されたレコードの数。
* **DataConnectの総KB数**  
すべてのレコードの保存サイズ（キロバイト単位）。
* **DataConnect Workatoタスク総数**  
実行されたWorkatoタスクの数。

### データレイヤーエンリッチメントレポート

データレイヤーエンリッチメントレポートは、[Customer Data Platformデータレイヤーエンリッチメント]()サービスに対応します。

* **CDPデータレイヤーエンリッチメント呼び出し総数**  
訪問プロファイルを取得するために、Tealium CollectタグがCustomer Data Platformデータレイヤーにリクエストを行った回数。
### Functionsレポート

[Functions]()レポートには、トリガーされた関数の数と、関数タイプ別の合計実行時間が表示されます。

* **カスタムアクションの合計呼び出し回数**  
トリガーされたイベント関数および訪問関数の合計数。
* **変換の合計呼び出し回数**  
トリガーされたデータ変換関数の合計数。
* **カスタムアクションの合計実行時間（時間）**  
すべてのイベント関数および訪問関数の合計実行時間。
* **変換の合計実行時間（時間）**  
すべてのデータ変換関数の合計実行時間。

### Insightsレポート

* **Insights Spice**  
使用中のSPICEメモリ容量（メガバイト）。
* **Insights作成者**  
Insightsアカウントに割り当てられている作成者ロールの数。
* **Insights閲覧者**  
Insightsアカウントに割り当てられている閲覧者ロールの数。

### Predictエンリッチメント

Predictエンリッチメントレポートには、デプロイ済みモデルが関連する属性に予測出力値を構成した回数が表示されます。

### ビュースルートラッキングレポート

* **ビュースルートラッキングの合計書き込み回数**  
ビュースルートラッキングサービスが実行した書き込みの回数。
* **ビュースルートラッキングの合計読み取り回数**  
ビュースルートラッキングサービスが実行した読み取りの回数。

詳細については、[view-through-tracking-extension](https://docs.tealium.com/view-through-tracking-extension/)を参照してください。

## レポートを表示する

使用状況レポートを表示するには、**分析 > 使用状況**に移動します。デフォルトでは、すべてのプロファイルおよびすべての製品機能が表示されます。

![](https://docs.tealium.com/images/server-side/usage-reports.png)

特定のプロファイル、機能、または期間のレポートを表示するには、次の手順に従います。

1. ドロップダウンリストからプロファイルと機能タイプを選択します。    
      ![](https://docs.tealium.com/images/server-side/usage-reports-report-selector.png)
1. 開始日または終了日をクリックし、レポートの期間を調整します。  
デフォルトの期間は、当年の1月1日から現在の日付までに構成されています。デフォルトを変更するには、アカウント管理者にお問い合わせください。
1. **レポートを取得**をクリックします。

## よくある質問

**レポートに今日のデータが表示されないのはなぜですか？**

使用状況レポートの処理と更新が完了するまで、最大48時間かかることがあります。期間が直近24～48時間のみの場合、レポートにデータが表示されない可能性があります。現在の日付より3日以上前の日付を開始日として選択してください。

**2016年4月1日より前の日付を選択できないのはなぜですか？**

使用状況レポートでは、リリース時点から最大1年分のデータが提供されます。この方法により、ほとんどのアカウントで年間請求サイクルの評価に必要なデータを利用できます。