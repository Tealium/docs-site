---
title: AppsFlyerアプリイベントコネクタ構成ガイド
description: この記事では、Customer Data HubアカウントでAppsFlyerアプリイベントコネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/appsflyer-app-events-connector/
---
## コネクタアクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
| インストールを追跡 | ✓ | ✓ |
| アプリ内イベントを追跡 | ✓ | ✓ |
| アプリ内イベントを追跡（SDKクライアント） | ✓ | ✓ |

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、以下の項目を構成します。

* **App ID**
  * データの送信先となるアプリのAppsFlyer App IDです。
* **Dev Key**
  * **AppsFlyer**ダッシュボードの**App Settings**画面に表示されるアカウントの開発者キーです。
* **S2S Key**  
サーバー間通信を使用してデータを送信するためのトークンです。詳細については、[AppsFlyer：AppsFlyerトークンの管理](https://support.appsflyer.com/hc/en-us/articles/360004562377-Managing-AppsFlyer-tokens)を参照してください。

S2S Keyは、アクセスを有効にするために使用します。詳細については、[AppsFlyer：APIおよびサーバー間通信用S2Sトークンの管理](https://support.appsflyer.com/hc/en-us/articles/360004562377-Managing-API-and-Server-to-server-S2S-tokens)を参照してください。

## アクション

アクション名を入力し、ドロップダウンメニューからアクションタイプを選択します。

以下のセクションでは、各アクションのパラメータとオプションを構成する方法について説明します。

### インストールを追跡

#### パラメータ

Platform Dataパラメータは必須です。Apple Search AdsパラメータとCustom Dataパラメータは任意です。
##### プラットフォームデータ

| **パラメーター** | **プラットフォーム** | **説明** |
|---|---|---|
| 広告ID有効化フラグ | すべて | （必須）ユーザーをAppsFlyerAnalyticsの対象外にするには、このパラメーターを`false`に構成します。AppsFlyerAnalyticsの対象にするには、フラグを`true`に構成します。 |
| アプリ起動カウンター | すべて | （必須）初回起動アトリビューションの場合は、このパラメーターを`1`または`2`に構成します。リターゲティングの場合は、`3`以上に構成します。 |
| デバイス広告ID | AndroidまたはWindows | （必須）デバイスの広告ID。例：`caf5555d48f22222d34f03bcd7ab333b`。 |
| デバイスのIPアドレス | すべて | （必須）デバイスのIPアドレス。 |
| デバイスのロケール | すべて | （必須）デバイスのロケール。例：`en-US`。 |
| デバイスのタイプ／モデル | すべて | （必須）デバイスのタイプまたはモデル。 |
| インストール日 | すべて | （必須）デバイス上でのアプリケーションの初回起動日時またはインストール日時（ISO 8601 UTC形式）。例：`2015-01-22T08:45:33.412`。 |
| iOS広告ID | iOS | （必須）広告主向けOS ID（`advertisingIdentifier`）。SHA1でハッシュ化できます。例：`AC9FB4FB-AAAA-BBBB-88E6-2840D9BB17F4`。 |
| OSバージョン | すべて | （必須）オペレーティングシステムのバージョン。 |
| 一意のユーザーID | すべて | （必須）一意のユーザーID。例：`1b1758cd-c22b-461e-924e-ceb0c7f849aa`。 |
| ユーザーエージェント | すべて | （必須）アプリケーションのユーザーエージェント。 |
| アプリバンドルID | iOS | アプリのバンドルID。例：`com.company.appname`。 |
| 顧客ユーザーID | iOSおよびAndroid | 開発者が構成した顧客ユーザーID。広告主のシステムでは、これをユーザー識別子として使用します。例：`3d4d05e5-9ae4-4755-9363-8166568f7935`。 |
| デバイスのIMEI | Android | デバイスのIMEI（国際移動体装置識別番号）。SHA1でハッシュ化できます。 |
| デバイスのAndroid ID | Android | デバイスのAndroid ID。SHA1でハッシュ化できます。 |
| FacebookトラッキングCookie値 | AndroidおよびWindows | FacebookトラッキングCookieの値。 |
| 完全なディープリンクURL | すべて | トラッキング呼び出しの完全なディープリンクURL。例：`myapp://page/1?param1=val1`。 |
| Google Playリファラー | Android | Google Playレシーバーから受信した、URLエンコードされていないリファラー。例：`af_tranid=1A4F123KJHG73F0P&c=c1&pid=MediaSource1`。 |
| Microsoft Storeリファラー | Windows | Microsoft Storeから受信した、URLエンコードされていないWindowsリファラー。例：`af_tranid=1A4F123KJHG73F0P`。 |
| ベンダー向けiOS識別子        | iOS                 | ベンダー向けのiOS識別子。例：`95C9BD22-4A4C-41C8-9548-ED07C5C8C145`。                                                                                                                                                                                                                                                                                |
| App Tracking Transparency        | iOS 14以降    | ユーザーがIDFAの使用をオプトアウトしたかどうかを示すには、このパラメーターを構成します。<ul><li>`0`：未決定。</li><li>`1`：制限。</li><li>`2`：拒否。</li><li>`3`：許可。</li></ul> 詳細については、[Apple：ATTrackingManager.AuthorizationStatus](https://developer.apple.com/documentation/apptrackingtransparency/attrackingmanager/authorizationstatus/)を参照してください。 |
| アプリタイプ                         | iOS                 | App Clipのインストールであるかどうか。                                                                                                                                                                                                                                                                                                                                        |
| Open Anonymous Device Identifier | Android             | Open Anonymous Device Identifier。例：`57cfbf44-edfc-9f25-7fcf-7 3fdffc59929`。                                                                                                                                                                                                                                                                            |
| Amazon広告ID            | Android             | Amazonデバイス固有の広告ID。例：`24c5f114-7718-4a12-97d9-1273397be3c6`。                                                                                                                                                                                                                                                                      |
| アプリストア                        | Android             | アプリをダウンロードしたストア。                                                                                                                                                                                                                                                                                                                           |

##### アプリIDのオーバーライド

コネクター構成画面で構成した**アプリID**をオーバーライドするには、このフィールドを使用します。

##### 開発者キーのオーバーライド

コネクター構成画面で構成した**開発者キー**をオーバーライドするには、このフィールドを使用します。

##### Apple Search Ads

| **パラメーター**       | **説明**          |
|:--------------------|:-------------------------|
| iad-adgroup-id      | 広告IDの広告グループID。          |
| iad-adgroup-name    | 広告IDの広告グループ名。        |
| iad-attribution     | 広告IDのアトリビューション。       |
| iad-campaign-id     | 広告IDのキャンペーンID。       |
| iad-campaign-name   | 広告IDのキャンペーン名。     |
| iad-click-date      | 広告IDのクリック日。        |
| iad-conversion-date | 広告IDのコンバージョン日。   |
| iad-keyword         | 広告IDのキーワード。           |
| iad-lineitem-id     | 広告IDのラインアイテム。         |
| iad-lineitem-name   | 広告IDのラインアイテム名。    |
| iad-org-name        | 広告IDの組織名。 |

##### カスタムデータ

イベントメッセージに任意のカスタム情報を追加するには、このセクションを使用します。

### アクション - アプリ内イベントの追跡

#### パラメーター

**プラットフォームデータ**および**イベントデータ**のパラメーターは必須です。**カスタムデータ**のパラメーターは任意です。

##### プラットフォームデータ

このアクションでは、「インストールの追跡」アクションと同じ**プラットフォームデータ**パラメーターを使用します。

##### イベントデータ

| **パラメーター**         | **説明**                                                                                                                                                                      |
|:----------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| イベント通貨        | <ul><li>イベントのデフォルト通貨</li><li>`USD`にのみ使用します。その他の通貨については、`af_currency`キーを使用して**イベントプロパティ**（`event_value`）セクション内にマッピングしてください。</li></ul> |
| イベント名 | （必須）イベント名を表す文字列。例：`af_purchase`。                                                                                                                      |

##### カスタムデータ

イベントメッセージに任意のカスタム情報を追加するには、このセクションを使用します。

### アプリ内イベントの追跡（SDKクライアント）

AppsFlyer SDKがインストールされており、アプリ外で発生したモバイルイベントを送信する場合は、このアクションを使用します。

#### プラットフォームデータ

| **パラメーター** | **プラットフォーム**   |**説明** |
| --- | --- |--- |
| AppsFlyer ID | すべて | （必須）アプリの初回起動時にAppsFlyerによって生成される一意の識別子。 |
| 広告ID | Android | デバイスの広告ID。 |
| Open Anonymous Device Identifier | Android | Open Anonymous Device Identifier。 |
| Amazon広告ID | Android | Amazon広告ID。 |
| デバイスIMEI | Android | デバイスのIMEI。SHA1でハッシュ化できます。 |
| iOS広告ID | iOS | 広告主向けOS ID（`advertisingIdentifier`）。SHA1でハッシュ化できます。 |
| ベンダー向けiOS識別子 | iOS | ベンダー向けのiOS識別子。 |
| 広告ID有効化フラグ | iOS | ユーザーが広告IDの共有をオプトアウトしたかどうかを示すには、このブール値フラグを使用します。 |
| App Tracking Transparency | iOS 14以降 | ユーザーがIDFAの使用をオプトアウトしたかどうかを示すには、このパラメーターを構成します。<ul><li>`0`：未決定。</li><li>`1`：制限。</li><li>`2`：拒否。</li><li>`3`：許可。</li></ul> 詳細については、[Apple：ATTrackingManager.AuthorizationStatus](https://developer.apple.com/documentation/apptrackingtransparency/attrackingmanager/authorizationstatus/)を参照してください。 |
| アプリストア | すべて             | App Clipのインストールであるかどうか。 |
| アプリタイプ | すべて             | ユーザーイベントが`app_clip`で発生する場合は、このパラメーターを送信します。それ以外の場合は送信しないでください。 |
| アプリバージョン名 | すべて             | アプリのバージョン名。 |
| バンドル識別子 | すべて             | アプリ固有の識別子。RAWデータでは、このパラメーターが**バンドルID**に入力されます。 |
| 顧客ユーザーID | すべて             | 開発者が構成した顧客ユーザーID。広告主のシステムでユーザー識別子として使用されます。 |
| イベント時刻 | すべて             | UTCタイムゾーンを使用したイベント発生時刻。構成されていない場合、AppsFlyerはイベントの受信時刻を使用します。 |
| IPアドレス | すべて             | イベント発生時のモバイルデバイスのIPアドレス。送信された場合、IPアドレスは位置情報フィールドへの入力に使用されます。送信されなかった場合、AppsFlyerはインストールアトリビューションイベントの値を使用して位置情報フィールドに入力します。 |
| オペレーティングシステム | すべて             | デバイスのオペレーティングシステムのバージョン。 |
| 共有フィルター | すべて             | 共有フィルターは、ポストバック/APIを介した統合パートナーおよびその他のサードパーティ統合へのS2Sイベントの共有をブロックします。すべてのパートナーをブロックするには、`all`に構成します。特定のパートナーをブロックするには、パートナーIDの配列を渡します。 |

#### イベントデータ

| **パラメーター** | **説明** |
| --- | --- |
| イベント名 | （必須）イベント名を表す文字列。例：`af_purchase`。 |
| イベント通貨 | イベントのデフォルト通貨。例：`USD`。 |
| カスタムデータ | イベントメッセージに追加のカスタム情報を追加するには、このセクションを使用します。 |