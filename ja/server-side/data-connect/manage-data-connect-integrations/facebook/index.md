---
title: Facebook Lead Adsデータコネクト統合セットアップガイド
description: この記事では、Tealium Data ConnectとFacebook Lead Ads間の統合を構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-connect/manage-data-connect-integrations/facebook/
---
Facebook Lead Adsデータコネクト統合は、マーケティング戦略を改善し、顧客データの管理を効率化するいくつかの方法を提供します。リードを収集し、CRMシステムに迅速にインポートし、自動フォローアップを構成し、リアルタイムのパーソナライゼーションをトリガーし、リードを顧客に変換するためのマーケティング努力を自動化できます。

**Send Lead Event**を使用して、変換リード広告を送信します。変換リードイベントを構成するには、以下のガイドに従ってください。

## 要件

* Tealium EventStreamまたはAudienceStream
* Tealium Data Connect
* Tealium DataAccess（EventStoreまたはEventDB用）
* リードID

## ユースケース

以下は、Tealium Data Connect統合をFacebook Lead Adsと使用する方法の例です：

1. **リード生成とエンリッチメント**：Facebook Lead Adsを使用して潜在顧客からリードを収集します。次に、これらのリードをCRMシステムに統合し、Tealium Data Connectを使用して追加データでリードをエンリッチし、より詳細な顧客プロファイルを作成します。
1. **シームレスなリードインポート**：Facebook Lead Adsから生成されたリードをTealium Data Connectを通じて自動的にCRMシステムにインポートします。これにより、営業およびマーケティングチームが新しいリードにすぐにアクセスできるようになります。
1. **自動フォローアップ**：CRMでFacebook Lead Adsを通じてリード提出がトリガーされた自動フォローアップシーケンスを構成します。これには、パーソナライズされたメール、SMSメッセージの送信、またはフォローアップコールのスケジュール構成が含まれる場合があります。
1. **リアルタイムパーソナライゼーション**：リードがFacebook Lead Adsと対話すると、Tealium Data Connectはウェブサイトまたはメールキャンペーンでリアルタイムのパーソナライゼーションをトリガーできます。これにより、リードはすぐにカスタマイズされたコンテンツで積極的に関与することが保証されます。
1. **リードスコアリングとセグメンテーション**：Facebook Lead Adsによって収集されたデータに基づいて自動的にリードをスコアリングおよびセグメント化します。これにより、リードを効果的に優先順位付けしてターゲットにし、営業チームが最も有望な見込み客に焦点を当てることができます。
1. **マーケティング自動化**：Facebook Lead Adsをマーケティング自動化プラットフォームと統合して、Tealium Data Connectを使用します。これにより、リードを営業プロセスを通じて進めるための自動フォローアップメール、SMSメッセージ、またはその他の通信が可能になります。
1. **抑制**：メール通信の登録を解除した個人、特定のメールキャンペーンのオプトアウト、または既に変換されたり特定のアクションを取ったりした個人を除外します。これにより、GDPRのような規制の遵守が保証され、メールマーケティングリストが整理され、既に変換を達成したオーディエンスに対する不要な広告支出が防止されます。

## 統合フロー

以下の図は、Facebook Lead Ads Data Connect統合フローを示しています。Facebook Lead AdsとTealium Data Connect統合を正常に構成するために、以下の詳細な手順に従ってください。

![](/images/server-side/data-connect/fb-lead-ads-data-connect-integration-flow.png)

## Facebook Lead Ads統合の作成

Tealium Data ConnectとFacebook Lead Ads統合を作成するために必要な手順は次のとおりです：

1. Tealium Connectデータソースを構成します。
1. FacebookからTealiumに新しいリードを送信するレシピを作成します。
1. 新しい/更新されたリードレコードをTealiumからSalesforceに送信するためのオーディエンスとオーディエンスコネクタを構成します。
1. SalesforceからTealiumに新しい/更新されたリードレコードを受け取るための別のレシピを作成します。
1. リードのためのイベントフィードを構成します。
1. 更新されたリードレコードをFacebookに送り返すためのイベントコネクタを構成します。
1. トレースでテストし、レシピをアクティブ化します。

### ステップ1: Tealium Connectデータソースを構成

Tealium Connectデータソースを構成します。手順については、[Tealium Connectデータソースの構成]()を参照してください。

### ステップ2: FacebookからTealiumに新しいリードを送信する新しいレシピを作成

新しいレシピの作成方法の詳細については、[Data Connectでレシピを作成]()を参照してください。

レシピを作成して構成するための次のステップを完了します：

1. **DataConnect &gt; Integrations**に移動し、Facebook Lead Adsアプリからトリガーされる新しいレシピを作成します。アプリからトリガーされるレシピの作成方法の詳細については、[Data Connectでレシピを作成]()の手順を参照してください。
1. レシピを構築するために：
    1. **Trigger**の下で**New Lead**を選択します。
    1. Facebook Business Managerアカウントに接続します。
    1. 接続したら、コネクタ構成を構成して、データを引き出すFacebook Lead Adsアカウントとフォームを指定します：
    1. **Setup**ステップで：
        * データを引き出す**Page**を選択します。
        * **Form ID**フィールドで**Use form ID**を選択し、Meta Business Suite（旧Facebook Business Manager）からフォームIDを入力します。
    1. 新しいリード生成をTealiumに送信するアクションを構成します。詳細については、[アクションの構成]()を参照してください。

        ![](/images/server-side/data-connect/new-lead-generations-to-Tealium-action.png)

