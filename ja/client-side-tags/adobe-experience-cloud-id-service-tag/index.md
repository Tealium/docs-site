---
title: Adobe Experience Cloud ID Serviceタグ構成ガイド
description: AdobeのExperience Cloud ID Serviceタグは、サイト訪問ごとにCloud IDと呼ばれる一意の識別子を生成します。Cloud IDを使用すると、Experience Cloudソリューション間で訪問のデータを共有および追跡できます。この記事では、Tag Managementプロファイルでタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/adobe-experience-cloud-id-service-tag/
---

<blockquote>
Cloud IDを必要とする他のAdobeタグ（AppMeasurement、JavaScript、Heartbeatなど）より前に、Cloud ID Serviceタグを読み込むことが重要です。このタグをすべてのページにバンドルし、**Tags**タブで他のすべてのAdobeタグより上に配置してください。これにより、ページ上で他のAdobeタグが読み込まれる前にCloud IDを確実に利用できるようになります。
</blockquote>


## サポートされているバージョン

* v5.5（最新かつ推奨）
* v5.4
* v5.3
* v5.2 
* v4.4
* v4.3
* v4.1
* v3.0

## Adobe Web SDKのオプトインモジュール

Adobe Analyticsでは、Web SDKバージョン4.0.0でオプトインモジュールが導入されました。オプトインモジュールは、ユーザーの同意を確認して適用するための仕組みを提供します。これは、GDPRやCCPAなどのプライバシー法を遵守するうえで極めて重要です。バージョン5.2.0でエンリッチメントされたチェックにより、Adobeツールの実行に必要な権限が付与されていることが確認されます。

Experience Cloud ID Serviceタグのバージョン4.0以降を使用している場合は、タグの構成後にオプトインモジュールを有効にする必要があります。有効にしないと、イベントデータはTealiumに送信されません。詳細については、[Adobe Web SDKのオプトインモジュールを有効にする]()を参照してください。

## タグの構成

