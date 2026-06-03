---
title: Adobe Experience Cloud ID Serviceタグ構成ガイド
description: AdobeのExperience Cloud ID Serviceタグは、サイト訪問のためのユニークな識別子、いわゆるCloud IDを生成します。Cloud IDにより、Experience Cloud Solutions全体で訪問のデータを共有し、追跡することが可能になります。この記事では、iQタグ管理（TiQ）プロファイルでタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/adobe-experience-cloud-id-service-tag/
---
Cloud ID Serviceタグは、Cloud IDが必要な他のAdobeタグ（Appmeasurement、JavaScript、Heartbeatなど）よりも先にロードすることが重要です。すべてのページでタグをバンドルし、Tagsタブで他のAdobeタグよりも上に配置します。これがCloud IDが他のAdobeタグがページ上でロードされる前にアクセス可能であることを確保する最善の方法です。

## サポートされているバージョン

* v5.5 (最新および推奨)
* v5.4
* v5.3
* v5.2 
* v4.4
* v4.3
* v4.1
* v3.0

## Adobe Web SDK Opt-inモジュール

Adobe AnalyticsはWeb SDKバージョン4.0.0でOpt-inモジュールを導入しました。Opt-inモジュールは、ユーザーの同意を確認し、強制するメカニズムを提供し、GDPRやCCPAなどのプライバシー法を遵守するために重要です。バージョン5.2.0でエンリッチメントされたチェックにより、Adobeツールが実行するための必要な許可があることを確認します。

Experience Cloud ID Serviceタグのバージョン4.0以降を使用している場合、タグを構成した後にOpt-inモジュールを有効にする必要があります。そうしないと、イベントデータはTealiumに送信されません。詳細については、[Adobe Web SDK Opt-inモジュールを有効にする]()を参照してください。

## タグ構成

まず、タグマーケットプレイスに移動し、プロファイルにExperience Cloud ID Serviceタグを追加します（[タグを追加する]()を参照）。

タグを追加したら、以下の構成を行います：

* **Adobe Org ID**
  * (必須) あなたの組織に割り当てられた英数字のExperience Cloud IDを入力します。
  * 大文字と小文字を区別します。
  * 例：`265H7Z562851TTX99W870V12`@AdobeOrg
* **Tracking Server**
  * (必須) Adobe Analyticsデータ収集に使用するドメインを入力します。
  * ここで画像リクエストとクッキーが処理されます。
  * 例：`site.mydomain.com`
* **Tracking Server Secure**
  * (オプション) セキュアなトラッキングサーバーを使用している場合、このフィールドにURLを入力します。
* **Experience Cloud Server**
  * (オプション) 第三者のコンテキストでファーストパーティクッキーを利用するためのファーストパーティデータ収集（CNAME）を使用している場合、このフィールドにトラッキングサーバーのURLを入力します。
* **Experience Cloud Server Secure**
  * (オプション) セキュアなExperience Cloud Serverを使用している場合、このフィールドにURLを入力します。
* **Code Version**
  * (必須) バージョン3.0以降は、Internet Explorerのバージョン6から9をサポートしていません。

タグ構成を動的に構成する場合は、データマッピング（下記参照）を使用します。

## ロードルール

[ロードルール]()は、このタグのインスタンスをサイトのどこで、いつロードするかを決定します。

推奨されるロードルール：**すべてのページでロード**。

## データマッピング

マッピングは、[データレイヤー変数]()からのデータをベンダータグの対応する宛先変数に送信するプロセスです。変数をタグ宛先にマッピングする方法については、[データマッピング]()を参照してください。

Cloud ID Serviceタグの宛先変数は、そのデータマッピングタブに組み込まれています。利用可能なカテゴリーは以下の通りです：

### 標準