### ステップ3: TealiumからSalesforceに新しい/更新されたリードレコードを送信

Tealiumから他のCRMに新しいまたは更新されたリードレコードを送信するための次のステップを完了します。この例ではSalesforceを使用します：

1. オーディエンスを構成します。詳細については、[オーディエンスの作成]()を参照してください。
1. **AudienceStream &gt; Audience Connectors**に移動します。
1. **&#43; Add Connector**をクリックし、[Salesforce Connector]()を追加します。
1. **Source**ステップで、
    1. 上記で作成した**Audience**を選択します。
    1. **Trigger**の下で**Joined Audience**を選択します。
1. **Configuration**ステップで、
    1. このコネクタインスタンスの**Name**を入力します。
    1. **Authentication**の下で、接続を確立するためのログイン資格情報を提供します。
1. **Action**ステップで：
    1. **Name**を入力します。
    1. **Action Type**で**Insert Contact**を選択します。
    1. 新しいリードが新しいオーディエンスになったときにSalesforceに送信するエンリッチされた属性をマッピングします。

### ステップ4: SalesforceからTealiumに新しい/更新されたリードレコードを受け取るための別のレシピを作成

![](/images/server-side/data-connect/recipe-to-receive-lead-records.png)

1. **DataConnect &gt; Integrations**に移動し、Salesforceアプリからトリガーされる新しいレシピを作成します。アプリからトリガーされるレシピの作成方法の詳細については、[Data Connectでレシピを作成]()の手順を参照してください。
1. レシピを構築するために：
    1. **Trigger**の下で**New/Updated Records**を選択します。ニーズに応じてバッチまたはリアルタイムを選択できます。
    1. Tealium Data ConnectアカウントをSalesforceで認証します。これにはAPIキーまたは資格情報の入力が含まれる場合があります。
    1. Facebook Lead AdsのフィールドをSalesforceの対応するフィールドにマッピングするためのコネクタ構成を構成します。データ同期の問題を避けるために、データマッピングが正確であることを確認してください。
    1. SalesforceからTealiumに新しい/更新されたレコードを送信するアクションを構成します。詳細については、[アクションの構成]()を参照してください。

        ![](/images/server-side/data-connect/action-parameter-mapping.png)

### ステップ5: リード用イベントフィードの構成

イベントフィードを作成するには、以下の手順を完了してください：

1. **EventStream &gt; Live Events** に移動し、**&#43; Add Event Feed** をクリックします。
1. **Create Event Feed** ダイアログで、**Title** と任意の **Notes** を入力します。
    イベントフィードのタイトルは、Data Connectにリードイベントがどのように入ってくるかに依存します。
1. （オプション）**Add Label** をクリックして、このイベントフィードに適用するラベルを選択します。
1. **Event Data Storage** の下で、EventStoreまたはEventDBのフィードを有効にします。
1. 新しいリードイベントに一致するイベントをキャプチャするための **Attribute Condition** を構成します。
    ![](/images/server-side/data-connect/fb-lead-ads-data-connect-event-feed.png)
1. **Save** をクリックします。
1. プロファイルを保存して公開します。

### ステップ6: Facebook Conversionsイベントコネクタを構成してリードを送信

以下の手順に従って、[Facebook Conversionsイベントコネクタ](https://docs.tealium.com/server-side-connectors/facebook-conversions-connector/)を構成し、Facebookにリードを送信します：

1. **EventStream &gt; Event Connectors** に移動します。
1. **&#43; Add Connector** をクリックし、Facebook Conversionsコネクタを追加します。
1. **Source** ステップで、
    1. **Data Source** を選択します。
    1. 前の手順で作成した **Event Feed** を選択します。
1. **Configuration** ステップで、
    1. このコネクタのインスタンスの **Name** を入力します。
    1. **Authentication** の下で、接続を確立するためのログイン情報を提供します。
1. **Action** ステップで：
    1. **Name** を入力します。
    1. **Action Type** で **Send Lead Event** を選択します。
    1. **Lead ID** と **Event Name** パラメータをマッピングします。
        ![](/images/server-side/data-connect/fb-lead-ads-event-connector-action.png)
1. **Finish** をクリックします。
1. プロファイルを保存して公開します。

### ステップ7: トレースでテストし、レシピをアクティブにする

レシピをアクティブにする前に、徹底的なテストを実施してください。テストが成功したら、自動データ統合プロセスを開始するためにレシピをアクティブにします。

トレースでテストし、レシピをアクティブにする手順は以下の通りです：

1. サイドバーで **Trace** を選択します。
1. **New Trace** の下で **Start** をクリックします。トレースIDが表示されるダイアログが現れます。
1. トレースIDをコピーして **Continue** をクリックします。
1. **Data Connect** &gt; **Integrations** に移動します。
1. **Integrations** 画面で、FacebookからTealiumへの新しいリードを送信するレシピと、SalesforceからTealiumへの新規/更新されたリードレコードを受け取るレシピの両方について、次の操作を行います：
    1. レシピを選択します。
    1. **Tealium Events V2** アクションを編集するために選択します。
    1. **Attributes to add** の下で、新しい **Key** `tealium_trace_id` を追加し、**Value** にトレースIDを貼り付けます。
    1. **Save** をクリックします。
    1. **Start recipe** ドロップダウンリストで **Test recipe** をクリックします。
1. **Trace** インターフェースに戻り、ログの詳細を検査します。
1. テストが終わったら、**Stop test** をクリックします。
1. レシピをアクティブにするために、**Start recipe** をクリックします。