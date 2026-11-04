---
title: リモートコマンド：Firebase
description: AndroidおよびSwift/iOS向けTealiumリモートコマンドのFirebase連携
url: https://docs.tealium.com/ja/platforms/remote-commands/integrations/firebase/
---
## 要件

* 次のいずれかのライブラリ：
  * [Tealium for Android-Kotlin](https://docs.tealium.com/ja/platforms/android-kotlin/)（1.0.0以降）
  * [Tealium for Android-Java](https://docs.tealium.com/ja/platforms/android-java/)（Firebase 2.0.0以降の場合は5.9.0以降、それ以前のバージョンの場合は5.9.0以前）
  * [Tealium for iOS-Swift](https://docs.tealium.com/ja/platforms/ios-swift/)
* 次のいずれかのリモートコマンド連携：
  * [FirebaseリモートコマンドJSONファイル](https://docs.tealium.com/ja/platforms/remote-commands/integrations/firebase/#json-template)（Android-Kotlin 1.0.0以降またはiOS-Swift 2.1.0以降が必要）
  * タグ管理の[Firebaseリモートコマンドタグ](https://docs.tealium.com/firebase-remote-command-tag/)

## 仕組み

Firebase連携では、次の3つの項目を使用します。

1. FirebaseネイティブSDK
1. Firebaseのメソッドをラップするリモートコマンドモジュール
1. イベントトラッキングをFirebaseのネイティブ呼び出しに変換するJSON構成ファイルまたはリモートコマンドタグ

Firebaseリモートコマンドモジュールをアプリに追加すると、必要なFirebaseライブラリが自動的にインストールおよびビルドされるため、ベンダー固有のコードをアプリに追加する必要はありません。依存関係マネージャーを使用してインストールする場合、Firebase SDKを個別にインストールする必要はありません。

リモートコマンドには、JSON構成ファイルを使用する方法と、タグ管理を使用してマッピングを構成する方法の2つがあります。ベンダー連携には、リモートまたはアプリ内のローカルでホストされるJSON構成ファイルの使用を推奨します。タグ管理を使用する場合は、ベンダー連携用のリモートコマンドタグを追加します。[ベンダー連携](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/#vendor-integrations)の詳細をご覧ください。

## インストール

### 依存関係マネージャー





1. Cartfileから`tealium-swift`を削除します。`tealium-swift`の依存関係は、すでに`TealiumFirebase`フレームワークに含まれています。

1. Cartfileに次の行が存在する場合は削除します。  
      ```bash
      binary "https://dl.google.com/dl/firebase/ios/carthage/FirebaseAnalyticsBinary.json"
      ```

1. Cartfileに次の依存関係を追加します。  
      ```bash
      github "tealium/tealium-ios-firebase-remote-command"
      ```


<blockquote>
FirebaseではCarthageのバイナリインストールが使用されるため、Carthageの`--use-xcframeworks`フラグを使用している場合、`TealiumFirebase`モジュールを`xcframework`としてビルドすることはできません。依存関係をビルドするには、Carthage公式の[Xcode 12向け回避策](https://github.com/Carthage/Carthage/blob/master/Documentation/Xcode12Workaround.md)を使用することをお勧めします。
</blockquote>






1. Podfileに次の行が存在する場合は削除します。  
      ```bash
      pod "Firebase/Analytics"
      ```  

1. Podfileに次の依存関係を追加します。  
      ```swift
      pod "TealiumFirebase"
      ```  
      `TealiumFirebase` Podには、次の`TealiumSwift`依存関係が含まれています。  
      ```bash
      'tealium-swift/Core'
      'tealium-swift/RemoteCommands'
      ```

1. `TealiumHelper`ファイル、および`Tealium`クラスまたはFirebaseリモートコマンドにアクセスするその他すべてのファイルで、`TealiumSwift`モジュールと`TealiumFirebase`モジュールをインポートします。





Cordova用Tealium Firebaseライブラリをインストールするには、Cordovaアプリプロジェクトで次のコマンドを実行します。

```
cordova plugin add tealium-cordova-firebase-plugin
```





Flutter用Tealium Firebaseライブラリをインストールするには、次のコマンドを実行します。

```
flutter pub add tealium_firebase
import 'package:tealium_firebase/tealium_firebase.dart';
```





1. まだ実行していない場合は、[Tealium for Android（Kotlin）](https://docs.tealium.com/ja/platforms/android-kotlin/install/)または[Tealium for Android（Java）](https://docs.tealium.com/ja/platforms/android-java/install/)をインストールし、プロジェクトの最上位の`build.gradle`ファイルにTealium Maven URLを追加します。


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

1. `build.gradle`ファイルに次の依存関係を追加します。

      ```groovy
      dependencies {
          implementation 'com.tealium.remotecommands:firebase:1.2.0'
      }
      ```





1. React Nativeプロジェクトのルートに移動します。

1. 次のコマンドを使用して、`tealium-react-firebase`パッケージをダウンロードしてインストールします。  
    ```bash
    yarn add tealium-react-firebase
    ```
1. NPMパッケージのバージョン1.0.7ではReact Native Autolinkingが有効になっているため、React Native 0.60以降を使用している場合は、`react-native link`を実行する必要はありません。





1. Xcodeプロジェクトで、**File > Add Packages... > Add Package Dependency**を選択します。
1. リポジトリURLとして`https://github.com/tealium/tealium-ios-firebase-remote-command`を入力します。
1. バージョンルールを構成します。通常は`Up to next major`を推奨します。現在の`TealiumFirebase`バージョンがリストに表示されない場合は、Swiftパッケージのキャッシュをリセットしてください。
1. インストールする`TealiumFirebase`モジュールを選択し、そのモジュールをインストールするアプリターゲットを選択します。

プロジェクトに複数のアプリターゲットがあり、複数のアプリターゲットで`TealiumFirebase`モジュールが必要な場合は、**Frameworks, Libraries, and Embedded Content**セクションで手動で追加する必要があります。

追加のアプリターゲットに`TealiumFirebase`をインストールするには、次の手順を実行します。

1. **Project Navigator**でXcodeプロジェクトを選択します。
1. Xcodeプロジェクトの**TARGETS**セクションで、アプリターゲットを選択します。
1. **General > Frameworks, Libraries & Embedded Content**に移動し、`TealiumFirebase`モジュールを選択してアプリターゲットに追加します。

Tealium Swiftライブラリから追加のモジュールを追加するには、[Swift Package Manager](https://docs.tealium.com/ja/platforms/ios-swift/install/#swift-package-manager-recommended)の手順に従ってください。





組み込みのNuGetパッケージマネージャーを使用して、Visual StudioからXamarin用Tealium Firebaseライブラリを直接インストールします。

[NuGetパッケージ：Tealium.RemoteCommands.Firebase.Xamarin](https://www.nuget.org/packages/Tealium.RemoteCommands.Firebase.Xamarin)




### 手動インストール




Firebaseリモートコマンドを手動でインストールするには、[Tealium for Swift](https://docs.tealium.com/ja/platforms/ios-swift/)ライブラリがインストールされている必要があります。iOSプロジェクトにFirebaseリモートコマンドをインストールするには、次の手順を実行します。

1. まだインストールしていない場合は、[Firebase SDK](https://firebase.google.com/docs/ios/setup)をインストールします。

1. [Tealium iOS Firebaseリモートコマンド](https://github.com/tealium/tealium-ios-firebase-remote-command)リポジトリをクローンし、`Sources`フォルダー内のファイルをプロジェクトにドラッグします。

1. [`remoteAPIEnabled`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#remoteapienabled)構成フラグを`true.`に構成します。




Firebaseリモートコマンドを手動でインストールするには、[Tealium for Android（Kotlin）](https://docs.tealium.com/ja/platforms/android-kotlin/install/)または[Tealium for Android（Java）](https://docs.tealium.com/ja/platforms/android-java/install/)がインストールされている必要があります。

AndroidプロジェクトにFirebaseリモートコマンドをインストールするには、次の手順を実行します。

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

1. `tealium-firebase.aar`を`<PROJECT_ROOT>/<MODULE>/libs`に追加します。

1. `build.gradle`ファイルにTealiumライブラリの依存関係を追加します。

      ```groovy
      dependencies {
            implementation(name:'tealium-firebase', ext:'aar')
      }
      ```



## 初期化

すべての Tealium ライブラリで、初期化時に Firebase モバイルリモートコマンドを登録します。





Tealium の Android（Java）ライブラリでは、Remote Command タグを使用してリモートコマンドを初期化します。
```java
RemoteCommand firebase = new FirebaseRemoteCommand(application);
teal.addRemoteCommand(firebase);
```




Tealium の Kotlin ライブラリでは、JSON 構成ファイルまたは Remote Command タグを使用してリモートコマンドを初期化します。
```kotlin
val config = TealiumConfig(application,
        "ACCOUNT",
        "PROFILE",
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands, Dispatchers.TagManagement));
val firebase = FirebaseRemoteCommand(application);

var tealium = Tealium.create(TEALIUM_MAIN, config) {

    // Webview Tag
    remoteCommands?.add(firebase); 

    // Local JSON
    //remoteCommands?.add(firebase, filename = "firebase.json"); 

    // Remote JSON
    //remoteCommands?.add(firebase, remoteUrl = "https://some.domain.com/firebase.json"); 
}
```






```javascript
    let Environment = tealium.utils.Environment;
    let Dispatchers = tealium.utils.Dispatchers;

    // Webview Tag
    let firebase = window.tealium.remotecommands.firebase.create() 

    // Local JSON
    //let firebase = window.tealium.remotecommands.firebase.create().setPath("firebase.json") 

    // Remote JSON
    //let firebase = window.tealium.remotecommands.firebase.create().setUrl("https://some.domain.com/firebase.json") 
    
    let config = { 
        account: ACCOUNT_NAME, 
        profile: PROFILE_NAME, 
        environment: Environment.dev, 
        dispatchers: [
            Dispatchers.TagManagement, 
            Dispatchers.RemoteCommands
        ],
        remoteCommands: [
            
        ]
    };

    window.tealium.initialize(config, function(success) {
        console.log("Init was: " + success)
    })
```





次の内容を含む `Google-Servives.json` または `.plist` ファイルをプラットフォームオブジェクトに追加します。

```json
// WebView remote command
var webViewFirebase = RemoteCommand(TealiumFirebase.commandName)

// Local JSON mappings
var localFirebase = RemoteCommand(
  TealiumFirebase.commandName, 
  path: "firebase.json"
)

// Remote JSON mappings
var remoteFirebase = RemoteCommand(
  TealiumFirebase.commandName, 
  url: "https://some.domain.com/firebase.json"
)

var config = TealiumConfig(
  // ...
  remoteCommands: [
    webViewFirebase // or `localFirebase`, or `remoteFirebase`
  ])
```





```javascript
import FirebaseRemoteCommand from 'tealium-react-firebase';
FirebaseRemoteCommand.initialize();

// Webview Tag
let firebase = { id: FirebaseRemoteCommand.name } 

// Local JSON
//let firebase = { id: FirebaseRemoteCommand.name, path: "firebase.json" } 

// Remote JSON
//let firebase = { id: FirebaseRemoteCommand.name, url: "https://some.domain.com/firebase.json" } 
let config = TealiumConfig {
    // ...
    remoteCommands: [firebase]
}
```




Tealium の iOS（Swift）ライブラリでは、JSON 構成ファイルまたは Remote Command タグを使用してリモートコマンドを初期化します。

```swift
var tealium : Tealium?
let config = TealiumConfig(account: "ACCOUNT",
                           profile: "PROFILE",
                           environment: "ENVIRONMENT",
                           dataSource: "DATASOURCE")
config.dispatchers = [Dispatchers.TagManagement, Dispatchers.RemoteCommands]
config.remoteAPIEnabled = true // Required to use Remote Commands

tealium = Tealium(config: config) { _ in
    guard let remoteCommands = self.tealium?.remoteCommands else {
        return
    }

    // Webview Tag
    let firebase = FirebaseRemoteCommand() 

    // Local JSON
    //let firebase = FirebaseRemoteCommand(type: .local(file: "firebase")) 

    // Remote JSON
    //let firebase = FirebaseRemoteCommand(type: .remote(url: "https://some.domain.com/firebase.json")) 
    
    remoteCommands.add(firebase)
}
```





```csharp

// Webview Tag
var firebase = new FirebaseRemoteCommandDroid(this.Application, null, null); 

// Local JSON
//var firebase = new FirebaseRemoteCommandDroid(this.Application, "firebase.json", null); 

// Remote JSON
//var firebase = new FirebaseRemoteCommandDroid(this.Application, null, "https://some.domain.com/firebase.json"); 

var commands = new List<IRemoteCommand> {
    firebase
};
TealiumConfig config = new TealiumConfig(ACCOUNT_NAME,
                                          PROFILE_NAME,
                                          ENVIRONMENT,
                                          new List<Dispatchers> {
                                              Dispatchers.RemoteCommands, Dispatchers.TagManagement
                                          },
                                          new List<Collectors> {},
                                          remoteCommands: commands
                                          );
```




```csharp

// Webview Tag
var firebase = new FirebaseRemoteCommandIOS(new RemoteCommandTypeWrapper()); 

// Local JSON
//var firebase = new FirebaseRemoteCommandIOS(new RemoteCommandTypeWrapper("firebase", NSBundle.MainBundle));

// Remote JSON
//var firebase = new FirebaseRemoteCommandIOS(new RemoteCommandTypeWrapper("https://some.domain.com/firebase.json")); 

var commands = new List<IRemoteCommand> {
    firebase
};
TealiumConfig config = new TealiumConfig(ACCOUNT_NAME,
                                          PROFILE_NAME,
                                          ENVIRONMENT,
                                          new List<Dispatchers> {
                                              Dispatchers.RemoteCommands, Dispatchers.TagManagement
                                          },
                                          new List<Collectors> {},
                                          remoteCommands: commands
                                          );
```


## JSONテンプレート

[JSON構成ファイル](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/#json-configuration-file)を使用してリモートコマンドを構成する場合は、以下のテンプレートを参照して開始してください。このテンプレートには、標準的なEコマース環境で使用される一般的なマッピングが含まれています。必要に応じてマッピングを編集してください。

```json
{
    "config": {
        "firebase_analytics_enabled": "true",
        "firebase_session_timeout_seconds": "30",
        "firebase_log_level": "max",
        "firebase_session_minimum_seconds": "100"
    },
    "mappings": {
        "achievement_id": "event.param_achievement_id",
        "ad_network_click_id": "event.param_ad_network_click_id",
        "affiliation": "event.param_affiliation",
        "campaign_keywords": "event.param_cp1",
        "campaign": "event.param_campaign",
        "game_character": "event.param_character",
        "checkout_option": "event.param_checkout_option",
        "checkout_step": "event.param_checkout_step",
        "content": "event.param_content",
        "content_type": "event.param_content_type",
        "coupon": "event.param_coupon",
        "creative_name": "event.param_creative_name",
        "creative_slot": "event.param_creative_slot",
        "currency_code": "event.param_currency",
        "travel_destination": "event.param_destination",
        "end_date": "event.param_end_date",
        "flight_number": "event.param_flight_number",
        "group_id": "event.param_group_id",
        "current_index": "param_index",
        "product_brand": "items.param_item_brand",
        "product_category": "items.param_item_category",
        "product_id": "items.param_item_id",
        "product_unit_price": "items.param_price",
        "product_quantity": "items.param_quantity",
        "product_list": "items.param_item_list",
        "product_location_id": "items.param_item_location_id",
        "product_name": "items.param_item_name",
        "product_variant": "items.param_item_variant",
        "current_level": "event.param_level",
        "most_recent_location": "event.param_location",
        "campaign_medium": "event.param_medium",
        "number_nights": "event.param_number_nights",
        "number_pax": "event.param_number_pax",
        "number_rooms": "event.param_number_rooms",
        "travel_origin": "event.param_origin",
        "score": "event.param_score",
        "search_keyword": "event.param_search_term",
        "order_shipping_amount": "event.param_shipping",
        "signup_method": "event.param_signup_method",
        "campaign_source": "event.param_source",
        "start_date": "event.param_start_date",
        "order_tax_amount": "event.param_tax",
        "product_term": "event.param_term",
        "order_id": "event.param_transaction_id",
        "travel_class": "event.param_travel_class",
        "order_total": "event.param_value",
        "currency_type": "event.param_virtual_currency_name",
        "user_signup_method": "event.param_user_signup_method",
        "event_title": "firebase_event_name",
        "screen_name": "firebase_screen_name",
        "screen_class": "firebase_screen_class",
        "customer_property": "firebase_property_name",
        "customer_value": "firebase_property_value",
        "customer_id": "firebase_user_id",
        "consent_ad_storage": "firebase_consent_settings.ad_storage",
        "consent_analytics_storage": "firebase_consent_settings.analytics_storage",
        "consent_ad_user_data": "firebase_consent_settings.ad_user_data",
        "consent_ad_personalization": "firebase_consent_settings.ad_personalization"
    },
    "commands": {
        "launch": "config",
        "user_login": "logevent",
        "user_register": "logevent,setuserproperty",
        "share": "logevent",
        "show_offers": "logevent",
        "join_group": "logevent",
        "travel_order": "logevent",
        "earn_currency": "logevent",
        "spend_currency": "logevent",
        "unlock_achievement": "logevent",
        "level_up": "logevent",
        "start_tutorial": "logevent",
        "stop_tutorial": "logevent",
        "record_score": "logevent",
        "category": "logevent,setscreenname",
        "product": "logevent,setscreenname",
        "cart_add": "logevent",
        "wishlist_add": "logevent",
        "checkout": "logevent,setscreenname",
        "checkout_progress": "logevent",
        "email_signup": "logevent",
        "order": "logevent,setscreenname",
        "setconsent": "setconsent",
        "initiateconversionmeasurement": "initiateconversionmeasurement",
        "resetanalyticsdata": "resetdata"
    }
}
```

## サポートされるメソッド

各Firebaseメソッドにコマンドをマッピングします。Firebaseメソッドをトリガーするには、対応するコマンドを指定された形式で渡します。

|リモートコマンド|Firebaseメソッド|
|--------------|------------|
| `config` | `configure()` |
| `logevent` | `logEvent(name, parameters)` |
| `setscreenname` | `logEvent(name (AnalyticsEventScreenView), parameters)` |
| `setdefaultparameters` | `setDefaultEventParameters(parameters)` |
| `setuserproperty` | `setUserProperty(value, name)` |
| `setuserid` | `setUserId(id)` |
| `initiateconversionmeasurement` (iOS) |`initiateOnDeviceConversionMeasurement(emailAddress)` |
| `setconsent` | `setConsent(consentSettings)` |
| `resetdata` | `resetAnalyticsData` |

### SDKのセットアップ

### 構成

| リモートコマンド | Firebaseメソッド |
|---|---|
| `config` | `configure()` |

SDKのセットアップには、以下のパラメーターを使用します。

| パラメーター | 型 | 説明 |
|---|---|---|
| `firebase_session_timeout_seconds` |  `String` | セッションの長さを秒単位で表した文字列。 |
| `firebase_analytics_enabled` |  `String` | アナリティクスを有効または無効にするブール値の文字列表現（デフォルトは`true`）。 |
| `firebase_log_level` (iOS) |  `String` | ログレベル：min|max|error|debug|notice|warning|info（デフォルトは`min`）。 |

### トラッキング

アプリでの基本的な操作によってトリガーされるイベントは、自動的にトラッキングされます。詳細については、[GA4：自動的に収集されるイベント](https://support.google.com/firebase/answer/6317485?hl=en)を参照してください。

#### イベントのログ記録

パラメーターと、必要に応じてアイテムの配列を指定してイベントをログに記録します。

| リモートコマンド | Firebaseメソッド |
|---|---|
| `logevent` | `logEvent(name, parameters)` |

| パラメーター | 型 | 説明 |
|---|---|---|
| `firebase_event_name` |  `String` | （必須）Firebaseイベント名のリストにマッピングされるイベント名。 |
| `event` (JSON) |  `[String:Any]` | このイベントのすべてのパラメーターを含み、Firebaseパラメーターのリストにマッピングされるオブジェクト。 |
| `firebase_event_params` (Tag) | `[String:Any]` | このイベントのすべてのパラメーターを含み、Firebaseパラメーターのリストにマッピングされるオブジェクト（タグで使用）。 |
| `items` (JSON) |  `[String:[Any]]` | このイベントのアイテム配列を含むオブジェクト。すべての配列には同じ数の要素が含まれ、すべての要素を単一のアイテム配列に正規化できます。 |
| `param_items` (Tag) | `[[String:Any]]` | このイベントのアイテム配列（タグで使用）。 |

#### 画面名の構成

このコマンドは、ユーティリティとして追加される特定のログイベントです。

| リモートコマンド | Firebaseメソッド（iOS） | Firebaseメソッド（Android） |
|---|---|---|
| `setscreenname` | `logEvent(name (AnalyticsEventScreenView), parameters)` | `setCurrentScreen(currentActivity, screenName, screenClass)` |

| パラメーター | 型 | 説明 |
|---|---|---|
| `firebase_screen_name` |  `String` | （必須）現在の画面の名前。 |
| `firebase_screen_class` |  `String` | 現在の画面のクラス。 |

#### デフォルトパラメーターの構成

このコマンドは、すべてのログイベントで送信されるパラメーターを構成します。

| リモートコマンド | Firebaseメソッド |
|---|---|
| `setdefaultparameters` | `setDefaultEventParameters(parameters)` |

| パラメーター | 型 | 説明 |
|---|---|---|
| `default` (JSON) |  `[String:Any]` | キーと値の形式のデフォルトパラメーターを含むオブジェクト。 |
| `firebase_default_params` (Tag) |  `String` | キーと値の形式のデフォルトパラメーターを含むオブジェクト（タグで使用）。 |
### マッピング

`logEvent` メソッドで送信されるパラメータとイベントは、Tealium の値から Firebase の定数名にマッピングされます。

次の表は、iOS と Android の定数にマッピングされる利用可能なキーの一覧です。Tealium のマッピングにパラメータがない場合は、Firebase の定数値を直接使用できます。

#### イベントのマッピング

| Tealium キー | Firebase イベント（iOS） | Firebase イベント（Android） |
|---|---|---|
| `event_ad_impression` | `AnalyticsEventAdImpression` | `AD_IMPRESSION` |
| `event_add_payment_info` | `AnalyticsEventAddPaymentInfo` | `ADD_PAYMENT_INFO` |
| `event_add_shipping_info` | `AnalyticsEventAddShippingInfo` | `ADD_SHIPPING_INFO` |
| `event_add_to_cart` | `AnalyticsEventAddToCart` | `ADD_TO_CART` |
| `event_add_to_wishlist` | `AnalyticsEventAddToWishlist` | `ADD_TO_WISHLIST` |
| `event_app_open` | `AnalyticsEventAppOpen` | `APP_OPEN` |
| `event_begin_checkout` | `AnalyticsEventBeginCheckout` | `BEGIN_CHECKOUT` |
| `event_campaign_details` | `AnalyticsEventCampaignDetails` | `CAMPAIGN_DETAILS` |
| `event_earn_virtual_currency` | `AnalyticsEventEarnVirtualCurrency` | `EARN_VIRTUAL_CURRENCY` |
| `event_generate_lead` | `AnalyticsEventGenerateLead` | `GENERATE_LEAD` |
| `event_join_group` | `AnalyticsEventJoinGroup` | `JOIN_GROUP` |
| `event_level_end` | `AnalyticsEventLevelEnd` | `LEVEL_END` |
| `event_level_start` | `AnalyticsEventLevelStart` | `LEVEL_START` |
| `event_level_up` | `AnalyticsEventLevelUp` | `LEVEL_UP` |
| `event_login` | `AnalyticsEventLogin` | `LOGIN` |
| `event_post_score` | `AnalyticsEventPostScore` | `POST_SCORE` |
| `event_purchase` | `AnalyticsEventPurchase` | `PURCHASE` |
| `event_refund` | `AnalyticsEventRefund` | `REFUND` |
| `event_remove_cart` | `AnalyticsEventRemoveFromCart` | `REMOVE_FROM_CART` |
| `event_screen_view` | `AnalyticsEventScreenView` | `SCREEN_VIEW` |
| `event_search` | `AnalyticsEventSearch` | `SEARCH` |
| `event_select_content` | `AnalyticsEventSelectContent` | `SELECT_CONTENT` |
| `event_select_item` | `AnalyticsEventSelectItem` | `SELECT_ITEM` |
| `event_select_promotion` | `AnalyticsEventSelectPromotion` | `SELECT_PROMOTION` |
| `event_share` | `AnalyticsEventShare` | `SHARE` |
| `event_signup` | `AnalyticsEventSignUp` | `SIGN_UP` |
| `event_spend_virtual_currency` | `AnalyticsEventSpendVirtualCurrency` | `SPEND_VIRTUAL_CURRENCY` |
| `event_tutorial_begin` | `AnalyticsEventTutorialBegin` | `TUTORIAL_BEGIN` |
| `event_tutorial_complete` | `AnalyticsEventTutorialComplete` | `TUTORIAL_COMPLETE` |
| `event_unlock_achievement` | `AnalyticsEventUnlockAchievement` | `UNLOCK_ACHIEVEMENT` |
| `event_view_cart` | `AnalyticsEventViewCart` | `VIEW_CART` |
| `event_view_item` | `AnalyticsEventViewItem` | `VIEW_ITEM` |
| `event_view_item_list` | `AnalyticsEventViewItemList` | `VIEW_ITEM_LIST` |
| `event_view_promotion` | `AnalyticsEventViewPromotion` | `VIEW_PROMOTION` |
| `event_view_search_results` | `AnalyticsEventViewSearchResults` | `VIEW_SEARCH_RESULTS` |

#### パラメータのマッピング

| Tealium キー | Firebase パラメータ（iOS） | Firebase パラメータ（Android） |
|---|---|---|
| `param_achievement_id` | `AnalyticsParameterAchievementID` | `ACHIEVEMENT_ID` |
| `param_ad_format` | `AnalyticsParameterAdFormat` | `AD_FORMAT` |
| `param_ad_network_click_id` | `AnalyticsParameterAdNetworkClickID` | `ACLID` |
| `param_ad_platform` | `AnalyticsParameterAdPlatform` | `AD_PLATFORM` |
| `param_ad_source` | `AnalyticsParameterAdSource` | `AD_SOURCE` |
| `param_ad_unit_name` | `AnalyticsParameterAdUnitName` | `AD_UNIT_NAME` |
| `param_affiliation` | `AnalyticsParameterAffiliation` | `AFFILIATION` |
| `param_cp1` | `AnalyticsParameterCP1` | `CP1` |
| `param_campaign` | `AnalyticsParameterCampaign` | `CAMPAIGN` |
| `param_campaign_id` | `AnalyticsParameterCampaignID` | N/A |
| `param_character` | `AnalyticsParameterCharacter` | `CHARACTER` |
| `param_content` | `AnalyticsParameterContent` | `CONTENT` |
| `param_content_type` | `AnalyticsParameterContentType` | `CONTENT_TYPE` |
| `param_coupon` | `AnalyticsParameterCoupon` | `COUPON` |
| `param_creative_format` | `AnalyticsParameterCreativeFormat` | N/A |
| `param_creative_name` | `AnalyticsParameterCreativeName` | `CREATIVE_NAME` |
| `param_creative_slot` | `AnalyticsParameterCreativeSlot` | `CREATIVE_SLOT` |
| `param_currency` | `AnalyticsParameterCurrency` | `CURRENCY` |
| `param_destination` | `AnalyticsParameterDestination` | `DESTINATION` |
| `param_discount` | `AnalyticsParameterDiscount` | `DISCOUNT` |
| `param_end_date` | `AnalyticsParameterEndDate` | `END_DATE` |
| `param_extend_session` | `AnalyticsParameterExtendSession` | `EXTEND_SESSION` |
| `param_flight_number` | `AnalyticsParameterFlightNumber` | `FLIGHT_NUMBER` |
| `param_group_id` | `AnalyticsParameterGroupID` | `GROUP_ID` |
| `param_index` | `AnalyticsParameterIndex` | `INDEX` |
| `param_item_brand` | `AnalyticsParameterItemBrand` | `ITEM_BRAND` |
| `param_item_category` | `AnalyticsParameterItemCategory` | `ITEM_CATEGORY` |
| `param_item_category2` | `AnalyticsParameterItemCategory2` | `ITEM_CATEGORY2` |
| `param_item_category3` | `AnalyticsParameterItemCategory3` | `ITEM_CATEGORY3` |
| `param_item_category4` | `AnalyticsParameterItemCategory4` | `ITEM_CATEGORY4` |
| `param_item_category5` | `AnalyticsParameterItemCategory5` | `ITEM_CATEGORY5` |
| `param_item_id` | `AnalyticsParameterItemID` | `ITEM_ID` |
| `param_item_list_id` | `AnalyticsParameterItemListID` | `ITEM_LIST_ID` |
| `param_item_list_name` | `AnalyticsParameterItemListName` | `ITEM_LIST_NAME` |
| `param_item_name` | `AnalyticsParameterItemName` | `ITEM_NAME` |
| `param_item_variant` | `AnalyticsParameterItemVariant` | `ITEM_VARIANT` |
| `param_items` | `AnalyticsParameterItems` | `ITEMS` |
| `param_level` | `AnalyticsParameterLevel` | `LEVEL` |
| `param_level_name` | `AnalyticsParameterLevelName` | `LEVEL_NAME` |
| `param_location` | `AnalyticsParameterLocation` | `LOCATION` |
| `param_location_id` | `AnalyticsParameterLocationID` | `LOCATION_ID` |
| `param_marketing_tactic` | `AnalyticsParameterMarketingTactic` | N/A |
| `param_medium` | `AnalyticsParameterMedium` | `MEDIUM` |
| `param_method` | `AnalyticsParameterMethod` | `METHOD` |
| `param_number_nights` | `AnalyticsParameterNumberOfNights` | `NUMBER_OF_NIGHTS` |
| `param_number_pax` | `AnalyticsParameterNumberOfPassengers` | `NUMBER_OF_PASSENGERS` |
| `param_number_rooms` | `AnalyticsParameterNumberOfRooms` | `NUMBER_OF_ROOMS` |
| `param_origin` | `AnalyticsParameterOrigin` | `ORIGIN` |
| `param_payment_type` | `AnalyticsParameterPaymentType` | `PAYMENT_TYPE` |
| `param_price` | `AnalyticsParameterPrice` | `PRICE` |
| `param_promotion_id` | `AnalyticsParameterPromotionID` | `PROMOTION_ID` |
| `param_promotion_name` | `AnalyticsParameterPromotionName` | `PROMOTION_NAME` |
| `param_quantity` | `AnalyticsParameterQuantity` | `QUANTITY` |
| `param_score` | `AnalyticsParameterScore` | `SCORE` |
| `param_search_term` | `AnalyticsParameterSearchTerm` | `SEARCH_TERM` |
| `param_shipping` | `AnalyticsParameterShipping` | `SHIPPING` |
| `param_shipping_tier` | `AnalyticsParameterShippingTier` | `SHIPPING_TIER` |
| `param_screen_name` | `AnalyticsParameterScreenName` | `SCREEN_NAME` |
| `param_screen_class` | `AnalyticsParameterScreenClass` | `SCREEN_CLASS` |
| `param_source` | `AnalyticsParameterSource` | `SOURCE` |
| `param_source_platform` | `AnalyticsParameterSourcePlatform` | N/A |
| `param_start_date` | `AnalyticsParameterStartDate` | `START_DATE` |
| `param_success` | `AnalyticsParameterSuccess` | `SUCCESS` |
| `param_tax` | `AnalyticsParameterTax` | `TAX` |
| `param_term` | `AnalyticsParameterTerm` | `TERM` |
| `param_transaction_id` | `AnalyticsParameterTransactionID` | `TRANSACTION_ID` |
| `param_travel_class` | `AnalyticsParameterTravelClass` | `TRAVEL_CLASS` |
| `param_value` | `AnalyticsParameterValue` | `VALUE` |
| `param_virtual_currency_name` | `AnalyticsParameterVirtualCurrencyName` | `VIRTUAL_CURRENCY_NAME` |
| `param_user_signup_method` | `AnalyticsUserPropertySignUpMethod` | N/A |
| `param_user_allow_ad_personalization_signals` | `AnalyticsUserPropertyAllowAdPersonalizationSignals` | N/A |

### ユーザーの構成
#### ユーザープロパティの構成

このコマンドは、単一または複数のユーザープロパティ名と値を構成します。

| リモートコマンド | Firebaseメソッド |
|---|---|
| `setuserproperty` | `setUserProperty(value, name)` |

| パラメータ | 型 | 説明 |
|---|---|---|
| `firebase_property_name` |  `String\|[String]` | （必須）プロパティ名またはプロパティ名の配列 |
| `firebase_property_value` |  `String\|[String]]` | （必須）プロパティ値またはプロパティ値の配列。このパラメータが配列の場合、`firebase_property_name`配列の長さおよび項目の順序と一致している必要があります。 |

#### ユーザーIDの構成

このコマンドはユーザーIDを構成します。

| リモートコマンド | Firebaseメソッド |
|---|---|
| `setuserid` | `setUserId(id)` |

| パラメータ | 型 | 説明 |
|---|---|---|
| `firebase_user_id`|  `String` | （必須）構成するユーザーID |

### コンバージョン測定（iOS）

このコマンドはコンバージョン測定を開始します。

| リモートコマンド | Firebaseメソッド |
|---|---|
| `initiateconversionmeasurement` | `initiateOnDeviceConversionMeasurement()` |

| パラメータ | 型 | 説明 |
|---|---|---|
| `param_hashed_email_address` | `String` | ハッシュ化されたユーザーのメールアドレス |
| `param_hashed_phone_number` | `String` | ハッシュ化されたユーザーの電話番号 |
| `param_email_address` | `String` | ユーザーのメールアドレス |
| `param_phone_number` | `String` | ユーザーの電話番号 |


<blockquote>
ハッシュ化したパラメータを送信する場合は、[iOS広告コンバージョンの測定に関するFirebaseドキュメント](https://firebase.google.com/docs/tutorials/ads-ios-on-device-measurement/step-3)に従って、正規化およびハッシュ化する必要があります。Tealiumがパラメータとして受け取る値は、引き続き`String`である必要があります。この値は、`Firebase`に渡される直前の最終ステップで`Data`に変換されます。
</blockquote>


### 同意

このコマンドは同意モードを構成します。

| リモートコマンド | Firebaseメソッド |
|---|---|
| `setconsent` | `setConsent(consentSettings)` |

| パラメータ | 型 | 説明 |
|---|---|---|
| `firebase_consent_settings` |  `[String:String]` | （必須）同意構成を含むオブジェクト。キーは同意タイプ、値は`granted`または`denied`です。 |

#### サポートされている同意タイプ

| 同意タイプ | Firebase iOSの最小バージョン | Firebase Androidの最小バージョン |
|---|---|---|
| `ad_storage`| 10.7.0 | 18.0.0 |
| `analytics_storage` | 10.7.0 | 18.0.0 |
| `ad_personalization`| 10.17.0 | 21.5.0 |
| `ad_user_data` | 10.17.0 | 21.5.0 |

詳細については、[Firebase：モバイルリモートコマンドタグの構成](https://docs.tealium.com/firebase-remote-command-tag/)を参照してください。

### アナリティクスデータのリセット

このインスタンスのすべてのアナリティクスデータをデバイスから消去し、アプリインスタンスIDをリセットします。

| リモートコマンド | Firebaseメソッド |
|---|---|
| `resetdata` | `resetAnalyticsData()` |