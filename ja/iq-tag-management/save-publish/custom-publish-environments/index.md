---
title: カスタム公開環境
description: 3つのデフォルト環境だけでは不十分な場合、より多くのオプションを提供するためにカスタム環境を作成できます。
url: https://docs.tealium.com/ja/iq-tag-management/save-publish/custom-publish-environments/
---
## 仕組み

カスタム環境は、以下のシナリオに役立ちます：

* 開発者が通常のワークフローに影響を与えることなく長期的な変更を行うためのサンドボックスまたはローカル環境を作成する。
* 組織の内部テスト環境に合わせたステージング環境を作成する。
* 変更を段階的に小規模な顧客グループにリリースして、潜在的な負の影響を最小限に抑えるための代替プロダクション環境を作成する。

プロファイルを公開する環境は、サイトでロードするユニバーサルタグ（`utag.js`）のURLに対応します。デフォルトの環境は以下のURLパスに対応しています：

* **Dev** - `/utag/account/profile/dev/utag.js`
* **QA** - `/utag/account/profile/qa/utag.js`
* **Prod** - `/utag/account/profile/prod/utag.js`

カスタム環境名は、`utag.js`のURLで大文字と小文字が区別されます。例えば、`Preview`というカスタム環境を作成した場合、その環境の`utag.js`ファイルへのURLパスは次のようになります：`/utag/ACCOUNT/PROFILE/Preview/utag.js`

カスタム公開環境をテストするには、[Web Companion]()または[Environment Switcher Tealium Tool]()を使用できます。

カスタム環境の作成と管理についての詳細情報：

* プラットフォーム権限：[環境管理](https://docs.tealium.com/manage-environments/)。
* 旧権限：[コードセンター](https://docs.tealium.com/code-center/)。

## カスタム環境への公開

カスタム環境に公開するには：

1. **保存/公開**をクリックします。
1. **公開場所**セクションで、**カスタム**チェックボックスを選択します。ドロップダウンリストが表示されます：
    ![](https://docs.tealium.com/images/iq-tag-management/save-publish/iq-custom-publish-environment-save-publish.png)
1. ドロップダウンリストから公開したい環境を選択します。
    * 一度に1つのカスタム環境にのみ公開できます。複数の環境に公開するには、それぞれの環境で公開プロセスを繰り返します。
1. **公開**をクリックします。