| **変数** |**宛先名**| **説明**|
|---| ---| --- |
|`adobe_org_id`| Adobe Org ID|  あなたの会社のExperience Cloud Solutionに割り当てられた英数字のID。 |
|`config.trackingServer`|Tracking Server|  データ収集サーバーのURL。 |
|`config.trackingServerSecure`| Tracking Server Secure| セキュアなデータ収集サーバーのURL。 |
|`config.marketingCloudServer`|Experience Cloud Server|  CNAMEが有効になっている場合のデータ収集サーバーのURL。 |
| config.marketingCloudServerSecure |Experience Cloud Server Secure|  CNAMEが有効になっている場合のデータ収集サーバーのURL。 |

### 顧客ID

追加の顧客識別子を送信するためのこれらの宛先にマッピングします。

宛先をマッピングするための次の手順を使用します：

1. **プロパティ**リストから顧客プロパティを選択します。
1. **Customer ID**フィールドに、マッピングされる変数の値を入力します。  
データレイヤーであなたの提供した値が見つかったときにプロパティが送信されます。  

|**プロパティ名**| **タイプ** | **説明**|
|:------------|:------------|:------------|
|`ID`|  String | 同じ訪問のための追加ID。 |
|`authState`| Integer |  認証状態を示します。可能な値は次のとおりです：  &lt;ul&gt;&lt;li&gt;`0` は未知または未認証を意味します&lt;/li&gt;&lt;li&gt;`1` は認証済みを意味します&lt;/li&gt;&lt;li&gt;`2` はログアウトを意味します&lt;/li&gt;&lt;/ul&gt; |

### イベント
イベントをマッピングするには、[イベントマッピングの作成]()を参照してください。

| **変数** | **タイプ** | **説明** |
|:---------|:------------|:------------|
| `setCustomerID` | String | 顧客IDを構成 |

## Adobe Web SDK Opt-inモジュールを有効にする

Experience Cloud ID Serviceタグのバージョン4.0以降を使用している場合、イベントデータがTealiumに送信されるためには、`doesOptInApply`オプションを`true`に構成する必要があります。`doesOptInApply`を構成するには、Adobe Experience Cloud ID Serviceタグにスコープを持つJavaScript拡張を作成します：

1. **iQタグ管理 &gt; 拡張機能**に移動します。
1. **Advanced**タブをクリックし、**JavaScript Code**の**&#43; Add**をクリックします。
1. **Scope**で、**Tag Scoped Extensions**を選択し、**Adobe Experience Cloud ID Service**を選択します。
1. **Configuration**の下に、次のコードを入力します：  
    ```js
    u.data.config = u.data.config || {};
    u.data.config[&#39;doesOptInApply&#39;] = true;
    u.data.config[&#39;preOptInApprovals&#39;] = [&#39;aa&#39;, &#39;ecid&#39;];
    u.data.config[&#39;isIabContext&#39;] = false;
    u.data.config[&#39;optInStorageExpiry&#39;] = 34128000; 
    ```  
    以下の図は、Adobe Opt-inモジュールを有効にする拡張の構成例を示しています：  
    ![](/images/client-side-tags/adobe-enable-optin-module-extension-example.png)
1. 保存し、公開します。

Opt-inサービスが期待通りに動作しているかどうかは、ブラウザの開発者ツールを使用して確認できます。詳細については、Adobeのドキュメンテーションの[Opt-in Serviceの検証](https://experienceleague.adobe.com/en/docs/id-service/using/implementation/opt-in-service/testing-optin-and-iab-plugin)を参照してください。

Adobe AnalyticsとAdobe Experience CloudのイベントデータがTealiumに送信されていることを確認するために、Live Eventsを使用します。詳細については、[Live Eventsについて]()を参照してください。

## ベンダードキュメンテーション

* [Adobe Experience Cloud ID Service](https://experienceleague.adobe.com/en/docs/id-service/using/home)
* [Opt-in Serviceの検証](https://experienceleague.adobe.com/en/docs/id-service/using/implementation/opt-in-service/testing-optin-and-iab-plugin)
* [顧客IDと認証状態](https://experienceleague.adobe.com/en/docs/id-service/using/reference/authenticated-state)
* [アナリティクストラッキングサーバーの使用](https://experienceleague.adobe.com/en/docs/target/using/integrate/a4t/analytics-tracking-server)