---
title: Adobe Experience Cloud IDサービスタグ構成ガイド
description: AdobeのExperience Cloud IDサービスタグは、サイト訪問に対してユニークな識別子であるCloud IDを生成します。Cloud IDにより、Experience Cloudソリューション間で訪問のデータを共有および追跡することが可能になります。この記事では、iQタグ管理（TiQ）プロファイルでタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/adobe-experience-cloud-id-service-tag/
---
他のAdobeタグ（Appmeasurement、JavaScript、Heartbeatなど）がCloud IDを必要とする前に、Cloud IDサービスタグを先に読み込むことが重要です。すべてのページにタグをバンドルし、タグタブで他のAdobeタグより上に配置することが、ページ上で他のAdobeタグが読み込まれる前にCloud IDがアクセス可能であることを保証する最良の方法です。

## 対応バージョン

* v5.5（最新および推奨）
* v5.4
* v5.3
* v5.2 
* v4.4
* v4.3
* v4.1
* v3.0

## Adobe Web SDKオプトインモジュール

Adobe Analyticsは、Web SDKバージョン4.0.0でオプトインモジュールを導入しました。オプトインモジュールは、GDPRやCCPAなどのプライバシー法規制に準拠するために、ユーザーの同意を確認および強制するメカニズムを提供します。バージョン5.2.0でのエンリッチメントされたチェックにより、Adobeツールが実行に必要な許可を持っていることが保証されます。

Experience Cloud IDサービスタグのバージョン4.0以降を使用している場合、タグを構成した後にオプトインモジュールを有効にする必要があります。詳細については、[Adobe Web SDKオプトインモジュールを有効にする]()を参照してください。

## タグ構成

まず、タグマーケットプレイスにアクセスし、プロファイルにExperience Cloud IDサービスタグを追加します（[タグを追加する]()を参照）。

タグを追加した後、以下の構成を構成します：

* **Adobe Org ID**
  * （必須）組織に割り当てられた英数字のExperience Cloud IDを入力します。
  * 大文字と小文字を区別します。
  * 例：`265H7Z562851TTX99W870V12`@AdobeOrg
* **Tracking Server**
  * （必須）Adobe Analyticsデータ収集用のドメインを入力します。
  * ここで画像リクエストとクッキーが処理されます。
  * 例：`site.mydomain.com`
* **Tracking Server Secure**
  * （オプション）セキュアなトラッキングサーバーを使用している場合、このフィールドにURLを入力します。
* **Experience Cloud Server**
  * （オプション）第一者データ収集（CNAME）を使用して第三者コンテキストで第一者クッキーを利用する場合、このフィールドにトラッキングサーバーのURLを入力します。
* **Experience Cloud Server Secure**
  * （オプション）セキュアなExperience Cloudサーバーを使用している場合、このフィールドにURLを入力します。
* **Code Version**
  * （必須）バージョン3.0以降は、Internet Explorerのバージョン6から9をサポートしていません。

タグ構成を動的に構成する場合は、データマッピング（以下参照）を使用してください。

## 読み込みルール

[読み込みルール]()は、サイト上でこのタグのインスタンスをいつ、どこで読み込むかを決定します。

推奨される読み込みルール：**すべてのページで読み込む**。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング]()を参照してください。

Cloud IDサービスタグの宛先変数は、そのデータマッピングタブに組み込まれています。利用可能なカテゴリは次のとおりです：

### 標準

| **変数** |**宛先名**| **説明**|
|---| ---| --- |
|`adobe_org_id`| Adobe Org ID|  会社のExperience Cloudソリューションに割り当てられた英数字ID。 |
|`config.trackingServer`|Tracking Server|  データ収集サーバーのURL。 |
|`config.trackingServerSecure`| Tracking Server Secure| データ収集セキュアサーバーのURL。 |
|`config.marketingCloudServer`|Experience Cloud Server|  CNAMEが有効な場合のデータ収集サーバーのURL。 |
| config.marketingCloudServerSecure |Experience Cloud Server Secure|  CNAMEが有効な場合のデータ収集サーバーのURL。 |

### 顧客ID

追加の顧客識別子を送信するためにこれらの宛先にマッピングします。

宛先にマッピングする手順は次のとおりです：

1. **プロパティ**リストから顧客プロパティを選択します。
1. **顧客ID**フィールドにマッピングされる変数の値を入力します。  
データレイヤーで指定された値が見つかった場合にプロパティが送信されます。  

|**プロパティ名**| **タイプ** | **説明**|
|:------------|:------------|:------------|
|`ID`|  文字列 | 同じ訪問の追加ID。 |
|`authState`| 整数 |  認証状態を示します。可能な値は次のとおりです：&lt;ul&gt;&lt;li&gt;`0` 未認証または不明&lt;/li&gt;&lt;li&gt;`1` 認証済み&lt;/li&gt;&lt;li&gt;`2` ログアウト済み&lt;/li&gt;&lt;/ul&gt; |

### イベント
イベントをマッピングするには、[イベントマッピングを作成する]()を参照してください。

| **変数** | **タイプ** | **説明** |
|:---------|:------------|:------------|
| `setCustomerID` | 文字列 | 顧客IDを構成 |

## Adobe Web SDKオプトインモジュールを有効にする

Experience Cloud IDサービスタグのバージョン4.0以降を使用している場合、イベントデータをTealiumに送信するためには`doesOptInApply`オプションを`true`に構成する必要があります。`doesOptInApply`を構成するには、Adobe Experience Cloud IDサービスタグにスコープされたJavaScript拡張機能を作成します：

1. **タグ管理 &gt; 拡張機能**に移動します。
1. **詳細**タブをクリックし、**&#43; 追加**で**JavaScriptコード**をクリックします。
1. **スコープ**で**タグスコープの拡張機能**を選択し、次に**Adobe Experience Cloud IDサービス**を選択します。
1. **構成**に次のコードを入力します：  
    ```js
    u.data.config = u.data.config || {};
    u.data.config[&#39;doesOptInApply&#39;] = true;
    u.data.config[&#39;preOptInApprovals&#39;] = [&#39;aa&#39;, &#39;ecid&#39;];
    u.data.config[&#39;isIabContext&#39;] = false;
    u.data.config[&#39;optInStorageExpiry&#39;] = 34128000; 
    ```  
    次の図は、Adobeオプトインモジュールを有効にする拡張機能の構成例を示しています：  
    ![](/images/client-side-tags/adobe-enable-optin-module-extension-example.png)
1. 保存して公開します。

ブラウザの開発ツールを使用してオプトインサービスが期待通りに動作しているかを検証できます。詳細については、[オプトインサービスの検証](https://experienceleague.adobe.com/en/docs/id-service/using/implementation/opt-in-service/testing-optin-and-iab-plugin)に関するAdobeのドキュメントを参照してください。

Live Eventsを使用して、Adobe AnalyticsおよびAdobe Experience CloudのイベントデータがTealiumに送信されていることを確認できます。詳細については、[Live Eventsについて]()を参照してください。

## ベンダードキュメント

* [Adobe Experience Cloud IDサービス](https://experienceleague.adobe.com/en/docs/id-service/using/home)
* [オプトインサービスの検証](https://experienceleague.adobe.com/en/docs/id-service/using/implementation/opt-in-service/testing-optin-and-iab-plugin)
* [顧客IDと認証状態](https://experienceleague.adobe.com/en/docs/id-service/using/reference/authenticated-state)
* [アナリティクストラッキングサーバーの使用](https://experienceleague.adobe.com/en/docs/target/using/integrate/a4t/analytics-tracking-server)