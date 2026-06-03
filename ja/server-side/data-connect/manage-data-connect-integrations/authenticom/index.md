---
title: Authenticom DealerVault データコネクト統合セットアップガイド
description: この記事では、Tealium Data ConnectとAuthenticom DealerVaultの間の統合を構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-connect/manage-data-connect-integrations/authenticom/
---
AuthenticomとTealium Data Connectの統合により、以下のベンダーデータフィードをインポートできます：

* 在庫
* 部品在庫
* 販売
* 未解決の修理注文
* 特別注文部品
* サービス
* サービス予約

## 必要条件

* Tealium EventStreamまたはAudienceStream
* Tealium Data Connect
* Tealium DataAccess（EventStoreまたはEventDB用）
* Authenticom APIアクセス

## Authenticom統合の作成

Tealium Data ConnectでAuthenticom統合を作成するには、以下の手順に従ってください：

1. Tealium Connectデータソースを構成します。
1. 実装エンジニアまたはカスタマーサクセスマネージャーに連絡して、レシピをデータコネクト環境にインポートしてもらいます。
1. Authenticom APIへの接続を確立します。
1. データタイプとベンダーを選択します。
1. Tealiumにイベントを送信します。
1. リードのためのイベントフィードを構成します。
1. トレースでテストし、レシピをアクティブにします。

## ステップ1: Tealium Connectデータソースの構成

Tealium Connectデータソースを構成します。詳細については、[Tealium Connectデータソースの構成]()を参照してください。

## ステップ2: Tealiumに連絡する

実装エンジニアまたはカスタマーサクセスマネージャーに連絡し、彼らが環境に統合をインポートします。

## ステップ3: Authenticom APIへの接続を確立する

Authenticom APIへの接続を確立するには、以下の手順を実行します：

1. **Data Connect &gt; Integrations**に移動します。
1. **Authenticom**接続を選択します。
1. **Base URL**は変更しないでください。
1. 本番環境のAuthenticom Developers APIポータルにある**Subscription Key**を入力します。

 ![](/images/server-side/data-connect/authenticom-data-connect-integration-establish-connection.png)

## ステップ4: データタイプとベンダーを選択する

データタイプとベンダーを選択するには、以下の手順を実行します：

1. **Authenticom - DealerVault**というレシピに移動します。
1. レシピのステップ4 **指定された日付以降に更新されたディーラーを取得する**を選択します。
1. Tealiumにインポートしたいデータタイプを選択します。利用可能なデータタイプは以下の通りです：
    * `INV`：在庫。
    * `PTINV`：部品在庫。
    * `SL`：販売。
    * `OPENRO`：未解決の修理注文。
    * `SOP`：特別注文部品。
    * `SV`：サービス。
    * `SV_APPT`：サービス予約。
1. ウィンドウの右上で**保存**をクリックします。

 ![](/images/server-side/data-connect/authenticom-data-connect-integration-select-data-type.png)

## ステップ5: Tealiumにイベントを送信する

Tealiumにイベントを送信するには、以下の手順を実行します：

1. **TealiumイベントV2でイベントを送信**に移動します。
1. Tealiumに送信したいデータを構成します。

 ![](/images/server-side/data-connect/authenticom-data-connect-integration-send-events.png)

詳細については、[レシピの作成：アクションの構成]()を参照してください。

## ステップ6: リードのためのイベントフィードを構成する

 ![](/images/server-side/data-connect/authenticom-data-connect-integration-set-up-event-feed.png)

イベントフィードを作成するには、以下の手順を実行します：

1. **EventStream &gt; Live Events**に移動し、**&#43; Add Event Feed**をクリックします。
1. **Create Event Feed**ダイアログで**Title**と任意の**Notes**を入力します。
1. （オプション）**Add Label**をクリックして、このイベントフィードに適用するラベルを選択します。
1. **Event Data Storage**の下で、EventStoreまたはEventDBのフィードを有効にします。
1. 新しいリードイベントに一致するイベントをキャプチャするための**Attribute Condition**を構成します。
1. **Save**をクリックします。
1. プロファイルを保存して公開します。

## ステップ7: トレースでテストし、レシピをアクティブにする

レシピをアクティブにする前に、徹底的なテストを実施します。テストが成功したら、自動データ統合プロセスを開始するためにレシピをアクティブにします。

トレースでテストし、レシピをアクティブにするための手順は以下の通りです：

1. **Trace**に移動します。
1. **New Trace**の下で**Start**をクリックします。トレースIDが表示されるダイアログが表示されます。
1. トレースIDをコピーして**Continue**をクリックします。
1. **Data Connect &gt; Integrations**に移動します。
1. **Integrations**画面で、AuthenticomからTealiumへ新しいリードを送信するレシピについて以下の手順を実行します：
    1. レシピを選択します。
    1. **Tealium Events V2 action**を編集します。
    1. **Attributes to add**の下で、`tealium_trace_id`キーを追加し、**Value**にトレースIDを貼り付けます。
    1. **Save**をクリックします。
    1. **Start recipe**リストから**Test recipe**をクリックします。
1. **Trace**インターフェースに戻り、ログの詳細を確認します。
1. テストが完了したら、**Stop test**をクリックします。
1. レシピをアクティブにするには、**Start recipe**をクリックします。