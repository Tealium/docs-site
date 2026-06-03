---
title: AppsFlyerアプリイベントコネクタ構成ガイド
description: この記事では、Customer Data HubアカウントでAppsFlyerアプリイベントコネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/appsflyer-app-events-connector/
---
## コネクタのアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
| インストールを追跡 | ✓ | ✓ |
| アプリ内イベントを追跡 | ✓ | ✓ |
| アプリ内イベントを追跡 (SDKクライアント) | ✓ | ✓ |


## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタについて]()を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **App ID**
  * これは、データを渡しているアプリのAppsFlyer App IDです。
* **Dev Key**
  * **AppsFlyer**ダッシュボードの**App Settings**画面から取得したアカウントのdev keyです。
* **S2S Key**  
サーバー間通信でデータを送信するために使用されるトークンです。詳細については、[AppsFlyer: AppsFlyerトークンの管理](https://support.appsflyer.com/hc/en-us/articles/360004562377-Managing-AppsFlyer-tokens)を参照してください。

S2S Keyはアクセスを有効にするために使用されます。詳細については、[AppsFlyer: APIとサーバー間S2Sトークンの管理](https://support.appsflyer.com/hc/en-us/articles/360004562377-Managing-API-and-Server-to-server-S2S-tokens)を参照してください。

## アクション

アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### インストールを追跡

#### パラメータ

Platform Dataパラメータは必須です。Apple Search AdsとCustom Dataパラメータはオプションです。

##### Platform Data

| **パラメータ** | **プラットフォーム** | **説明** |
|---| ---| ---|
| Ad ID Enabled Flag (必須)    | すべて                 | このパラメータを`false`に構成してAppsFlyerAnalyticsからユーザーをオプトアウトします。フラグを`true`に構成してAppsFlyerAnalyticsにオプトインします。                                                                                                                                                                                                                                                                                               |
| App Open Counter (必須)      | すべて                 | このパラメータを`1`または`2`に構成して初回起動のアトリビューションを行い、`3`以上に構成してリターゲティングを行います。                                                                                                                                                                                                                                                             |
| Device Advertising ID (必須) | AndroidまたはWindows  | デバイスの広告ID。例えば、`caf5555d48f22222d34f03bcd7ab333b`。                                                                                                                                                                                                                                                                                          |
| Device IP Address (必須)     | すべて                 | デバイスのIPアドレス。                                                                                                                                                                                                                                                                                                                                               |
| Device Locale (必須)         | すべて                 | デバイスのロケール。例えば、`en-US`。                                                                                                                                                                                                                                                                                                                             |
| Device Type/Model (必須)     | すべて                 | デバイスのタイプまたはモデル。                                                                                                                                                                                                                                                                                                                                            |
| Install Date (必須)          | すべて                 | デバイス上のアプリケーションの初回起動日またはインストール日。ISO 8601 UTC形式。例えば、`2015-01-22T08:45:33.412`。                                                                                                                                                                                                                                |
| iOS Ad ID (必須)             | iOS                 | 広告主向けのOS ID (`advertisingIdentifier`)。SHA1ハッシュ化可能。例えば、`AC9FB4FB-AAAA-BBBB-88E6-2840D9BB17F4`。                                                                                                                                                                                                                                    |
| OS Version (必須)            | すべて                 | オペレーティングシステムのバージョン。                                                                                                                                                                                                                                                                                                                                          |
| Unique User ID (必須)        | すべて                 | ユニークなユーザーID。例えば、`1b1758cd-c22b-461e-924e-ceb0c7f849aa`。                                                                                                                                                                                                                                                                                               |
| User Agent (必須)            | すべて                 | アプリケーションのユーザーエージェント。                                                                                                                                                                                                                                                                                                                                          |
| App Bundle ID                    | iOS                 | アプリのバンドルID。例えば、`com.company.appname`。                                                                                                                                                                                                                                                                                                                 |
| Customer User ID                 | IOSとAndroid     | 開発者が構成したカスタマーユーザーID。広告主のシステムはこれをユーザー識別子として使用します。例えば、`3d4d05e5-9ae4-4755-9363-8166568f7935`。                                                                                                                                                                                                      |
| Device IMEI                      | Android             | デバイスのIMEI（International Mobile Equipment Identity）。SHA1ハッシュ化可能。                                                                                                                                                                                                                                                                                                                           |
| Device Android ID                | Android             | デバイスのAndroid ID。SHA1ハッシュ化することができます。                                                                                                                                                                                                                                                                                                                     |
| Facebook Tracking Cookie Value   | Android and Windows | Facebook Tracking Cookieの値。                                                                                                                                                                                                                                                                                                                                  |
| Full DeepLink URL                | All                 | トラッキングコールの完全なDeepLink URL。例えば、`myapp://page/1?param1=val1`。                                                                                                                                                                                                                                                                                  |
| Google Play Referrer             | Android             | Google Playレシーバーから受け取ったリファラー、URLエンコーディングなし。例えば、`af_tranid=1A4F123KJHG73F0P&amp;c=c1&amp;pid=MediaSource1`。                                                                                                                                                                                                                                |
| Microsoft Store Referrer           | Windows             | Microsoft Storeから受け取ったWindowsリファラー、URLエンコーディングなし。例えば、`af_tranid=1A4F123KJHG73F0P`。                                                                                                                                                                                                                                                     |
| iOS Identifier for Vendor        | iOS                 | ベンダーのiOS識別子。例えば、`95C9BD22-4A4C-41C8-9548-ED07C5C8C145`。                                                                                                                                                                                                                                                                                |
| App Tracking Transparency        | iOS 14 and above    | ユーザーがIDFAの使用をオプトアウトしたかどうかを示すためにこのパラメータを構成します:  &lt;ul&gt;&lt;li&gt;`0`: 未決定。&lt;/li&gt;&lt;li&gt;`1`: 制限。&lt;/li&gt;&lt;li&gt;`2`: 拒否。&lt;/li&gt;&lt;li&gt;`3`: 許可。&lt;/li&gt;&lt;/ul&gt;  詳細は、[Apple: ATTrackingManager.AuthorizationStatus](https://developer.apple.com/documentation/apptrackingtransparency/attrackingmanager/authorizationstatus/)を参照してください。 |
| App Type                         | iOS                 | これがアプリクリップのインストールであるかどうか。                                                                                                                                                                                                                                                                                                                                        |
| Open Anonymous Device Identifier | Android             | Open Anonymous Device Identifier。例えば、`57cfbf44-edfc-9f25-7fcf-7 3fdffc59929`。                                                                                                                                                                                                                                                                            |
| Amazon Advertising ID            | Android             | Amazonデバイスのユニークな広告ID。例えば、`24c5f114-7718-4a12-97d9-1273397be3c6`。                                                                                                                                                                                                                                                                      |
| App Store                        | Android             | アプリがダウンロードされたストア。                                                                                                                                                                                                                                                                                                                           |

##### App ID Override

このフィールドを使用して、コネクタ構成画面で構成した**App ID**を上書きします。

##### Dev Key Override

このフィールドを使用して、コネクタ構成画面で構成した**Dev Key**を上書きします。

##### Apple Search Ads

| **パラメータ**       | **説明**          |
|:--------------------|:-------------------------|
| iad-adgroup-id      | Ad IDグループID。          |
| iad-adgroup-name    | Ad IDグループ名。        |
| iad-attribution     | Ad ID属性。       |
| iad-campaign-id     | Ad IDキャンペーンID。       |
| iad-campaign-name   | Ad IDキャンペーン名。     |
| iad-click-date      | Ad IDクリック日。        |
| iad-conversion-date | Ad IDコンバージョン日。   |
| iad-keyword         | Ad IDキーワード。           |
| iad-lineitem-id     | Ad IDラインアイテム。         |
| iad-lineitem-name   | Ad IDラインアイテム名。    |
| iad-org-name        | Ad ID組織名。 |

##### Custom Data

このセクションを使用して、イベントメッセージにカスタマイズされた情報を追加します。

### Action - Track in App Event

#### Parameters

**Platform Data**と**Event Data**パラメータは必須です。**Custom Data**パラメータはオプションです。

##### Platform Data

このアクションは、Track Installアクションと同じ**Platform Data**パラメータを使用します。

##### Event Data

| **パラメータ**         | **説明**                                                                                                                                                                      |
|:----------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Event Currency        | &lt;ul&gt;&lt;li&gt;イベントのデフォルト通貨&lt;/li&gt;&lt;li&gt;`USD`のみ使用し、他のすべての通貨は、**Event Properties** (`event_value`)セクションで`af_currency`キーを使用してマッピングします。&lt;/li&gt;&lt;/ul&gt; |
| Event Name (required) | イベント名を表す文字列。例えば、`af_purchase`。                                                                                                                      |

##### Custom Data

このセクションを使用して、イベントメッセージにカスタマイズされた情報を追加します。

### Track In App Event (SDK Clients)

AppsFlyer SDKがインストールされていて、アプリの外で発生するモバイルイベントを送信したい場合にこのアクションを使用します。

#### Platform Data

| **パラメータ** | **プラットフォーム**   |**説明** |
| --- | --- |--- |
| Appsflyer ID | All |  (必須) アプリが初めて起動したときにAppsFlyerが生成する一意の識別子。 |
| Advertising ID | Android | デバイスの広告ID。 |
| Open Anonymous Device Identifier | Android | Open Anonymous Device Identifier。  |
| Amazon Advertising ID | Android | Amazon Advertising ID。 |
| Device IMEI | Android | デバイスのIMEI。SHA1ハッシュ化することができます。 |
| iOS Ad ID | IOS | 広告主向けのOS ID (`advertisingIdentifier`)。SHA1ハッシュ化することができます。 |
| iOS Identifier for Vendor | IOS | ベンダーのiOS識別子。 |
| Advertising ID Enabled Flag | IOS | ユーザーが広告主IDの共有をオプトアウトしたかどうかを示すためのブールフラグを使用します。 |
| App Tracking Transparency | IOS 14以降 | ユーザーがIDFAの使用をオプトアウトしたかどうかを示すためにこのパラメータを構成します:  &lt;ul&gt;&lt;li&gt;`0`: 未決定。&lt;/li&gt;&lt;li&gt;`1`: 制限されています。&lt;/li&gt;&lt;li&gt;`2`: 拒否されました。&lt;/li&gt;&lt;li&gt;`3`: 認証済み。&lt;/li&gt;&lt;/ul&gt;  詳細は、[Apple: ATTrackingManager.AuthorizationStatus](https://developer.apple.com/documentation/apptrackingtransparency/attrackingmanager/authorizationstatus/)を参照してください。 |
| App Store | 全て             |これがアプリクリップのインストールであるかどうか。 |
| App Type | 全て             |ユーザーイベントが`app_clip`で発生した場合は、パラメータを送信します。それ以外の場合はパラメータを送信しないでください。 |
| App Version Name | 全て             |あなたの名前付きアプリバージョン。 |
| Bundle Identifier | 全て             |ユニークなアプリ識別子。生データでは、このパラメータは**Bundle ID**を埋めます。 |
| Customer User ID | 全て             |開発者が構成した顧客ユーザーID。これは広告主のシステムでのユーザー識別子として使用されます。 |
| Event Time | 全て             |イベントが発生した時間をUTCタイムゾーンで使用します。構成されていない場合、Appsflyerは着信イベントの時間を使用します。 |
| IP Address | 全て             |イベント発生時のモバイルデバイスのIPアドレス。送信された場合、IPアドレスは地理位置情報フィールドを埋めるために使用されます。送信されなかった場合、AppsFlyerはインストール属性イベントからの値を使用して地理位置情報フィールドを埋めます。 |
| Operating System |  全て             |デバイスのオペレーティングシステムのバージョン。 |
| Sharing Filter |  全て             |共有フィルタは、統合パートナーや他のサードパーティ統合とのポストバック/API経由でのS2Sイベントの共有をブロックします。すべてのパートナーをブロックするには`all`を構成します。特定のパートナーをブロックするには、パートナーIDの配列を渡します。 |

#### イベントデータ

| **パラメータ** | **説明** |
| --- | --- |
| Event Name | (必須) イベント名を記述する文字列。例えば、`af_purchase`。 |
| Event Currency |  イベントのデフォルト通貨。例えば、`USD`。 |
| Custom Data | このセクションを使用して、イベントメッセージに追加のカスタマイズ情報を追加します。 |

