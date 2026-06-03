---
title: DealerTrack Data Connect統合セットアップガイド
description: この記事では、Tealium Data ConnectとDealerTrack間の統合を構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-connect/manage-data-connect-integrations/dealertrack/
---
Tealium Data ConnectとのDealerTrack統合により、以下のデータをインポートできます。

* 取引履歴
* サービス予約
* 未完了修理オーダー
* 完了修理オーダー

## 要件

* Tealium EventStreamまたはAudienceStream
* Tealium Data Connect
* Tealium DataAccess（EventStoreまたはEventDB用）
* OpenTrackアクセス

## DealerTrack統合の作成

Tealium Data ConnectでDealerTrack統合を作成するには、以下の手順に従います：

1. Tealium Connectデータソースを構成します。
1. DealerTrack APIへの接続を確立します。
1. DealerTrackからTealiumへデータを送信するレシピを作成します。
1. Tealiumへイベントを送信します。
1. データのイベントフィードを構成します。
1. トレースでテストし、レシピをアクティブにします。

## ステップ1: Tealium Connectデータソースの構成

Tealium Connectデータソースを構成します。詳細については、[Tealium Connectデータソースの構成]()を参照してください。

## ステップ2: DealerTrack APIへの接続を確立する

DealerTrack APIへの接続を確立するには、以下の手順を実行します：

1. **Data Connect &gt; Integrations**に移動します。
1. **Connections**をクリックし、**Create**をクリックします。
1. **DealerTrack**接続を選択します。
1. **Base URL**に`https://ot.dms.dealertrack.com`を入力します。
1. **Username**と**Password**を入力します。
1. **Connect**をクリックします。

 ![](/images/server-side/data-connect/dealertrack-data-connect-integration-establish-connection1.png)

 ![](/images/server-side/data-connect/dealertrack-data-connect-integration-establish-connection2.png)

## ステップ3: DealerTrackからTealiumへデータを送信するレシピを作成する

DealerTrackからTealiumへデータを送信するレシピを作成するには、以下の手順を実行します：

新しいレシピの作成方法については、[Data Connectでレシピを作成する]()を参照してください。

1. **DataConnect &gt; Integrations**に移動します。
1. **Integrations**画面で、**Create &gt; Recipe**をクリックします。
1. スケジュールアプリからトリガーされる新しいレシピを作成します。アプリからトリガーされるレシピの作成方法については、[Data Connectでレシピを作成する]()を参照してください。

