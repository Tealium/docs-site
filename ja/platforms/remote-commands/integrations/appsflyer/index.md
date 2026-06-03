---
title: リモートコマンド：AppsFlyer
description: AndroidおよびSwift/iOSにおけるAppsFlyerのTealiumリモートコマンド統合です。
url: https://docs.tealium.com/ja/platforms/remote-commands/integrations/appsflyer/
---
## 要件

- AppsFlyer [アプリ ID](https://support.appsflyer.com/hc/en-us/articles/207377436#available-in-the-app-store-google-play-store-windows-phone-store) および [デバイス キー](https://support.appsflyer.com/hc/en-us/articles/211719806-App-Settings#sdk-dev-key)
- これらのモバイル ライブラリのうちのいずれか:
  - [Tealium for Android-Kotlin](/ja/platforms/android-kotlin/) (1.0.0 以降)
  - [Tealium for Android-Java](/ja/platforms/android-java/) (5.9.0 以降 (AppsFlyer 1.0.0 以降用) または 5.9.0 以前 (旧バージョン用))
  - [Tealium for iOS-Swift](/ja/platforms/ios-swift/)
- これらのリモート コマンド統合のいずれか:
  - [AppsFlyer Remote Command JSON File](/ja/platforms/remote-commands/integrations/appsflyer/#json-template) (Android-Kotlin 1.0.0 以降または iOS-Swift 2.1.0 以降が必要)
  - AppsFlyerリモート コマンド タグ (Tealium iQ タグ管理)

## 仕組み

AppsFlyer 統合は、これらのアイテムを使用します:

1. AppsFlyer ネイティブ SDK
2. AppsFlyer メソッドをラップするリモート コマンド モジュール
3. イベント トラッキングをネイティブ AppsFlyer コールに翻訳する、JSON 構成ファイルまたは Remote Command タグのいずれか

AppsFlyer リモート コマンド モジュールをアプリに追加すると、必要な AppsFlyer ライブラリが自動的にインストールされ、ビルドされます。この際、ベンダー固有のコードをアプリに追加する必要はありません。依存関係マネージャのインストールを使用している場合、AppsFlyer SDKを個別にインストールする必要はありません。

リモート コマンド オプションは、次の 2 つがあります: A JSON 構成ファイル、または、マッピングを構成するための iQ タグ管理の使用。A JSON 構成ファイルは、リモートでホスティングするか、またはアプリ内でローカルでホスティングするかのいずれでも、ベンダー統合の推奨オプションです。iQ タグ管理を使用する場合は、ベンダー統合用のリモート コマンド タグを追加します。[ベンダー統合](/ja/platforms/remote-commands/how-it-works/#vendor-integrations)の詳細は、こちらから参照してください。

iOS：AppsFlyerバージョン4.8.11以降の場合、SDKはネイティブフレームワーク`AdSupport.framework`および`iAd.framework`を自動的に追加します。詳細については、[AppsFlyer iOS SDK統合](https://support.appsflyer.com/hc/en-us/articles/207032066#integration)に関するガイドを参照してください。

## インストール

### 依存関係マネージャ

次の依存関係マネージャのいずれかをインストールに使用することをお勧めします。




CocoaPodsを使用してiOSのAppsFlyerリモートコマンドをインストールするには：

1. `tealium-swift`と`pod &#34;AppsFlyerFramework&#34;`がPodfileに存在する場合は削除します。`tealium-swift`の依存関係は`TealiumAppsFlyer`フレームワークに既に含まれています。

2. 次の依存関係をPodfileに追加します。
```ruby
pod &#34;TealiumAppsFlyer&#34;
```  
`TealiumAppsFlyer`ポッドには以下の`TealiumSwift`依存関係が含まれています。
```bash
&#39;tealium-swift/Core&#39;
&#39;tealium-swift/RemoteCommands&#39;
&#39;tealium-swift/TagManagement&#39;
```

3. モジュール`TealiumSwift`および`TealiumAppsFlyer`を、`TealiumHelper`ファイル、`Tealium`クラスにアクセスするその他のファイル、またはAppsFlyerリモートコマンドにインポートします。




Carthageを使用してiOSのAppsFlyerリモートコマンドをインストールするには：

1. `tealium-swift`をCartfileから削除します。`tealium-swift`の依存関係は`TealiumAppsFlyer`フレームワークに既に含まれています。

2. 以下の行がCartfileに存在する場合は、その行を削除します。
```bash
`binary &#34;https://raw.githubusercontent.com/AppsFlyerSDK/AppsFlyerFramework/master/AppsFlyerLib.json&#34;`
```

3. 次の依存関係をCartfileに追加します。
```bash
github &#34;tealium/tealium-ios-appsflyer-remote-command&#34;
```

Tealium for Swift SDK (バージョン 1.x) および `TealiumAppsFlyer` バージョン 1.x では、 `TealiumDelegate` モジュールがインストールに含まれている必要があります。






Mavenを使用してAndroidのAppsFlyerリモートコマンドをインストールするには：

1. [Tealium for Android (Kotlin)](/ja/platforms/android-kotlin/install/) または [Tealium for Android (Java)](/ja/platforms/android-java/install/) をインストールして、Tealium Maven URL を、プロジェクトのトップレベル `build.gradle` ファイルに追加します (まだ済んでいない場合)。

    ```groovy
    allprojects {
      repositories {
        mavenCentral()
        maven {
          url &#34;https://maven.tealiumiq.com/android/releases/&#34;
        }
      }
    }
    ```

2. アプリプロジェクトの`build.gradle`ファイルに次の依存関係を追加して、AppsFlyer SDKとTealium-AppsFlyerの両方のリモートコマンドをインポートします。
```groovy
dependencies {
    implementation &#39;com.tealium.remotecommands:appsflyer:1.0.0&#39;
}
```




### 手動による手順（iOS）

AppsFlyer リモート コマンドを手動でインストールするには、 [Tealium for Swift](/ja/platforms/ios-swift/) ライブラリがインストールされている必要があります。iOSプロジェクトのAppsFlyerリモートコマンドをインストールするには：

1. [AppsFlyer SDK](https://github.com/AppsFlyerSDK/AppsFlyerFramework)をまだインストールしていない場合はインストールします。

2. [Tealium iOS AppsFlyerリモートコマンド](https://github.com/tealium/tealium-ios-appsflyer-remote-command)レポジトリをクローンして、`Sources`フォルダ内のファイルをプロジェクトにドラッグします。

3. [`remoteAPIEnabled`](/ja/platforms/ios-swift/api/tealium-config/#remoteapienabled) 構成フラッグを `true`に構成します

### 手動（Android）

AppsFlyer リモート コマンドを手動でインストールするには、 [Tealium for Android (Kotlin)](/ja/platforms/android-kotlin/install/) または [Tealium for Android (Java)](/ja/platforms/android-java/install/) がインストールされている必要があります。AndroidプロジェクトのAppsFlyerリモートコマンドをインストールするには：

1. `flatDir`をプロジェクトのルートにある`build.gradle`ファイルに追加します。
```groovy
allprojects {
      repositories {
         mavenCentral()
         flatDir {
             dirs &#39;libs&#39;
         }
      }
}
```

2. `tealium-appsflyer.aar`を`&lt;PROJECT_ROOT&gt;/&lt;MODULE&gt;/libs`に追加します。

3. Tealiumライブラリの依存関係を`build.gradle`ファイルに追加します。
```groovy
dependencies {
      implementation(name:&#39;tealium-appsflyer&#39;, ext:&#39;aar&#39;)
}
```

## 初期化

すべてのTealiumライブラリについて、初期化時にAppsFlyerリモートコマンドを登録します。

### Android (Kotlin)

Tealium の Android (Kotlin) ライブラリ用の JSON 構成ファイルまたはリモート コマンド タグを用いてリモート コマンドを初期化します。



以下のコードは、ローカル ファイル オプションを使用して、JSON Remote Command 機能とともに用いるために設計されています。
```kotlin
// Sets up a config object and creates a Tealium instance
val config = TealiumConfig(application,
        &#34;ACCOUNT&#34;,
        &#34;PROFILE&#34;,
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands));
var tealium = Tealium.create(TEALIUM_MAIN, config) {
    // New code to add the AppsFlyer Remote Command
    val appsFlyerRemoteCommand = AppsFlyerRemoteCommand(application,
                                      appsFlyerDevKey = devKey)
    // register the command
    remoteCommands?.add(appsFlyerRemoteCommand, filename = &#34;appsflyer.json&#34;);
}
```


以下のコードは、Remote Command タグ機能とともに用いるために設計されています。
```kotlin
// Sets up a config object and creates a Tealium instance
val config = TealiumConfig(application,
        &#34;ACCOUNT&#34;,
        &#34;PROFILE&#34;,
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands));
var tealium = Tealium.create(TEALIUM_MAIN, config) {
    // New code to add the AppsFlyer Remote Command
    val appsFlyer = AppsFlyerRemoteCommand(application,
                                      appsFlyerDevKey = devKey)
    // register the command
    remoteCommands?.add(appsFlyer);
}
```



### Android (Java)



Android 向けの JSON Remote Command ファイル機能は、Kotlin SDK でのみ利用できます。



以下のコードは、Remote Command タグ機能とともに用いるために設計されています。
```java
// Sets up a config object and creates a Tealium instance
Tealium.Config config = Tealium.Config.create(application, &#34;ACCOUNT&#34;, &#34;PROFILE&#34;, &#34;ENVIRONMENT&#34;);
Tealium teal = Tealium.createInstance(TEALIUM_MAIN, config);
    // New code to add the AppsFlyer Remote Command
AppsFlyerRemoteCommand appsFlyer = new AppsFlyerRemoteCommand(application, appsFlyerDevKey = devKey)
teal.addRemoteCommand(appsFlyer);
```



### iOS (Swift)

Tealium の iOS (Swift) ライブラリ用の JSON 構成ファイルまたはリモート コマンド タグを用いてリモート コマンドを初期化します。




以下のコードは、ローカル ファイル オプションを使用して、JSON Remote Command 機能とともに用いるために設計されています。
```swift
var tealium : Tealium?
let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                           profile: &#34;PROFILE&#34;,
                           environment: &#34;ENVIRONMENT&#34;,
                           dataSource: &#34;DATASOURCE&#34;,
                           optionalData: nil)

config.remoteAPIEnabled = true // Required to use Remote Commands

tealium = Tealium(config: config) { _ in
    guard let remoteCommands = self.tealium?.remoteCommands else {
        return
    }

	let appsflyer = AppsFlyerRemoteCommand(type: .local(file: &#34;appsflyer&#34;))
	remoteCommands.add(appsflyer)
}
```




以下のコードは、Remote Command タグ機能とともに用いるために設計されています。
```swift
var tealium : Tealium?
let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                           profile: &#34;PROFILE&#34;,
                           environment: &#34;ENVIRONMENT&#34;,
                           dataSource: &#34;DATASOURCE&#34;,
                           optionalData: nil)

config.remoteAPIEnabled = true // Required to use Remote Commands

tealium = Tealium(config: config) { _ in
    guard let remoteCommands = self.tealium?.remoteCommands else {
        return
    }

	let appsFlyer = AppsFlyerRemoteCommand()
	remoteCommands.add(appsFlyer)
}

```




## プッシュメッセージトラッキング

Tealium Swiftライブラリには、Tealium と AppsFlyer リモート コマンドを介してプッシュ メッセージ トラッキングに対処するための `TealiumRegistration` プロトコルが含まれています。Tealium は ラッパー クラス `AppsFlyerInstance` でこのプロトコルに準拠し、プッシュ メッセージ認証イベントとプッシュ メッセージ オープン イベントの送信、およびトラッキングのアンインストールにこのプロトコルを使用しています。プッシュメッセージトラッキング機能を利用することをお勧めします。

iOSプロジェクトのプッシュメッセージトラッキングを統合するには、次の手順を実行します。

1. `TealiumHelper.swift`ファイルで、`TealiumRegistration`プロトコルに準拠しているオブジェクトの空の配列を初期化します。例：
```swift
var pushMessagingTrackers = [TealiumRegistration]()
```
2. `AppsFlyerRemoteCommand`の前に `AppsFlyerInstance` を初期化します
3. 前述の配列に `AppsFlyerInstance` を追加します

以下は、プッシュメッセージトラッキング統合の例の全文です。

```swift
var pushMessagingTrackers = [TealiumRegistration]()
var tealium : Tealium?
let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                           profile: &#34;PROFILE&#34;,
                           environment: &#34;ENVIRONMENT&#34;,
                           dataSource: &#34;DATASOURCE&#34;,
                           optionalData: nil)
config.remoteAPIEnabled = true // Required to use Remote Commands

tealium = Tealium(config: config) { _ in
    guard let remoteCommands = self.tealium?.remoteCommands else {
        return
    }

	let appsflyerInstance = AppsFlyerInstance()
	let appsflyer = AppsFlyerRemoteCommand(appsflyerInstance: appsflyerInstance, type: .local(file: &#34;appsflyer&#34;))
	pushMessagingTrackers.append(appsflyerInstance)
	remoteCommands.add(appsflyer)
}
```

`TealiumHelper.swift`ファイル全体を表示するには、[AppsFlyerリモートコマンドサンプルアプリ](https://github.com/Tealium/tealium-ios-appsflyer-remote-command/tree/master/TealiumAppsFlyerExample)を確認してください。ユーザーが通知の登録、プッシュメッセージのオープン、またはアプリのアンインストールを行った後でAppsFlyerにイベントを送信するには、ファイル`AppDelegate.swift`を参照してください

AppsFlyerのプッシュメッセージ、およびトラッキング機能のアンインストールの詳細については、[開発者向けiOS SDK統合](https://support.appsflyer.com/hc/en-us/articles/207032066)に関するガイドを参照してください。

## JSON テンプレート

[JSON 構成ファイル](/ja/platforms/remote-commands/how-it-works/#json-configuration-file)を使用してリモート コマンドを構成しようとする場合は、まず、以下のテンプレートを参照します。テンプレートには、標準的な E コマースのインストールに用いられる共通マッピングが含まれます。必要に応じて、マッピングを編集します。

```json
{
    &#34;config&#34;: {
        &#34;app_id&#34;: &#34;YOUR_APP_ID&#34;,
        &#34;app_dev_key&#34;: &#34;YOUR_APPSFLYER_DEV_KEY&#34;,
        &#34;settings&#34;: {
            &#34;custom_data&#34;: {&#34;custom_key&#34;: &#34;custom_value&#34;},
            &#34;debug&#34;: true,
            &#34;disable_ad_tracking&#34;: false,
            &#34;disable_apple_ad_tracking&#34;: false,
            &#34;time_between_sessions&#34;: 30,
            &#34;anonymize_user&#34;: false,
            &#34;collect_device_name&#34;: false
        }
    },
    &#34;mappings&#34;: {
        &#34;latitude&#34;: &#34;af_lat&#34;,
        &#34;longitude&#34;: &#34;af_long&#34;,
        &#34;customer_email&#34;: &#34;customer_emails&#34;,
        &#34;hash_type&#34;: &#34;email_hash_type&#34;,
        &#34;currency_code&#34;: &#34;af_currency&#34;,
        &#34;customer_id&#34;: &#34;af_customer_user_id&#34;,
        &#34;signup_method&#34;: &#34;event.signup_method&#34;,
        &#34;achievement_id&#34;: &#34;event.achievement_id&#34;,
        &#34;checkout_option&#34;: &#34;event.checkout_option&#34;,
        &#34;checkout_step&#34;: &#34;event.checkout_step&#34;,
        &#34;content&#34;: &#34;event.content&#34;,
        &#34;content_type&#34;: &#34;event.content_type&#34;,
        &#34;coupon&#34;: &#34;event.coupon&#34;,
        &#34;product_brand&#34;: &#34;event.product_brand&#34;,
        &#34;product_category&#34;: &#34;event.product_category&#34;,
        &#34;product_id&#34;: &#34;event.af_content_id&#34;,
        &#34;product_list&#34;: &#34;event.product_list&#34;,
        &#34;product_location_id&#34;: &#34;event.product_location_id&#34;,
        &#34;product_name&#34;: &#34;event.product_name&#34;,
        &#34;product_variant&#34;: &#34;event.product_variant&#34;,
        &#34;product_unit_price&#34;: &#34;event.af_price&#34;,
        &#34;product_quantity&#34;: &#34;event.af_quantity&#34;,
        &#34;current_level&#34;: &#34;event.level&#34;,
        &#34;score&#34;: &#34;event.score&#34;,
        &#34;search_keyword&#34;: &#34;event.search_keyword&#34;,
        &#34;order_shipping_amount&#34;: &#34;event.order_shipping&#34;,
        &#34;order_tax_amount&#34;: &#34;event.order_tax&#34;,
        &#34;order_id&#34;: &#34;event.af_order_id&#34;,
        &#34;order_total&#34;: &#34;event.af_revenue&#34;,
        &#34;currency_type&#34;: &#34;event.currency_type&#34;,
    },
    &#34;commands&#34;: {
        &#34;launch&#34;: &#34;initialize,launch&#34;,
        &#34;geofence_entered&#34;: &#34;tracklocation&#34;,
        &#34;geofence_exited&#34;: &#34;tracklocation&#34;,
        &#34;user_login&#34;: &#34;login&#34;,
        &#34;user_register&#34;: &#34;setuseremails,setcustomerid,completeregistration&#34;,
        &#34;show_offers&#34;: &#34;adclick&#34;,
        &#34;cart_add&#34;: &#34;addtocart&#34;,
        &#34;wishlist_add&#34;: &#34;addtowishlist&#34;,
        &#34;payment&#34;: &#34;addpaymentinfo&#34;,
        &#34;unlock_achievement&#34;: &#34;unlockachievement&#34;,
        &#34;level_up&#34;: &#34;achievelevel,customersegment&#34;,
        &#34;email_signup&#34;: &#34;subscribe&#34;,
        &#34;product&#34;: &#34;viewedcontent&#34;,
        &#34;category&#34;: &#34;listview&#34;,
        &#34;share&#34;: &#34;share&#34;,
        &#34;search&#34;: &#34;search&#34;,
        &#34;checkout&#34;: &#34;initiatecheckout&#34;,
        &#34;order&#34;:&#34;purchase&#34;
    }
}
```

## サポートされているメソッド

以下のAppsFlyerメソッドは、以下のTealiumコマンドを使用し、AppsFlyerリモートコマンドタグのデータマッピングを使用してトリガーできます。

| リモートコマンド | AppsFlyerメソッド|
| :-- | :--|
| `initialize` | `initialize()` |
| `trackLaunch` | `trackLaunch()` |
| 以下のいずれかのイベント名 | `trackEvent()` |
| `setHost` | `setHost()` |
| `setUserEmails` | `setUserEmails()` |
| `setCurrencyCode` | `currencyCode (property on the AppsFlyerTracker.shared object)`|
| `setCustomerId` | `customerUserID (property on the AppsFlyerTracker.shared object)` |
| `disableDeviceTracking` | `setDeviceTrackingDisabled` |
| `disableTracking` | `isStopTracking (property on the AppsFlyerTracker.shared object)` |
| `resolveDeeplinkUrls` | `resolveDeepLinkURLs (property on the AppsFlyerTracker.shared object)` |
| `didReceiveRemoteNotification`内の`AppDelegate`で手動で呼び出されます| `handlePushNotification()` |
| `didReceiveRemoteNotification`内の`AppDelegate`で手動で呼び出されます| `trackEvent() - event name: af_opened_from_push_notification` |
| `didRegisterForRemoteNotificationsWithDeviceToken`内の`AppDelegate`で手動で呼び出されます| `registerPushToken()` |

### 標準イベント名

以下は、`trackEvent`メソッドでサポートされている標準イベント名のリストです。以下のコマンド名のいずれかが送信された場合は、AppsFlyer SDKで自動的にトリガーされます。ここでは、その特定のイベントに対する必要なすべての変数のマッピングおよび定義も行われていることが前提となっています。[アプリ内イベントの記録](https://support.appsflyer.com/hc/en-us/articles/207032066#core-apis-5-recording-inapp-events)に関する詳細と、[推奨される業種別アプリ内イベント](https://support.appsflyer.com/hc/en-us/articles/115005544169#Verticals)のリストをご確認ください。

| リモートコマンド | AppsFlyerイベント名|
| :-- | :--|
|`achievedLevel`| `&#34;af_level_achieved&#34;`|
|`addPaymentInfo`| `&#34;af_add_payment_info&#34;`|
|`addToCart`| `&#34;af_add_to_cart&#34;`|
|`addToWishlist`| `&#34;af_add_to_wishlist&#34;`|
|`completeRegistration`| `&#34;af_complete_registration&#34;`|
|`completeTutorial`| `&#34;af_tutorial_completion&#34;`|
|`initiateCheckout`| `&#34;af_initiated_checkout&#34;`|
|`purchase`| `&#34;af_purchase&#34;`|
|`subscribe`| `&#34;af_subscribe&#34;`|
|`startTrial`| `&#34;af_start_trial&#34;`|
|`rate`| `&#34;af_rate&#34;`|
|`search`| `&#34;af_search&#34;`|
|`spentCredits`| `&#34;af_spent_credits&#34;`|
|`unlockAchievement`| `&#34;af_achievement_unlocked&#34;`|
|`contentView`| `&#34;af_content_view&#34;`|
|`listView`| `&#34;af_list_view&#34;`|
|`adClick`| `&#34;af_ad_click&#34;`|
|`adView`| `&#34;af_ad_view&#34;`|
|`travelBooking`| `&#34;af_travel_booking&#34;`|
|`share`| `&#34;af_share`&#34;|
|`invite`| `&#34;af_invite&#34;`|
|`reEngage`| `&#34;af_re_engage&#34;`|
|`update`| `&#34;af_update&#34;`|
|`login`| `&#34;af_login&#34;`|
|`customerSegment`| `&#34;af_customer_segment&#34;`|
|`pushNotificationOpened`| `&#34;af_opened_from_push_notification&#34;`|

AppsFlyer SDKはTealium SDKとともにインストールされるので、対応するタグ構成があれば任意のネイティブAppsFlyer機能をトリガーできます。

### SDKのセットアップ

#### 初期化

AppsFlyer SDKは起動時に自動的に初期化されます。AppsFlyer APIキーはタグ構成で構成されます。

| リモートコマンド | AppsFlyerメソッド|
|---|---|
| `initialize`  | `initialize()` |

AppsFlyer開発者ガイド：SDKの初期セットアップ

- [iOS](https://support.appsflyer.com/hc/en-us/articles/207032066#integration-33-initializing-the-sdk)

AppsFlyer リモート コマンド タグで構成できる構成オプションはいくつかあります。以下のいずれかが起動時に構成された場合は、初期化メソッドの実行中に送信されます。

##### 構成オプション

| Name | iQ 変数マッピング| 型|
|---|---|---|
| `debug`  | `debug` | `Bool` |
| `disableIAdTracking`| `disable_apple_ad_tracking`  | `Bool` |
| `minTimeBetweenSessions` | `time_between_sessions` | `Int` |
| `anonymizeUser`| `anonymize_user` | `Bool` |
| `shouldCollectDeviceName`| `collect_device_name` | `Bool` |
| `customData`| `custom_data` | `Dictionary`または`Map`|

AppsFlyer開発者ガイド：追加のAPI

- [iOS](https://support.appsflyer.com/hc/en-us/articles/207032066#additional-apis)
- [Android](https://support.appsflyer.com/hc/en-us/articles/207032126-Android-SDK-integration-for-developers#additional-apis)

#### 起動のトラッキング

| リモートコマンド | AppsFlyerメソッド|
|---|---|
| `initialize` or `launch`  | `trackLaunch()` |


ライフサイクルモジュールがインストールされている場合、このイベントはすべてのアプリ起動を自動的に送信します。

AppsFlyer開発者ガイド：SDKの初期化

- [iOS](https://support.appsflyer.com/hc/en-us/articles/207032066#integration-33-initializing-the-sdk)
- [Android](https://support.appsflyer.com/hc/en-us/articles/207032126-Android-SDK-integration-for-developers#integration-3-implementing-and-initializing-the-sdk)

### ロケーション

#### ロケーションのトラッキング

| リモートコマンド | AppsFlyerメソッド|
| :--- | :---|
| `tracklocation`  | `trackEvent()` - イベント名`af_location_coordinates`|

|  パラメータ | 型|
|---|---|
|  `latitude` (required) | `Bool` |
|  `longitude` (required) | `Bool` |

ロケーションモジュールがインストールされている場合は、緯度と経度がすべてのイベントで送信されます。

AppsFlyer APIリファレンス：ロケーショントラッキング

- [iOS](https://github.com/AppsFlyerSDK/AppsFlyerFramework/blob/19ab52e9133ae86626c013e8cf0ed34aaf3721f0/iOS/AppsFlyerLib.framework/Versions/A/Headers/AppsFlyerTracker.h#L443)

### その他のオプション

#### ホストの構成

|  リモートコマンド | AppsFlyerメソッド|
|---|---|
| `sethost`  | `setHost` |

|  パラメータ | 型|
|---|---|
|  `host` (required) | `String` |
|  `hostPrefix` (required) | `String` |

AppsFlyer APIリファレンス：ホストの構成

- [iOS](https://github.com/AppsFlyerSDK/AppsFlyerFramework/blob/19ab52e9133ae86626c013e8cf0ed34aaf3721f0/iOS/AppsFlyerLib.framework/Versions/A/Headers/AppsFlyerTracker.h#L534)

#### ユーザーのEメールの構成

|  リモートコマンド | AppsFlyerメソッド|
|---|---|
| `setsermails`  | `setUserEmails` |

|  パラメータ | 型|
|----|---|
| `emails` (required) | `[String]` |
| `cryptType` (required) | `Int` |

##### 暗号タイプリファレンス

|  値| 型|
|---|---|
| `0` | `None` |
| `1` | `SHA1` |
| `2` | `MD5` |
| `3` | `SHA256` |

AppsFlyer APIリファレンス：ユーザーのEメールの構成

- [iOS](https://github.com/AppsFlyerSDK/AppsFlyerFramework/blob/19ab52e9133ae86626c013e8cf0ed34aaf3721f0/iOS/AppsFlyerLib.framework/Versions/A/Headers/AppsFlyerTracker.h#L361)

#### 通貨コードの構成

|  リモートコマンド | AppsFlyerプロパティ|
|---|---|
| `setcurrencycode`  | `currencyCode` |

|  パラメータ | 型|
|----|---|
| `currency` (required) | `String` |

AppsFlyer APIリファレンス：通貨コードの構成

- [iOS](https://support.appsflyer.com/hc/en-us/articles/207032066#api-reference-currencycode)

#### 顧客IDの構成

|  リモートコマンド | AppsFlyerプロパティ|
|---|---|
| `setcustomerid`  | `customerUserID` |

|  パラメータ | 型|
|----|---|
| `customerId` (required) | `String` |

- AppsFlyer追加のAPI：顧客IDの構成
- [iOS](https://support.appsflyer.com/hc/en-us/articles/207032066#additional-apis-set-customer-user-id)
- [Android](https://support.appsflyer.com/hc/en-us/articles/207032126-Android-SDK-integration-for-developers#api-reference-setcustomeruserid)

#### ディープリンクURLの解決

| リモートコマンド | AppsFlyerプロパティ|
|---|---|
| resolvedeeplinkurls  | `resolveDeepLinkURLs` |

|  パラメータ | 型|
|---|---|
|  `deepLinkUrls` (required) | `[String]` |

AppsFlyer APIリファレンス：ディープリンクURLの解決

- [iOS](https://support.appsflyer.com/hc/en-us/articles/207032066#api-reference-resolvedeeplinkurls)
- [Android](https://support.appsflyer.com/hc/en-us/articles/207032126-Android-SDK-integration-for-developers#api-reference-setresolvedeeplinkurls)

#### トラッキングの無効化

|  リモートコマンド | AppsFlyerプロパティ|
|---|---|
| disabletracking  | `isStopTracking` |


|  パラメータ | 型|
|----|---|
| `stopTracking` (required) | ブーリアン|

AppsFlyer追加のAPI：トラッキングの停止（オプトアウト）

- [iOS](https://support.appsflyer.com/hc/en-us/articles/207032066#additional-apis-optout)
- [Android](https://support.appsflyer.com/hc/en-us/articles/207032126-Android-SDK-integration-for-developers#additional-apis-optout)
