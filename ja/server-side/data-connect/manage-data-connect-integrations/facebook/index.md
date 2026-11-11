---
title: Facebook Lead Ads Data Connect統合セットアップガイド
description: この記事では、Tealium Data ConnectとFacebook Lead Adsの統合をセットアップする方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-connect/manage-data-connect-integrations/facebook/
---
Facebook Lead Ads Data Connect統合には、マーケティング戦略を改善し、顧客データ管理を効率化するためのさまざまな方法があります。リードを収集してCRMシステムにインポートすることで迅速にアクセスできるようにするほか、自動フォローアップの構成、リアルタイムパーソナライゼーションのトリガー、マーケティング施策の自動化を行い、リードを顧客へと転換できます。

Data Connectの**リードイベントを送信**を使用して、コンバージョンリード広告を送信します。コンバージョンリードイベントをセットアップするには、以下のガイドに従ってください。

## 要件

* Event StreamingまたはCustomer Data Platform（CDP）
* Tealium Data Connect
* Tealium DataAccess（EventStoreまたはEventDB用）
* リードID

## ユースケース

Tealium Data ConnectとFacebook Lead Adsの統合は、次のように利用できます。

1. **リードの獲得とエンリッチメント**：Facebook Lead Adsを使用して、潜在顧客からリードを収集します。その後、これらのリードをCRMシステムに統合し、Tealium Data Connectを使用して追加データでエンリッチすることで、より詳細な顧客プロファイルを作成します。
1. **シームレスなリードのインポート**：Facebook Lead Adsで生成されたリードを、Tealium Data Connectを介してCRMシステムに自動的にインポートします。これにより、営業チームとマーケティングチームは新しいリードに即座にアクセスできます。
1. **自動フォローアップ**：Facebook Lead Adsからのリード送信によってトリガーされる、自動フォローアップシーケンスをCRMにセットアップします。これには、パーソナライズされたメールやSMSメッセージの送信、フォローアップ電話のスケジュール構成などが含まれます。
1. **リアルタイムパーソナライゼーション**：リードがFacebook Lead Adsを操作すると、Tealium Data ConnectはWebサイトまたはメールキャンペーンでリアルタイムパーソナライゼーションをトリガーできます。これにより、リードに対してカスタマイズされたコンテンツを即座に提供できます。
1. **リードのスコアリングとセグメンテーション**：Facebook Lead Adsによって収集されたデータに基づき、リードを自動的にスコアリングおよびセグメント化します。これにより、リードに効果的に優先順位を付けてターゲティングできるため、営業チームは最も有望な見込み客に注力できます。
1. **マーケティングオートメーション**：Tealium Data Connectを使用して、Facebook Lead Adsをマーケティングオートメーションプラットフォームと統合できます。これにより、フォローアップメール、SMSメッセージ、その他のコミュニケーションを自動化し、リードを販売プロセスの各段階へ進めることができます。
1. **サプレッション**：メール配信を停止したユーザー、特定のメールキャンペーンをオプトアウトしたユーザー、すでにコンバージョン済みまたは指定されたアクションを実行済みのユーザーを除外します。これにより、GDPRなどの規制に準拠し、整理されたメールマーケティングリストを維持するとともに、すでにコンバージョンを達成したオーディエンスに対する不要な広告費の支出を防止できます。

## 統合フロー

以下の図は、Facebook Lead Ads Data Connectの統合フローを示しています。Tealium Data ConnectとFacebook Lead Adsの統合を正常にセットアップするには、以下の詳細な手順に従ってください。

