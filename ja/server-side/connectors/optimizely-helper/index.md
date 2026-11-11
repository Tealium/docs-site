---
title: TealiumツールOptimizelyヘルパー
url: https://docs.tealium.com/ja/server-side/connectors/optimizely-helper/
---### Tealium Toolsのインストール

最新バージョンのTealium Toolsがインストールされていることを確認してください。このGoogle Chrome拡張機能には、Optimizely Helperを含むさまざまなツールが用意されています。詳細については、[Tealium Toolsブラウザー拡張機能](https://docs.tealium.com/tealium-tools-browser-extension/)を参照してください。

### Optimizelyアカウントへの接続

Tealium Toolsをインストールしたら、以下の手順に従い、OptimizelyのAPIトークンとプロジェクトIDを使用してCustomer Data Platform（CDP）とOptimizelyを接続します。

1. Optimizelyで、**Account Settings**に移動し、API Tokensセクションの**View Tokens**をクリックします。
1. 新しいAPIトークンを作成し、そのトークンをクリップボードにコピーします。
1. Google Chromeの右上隅にあるTealiumアイコンをクリックして、**Tealium Tools**を開きます。
1. **Optimizely Helper**を選択します。
1. APIトークンを**Token**フィールドに貼り付けます。
1. CDPオーディエンスをマッピングするプロジェクトに移動し、プロジェクトIDをコピーします。プロジェクトIDは、Projectページの右上隅にある**Project Code**ドロップダウンメニューで確認できます。  
    ![](https://docs.tealium.com/images/server-side/optimizely-helper-project-id.png)
1. Optimizely Helperで、プロジェクトIDを**Project ID**フィールドに貼り付けます。
1. このOptimizelyプロジェクトに関連付けるTealiumアカウントとプロファイルの名前を入力します。
1. **Import Audience Data**をクリックします。

Optimizely Helperに、Optimizelyの新規または既存のオーディエンスにマッピングできるオーディエンスとバッジのリストが表示されます。

### オーディエンスのOptimizelyプロジェクトへのマッピング

1. Optimizely Helperで、Optimizelyに追加するCDPオーディエンスまたはバッジを選択します。
1. Optimizely Audienceドロップダウンメニューで、既存のOptimizelyオーディエンスを選択するか、新しいオーディエンスを作成します。新しいOptimizelyオーディエンスを作成した場合、その名前には、選択したCDPバッジまたはオーディエンスと同じ名前が使用されます。
1. **Create Audience**をクリックして確定します。
1. オーディエンスのマッピングを追加するには、上記の手順を繰り返します。

オーディエンスのマッピングが完了したら、**Generate Code Snippet**をクリックします。このコードをutag.sync.jsファイルに追加する必要があります。<br>
![](https://docs.tealium.com/images/server-side/optimizely-helper-code-snippet.png)

utag.sync.jsテンプレートにコードを追加するには、**Copy Code Snippet to Clipboard**をクリックします。詳細については、[utag.sync.jsスクリプトの使用](https://docs.tealium.com/utag-sync/)を参照してください。

### オーディエンスベースの実験の作成

これで、マッピングされたCDPバッジとオーディエンスをプロジェクトのターゲティングに使用できるようになります。新しいターゲットオーディエンスを選択するには、次の手順を実行します。

1. 新しい実験を作成するか、既存の実験を編集して、**Audience Targeting**をクリックします。
1. **Add a Saved Audience**をクリックし、CDPバッジまたはオーディエンスを選択します。
    ![](https://docs.tealium.com/images/server-side/audiencebasedexperiments.png)
1. 実験を保存します。

Optimizelyでのオーディエンスのターゲティングについて詳しくは、[Optimizelyナレッジベースの記事](https://help.optimizely.com/hc/en-us/articles/200039685#changes)を参照してください。