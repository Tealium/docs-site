---
title: DealerTrack Data Connect連携構成ガイド
description: この記事では、Tealium Data ConnectとDealerTrackの連携を構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-connect/manage-data-connect-integrations/dealertrack/
---
DealerTrackとTealium Data Connectを連携すると、次のデータをインポートできます。

* 商談履歴
* サービス予約
* 未完了の修理オーダー
* 完了済みの修理オーダー

## 要件

* Event StreamingまたはCustomer Data Platform（CDP）
* Tealium Data Connect
* Tealium DataAccess（EventStoreまたはEventDB用）
* OpenTrackへのアクセス権

## DealerTrack連携の作成

次の手順で、Tealium Data ConnectとDealerTrackの連携を作成します。

1. Tealium Connectデータソースを構成します。
1. DealerTrack APIへの接続を確立します。
1. DealerTrackからTealiumへデータを送信するレシピを作成します。
1. Tealiumへイベントを送信します。
1. データ用のイベントフィードを構成します。
1. Traceでテストし、レシピを有効化します。

## ステップ1：Tealium Connectデータソースの構成

Tealium Connectデータソースを構成します。詳細については、[Tealium Connectデータソースの構成](https://docs.tealium.com/tealium-connect-data-source/)を参照してください。

## ステップ2：DealerTrack APIへの接続の確立

DealerTrack APIへの接続を確立するには、次の手順を実行します。

1. **Connect > Data Connect > Integrations**に移動します。
1. **Connections**をクリックし、**Create**をクリックします。
1. **DealerTrack**接続を選択します。
1. **Base URL**に`https://ot.dms.dealertrack.com`と入力します。
1. **Username**と**Password**を入力します。
1. **Connect**をクリックします。

 ![](https://docs.tealium.com/images/server-side/data-connect/dealertrack-data-connect-integration-establish-connection1.png)

 ![](https://docs.tealium.com/images/server-side/data-connect/dealertrack-data-connect-integration-establish-connection2.png)

## ステップ3：DealerTrackからTealiumへデータを送信するレシピの作成

DealerTrackからTealiumへデータを送信するレシピを作成するには、次の手順を実行します。

新しいレシピの作成方法について詳しくは、[Data Connectでのレシピの作成](https://docs.tealium.com/create-recipe-data-connect/)を参照してください。

1. **Connect > Data Connect > Integrations**に移動します。
1. **Integrations**画面で、**Create > Recipe**をクリックします。
1. Scheduleアプリからトリガーされる新しいレシピを作成します。アプリからトリガーされるレシピの作成方法については、[Data Connectでのレシピの作成](https://docs.tealium.com/create-recipe-data-connect/)を参照してください。

DealerTrackから取得できるデータの詳細については、以下の[アクション](#actions)セクションを参照してください。

## ステップ4：Tealiumへのイベントの送信

Tealiumへイベントを送信するには、次の手順を実行します。

1. **Send Events in Tealium Events V2**に移動します。
1. Tealiumへ送信するデータを構成します。

 ![](https://docs.tealium.com/images/server-side/data-connect/dealertrack-data-connect-integration-send-events.png)

詳細については、[レシピの作成：アクションの構成](https://docs.tealium.com/create-recipe-data-connect/#step-2-configure-an-action)を参照してください。

## ステップ5：リード用イベントフィードの構成

 ![](https://docs.tealium.com/images/server-side/data-connect/dealertrack-data-connect-integration-event-feed.png)

次の手順でイベントフィードを作成します。

1. **Validate > Live Events**に移動し、**+ Add Event Feed**をクリックします。
1. **Create Event Feed**ダイアログで、**Title**と必要に応じて**Notes**を入力します。
    * イベントフィードのタイトルは、リードイベントがData Connectに取り込まれる方法に応じて決まります。
1. （任意）**Add Label**をクリックし、このイベントフィードに適用するラベルを選択します。
1. **Event Data Storage**で、EventStoreまたはEventDB用のフィードを有効にします。
1. 新しいリードイベントに一致するイベントを取得できるように、フィードの**Attribute Condition**を構成します。
1. **Save**をクリックします。
1. プロファイルを保存してパブリッシュします。

## ステップ6：Traceでのテストとレシピの有効化

レシピを有効化する前に、十分なテストを実施してください。テストが正常に完了したら、レシピを有効化して自動データ連携プロセスを開始します。

次の手順でTraceによるテストを行い、レシピを有効化します。

1. **Trace**に移動します。
1. **New Trace**で**Start**をクリックします。Trace IDが記載されたダイアログが表示されます。
1. Trace IDをコピーし、**Continue**をクリックします。
1. **Connect > Data Connect > Integrations**に移動します。
1. **Integrations**画面で、DealerTrackからTealiumへ新しいリードを送信するレシピについて、次の手順を実行します。
    1. レシピを選択します。
    1. **Tealium events V2 action**を選択して編集します。
    1. **Attributes to add**で、`tealium_trace_id`キーを追加し、**Value**にTrace IDを貼り付けます。
    1. **Save**をクリックします。
    1. **Start recipe**リストで、**Test recipe**をクリックします。
1. **Trace**インターフェイスに戻り、ログの詳細を確認します。
1. テストが完了したら、**Stop test**をクリックします。
1. レシピを有効化するには、**Start recipe**をクリックします。

## アクション

この連携では、次のアクションを追跡できます。

### 生成日による商談の検索

| パラメータ | 説明 |
| --------- | ----------- |
| Company Number | 会社番号。例：`ZE7`。 |
| Enterprise Code | エンタープライズコード。例：`ZE`。 |
| Server Name | サーバー名。例：`arkonap.arkona.com`。 |
| Origination Date Start | 自動車商談の日付。この日付から検索を開始します。形式は`YYYY-MM-DD`です。 |
| Origination Date End | 自動車商談の日付。この日付で検索を終了します。形式は`YYYY-MM-DD`です。 |
| Deal Status | 商談のステータス。空白または未送信の場合は、すべての商談ステータスを取得します。指定可能なパラメータは、`Accepted`、`Capped`、`Closed`、`Unaccepted`、または空白です。 |

### 予約の検索

| パラメータ | 説明 |
| --------- | ----------- |
| Company Number | 会社番号。例：`ZE7`。 |
| Enterprise Code | エンタープライズコード。例：`ZE`。 |
| Server Name | サーバー名。例：`arkonap.arkona.com`。 |
| Date From | 予約検索の開始日。予約が作成された日ではなく、実際の予約日です。形式は`YYYY-MM-DD`です。 |
| Date To | 予約検索の終了日。予約が作成された日ではなく、実際の予約日です。形式は`YYYY-MM-DD`です。 |
| Created Date Time Start | 予約が作成された日時の検索を開始する日時。形式は`yyyy-mm-ddThh:mm:ssZ.`です。 |
| Created Date Time End | 予約が作成された日時の検索を終了する日時。形式は`yyyy-mm-ddThh:mm:ssZ`です。 |

### 未完了の修理オーダーの検索

| パラメータ | 説明 |
| --------- | ----------- |
| Company Number | 会社番号。例：`ZE7`。 |
| Enterprise Code | エンタープライズコード。例：`ZE`。 |
| Server Name | サーバー名。例：`arkonap.arkona.com`。 |
| Created Date Time Start | 未完了の修理オーダーが作成された日時の検索を開始する日時。形式は`yyyy-mm-ddThh:mm:ssZ`です。 |
| Created Date Time End | 未完了の修理オーダーが作成された日時の検索を終了する日時。形式は`yyyy-mm-ddThh:mm:ssZ`です。 |

### 完了済みの修理オーダーの取得

| パラメータ | 説明 |
| --------- | ----------- |
| Company Number | 会社番号。例：`ZE7`。 |
| Enterprise Code | エンタープライズコード。例：`ZE`。 |
| Server Name | サーバー名。例：`arkonap.arkona.com`。 |
| Final Close Date Start | 最終的に完了した修理オーダーの検索を開始する日時。形式は`yyyy-mm-ddThh:mm:ssZ`です。 |
| Final Close Date End | 最終的に完了した修理オーダーの検索を終了する日時。形式は`yyyy-mm-ddThh:mm:ssZ`です。 |