![](https://docs.tealium.com/images/server-side/data-connect/fb-lead-ads-data-connect-integration-flow.png)

## Facebook Lead Ads統合の作成

Tealium Data ConnectとFacebook Lead Adsの統合を作成するには、次の手順を実行します。

1. Tealium Connectデータソースをセットアップします。
1. FacebookからTealiumに新しいリードを送信するレシピを作成します。
1. TealiumからSalesforceに新規または更新されたリードレコードを送信するためのオーディエンスとオーディエンスコネクタをセットアップします。
1. SalesforceからTealiumに新規または更新されたリードレコードを受信するための別のレシピを作成します。
1. リード用のイベントフィードをセットアップします。
1. 更新されたリードレコードをFacebookに送り返すためのイベントコネクタをセットアップします。
1. Traceを使用してテストし、レシピを有効化します。

### 手順1：Tealium Connectデータソースのセットアップ

Tealium Connectデータソースをセットアップします。手順については、[Tealium Connectデータソースのセットアップ](https://docs.tealium.com/tealium-connect-data-source/)を参照してください。

### 手順2：FacebookからTealiumに新しいリードを送信する新規レシピの作成

新規レシピの作成方法について詳しくは、[Data Connectでのレシピの作成](https://docs.tealium.com/create-recipe-data-connect/)を参照してください。

レシピを作成してセットアップするには、次の手順を実行します。

1. **DataConnect > Integrations**に移動し、Facebook Lead Adsアプリからトリガーされる新規レシピを作成します。**アプリからトリガー**されるレシピの作成方法について詳しくは、[Data Connectでのレシピの作成](https://docs.tealium.com/create-recipe-data-connect/)に記載されているレシピ作成手順を参照してください。
1. レシピを構築します。
    1. **Trigger**で、**New Lead**を選択します。
    1. Facebook Business Managerアカウントに接続します。
    1. 接続したら、データを取得するFacebook Lead Adsアカウントとフォームを指定するように、コネクタ構成を構成します。
    1. **Setup**手順で、次の操作を行います。
        * データの取得元となる**Page**を選択します。
        * **Form ID**フィールドで、**Use form ID**を選択し、Meta Business Suite（旧Facebook Business Manager）のフォームIDを入力します。
    1. 新たに生成されたリードをTealiumに送信するアクションをセットアップします。詳しくは、[アクションの構成](https://docs.tealium.com/create-recipe-data-connect/#step-2-configure-an-action)を参照してください。

        ![](https://docs.tealium.com/images/server-side/data-connect/new-lead-generations-to-Tealium-action.png)

### 手順3：TealiumからSalesforceへの新規または更新されたリードレコードの送信

Tealiumから任意のCRMに新規または更新されたリードレコードを送信するには、次の手順を実行します。この例ではSalesforceを使用します。

1. オーディエンスをセットアップします。詳しくは、[オーディエンスの作成](https://docs.tealium.com/manage-audiences/#create-an-audience)を参照してください。
1. **Connect > Audience Connectors**に移動します。
1. **+ Add Connector**をクリックし、[Salesforceコネクタ](https://docs.tealium.com/salesforce-connector/)を追加します。
1. **Source**手順で、次の操作を行います。
    1. 上記で作成した**Audience**を選択します。
    1. **Trigger**で、**Joined Audience**を選択します。
1. **Configuration**手順で、次の操作を行います。
    1. このコネクタインスタンスの**Name**を入力します。
    1. **Authentication**で、接続を確立するためのログイン認証情報を入力します。
1. **Action**手順で、次の操作を行います。
    1. **Name**を入力します。
    1. **Action Type**で、**Insert Contact**を選択します。
    1. 新しいリードを含む新規オーディエンスが作成されたときにSalesforceへ送信する、エンリッチ済み属性をマッピングします。

### 手順4：SalesforceからTealiumに新規または更新されたリードレコードを受信する別のレシピの作成

![](https://docs.tealium.com/images/server-side/data-connect/recipe-to-receive-lead-records.png)

1. **DataConnect > Integrations**に移動し、Salesforceアプリからトリガーされる新規レシピを作成します。**アプリからトリガー**されるレシピの作成方法について詳しくは、[Data Connectでのレシピの作成](https://docs.tealium.com/create-recipe-data-connect/)に記載されているレシピ作成手順を参照してください。
1. レシピを構築します。
    1. **Trigger**で、**New/Updated Records**を選択します。必要に応じて、バッチまたはリアルタイムのいずれかを選択できます。  
    1. Salesforceを使用してTealium Data Connectアカウントを認証します。この操作では、APIキーまたは認証情報の入力が必要になる場合があります。
    1. Facebook Lead AdsのフィールドをSalesforceの対応するフィールドにマッピングするように、コネクタ構成を構成します。データ同期の問題を防ぐため、データが正確にマッピングされていることを確認してください。
    1. SalesforceからTealiumに新規または更新されたレコードを送信するアクションをセットアップします。詳しくは、[アクションの構成](https://docs.tealium.com/create-recipe-data-connect/#step-2-configure-an-action)を参照してください。

        ![](https://docs.tealium.com/images/server-side/data-connect/action-parameter-mapping.png)
### ステップ5：リード用のイベントフィードを構成する

イベントフィードを作成するには、次の手順を実行します。

1. **Validate > Live Events**に移動し、**+ Add Event Feed**をクリックします。
1. **Create Event Feed**ダイアログで、**Title**と任意の**Notes**を入力します。
    
<blockquote>
イベントフィードのタイトルは、リードイベントがData Connectに取り込まれる方法によって異なります。
</blockquote>

1. （任意）**Add Label**をクリックし、このイベントフィードに適用するラベルを選択します。
1. **Event Data Storage**で、EventStoreまたはEventDBに対してフィードを有効にします。
1. 新しいリードイベントに一致するイベントをフィードで取得できるように、**Attribute Condition**を構成します。
    ![](https://docs.tealium.com/images/server-side/data-connect/fb-lead-ads-data-connect-event-feed.png)
1. **Save**をクリックします。
1. プロファイルを保存してパブリッシュします。

### ステップ6：リードを送信するFacebook Conversionsイベントコネクタを構成する

リードをFacebookに送り返すように[Facebook Conversionsイベントコネクタ](https://docs.tealium.com/server-side-connectors/facebook-conversions-connector/)を構成するには、次の手順を実行します。

1. **Connect > Event Connectors**に移動します。
1. **+ Add Connector**をクリックし、Facebook Conversionsコネクタを追加します。
1. **Source**ステップで、次の操作を行います。
    1. **Data Source**を選択します。
    1. [前の手順](#step-5-set-up-event-feed-for-leads)で作成した**Event Feed**を選択します。
1. **Configuration**ステップで、次の操作を行います。
    1. このコネクタインスタンスの**Name**を入力します。
    1. **Authentication**で、接続を確立するためのログイン認証情報を入力します。
1. **Action**ステップで、次の操作を行います。
    1. **Name**を入力します。
    1. **Action Type**で、**Send Lead Event**を選択します。
    1. **Lead ID**パラメータと**Event Name**パラメータをマッピングします。
        ![](https://docs.tealium.com/images/server-side/data-connect/fb-lead-ads-event-connector-action.png)
1. **Finish**をクリックします。
1. プロファイルを保存してパブリッシュします。

### ステップ7：Traceでテストしてレシピを有効化する

レシピを有効化する前に、十分なテストを実施します。テストが成功したら、レシピを有効化して自動データ統合プロセスを開始します。

Traceでテストしてレシピを有効化するには、次の手順を実行します。

1. サイドバーで**Trace**を選択します。
1. **New Trace**で**Start**をクリックします。Trace IDが表示されたダイアログが開きます。
1. Trace IDをコピーし、**Continue**をクリックします。
1. **Data Connect** > **Integrations**に移動します。
1. **Integrations**画面で、FacebookからTealiumに新しいリードを送信するレシピと、SalesforceからTealiumに新規または更新済みのリードレコードを送信するレシピの両方に対して、次の操作を行います。
    1. レシピを選択します。
    1. **Tealium Events V2**アクションを選択して編集します。
    1. **Attributes to add**で新しい**Key**として`tealium_trace_id`を追加し、**Value**にTrace IDを貼り付けます。
    1. **Save**をクリックします。
    1. **Start recipe**ドロップダウンリストで、**Test recipe**をクリックします。
1. **Trace**インターフェイスに戻り、ログの詳細を確認します。
1. テストが完了したら、**Stop test**をクリックします。
1. レシピを有効化するには、**Start recipe**をクリックします。