[Actions](#actions)セクションには、DealerTrackから取得可能なデータの詳細が含まれています。

## ステップ4: Tealiumへイベントを送信する

Tealiumへイベントを送信するには、以下の手順を実行します：

1. **Tealium Events V2でイベントを送信**に移動します。
1. Tealiumへ送信したいデータを構成します。

 ![](/images/server-side/data-connect/dealertrack-data-connect-integration-send-events.png)

追加情報については、[レシピの作成: アクションの構成]()を参照してください。

## ステップ5: リードのイベントフィードを構成する

 ![](/images/server-side/data-connect/dealertrack-data-connect-integration-event-feed.png)

イベントフィードを作成するには、以下の手順を使用します：

1. **EventStream &gt; Live Events**に移動し、**&#43; Add Event Feed**をクリックします。
1. **Create Event Feed**ダイアログで**Title**と任意の**Notes**を入力します。
    * イベントフィードのタイトルは、Data Connectにリードイベントが入ってくる方法に依存します。
1. （オプション）**Add Label**をクリックして、このイベントフィードに適用するラベルを選択します。
1. **Event Data Storage**の下で、EventStoreまたはEventDBのためにフィードを有効にします。
1. 新しいリードイベントに一致するイベントをキャプチャするために、フィードに**Attribute Condition**を構成します。
1. **Save**をクリックします。
1. プロファイルを保存して公開します。

## ステップ6: トレースでテストし、レシピをアクティブにする

レシピをアクティブにする前に、徹底的なテストを実施します。テストが成功したら、自動データ統合プロセスを開始するためにレシピをアクティブにします。

トレースでテストし、レシピをアクティブにするための手順は以下の通りです：

1. **Trace**に移動します。
1. **New Trace**の下で**Start**をクリックします。トレースIDが表示されるダイアログが現れます。
1. トレースIDをコピーして**Continue**をクリックします。
1. **Data Connect &gt; Integrations**に移動します。
1. **Integrations**画面で、DealerTrackからTealiumへ新しいリードを送信するレシピについて、以下の手順を実行します：
    1. レシピを選択します。
    1. **Tealium events V2 action**を編集するために選択します。
    1. **Attributes to add**の下で、`tealium_trace_id`キーを追加し、**Value**にトレースIDを貼り付けます。
    1. **Save**をクリックします。
    1. **Start recipe**リストから**Test recipe**をクリックします。
1. **Trace**インターフェースに戻り、ログの詳細を検査します。
1. テストが終わったら、**Stop test**をクリックします。
1. レシピをアクティブにするために、**Start recipe**をクリックします。

## アクション

この統合を通じて追跡可能な以下のアクションがあります：

### 発行日による取引検索

| パラメータ | 説明 |
| --------- | ----------- |
| 会社番号 | 例：`ZE7`。 |
| エンタープライズコード | 例：`ZE`。 |
| サーバー名 | 例：`arkonap.arkona.com`。 |
| 発行日開始 | 車の取引日、この日付から検索を開始します。形式は`YYYY-MM-DD`です。 |
| 発行日終了 | 車の取引日、この日付で検索を終了します。形式は`YYYY-MM-DD`です。 |
| 取引状況 | 取引の状況、空白または送信されない場合はすべての取引状況を引っ張ります。許容されるパラメータは`Accepted`, `Capped`, `Closed`, `Unaccepted`、または空白です。 |

### 予約検索

| パラメータ | 説明 |
| --------- | ----------- |
| 会社番号 | 例：`ZE7`。 |
| エンタープライズコード | 例：`ZE`。 |
| サーバー名 | 例：`arkonap.arkona.com`。 |
| 開始日 | 予約検索の開始日、これは実際の予約の日であり、作成された日ではありません。形式は`YYYY-MM-DD`です。 |
| 終了日 | 予約検索の終了日、これは実際の予約の日であり、作成された日ではありません。形式は`YYYY-MM-DD`です。 |
| 作成日時開始 | 予約が作成されたときの検索を開始する日時。形式は`yyyy-mm-ddThh:mm:ssZ`です。 |
| 作成日時終了 | 予約が作成されたときの検索を終了する日時。形式は`yyyy-mm-ddThh:mm:ssZ`です。 |

### 未完了修理オーダー検索

| パラメータ | 説明 |
| --------- | ----------- |
| 会社番号 | 例：`ZE7`。 |
| エンタープライズコード | 例：`ZE`。 |
| サーバー名 | 例：`arkonap.arkona.com`。 |
| 作成日時開始 | 未完了修理オーダーが作成されたときの検索を開始する日時。形式は`yyyy-mm-ddThh:mm:ssZ`です。 |
| 作成日時終了 | 未完了修理オーダーが作成されたときの検索を終了する日時。形式は`yyyy-mm-ddThh:mm:ssZ`です。 |

### 完了修理オーダー取得

| パラメータ | 説明 |
| --------- | ----------- |
| 会社番号 | 例：`ZE7`。 |
| エンタープライズコード | 例：`ZE`。 |
| サーバー名 | 例：`arkonap.arkona.com`。 |
| 最終クローズ日時開始 | 最終クローズ修理オーダーの検索を開始する日時。形式は`yyyy-mm-ddThh:mm:ssZ`です。 |
| 最終クローズ日時終了 | 最終クローズ修理オーダーの検索を終了する日時。形式は`yyyy-mm-ddThh:mm:ssZ`です。 |
