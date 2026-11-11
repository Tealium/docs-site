---
title: Authenticom DealerVault Data Connect統合セットアップガイド
description: この記事では、Tealium Data ConnectとAuthenticom DealerVaultの統合を構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-connect/manage-data-connect-integrations/authenticom/
---
AuthenticomとTealium Data Connectの統合により、次のベンダーデータフィードをインポートできます。

* 在庫
* 部品在庫
* 販売
* 未完了の修理注文
* 特別注文部品
* サービス
* サービス予約

## 要件

* Event StreamingまたはCustomer Data Platform（CDP）
* Tealium Data Connect
* Tealium DataAccess（EventStoreまたはEventDB用）
* Authenticom APIへのアクセス権

## Authenticom統合の作成

次の手順に従って、Tealium Data ConnectとAuthenticomの統合を作成します。

1. Tealium Connectデータソースを構成します。
1. [サポートにお問い合わせ](https://docs.tealium.com/support/)のうえ、レシピをData Connect環境にインポートするよう依頼します。
1. Authenticom APIへの接続を確立します。
1. データタイプとベンダーを選択します。
1. Tealiumにイベントを送信します。
1. リード用のイベントフィードを構成します。
1.Traceでテストし、レシピを有効化します。

## 手順1：Tealium Connectデータソースの構成

Tealium Connectデータソースを構成します。詳細については、[Tealium Connectデータソースの構成](https://docs.tealium.com/tealium-connect-data-source/)を参照してください。

## 手順2：Tealiumへの問い合わせ

[サポートにお問い合わせ](https://docs.tealium.com/support/)ください。担当者がお客様の環境に統合をインポートします。

## 手順3：Authenticom APIへの接続の確立

Authenticom APIへの接続を確立するには、次の手順を実行します。

1. **Connect > Data Connect > Integrations**に移動します。
1. **Authenticom**接続を選択します。
1. **Base URL**は変更しないでください。
1. 本番環境のAuthenticom Developers APIポータルにある**Subscription Key**を入力します。

 ![](https://docs.tealium.com/images/server-side/data-connect/authenticom-data-connect-integration-establish-connection.png)

## 手順4：データタイプとベンダーの選択

データタイプとベンダーを選択するには、次の手順を実行します。

1. **Authenticom - DealerVault**という名前のレシピに移動します。
1. レシピの手順4、**Retrieve dealers with updated data since a given date**を選択します。
1. Tealiumにインポートするデータタイプを選択します。次のデータタイプを使用できます。
    * `INV`：在庫。
    * `PTINV`：部品在庫。
    * `SL`：販売。
    * `OPENRO`：未完了の修理注文。
    * `SOP`：特別注文部品。
    * `SV`：サービス。
    * `SV_APPT`：サービス予約。
1. ウィンドウの右上にある**Save**をクリックします。

 ![](https://docs.tealium.com/images/server-side/data-connect/authenticom-data-connect-integration-select-data-type.png)

## 手順5：Tealiumへのイベントの送信

Tealiumにイベントを送信するには、次の手順を実行します。

1. **Send events in Tealium events V2**に移動します。
1. Tealiumに送信するデータを構成します。

 ![](https://docs.tealium.com/images/server-side/data-connect/authenticom-data-connect-integration-send-events.png)

詳細については、[レシピの作成：アクションの構成](https://docs.tealium.com/create-recipe-data-connect/#step-2-configure-an-action)を参照してください。

## 手順6：リード用イベントフィードの構成

 ![](https://docs.tealium.com/images/server-side/data-connect/authenticom-data-connect-integration-set-up-event-feed.png)

次の手順に従ってイベントフィードを作成します。

1. **Validate > Live Events**に移動し、**+ Add Event Feed**をクリックします。
1. **Create Event Feed**ダイアログで、**Title**と任意の**Notes**を入力します。
1. （任意）**Add Label**をクリックし、このイベントフィードに適用するラベルを選択します。
1. **Event Data Storage**で、EventStoreまたはEventDBのフィードを有効にします。
1. 新しいリードイベントに一致するイベントをフィードで取得できるよう、**Attribute Condition**を構成します。
1. **Save**をクリックします。
1. プロファイルを保存してパブリッシュします。

## 手順7：Traceでのテストとレシピの有効化

レシピを有効化する前に、十分なテストを実施してください。テストが成功したら、レシピを有効化して自動データ統合プロセスを開始します。

次の手順に従って、Traceでテストし、レシピを有効化します。

1. **Trace**に移動します。
1. **New Trace**で**Start**をクリックします。Trace IDが記載されたダイアログが表示されます。
1. Trace IDをコピーし、**Continue**をクリックします。
1. **Connect > Data Connect > Integrations**に移動します。
1. **Integrations**画面で、AuthenticomからTealiumに新しいリードを送信するレシピについて、次の手順を実行します。
    1. レシピを選択します。
    1. **Tealium Events V2 action**を選択して編集します。
    1. **Attributes to add**で`tealium_trace_id`キーを追加し、**Value**にTrace IDを貼り付けます。
    1. **Save**をクリックします。
    1. **Start recipe**リストで**Test recipe**をクリックします。
1. **Trace**インターフェイスに戻り、ログの詳細を確認します。
1. テストが完了したら、**Stop test**をクリックします。
1. レシピを有効化するには、**Start recipe**をクリックします。