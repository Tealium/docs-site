---
title: TealiumツールOptimizelyヘルパー
url: https://docs.tealium.com/ja/server-side/connectors/optimizely-helper/
---### Tealiumツールのインストール

最新版のTealiumツールがインストールされていることを確認してください。このGoogle Chrome拡張機能は、Optimizelyヘルパーを含むさまざまなツールを提供します。詳細については、[Tealiumツールブラウザ拡張機能](https://docs.tealium.com/tealium-tools-browser-extension/)を参照してください。

### Optimizelyアカウントの接続

Tealiumツールをインストールした後、OptimizelyからのAPIトークンとプロジェクトIDを使用して、AudienceStreamとOptimizelyを接続します：

1. Optimizelyで**アカウント構成**に移動し、APIトークンセクションの下の**トークンを表示**をクリックします。
1. 新しいAPIトークンを作成し、新しいトークンをクリップボードにコピーします。
1. Google Chromeの右上隅にあるTealiumアイコンをクリックして**Tealiumツール**を開きます。
1. **Optimizelyヘルパー**を選択します。
1. APIトークンを**トークン**フィールドに貼り付けます。
1. AudienceStreamのオーディエンスをマップしたいプロジェクトに移動し、プロジェクトIDをコピーします。プロジェクトIDは、プロジェクトページの右上隅にある**プロジェクトコード**ドロップダウンメニューから利用できます。  
    ![](https://docs.tealium.com/images/server-side/optimizely-helper-project-id.png)
1. Optimizelyヘルパーで、プロジェクトIDを**プロジェクトID**フィールドに貼り付けます。
1. このOptimizelyプロジェクトに関連付けたいTealiumアカウントとプロファイルの名前を入力します。
1. **オーディエンスデータをインポート**をクリックします。

Optimizelyヘルパーには、Optimizelyで新規または既存のオーディエンスにマップできるオーディエンスとバッジのリストが含まれています。

### オーディエンスをOptimizelyプロジェクトにマッピング

1. Optimizelyヘルパーで、Optimizelyに追加するAudienceStreamのオーディエンスまたはバッジを選択します。
1. Optimizelyオーディエンスのドロップダウンメニューで、既存のOptimizelyオーディエンスを選択するか、新しいものを作成します。新しいOptimizelyオーディエンスを作成する場合、名前は選択したAudienceStreamのバッジまたはオーディエンスの名前と同じです。
1. **オーディエンスを作成**をクリックして確認します。
1. 追加のオーディエンスマッピングを作成するには、上記の手順を繰り返します。

オーディエンスをマッピングした後、**コードスニペットを生成**をクリックします。このコードはutag.sync.jsファイルに追加する必要があります。<br>
![](https://docs.tealium.com/images/server-side/optimizely-helper-code-snippet.png)

コードをutag.sync.jsテンプレートに追加するには、**コードスニペットをクリップボードにコピー**をクリックします。詳細については、[utag.sync.jsスクリプトの使用](https://docs.tealium.com/utag-sync/)を参照してください。

### オーディエンスベースの実験を作成

プロジェクトには、ターゲティングに利用できるマッピングされたAudienceStreamのバッジとオーディエンスが含まれています。新しいターゲットオーディエンスを選択するには：

1. 新しい実験を作成するか、既存の実験を編集し、**オーディエンスターゲティング**をクリックします。
1. **保存されたオーディエンスを追加**をクリックし、AudienceStreamのバッジまたはオーディエンスを選択します。
    ![](https://docs.tealium.com/images/server-side/audiencebasedexperiments.png)
1. 実験を保存します。

Optimizelyでのオーディエンスターゲティングについての詳細は、[Optimizely知識ベースの記事](https://help.optimizely.com/hc/en-us/articles/200039685#changes)を参照してください。