まず、タグマーケットプレイスに移動し、Experience Cloud ID Serviceタグをプロファイルに追加します（[タグの追加](https://docs.tealium.com/manage-tags/#add-a-tag)を参照）。

タグを追加する際は、以下の構成を行います。

* **Adobe Org ID**
  * （必須）組織に割り当てられた英数字のExperience Cloud IDを入力します。
  * 大文字と小文字が区別されます。
  * 例：`265H7Z562851TTX99W870V12`@AdobeOrg
* **Tracking Server**
  * （必須）Adobe Analyticsのデータ収集に使用するドメインを入力します。
  * 画像リクエストとCookieはここで処理されます。
  * 例：`site.mydomain.com`
* **Tracking Server Secure**
  * （任意）セキュアトラッキングサーバーを使用している場合は、このフィールドにURLを入力します。
* **Experience Cloud Server**
  * （任意）サードパーティコンテキストでファーストパーティCookieを利用するためにファーストパーティデータ収集（CNAME）を使用している場合は、このフィールドにトラッキングサーバーのURLを入力します。
* **Experience Cloud Server Secure**
  * （任意）セキュアなExperience Cloud Serverを使用している場合は、このフィールドにURLを入力します。
* **Code Version**
  * （必須）バージョン3.0以降では、Internet Explorerバージョン6～9はサポートされなくなりました。


<blockquote>
タグの構成を動的に構成する場合は、Data Mappings（以下を参照）を使用してください。
</blockquote>


## ロードルール

[ロードルール](https://docs.tealium.com/about-load-rules/)は、サイト上でこのタグのインスタンスをいつ、どこで読み込むかを決定します。

推奨ロードルール：**すべてのページで読み込む**。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

Cloud ID Serviceタグの宛先変数は、その**Data Mapping**タブに組み込まれています。使用可能なカテゴリは以下のとおりです。

### 標準

| **変数** | **宛先名** | **説明** |
|---|---|---|
|`adobe_org_id`| Adobe Org ID | 会社のExperience Cloudソリューションに割り当てられた英数字のID。 |
|`config.trackingServer`|Tracking Server| データ収集サーバーのURL。 |
|`config.trackingServerSecure`| Tracking Server Secure| セキュアなデータ収集サーバーのURL。</li></ul> |
|`config.marketingCloudServer`|Experience Cloud Server| CNAMEが有効な場合のデータ収集サーバーのURL。 |
| config.marketingCloudServerSecure |Experience Cloud Server Secure| CNAMEが有効な場合のデータ収集サーバーのURL。 |

### 顧客ID

追加の顧客識別子を送信するには、これらの宛先にマッピングします。

以下の手順で宛先をマッピングします。

1. **Property**リストから顧客プロパティを選択します。
1. **Customer ID**フィールドに、マッピングする変数の値を入力します。  
指定した値がデータレイヤー内で見つかると、プロパティが送信されます。  

| **プロパティ名** | **型** | **説明** |
|:------------|:------------|:------------|
|`ID`| String | 同じ訪問に対する追加のID。 |
|`authState`| Integer | 認証ステータスを示します。指定可能な値は次のとおりです。<ul><li>`0`：不明または未認証</li><li>`1`：認証済み</li><li>`2`：ログアウト済み</li></ul> |

### イベント

イベントをマッピングする方法については、[イベントマッピングの作成](https://docs.tealium.com/manage-data-mappings/#add-an-event-mapping)を参照してください。

| **変数** | **型** | **説明** |
|:---------|:------------|:------------|
| `setCustomerID` | String | 顧客IDを構成 |

## Adobe Web SDKのオプトインモジュールを有効にする

Experience Cloud ID Serviceタグのバージョン4.0以降を使用している場合、イベントデータをTealiumに送信するには、`doesOptInApply`オプションを`true`に構成する必要があります。`doesOptInApply`を構成するには、次の手順に従って、Adobe Experience Cloud ID ServiceタグをスコープとするJavaScript拡張機能を作成します。

1. **Tag Management > Extensions**に移動します。
1. **Advanced**タブをクリックし、**JavaScript Code**の**+ Add**をクリックします。
1. **Scope**で**Tag Scoped Extensions**を選択し、次に**Adobe Experience Cloud ID Service**を選択します。
1. **Configuration**に、次のコードを入力します。  
    ```js
    u.data.config = u.data.config || {};
    u.data.config['doesOptInApply'] = true;
    u.data.config['preOptInApprovals'] = ['aa', 'ecid'];
    u.data.config['isIabContext'] = false;
    u.data.config['optInStorageExpiry'] = 34128000; 
    ```  
    次の図は、Adobeオプトインモジュールを有効にする拡張機能の構成例を示しています。  
    ![](https://docs.tealium.com/images/client-side-tags/adobe-enable-optin-module-extension-example.png)
1. 保存してパブリッシュします。

ブラウザーの開発者ツールを使用して、オプトインサービスが想定どおりに動作していることを検証できます。詳細については、Adobeのドキュメントの[オプトインサービスの検証](https://experienceleague.adobe.com/en/docs/id-service/using/implementation/opt-in-service/testing-optin-and-iab-plugin)を参照してください。

Live Eventsを使用して、Adobe AnalyticsとAdobe Experience CloudのイベントデータがTealiumに送信されていることを確認します。詳細については、[Live Eventsについて]()を参照してください。

## ベンダーのドキュメント

* [Adobe Experience Cloud ID Service](https://experienceleague.adobe.com/en/docs/id-service/using/home)
* [オプトインサービスの検証](https://experienceleague.adobe.com/en/docs/id-service/using/implementation/opt-in-service/testing-optin-and-iab-plugin)
* [顧客IDと認証状態](https://experienceleague.adobe.com/en/docs/id-service/using/reference/authenticated-state)
* [Analyticsトラッキングサーバーの使用](https://experienceleague.adobe.com/en/docs/target/using/integrate/a4t/analytics-tracking-server)