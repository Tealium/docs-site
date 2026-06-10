---
title: Data Connectでレシピを作成する
description: この記事では、Data Connectでレシピを作成する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-connect/manage-data-connect-integrations/create-recipe/
---
 Data Connectを有効にしてレシピの作成と管理を開始するには、Tealiumのカスタマーサクセスマネージャーに連絡してください。 

レシピを作成するには、以下の手順を完了してください：

1. **DataConnect &gt; Integrations**に移動します。
1. **Integrations**画面で、**Create &gt; Recipe**をクリックします。
1. **My new recipe**スライドアウトで、レシピの名前を入力し、レシピに関連付けられたプロファイルを選択します。
1. **Pick a starting point**の下で、Workatoでアプリをトリガーする方法を選択します。
    * ビジネスケースに合わせてスケジュールで実行されるレシピを構築するには、**Run on a schedule**を選択します。
    * 定期的にソースシステムから新しいデータをポーリングするレシピを構築するには、**Trigger from an App**を選択します。 Workatoトリガーについての詳細は、Workato Recipe Componentsのドキュメントの[Triggers](https://docs.workato.com/recipes/triggers.html)記事を参照してください。アプリに利用可能なトリガーを確認するには、[Pre-built Connectors](https://docs.workato.com/connectors/prebuilt-connectors.html)のドキュメントでアプリ固有のドキュメントを読んでください。
1. **Start building**をクリックします。

## レシピを構築する

これで、Workatoでレシピの構築を開始できます。一般的に、レシピは特定のワークフローに従います：

1. [トリガーを選択する](#step-1-select-a-trigger)。
1. [アクションを構成する](#step-2-configure-an-action)。
1. [エラー処理を構成する](#step-3-configure-error-handling)。

### ステップ1: トリガーを選択する

**アプリベースのトリガー**  
Tealiumに統合したい**アプリ**を検索します。スケジュールベースのレシピの場合、トリガーは構成したスケジュールです。
   1. **Trigger**ステップで、ビジネスケースに合ったトリガーを選択します。 可能な場合はバッチ処理を使用して、レシピごとのタスク数を減らします。
   1. **Connection**ステップで、アプリに接続します。接続名を入力し、構成を完了して**Connect**をクリックします。
   1. **Setup**ステップで、このアプリトリガーに追加の構成を追加します。より具体的なトリガーを構成したい場合は、トリガー条件を構成します。

### ステップ2: アクションを構成する

1. **Actions**の下で**&#43;**をクリックします。
1. **What happens next?**で**Handle errors**を選択します。
エラーモニタリングステップでTealium Eventsアプリと関連アクションをラップすることをお勧めします。[ステップ3]()を完了して、レシピのエラー処理の構成を完了してください。ステップ3で説明されているようにレシピを停止しない場合、自動エラー通知は機能しません。
1. Tealiumにインポートするデータを準備するために必要なアプリを選択します。たとえば、Amazon S3に保存されている暗号化されたCSVデータを準備するために、**Download file contents in Amazon S3**、**Decrypt and verify data**、および**Parse CSV**アプリを一緒に使用します。
1. (オプション) データペイロードのサイズが500レコードを超える場合は、Tealium Eventsアプリでデータをより小さなペイロードサイズに分割するために**Repeat action**ループを使用します。
このループを使用するには：
    1. **&#43;**をクリックしてアクションのリストを表示します。
    1. **Repeat action**をクリックします。
    1. ループの**Repeat mode**を**Batch of items**に構成します。
    1. **Batch size**をアプリの最大バッチサイズに構成します。
1. **Select an app and action**の下で、**Tealium Events V2**アプリを選択します。
1. [Tealium Connectデータソース]()からの情報を入力します。
    * **Tealium Connect API Domain** - Tealium Connectデータソースで使用されている地域のTealium Collect APIドメインを入力します。
    * **Data Source Key** - Tealium Connectデータソースからデータソースキーを入力します。
    * **Tealium Account Name**および**Tealium Profile Name** - 対応するフィールドにTealiumアカウント名とプロファイル名を入力します。単一のアカウントには複数の対応するプロファイルがあります。このレシピからイベントを送信するTealiumプロファイルを指定してください。
1. **Source Data**セクションで、アプリにソースデータを追加します。
    * **Source Data source list** - **Recipe data**スライドアウトからデータをTealiumに送信するためのデータピルを選択します。**Recipe data**スライドアウトからバッチ処理されたデータを挿入できます。
    * **Visitor ID Value** - 訪問ID値のデータピルを選択します。
        * **既知のユーザー識別子を使用して訪問ID属性でスティッチングする場合**：レシピ内でユーザー識別子の値を含むデータピルを選択します。**Visitor Attribute ID**フィールドに対応する訪問属性IDを入力します。レシピからのイベントに構成される訪問ID属性を構成するために、任意の訪問ID属性のエンリッチメントを構成する必要があります。詳細については、[Visitor ID attribute enrichment for Tealium Connect]()を参照してください。
        * **匿名識別子に基づいてデータをインポートする場合**：レシピ内で匿名識別子を含むデータピルを選択します。**Visitor Attribute ID**フィールドを空のままにします。この値は直接`tealium_visitor_id`を構成します。
    * **Visitor Attribute ID** - この数値は、既存の訪問ID属性に`tealium_visitor_id`をマッチングするのに役立ちます。たとえば`_{Account}_{Profile}_{Visitor Attribute ID}_{Visitor ID Value}_`です。
        * **既知のユーザー識別子を使用して訪問ID属性でスティッチングする場合**：訪問属性IDを入力します。**Transform &gt; Visitor / Visit Attributes**に移動し、使用したい訪問属性を選択し、属性IDをTealium Eventsアプリにコピーします。詳細については、[Attribute IDs]()を参照してください。
        * **匿名識別子に基づいてデータをインポートする場合**：このフィールドを空のままにします。
    * **Attributes to add** - **Attributes to add**セクションを展開します。WorkatoがTealiumに送信するイベントの各イベント属性のキーと値を指定します。**Attributes to add**には、大文字小文字を無視して一意の名前を持つフィールドが含まれていることを確認してください。&lt;br&gt;Tealiumはすべてのイベントフィールド名を小文字で処理します。
        * ここに追加しないレシピのデータはTealiumに送信されません。
        * キーについては、**Text**入力を使用してイベント属性名を入力します。
        * 値については、**Text**入力を使用してイベント属性値をハードコードするか、データピルから値を作成します。
        * この機能を使用して、既存のTealium構成に合わせてキー名を編集し、新しい属性、エンリッチメント、および/またはルールの追加作業を最小限に抑えます。
        * イベント仕様を作成するには、このセクションに`tealium_event`値を追加します。
        * (オプション) アプリからではなく、Tealiumに送信したい追加の属性を追加します。たとえば、`tealium_event`、`tealium_trace_id`、または`_dc_ttl_`などです。これは訪問がどれくらい続くかを説明します。`tealium_trace_id`をデバッグ目的で使用する場合、1バッチで5イベント以上を送信することはできません。
1. (オプション) **Hash Visitor ID**を有効にするかどうかを選択します。訪問IDのハッシュ化が必要なユースケースの場合、**Show optional fields**をクリックし、**Hash Visitor ID**を有効にします。
    * 以前に**Visitor Attribute ID**を定義した場合、構築された`tealium_visitor_id`にSHA-256ハッシュを適用する場合は**Yes**を選択します。ほとんどの目的では、この値を**No**に構成します。
    * スティッチングしている訪問ID属性の値にSHA-256ハッシュを適用する場合は、**Visitor ID Value**フィールドでWorkatoの`encode_sha256`関数を使用します。
### ステップ3: エラーハンドリングの構成

1. **On Error** ステップをクリックします。
1. **Retry actions in Monitor block?** で、アクションのリトライを選択します。
1. ジョブレポートにログメッセージを追加します。
    1. エラー発生時に追加アクションを追加するため **&#43;** をクリックします。
    1. **Action in an app** をクリックし、**Logger by Workato** アプリを選択します。
    1. ログのメッセージを構成します。
1. レシピを停止します。
    1. エラー発生時に追加アクションを追加するため **&#43;** をクリックします。
    1. **Action in an app** をクリックし、**ReceipeOps by Workato** アプリを選択します。
    1. **Stop a recipe** アクションを選択します。
    1. **Whose account are you managing?** で **My account** を選択します。
    1. **Connect** をクリックします。
    1. **Setup** ステップで、**Recipe** ドロップダウンリストから現在のレシピ名を選択します。
    1. **Force stop** ドロップダウンリストから **Yes** を選択します。
1. 現在のジョブを停止します。
    1. レシピの最後の **&#43;** をクリックして、エラー発生時に追加アクションを追加します。
    1. **Stop job** をクリックします。
    1. **In job report, mark stopped job as** で、ドロップダウンリストから **Failed** を選択します。
    1. **Reason for failure** に **Error** と入力します。
1. **Save** をクリックします。
1. **Test** をクリックして、レシピの構成をテストします。
 エラーハンドリングをテストするために、一時的に Tealium Events V2 アプリの **Tealium Connect API Domain** 構成を存在しないドメインに変更します。例えば、ドメインを `xcollect-eu-west-1.tealiumiq.com` に変更してエラーハンドリングをテストし、テストが完了したらドメインを `collect-eu-west-1.tealiumiq.com` に戻します。 