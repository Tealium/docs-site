---
title: リモートコマンド：AppsFlyer
description: AndroidおよびSwift/iOS向けのTealiumリモートコマンドとAppsFlyerの統合。
url: https://docs.tealium.com/ja/platforms/remote-commands/integrations/appsflyer/
---
## 要件

* AppsFlyerの[アプリID](https://support.appsflyer.com/hc/en-us/articles/207377436#available-in-the-app-store-google-play-store-windows-phone-store)と[開発者キー](https://support.appsflyer.com/hc/en-us/articles/211719806-App-Settings#sdk-dev-key)
* 次のいずれかのモバイルライブラリ：
  * [Tealium for Android-Kotlin](https://docs.tealium.com/ja/platforms/android-kotlin/)（1.0.0以降）
  * [Tealium for Android-Java](https://docs.tealium.com/ja/platforms/android-java/)（AppsFlyer 1.0.0以降の場合は5.9.0以降、それ以前のバージョンの場合は5.9.0以前）
  * [Tealium for iOS-Swift](https://docs.tealium.com/ja/platforms/ios-swift/)
  * [Tealium for React Native](https://docs.tealium.com/ja/platforms/react-native/)
* 次のいずれかのリモートコマンド統合：
  * [AppsFlyerリモートコマンドJSONファイル](https://docs.tealium.com/ja/platforms/remote-commands/integrations/appsflyer/#json-template)（Android-Kotlin 1.0.0以降、またはiOS-Swift 2.1.0以降が必要）
  * タグ管理のAppsFlyerリモートコマンドタグ

## 仕組み

AppsFlyer統合では、次の3つの項目を使用します。

1. AppsFlyerネイティブSDK
1. AppsFlyerメソッドをラップするリモートコマンドモジュール
1. イベントトラッキングをAppsFlyerのネイティブ呼び出しに変換するJSON構成ファイルまたはリモートコマンドタグ

AppsFlyerリモートコマンドモジュールをアプリに追加すると、必要なAppsFlyerライブラリが自動的にインストールおよびビルドされるため、ベンダー固有のコードをアプリに追加する必要はありません。依存関係マネージャーを使用してインストールする場合は、AppsFlyer SDKを個別にインストールする必要はありません。

リモートコマンドには、JSON構成ファイルを使用する方法と、タグ管理を使用してマッピングを構成する方法の2つがあります。ベンダー統合には、リモートでホストするかアプリ内にローカルで配置したJSON構成ファイルの使用を推奨します。タグ管理を使用する場合は、ベンダー統合用のリモートコマンドタグを追加します。[ベンダー統合](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/#vendor-integrations)の詳細を参照してください。

## インストール

### 依存関係マネージャー




1. Xcodeプロジェクトで、**File > Add Packages... > Add Package Dependency**を選択します。
1. リポジトリURLとして`https://github.com/tealium/tealium-ios-appsflyer-remote-command`を入力します。
1. バージョンルールを構成します。通常は`Up to next major`を推奨します。現在の`TealiumAppsFlyer`バージョンがリストに表示されない場合は、Swiftパッケージキャッシュをリセットしてください。
1. インストールする`TealiumAppsFlyer`モジュールを選択し、そのモジュールをインストールするアプリターゲットを選択します。

プロジェクトに複数のアプリターゲットがあり、追加のアプリターゲットでも`TealiumAppsFlyer`モジュールが必要な場合は、**Frameworks, Libraries, and Embedded Content**セクションで手動で追加する必要があります。

追加のアプリターゲットに`TealiumAppsFlyer`をインストールするには、次の手順を実行します。

1. **Project Navigator**でXcodeプロジェクトを選択します。
1. Xcodeプロジェクトの**TARGETS**セクションでアプリターゲットを選択します。
1. **General > Frameworks, Libraries & Embedded Content**に移動し、`TealiumAppsFlyer`モジュールを選択してアプリターゲットに追加します。

Tealium Swiftライブラリから追加のモジュールを追加するには、[Swift Package Manager](https://docs.tealium.com/ja/platforms/ios-swift/install/#swift-package-manager-recommended)の手順に従ってください。




1. Podfileに`tealium-swift`および`pod "AppsFlyerFramework"`が存在する場合は削除します。`tealium-swift`への依存関係は、すでに`TealiumAppsFlyer`フレームワークに含まれています。
2. Podfileに次の依存関係を追加します。  
      ```ruby
      pod "TealiumAppsFlyer"
      ```  
      `TealiumAppsFlyer` Podには、次の`TealiumSwift`依存関係が含まれています。  
      ```bash
      'tealium-swift/Core'
      'tealium-swift/RemoteCommands'
      ```

3. `TealiumHelper`ファイル、および`Tealium`クラスまたはAppsFlyerリモートコマンドにアクセスするその他のファイルで、`TealiumSwift`モジュールと`TealiumAppsFlyer`モジュールをインポートします。




Carthageを使用してiOS向けAppsFlyerリモートコマンドをインストールするには、次の手順を実行します。

1. Cartfileから`tealium-swift`を削除します。`tealium-swift`への依存関係は、すでに`TealiumAppsFlyer`フレームワークに含まれています。
2. Cartfileに次の行が存在する場合は削除します。  
      ```bash
      `binary "https://raw.githubusercontent.com/AppsFlyerSDK/AppsFlyerFramework/master/AppsFlyerLib.json"`
      ```

3. Cartfileに次の依存関係を追加します。  
      ```bash
      github "tealium/tealium-ios-appsflyer-remote-command"
      ```


<blockquote>
Tealium for Swift SDK（バージョン1.x）および`TealiumAppsFlyer`バージョン1.xでは、インストール時に`TealiumDelegate`モジュールを含める必要があります。
</blockquote>








1. まだインストールしていない場合は、[Tealium for Android（Kotlin）](https://docs.tealium.com/ja/platforms/android-kotlin/install/)または[Tealium for Android（Java）](https://docs.tealium.com/ja/platforms/android-java/install/)をインストールし、プロジェクトの最上位`build.gradle`ファイルにTealium Maven URLを追加します。

      ```groovy
      allprojects {
        repositories {
          mavenCentral()
          maven {
            url "https://maven.tealiumiq.com/android/releases/"
          }
        }
      }
      ```

2. アプリプロジェクトの`build.gradle`ファイルに次の依存関係を追加して、AppsFlyer SDKとTealium-AppsFlyerリモートコマンドの両方をインポートします。  
      ```groovy
      dependencies {
      implementation 'com.tealium.remotecommands:appsflyer:1.0.0'
      }
      ```



メインの[Tealium React Nativeライブラリ](https://docs.tealium.com/ja/platforms/react-native)のインストール手順に従ってください。バージョン2.2.0以降がインストールされていることを確認してください。

React Nativeプロジェクトのルートに移動します。

次のコマンドを使用して、`tealium-react-appsflyer`パッケージをダウンロードしてインストールします。

AppsFlyerリモートコマンドパッケージをインストールします。
```yarn add tealium-react-appsflyer```




### 手動インストール




AppsFlyerリモートコマンドを手動でインストールするには、[Tealium for Swift](https://docs.tealium.com/ja/platforms/ios-swift/)ライブラリがインストールされている必要があります。iOSプロジェクトにAppsFlyerリモートコマンドをインストールするには、次の手順を実行します。

1. まだインストールしていない場合は、[AppsFlyer SDK](https://github.com/AppsFlyerSDK/AppsFlyerFramework)をインストールします。
1. [Tealium iOS AppsFlyerリモートコマンド](https://github.com/tealium/tealium-ios-appsflyer-remote-command)リポジトリをクローンし、`Sources`フォルダー内のファイルをプロジェクトにドラッグします。
1. [`remoteAPIEnabled`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#remoteapienabled)構成フラグを`true`に構成します。




AppsFlyerリモートコマンドを手動でインストールするには、[Tealium for Android（Kotlin）](https://docs.tealium.com/ja/platforms/android-kotlin/install/)または[Tealium for Android（Java）](https://docs.tealium.com/ja/platforms/android-java/install/)がインストールされている必要があります。AndroidプロジェクトにAppsFlyerリモートコマンドをインストールするには、次の手順を実行します。

1. プロジェクトルートの`build.gradle`ファイルに`flatDir`を追加します。  
      ```groovy
      allprojects {
            repositories {
              mavenCentral()
              flatDir {
                  dirs 'libs'
              }
            }
      }
      ```

2. `tealium-appsflyer.aar`を`<PROJECT_ROOT>/<MODULE>/libs`に追加します。

3. `build.gradle`ファイルにTealiumライブラリの依存関係を追加します。  
      ```groovy
      dependencies {
            implementation(name:'tealium-appsflyer', ext:'aar')
      }
      ```



## 初期化

すべての Tealium ライブラリで、初期化時に AppsFlyer Remote Command を登録します。




Tealium の iOS（Swift）ライブラリでは、JSON 構成ファイルまたは Remote Command タグを使用してリモートコマンドを初期化します。
```swift
// Sets up a config object and creates a Tealium instance
    let config = TealiumConfig(account: "ACCOUNT",
                               profile: "PROFILE",
                               environment: "ENVIRONMENT")
    
    // Webview Tag
    let appsFlyerRemoteCommand = AppsFlyerRemoteCommand()

    // Local JSON
    //let appsFlyerRemoteCommand = AppsFlyerRemoteCommand(type: .local(file: "appsflyer"))

    // Remote JSON
    //let appsFlyerRemoteCommand = AppsFlyerRemoteCommand(type: .remote(url: "https://some.domain.com/path/to/appsflyer.json"))

    config.remoteAPIEnabled = true
    config.collectors = [Collectors.Lifecycle]
    config.dispatchers = [Dispatchers.TagManagement, Dispatchers.RemoteCommands]
    
    config.addRemoteCommand(appsFlyerRemoteCommand)
    
    var tealium = Tealium(config: config)
```


Tealium の Android（Kotlin）ライブラリでは、JSON 構成ファイルまたは Remote Command タグを使用してリモートコマンドを初期化します。  
```kotlin
val config = TealiumConfig(application,
        "ACCOUNT",
        "PROFILE",
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands, Dispatchers.TagManagement));
val appsFlyer = AppsFlyerRemoteCommand(applicationm, appsFlyerDevKey = devKey);

var tealium = Tealium.create(TEALIUM_MAIN, config) {

    // Webview Tag
    remoteCommands?.add(appsFlyer); 

    // Local JSON
    //remoteCommands?.add(appsFlyer, filename = "appsFlyer.json");

    // Remote JSON
    //remoteCommands?.add(appsFlyer, remoteUrl = "https://some.domain.com/appsFlyer.json");
}
```



Tealium の Android（Java）ライブラリでは、Remote Command タグを使用してリモートコマンドを初期化します。  
```java
// Sets up a config object and creates a Tealium instance
Tealium.Config config = Tealium.Config.create(application, "ACCOUNT", "PROFILE", "ENVIRONMENT");
Tealium teal = Tealium.createInstance(TEALIUM_MAIN, config);

// New code to add the AppsFlyer Remote Command
AppsFlyerRemoteCommand appsFlyer = new AppsFlyerRemoteCommand(application, appsFlyerDevKey = devKey)
teal.addRemoteCommand(appsFlyer);
```


```js
import AppsflyerRemoteCommand from 'tealium-react-appsflyer';

AppsflyerRemoteCommand.initialize();

let config = TealiumConfig {
    // ...
    remoteCommands: [{
        id: AppsflyerRemoteCommand.name,
        // Optional - path to local JSON mappings
        // path: "appsflyer.json"
        // Optional - path to remote JSON mappings
        // url: "https://some.domain.com/appsflyer.json"
    }]
}
Tealium.initialize(config, success => {});
```



## プッシュメッセージのトラッキング（iOS）

iOS 向け TealiumAppsFlyer SDK バージョン 3.0.0 では、異なるリモートコマンド間でプッシュメッセージングを一般化し、統一するために以前使用されていた `TealiumRegistration` フレームワークのサポートを削除しました。プッシュ通知は、基盤となる `AppsFlyerLib` フレームワークで直接処理されます。詳細については、[AppsFlyer のプッシュ通知に関するドキュメント](https://dev.appsflyer.com/hc/docs/push-notifications)を参照してください。

## JSON テンプレート

[JSON 構成ファイル](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/#json-configuration-file)を使用してリモートコマンドを構成する場合は、次のテンプレートを出発点として使用してください。このテンプレートには、標準的な e コマース実装で使用される一般的なマッピングが含まれています。必要に応じてマッピングを編集してください。

```json
{
    "config": {
        "app_id": "YOUR_APP_ID",
        "app_dev_key": "YOUR_APPSFLYER_DEV_KEY",
        "settings": {
            "custom_data": {"custom_key": "custom_value"},
            "debug": true,
            "disable_ad_tracking": false,
            "disable_apple_ad_tracking": false,
            "time_between_sessions": 30,
            "anonymize_user": false,
            "collect_device_name": false
        }
    },
    "mappings": {
        "latitude": "af_lat",
        "longitude": "af_long",
        "customer_email": "customer_emails",
        "hash_type": "email_hash_type",
        "currency_code": "af_currency",
        "customer_id": "af_customer_user_id",
        "signup_method": "event.signup_method",
        "achievement_id": "event.achievement_id",
        "checkout_option": "event.checkout_option",
        "checkout_step": "event.checkout_step",
        "content": "event.content",
        "content_type": "event.content_type",
        "coupon": "event.coupon",
        "product_brand": "event.product_brand",
        "product_category": "event.product_category",
        "product_id": "event.af_content_id",
        "product_list": "event.product_list",
        "product_location_id": "event.product_location_id",
        "product_name": "event.product_name",
        "product_variant": "event.product_variant",
        "product_unit_price": "event.af_price",
        "product_quantity": "event.af_quantity",
        "current_level": "event.level",
        "score": "event.score",
        "search_keyword": "event.search_keyword",
        "order_shipping_amount": "event.order_shipping",
        "order_tax_amount": "event.order_tax",
        "order_id": "event.af_order_id",
        "order_total": "event.af_revenue",
        "currency_type": "event.currency_type",
    },
    "commands": {
        "launch": "initialize,launch",
        "geofence_entered": "tracklocation",
        "geofence_exited": "tracklocation",
        "user_login": "login",
        "user_register": "setuseremails,setcustomerid,completeregistration",
        "show_offers": "adclick",
        "cart_add": "addtocart",
        "wishlist_add": "addtowishlist",
        "payment": "addpaymentinfo",
        "unlock_achievement": "unlockachievement",
        "level_up": "achievelevel,customersegment",
        "email_signup": "subscribe",
        "product": "viewedcontent",
        "category": "listview",
        "share": "share",
        "search": "search",
        "checkout": "initiatecheckout",
        "order":"purchase"
    }
}
```

## サポートされているメソッド

各 AppsFlyer メソッドにコマンドをマッピングします。AppsFlyer メソッドをトリガーするには、対応するコマンドを指定された形式で渡します。

| Remote Command | AppsFlyer メソッド |
| :-- | :-- |
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
### 標準イベント名

以下は、`trackEvent` メソッドでサポートされている標準イベント名の一覧です。以下のコマンド名のいずれかが送信されると、AppsFlyer SDK で自動的にトリガーされます。ただし、そのイベントに必要なすべての変数がマッピングおよび定義されていることが前提です。[アプリ内イベントの記録](https://support.appsflyer.com/hc/en-us/articles/207032066#core-apis-5-recording-inapp-events)の詳細と、[業種別に推奨されるアプリ内イベントの全一覧](https://support.appsflyer.com/hc/en-us/articles/115005544169#Verticals)を参照してください。

| リモートコマンド | AppsFlyerイベント名 |
| :-- | :-- |
|`achievedLevel`| `"af_level_achieved"`|
|`addPaymentInfo`| `"af_add_payment_info"`|
|`addToCart`| `"af_add_to_cart"`|
|`addToWishlist`| `"af_add_to_wishlist"`|
|`completeRegistration`| `"af_complete_registration"`|
|`completeTutorial`| `"af_tutorial_completion"`|
|`initiateCheckout`| `"af_initiated_checkout"`|
|`purchase`| `"af_purchase"`|
|`subscribe`| `"af_subscribe"`|
|`startTrial`| `"af_start_trial"`|
|`rate`| `"af_rate"`|
|`search`| `"af_search"`|
|`spentCredits`| `"af_spent_credits"`|
|`unlockAchievement`| `"af_achievement_unlocked"`|
|`contentView`| `"af_content_view"`|
|`listView`| `"af_list_view"`|
|`adClick`| `"af_ad_click"`|
|`adView`| `"af_ad_view"`|
|`travelBooking`| `"af_travel_booking"`|
|`share`| `"af_share`"|
|`invite`| `"af_invite"`|
|`reEngage`| `"af_re_engage"`|
|`update`| `"af_update"`|
|`login`| `"af_login"`|
|`customerSegment`| `"af_customer_segment"`|
|`pushNotificationOpened`| `"af_opened_from_push_notification"`|


<blockquote>
AppsFlyer SDKはTealium SDKとともにインストールされるため、対応するタグ構成を指定することで、AppsFlyerの任意のネイティブ機能をトリガーできます。
</blockquote>


### SDKのセットアップ

#### 初期化

AppsFlyer SDKは、起動時に自動的に初期化されます。AppsFlyer APIキーはタグ構成で指定します。

| リモートコマンド | AppsFlyerメソッド |
|---|---|
| `initialize`  | `initialize()` |

AppsFlyer開発者ガイド：SDKの初期セットアップ

- [iOS](https://support.appsflyer.com/hc/en-us/articles/207032066#integration-33-initializing-the-sdk)

AppsFlyerリモートコマンドタグでは、複数の構成オプションを指定できます。以下のいずれかが起動時に構成されている場合、初期化メソッドの実行中に送信されます。

##### 構成オプション

| 名前 | iQ変数マッピング | 型 |
|---|---|---|
| `debug`  | `debug` | `Bool` |
| `disableIAdTracking`| `disable_apple_ad_tracking`  | `Bool` |
| `minTimeBetweenSessions` | `time_between_sessions` | `Int` |
| `anonymizeUser`| `anonymize_user` | `Bool` |
| `shouldCollectDeviceName`| `collect_device_name` | `Bool` |
| `customData`| `custom_data` | `Dictionary`または`Map` |

AppsFlyer開発者ガイド：追加API

- [iOS](https://support.appsflyer.com/hc/en-us/articles/207032066#additional-apis)
- [Android](https://support.appsflyer.com/hc/en-us/articles/207032126-Android-SDK-integration-for-developers#additional-apis)

##### OnReady（iOS）

`AppsFlyerLib`を使用する必要があるものの、初期化済みかどうかが不明な場合は、このメソッドを使用します。  
`AppsFlyerLib`がすでに初期化されている場合、完了処理は直ちに呼び出されます。初期化されていない場合は、初期化が完了するまで待機します。

これは、クライアントがリモートコマンド構成を使用してライブラリを初期化しており、その結果、`AppsFlyerLib`が非同期で初期化される場合に役立ちます。

例：

```swift
appsFlyerRemoteCommand.onReady { appsFlyer in
    appsFlyer.registerUninstall(deviceToken)
}
```

### 位置情報

#### 位置情報のトラッキング

| リモートコマンド | AppsFlyerメソッド |
| :--- | :---|
| `tracklocation`  | `trackEvent()` - イベント名 `af_location_coordinates` |

| パラメータ | 型 |
|---|---|
| `latitude`（必須） | `Bool` |
| `longitude`（必須） | `Bool` |


<blockquote>
位置情報モジュールをインストールしている場合、すべてのイベントで緯度と経度が送信されます。
</blockquote>


AppsFlyer APIリファレンス：位置情報のトラッキング

- [iOS](https://github.com/AppsFlyerSDK/AppsFlyerFramework/blob/19ab52e9133ae86626c013e8cf0ed34aaf3721f0/iOS/AppsFlyerLib.framework/Versions/A/Headers/AppsFlyerTracker.h#L443)

### その他のオプション

#### ホストの構成

| リモートコマンド | AppsFlyerメソッド |
|---|---|
| `sethost`  | `setHost` |

| パラメータ | 型 |
|---|---|
| `host`（必須） | `String` |
| `hostPrefix`（必須） | `String` |

AppsFlyer APIリファレンス：ホストの構成

- [iOS](https://github.com/AppsFlyerSDK/AppsFlyerFramework/blob/19ab52e9133ae86626c013e8cf0ed34aaf3721f0/iOS/AppsFlyerLib.framework/Versions/A/Headers/AppsFlyerTracker.h#L534)

#### ユーザーのメールアドレスの構成

| リモートコマンド | AppsFlyerメソッド |
|---|---|
| `setsermails`  | `setUserEmails` |

| パラメータ | 型 |
|----|---|
| `emails`（必須） | `[String]` |
| `cryptType`（必須） | `Int` |

##### 暗号化タイプのリファレンス

| 値 | タイプ |
|---|---|
| `0` | `None` |
| `1` | `SHA1` |
| `2` | `MD5` |
| `3` | `SHA256` |

AppsFlyer APIリファレンス：ユーザーのメールアドレスの構成

- [iOS](https://github.com/AppsFlyerSDK/AppsFlyerFramework/blob/19ab52e9133ae86626c013e8cf0ed34aaf3721f0/iOS/AppsFlyerLib.framework/Versions/A/Headers/AppsFlyerTracker.h#L361)

#### 通貨コードの構成

| リモートコマンド | AppsFlyerプロパティ |
|---|---|
| `setcurrencycode`  | `currencyCode` |

| パラメータ | 型 |
|----|---|
| `currency`（必須） | `String` |

AppsFlyer APIリファレンス：通貨コードの構成

- [iOS](https://support.appsflyer.com/hc/en-us/articles/207032066#api-reference-currencycode)

#### 顧客IDの構成

| リモートコマンド | AppsFlyerプロパティ |
|---|---|
| `setcustomerid`  | `customerUserID` |

| パラメータ | 型 |
|----|---|
| `customerId`（必須） | `String` |

- AppsFlyer追加API：顧客IDの構成
- [iOS](https://support.appsflyer.com/hc/en-us/articles/207032066#additional-apis-set-customer-user-id)
- [Android](https://support.appsflyer.com/hc/en-us/articles/207032126-Android-SDK-integration-for-developers#api-reference-setcustomeruserid)

#### ディープリンクURLの解決

| リモートコマンド | AppsFlyerプロパティ |
|---|---|
| resolvedeeplinkurls  | `resolveDeepLinkURLs` |

| パラメータ | 型 |
|---|---|
| `deepLinkUrls`（必須） | `[String]` |

AppsFlyer APIリファレンス：ディープリンクURLの解決

- [iOS](https://support.appsflyer.com/hc/en-us/articles/207032066#api-reference-resolvedeeplinkurls)
- [Android](https://support.appsflyer.com/hc/en-us/articles/207032126-Android-SDK-integration-for-developers#api-reference-setresolvedeeplinkurls)


### 同意オプション

#### トラッキングの無効化

| リモートコマンド | AppsFlyerプロパティ |
|---|---|
| disabletracking  | `isStopTracking` |

| パラメータ | 型 |
|----|---|
| `stopTracking`（必須） | Bool |

AppsFlyer追加API：トラッキングの停止（オプトアウト）

- [iOS](https://support.appsflyer.com/hc/en-us/articles/207032066#additional-apis-optout)
- [Android](https://support.appsflyer.com/hc/en-us/articles/207032126-Android-SDK-integration-for-developers#additional-apis-optout)