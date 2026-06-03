---
title: 公開環境を切り替える方法
description: この記事では、サイトにロードされるUniversal Tag（utag.js）ファイルの公開環境を切り替えるための利用可能な方法について説明します。
url: https://docs.tealium.com/ja/iq-tag-management/troubleshooting/switch-environoment/
---
## 仕組み

サイトで変更をテストしたいが、インストールされたTealiumファイルを編集するアクセス権がない場合、環境スイッチャーという方法を使用して、サイトに異なるバージョンのTealiumファイル（`utag.js`、`utag.sync.js`）をロードします。環境スイッチャーは、**Prod**環境に公開せずに本番サイトで変更をテストする安全な方法です。

環境を切り替えるために使用できる3つの方法があります：

* Tealiumツール：環境スイッチャー
* Web Companion
* Cookieの構成

### Tealiumツール：環境スイッチャー

環境スイッチャーは、Chromeブラウザで実行されるTealiumツールであり、サイトで異なる環境バージョンの`utag.js`をテストするための推奨方法です。

Tealiumファイルの異なるバージョンをロードするために[環境スイッチャー](/ja/iq-tag-management/tealium-tools/environment-switcher/)の使用方法について詳しく学びましょう。

### Web Companion

Web Companionは、Dev、QA、またはProdなどの標準的な環境からTealiumファイルをロードする方法を提供します。

この機能はデフォルトでは無効になっています。この機能を有効にするには、[公開構成のWeb Companion構成]()をオンにします。

Web Companionを使用して環境を変更するための次の手順を使用します：

1. [Web Companion]()を起動します。  
**Target Environment**セクションには、現在の環境が青で表示され、コード化された環境がオレンジの境界線で表示されます。  
例えば、本番サイトでは次のように表示されます：  
    ![](/images/iq-tag-management/iq-web-companion-environments.png)
1. ページにロードされる環境を変更するには、**Dev**または**QA**をクリックし、次に**Refresh Page**をクリックします。ページは新しく選択された環境で更新されます。
例えば、**QA**をクリックし、ページを更新し、Web Companionを再度開くと、次のように表示されます：  
    ![](/images/iq-tag-management/iq-web-companion-switched-to-qa.png)  
切り替えられた環境は、あなたのローカルセッションにのみ有効です。本番サイトには影響しません。

### Cookieの構成

Cookieを構成することで環境を変更することもできます。

この方法を機能させるためには、[公開構成のWeb Companion構成]()をオンにする必要があります。

環境Cookieを構成するための次の手順を使用します：

1. ブラウザのコンソールを開きます。
1. 次のコマンドを使用してCookieを構成します：  
    ```
    document.cookie = &#34;utag_env_ACCOUNT_PROFILE=//tags.tiqcdn.com/utag/ACCOUNT/PROFILE/ENV/utag.js; path=/; domain=YOURSITE.com&#34;;
    ```
    コマンドラインの例では、次のように変数を置き換えます：
      * **ACCOUNT** – Tealium iQアカウント名に置き換えます
      * **PROFILE** – Tealium iQプロファイル名に置き換えます
      * **ENV** – ロードする環境（`dev`、`qa`、またはカスタムエントリ）に置き換えます
      * **YOURSITE** – サイトのドメイン名に置き換えます

1. Cookieを作成した後、新しい環境をロードするためにブラウザを更新します。
