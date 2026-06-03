---
title: リモートコマンド：Firebase
description: AndroidおよびSwift/iOS用Firebaseに対するTealiumリモートコマンド統合
url: https://docs.tealium.com/ja/platforms/remote-commands/integrations/firebase/
---
## 要件

* 以下のいずれかのライブラリ：
  * [Tealium for Android-Kotlin](/ja/platforms/android-kotlin/)（1.0.0以降）
  * [Tealium for Android-Java](/ja/platforms/android-java/)（Firebase 2.0.0&#43;の場合は5.9.0以降、それ以前のバージョンの場合は5.9.0以前）
  * [Tealium for iOS-Swift](/ja/platforms/ios-swift/)
* 以下のいずれかのリモートコマンド統合：
  * [FirebaseリモートコマンドJSONファイル](/ja/platforms/remote-commands/integrations/firebase/#json-template)（Android-Kotlin 1.0.0以降またはiOS-Swift 2.1.0以降が必要）
  * Tealium iQタグ管理の[Firebaseリモートコマンドタグ]()

## 動作原理

Firebase統合は3つの要素を使用します：

1. FirebaseネイティブSDK
1. Firebaseメソッドをラップするリモートコマンドモジュール
1. イベントトラッキングをネイティブFirebaseコールに変換するJSON構成ファイルまたはリモートコマンドタグ

Firebaseリモートコマンドモジュールをアプリに追加すると、アプリにベンダー固有のコードを追加することなく、必要なFirebaseライブラリが自動的にインストールされてビルドされます。依存関係マネージャーのインストールを使用している場合、Firebase SDKを別途インストールする必要はありません。

リモートコマンドオプションには2つあります：JSON構成ファイル、またはiQタグ管理を使用してマッピングを構成します。JSON構成ファイルは、ベンダー統合のためにリモートまたはアプリ内にローカルでホストされることを推奨されるオプションです。iQタグ管理を使用している場合は、ベンダー統合のリモートコマンドタグを追加します。[ベンダー統合についての詳細はこちら](/ja/platforms/remote-commands/how-it-works/#vendor-integrations)。

## インストール

### 依存関係マネージャ





1. Cartfileから`tealium-swift`を削除します。`TealiumFirebase`フレームワークには`tealium-swift`の依存関係がすでに含まれています。

1. Cartfileに以下の行が存在する場合は削除します：  
      ```bash
      binary &#34;https://dl.google.com/dl/firebase/ios/carthage/FirebaseAnalyticsBinary.json&#34;
      ```

1. Cartfileに以下の依存関係を追加します：  
      ```bash
      github &#34;tealium/tealium-ios-firebase-remote-command&#34;
      ```

FirebaseはCarthageバイナリインストールを使用しているため、Carthageの`--use-xcframeworks`フラグを使用して`TealiumFirebase`モジュールを`xcframework`としてビルドすることはできません。依存関係をビルドするためにCarthage公式の[Xcode 12ワークアラウンド](https://github.com/Carthage/Carthage/blob/master/Documentation/Xcode12Workaround.md)を使用することをお勧めします。






1. Podfileに以下の行が存在する場合は削除します：  
      ```bash
      pod &#34;Firebase/Analytics&#34;
      ```  

1. Podfileに以下の依存関係を追加します：  
      ```swift
      pod &#34;TealiumFirebase&#34;
      ```  
      `TealiumFirebase`ポッドには以下の`TealiumSwift`依存関係が含まれています：  
      ```bash
      &#39;tealium-swift/Core&#39;
      &#39;tealium-swift/RemoteCommands&#39;
      ```

1. `TealiumHelper`ファイルおよび`Tealium`クラスまたはFirebaseリモートコマンドにアクセスするその他のファイルで`TealiumSwift`および`TealiumFirebase`モジュールをインポートします。





Cordovaアプリプロジェクトで以下のコマンドを実行して、Tealium Firebaseライブラリをインストールします：

```
cordova plugin add tealium-cordova-firebase-plugin
```





以下のコマンドを実行して、Flutter用のTealium Firebaseライブラリをインストールします：

```
flutter pub add tealium_firebase
import &#39;package:tealium_firebase/tealium_firebase.dart&#39;;
```





[Tealium for Android (Kotlin)](/ja/platforms/android-kotlin/install/)または[Tealium for Android (Java)](/ja/platforms/android-java/install/)をインストールし、まだ行っていない場合はプロジェクトのトップレベルの`build.gradle`ファイルにTealium Maven URLを追加します。


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

1. `build.gradle`ファイルに以下の依存関係を追加します：

      ```groovy
      dependencies {
          implementation &#39;com.tealium.remotecommands:firebase:1.2.0&#39;
      }
      ```





1. React Nativeプロジェクトのルートに移動します。

1. 以下のコマンドで`tealium-react-firebase`パッケージをダウンロードしてインストールします：  
    ```bash
    yarn add tealium-react-firebase
    ```
1. NPMパッケージのバージョン1.0.7ではReact Native Autolinkingが有効になっており、React Nativeのバージョン0.60&#43;を使用している場合、`react-native link`を実行する必要はありません。





1. Xcodeプロジェクトで**File &gt; Add Packages... &gt; Add Package Dependency**を選択します。
1. リポジトリURLを入力します：`https://github.com/tealium/tealium-ios-firebase-remote-command`。
1. バージョンルールを構成します。通常、`Up to next major`を推奨します。現在の`TealiumFirebase`バージョンがリストに表示されない場合は、Swiftパッケージキャッシュをリセットしてください。
1. インストールする`TealiumFirebase`モジュールを選択し、そのモジュールをインストールするアプリターゲットを選択します。

プロジェクトに複数のアプリターゲットがあり、複数のアプリターゲットに`TealiumFirebase`モジュールが必要な場合は、**Frameworks, Libraries, and Embedded Content**セクションで手動で追加する必要があります。

`TealiumFirebase`を追加のアプリターゲットにインストールするには：

1. **Project Navigator**でXcodeプロジェクトを選択します。
1. Xcodeプロジェクトで、**TARGETS**セクションのアプリターゲットを選択します。
1. **General &gt; Frameworks, Libraries &amp; Embedded Content**に移動し、`TealiumFirebase`モジュールをアプリターゲットに追加します。

Tealium Swiftライブラリから追加のモジュールを追加するには、[Swift Package Manager](/ja/platforms/ios-swift/install/#swift-package-manager-recommended)の指示に従ってください。





Visual Studioの組み込みNuGetパッケージマネージャを使用して、Xamarin用のTealium Firebaseライブラリを直接インストールします。

[NuGetパッケージ：Tealium.RemoteCommands.Firebase.Xamarin](https://www.nuget.org/packages/Tealium.RemoteCommands.Firebase.Xamarin)




### 手動インストール




Firebaseリモートコマンドの手動インストールには、[Tealium for Swift](/ja/platforms/ios-swift/)ライブラリがインストールされている必要があります。iOSプロジェクト用のFirebaseリモートコマンドをインストールするには：

1. まだ行っていない場合は、[Firebase SDK](https://firebase.google.com/docs/ios/setup)をインストールします。

1. [Tealium iOS Firebaseリモートコマンド](https://github.com/tealium/tealium-ios-firebase-remote-command)リポジトリをクローンし、`Sources`フォルダ内のファイルをプロジェクトにドラッグします。

1. [`remoteAPIEnabled`](/ja/platforms/ios-swift/api/tealium-config/#remoteapienabled)構成フラグを`true`に構成します。




Firebaseリモートコマンドの手動インストールには、[Tealium for Android (Kotlin)](/ja/platforms/android-kotlin/install/)または[Tealium for Android (Java)](/ja/platforms/android-java/install/)がインストールされている必要があります。

Androidプロジェクト用のFirebaseリモートコマンドをインストールするには：

1. プロジェクトルートの`build.gradle`ファイルに`flatDir`を追加します：

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

1. `&lt;PROJECT_ROOT&gt;/&lt;MODULE&gt;/libs`に`tealium-firebase.aar`を追加します。

1. `build.gradle`ファイルにTealiumライブラリの依存関係を追加します：

      ```groovy
      dependencies {
            implementation(name:&#39;tealium-firebase&#39;, ext:&#39;aar&#39;)
      }
      ```



## 初期化

すべてのTealiumライブラリにおいて、初期化時にFirebaseモバイルリモートコマンドを登録します。





TealiumのAndroid（Java）ライブラリ用のリモートコマンドタグでリモートコマンドを初期化します：
```java
RemoteCommand firebase = new FirebaseRemoteCommand(application);
teal.addRemoteCommand(firebase);
```




JSON構成ファイルまたはTealiumのKotlinライブラリ用のリモートコマンドタグでリモートコマンドを初期化します：
```kotlin
val config = TealiumConfig(application,
        &#34;ACCOUNT&#34;,
        &#34;PROFILE&#34;,
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands, Dispatchers.TagManagement));
val firebase = FirebaseRemoteCommand(application);

var tealium = Tealium.create(TEALIUM_MAIN, config) {

    // Webviewタグ
    remoteCommands?.add(firebase); 

    // ローカルJSON
    //remoteCommands?.add(firebase, filename = &#34;firebase.json&#34;); 

    // リモートJSON
    //remoteCommands?.add(firebase, remoteUrl = &#34;https://some.domain.com/firebase.json&#34;); 
}
```






```javascript
    let Environment = tealium.utils.Environment;
    let Dispatchers = tealium.utils.Dispatchers;

    // Webviewタグ
    let firebase = window.tealium.remotecommands.firebase.create() 

    // ローカルJSON
    //let firebase = window.tealium.remotecommands.firebase.create().setPath(&#34;firebase.json&#34;) 

    // リモートJSON
    //let firebase = window.tealium.remotecommands.firebase.create().setUrl(&#34;https://some.domain.com/firebase.json&#34;) 
    
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
        console.log(&#34;Init was: &#34; &#43; success)
    })
```





プラットフォームオブジェクトに以下の内容の`Google-Servives.json`または`.plist`ファイルを追加します：

```json
// WebViewリモートコマンド
var webViewFirebase = RemoteCommand(TealiumFirebase.commandName)

// ローカルJSONマッピング
var localFirebase = RemoteCommand(
  TealiumFirebase.commandName, 
  path: &#34;firebase.json&#34;
)

// リモートJSONマッピング
var remoteFirebase = RemoteCommand(
  TealiumFirebase.commandName, 
  url: &#34;https://some.domain.com/firebase.json&#34;
)

var config = TealiumConfig(
  // ...
  remoteCommands: [
    webViewFirebase // または `localFirebase`, または `remoteFirebase`
  ])
```





```javascript
import FirebaseRemoteCommand from &#39;tealium-react-firebase&#39;;
FirebaseRemoteCommand.initialize();

// Webviewタグ
let firebase = { id: FirebaseRemoteCommand.name } 

// ローカルJSON
//let firebase = { id: FirebaseRemoteCommand.name, path: &#34;firebase.json&#34; } 

// リモートJSON
//let firebase = { id: FirebaseRemoteCommand.name, url: &#34;https://some.domain.com/firebase.json&#34; } 
let config = TealiumConfig {
    // ...
    remoteCommands: [firebase]
}
```




JSON構成ファイルまたはTealiumのiOS（Swift）ライブラリ用のリモートコマンドタグでリモートコマンドを初期化します：

```swift
var tealium : Tealium?
let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                           profile: &#34;PROFILE&#34;,
                           environment: &#34;ENVIRONMENT&#34;,
                           dataSource: &#34;DATASOURCE&#34;)
config.dispatchers = [Dispatchers.TagManagement, Dispatchers.RemoteCommands]
config.remoteAPIEnabled = true // リモートコマンドを使用するために必要

tealium = Tealium(config: config) { _ in
    guard let remoteCommands = self.tealium?.remoteCommands else {
        return
    }

    // Webviewタグ
    let firebase = FirebaseRemoteCommand() 

    // ローカルJSON
    //let firebase = FirebaseRemoteCommand(type: .local(file: &#34;firebase&#34;)) 

    // リモートJSON
    //let firebase = FirebaseRemoteCommand(type: .remote(url: &#34;https://some.domain.com/firebase.json&#34;)) 
    
    remoteCommands.add(firebase)
}
```





```csharp

// Webviewタグ
var firebase = new FirebaseRemoteCommandDroid(this.Application, null, null); 

// ローカルJSON
//var firebase = new FirebaseRemoteCommandDroid(this.Application, &#34;firebase.json&#34;, null); 

// リモートJSON
//var firebase = new FirebaseRemoteCommandDroid(this.Application, null, &#34;https://some.domain.com/firebase.json&#34;); 

var commands = new List&lt;IRemoteCommand&gt; {
    firebase
};
TealiumConfig config = new TealiumConfig(ACCOUNT_NAME,
                                          PROFILE_NAME,
                                          ENVIRONMENT,
                                          new List&lt;Dispatchers&gt; {
                                              Dispatchers.RemoteCommands, Dispatchers.TagManagement
                                          },
                                          new List&lt;Collectors&gt; {},
                                          remoteCommands: commands
                                          );
```




```csharp

// Webviewタグ
var firebase = new FirebaseRemoteCommandIOS(new RemoteCommandTypeWrapper()); 

// ローカルJSON
//var firebase = new FirebaseRemoteCommandIOS(new RemoteCommandTypeWrapper(&#34;firebase&#34;, NSBundle.MainBundle));

// リモートJSON
//var firebase = new FirebaseRemoteCommandIOS(new RemoteCommandTypeWrapper(&#34;https://some.domain.com/firebase.json&#34;)); 

var commands = new List&lt;IRemoteCommand&gt; {
    firebase
};
TealiumConfig config = new TealiumConfig(ACCOUNT_NAME,
                                          PROFILE_NAME,
                                          ENVIRONMENT,
                                          new List&lt;Dispatchers&gt; {
                                              Dispatchers.RemoteCommands, Dispatchers.TagManagement
                                          },
                                          new List&lt;Collectors&gt; {},
                                          remoteCommands: commands
                                          );
```


## JSONテンプレート

[JSON構成ファイル](/ja/platforms/remote-commands/how-it-works/#json-configuration-file)を使用してリモートコマンドを構成する場合は、以下のテンプレートを参照してください。このテンプレートには、標準的なeコマースインストールで使用される一般的なマッピングが含まれています。必要に応じてマッピングを編集してください。

```json
{
    &#34;config&#34;: {
        &#34;firebase_analytics_enabled&#34;: &#34;true&#34;,
        &#34;firebase_session_timeout_seconds&#34;: &#34;30&#34;,
        &#34;firebase_log_level&#34;: &#34;max&#34;,
        &#34;firebase_session_minimum_seconds&#34;: &#34;100&#34;
    },
    &#34;mappings&#34;: {
        &#34;achievement_id&#34;: &#34;event.param_achievement_id&#34;,
        &#34;ad_network_click_id&#34;: &#34;event.param_ad_network_click_id&#34;,
        &#34;affiliation&#34;: &#34;event.param_affiliation&#34;,
        &#34;campaign_keywords&#34;: &#34;event.param_cp1&#34;,
        &#34;campaign&#34;: &#34;event.param_campaign&#34;,
        &#34;game_character&#34;: &#34;event.param_character&#34;,
        &#34;checkout_option&#34;: &#34;event.param_checkout_option&#34;,
        &#34;checkout_step&#34;: &#34;event.param_checkout_step&#34;,
        &#34;content&#34;: &#34;event.param_content&#34;,
        &#34;content_type&#34;: &#34;event.param_content_type&#34;,
        &#34;coupon&#34;: &#34;event.param_coupon&#34;,
        &#34;creative_name&#34;: &#34;event.param_creative_name&#34;,
        &#34;creative_slot&#34;: &#34;event.param_creative_slot&#34;,
        &#34;currency_code&#34;: &#34;event.param_currency&#34;,
        &#34;travel_destination&#34;: &#34;event.param_destination&#34;,
        &#34;end_date&#34;: &#34;event.param_end_date&#34;,
        &#34;flight_number&#34;: &#34;event.param_flight_number&#34;,
        &#34;group_id&#34;: &#34;event.param_group_id&#34;,
        &#34;current_index&#34;: &#34;param_index&#34;,
        &#34;product_brand&#34;: &#34;items.param_item_brand&#34;,
        &#34;product_category&#34;: &#34;items.param_item_category&#34;,
        &#34;product_id&#34;: &#34;items.param_item_id&#34;,
        &#34;product_unit_price&#34;: &#34;items.param_price&#34;,
        &#34;product_quantity&#34;: &#34;items.param_quantity&#34;,
        &#34;product_list&#34;: &#34;items.param_item_list&#34;,
        &#34;product_location_id&#34;: &#34;items.param_item_location_id&#34;,
        &#34;product_name&#34;: &#34;items.param_item_name&#34;,
        &#34;product_variant&#34;: &#34;items.param_item_variant&#34;,
        &#34;current_level&#34;: &#34;event.param_level&#34;,
        &#34;most_recent_location&#34;: &#34;event.param_location&#34;,
        &#34;campaign_medium&#34;: &#34;event.param_medium&#34;,
        &#34;number_nights&#34;: &#34;event.param_number_nights&#34;,
        &#34;number_pax&#34;: &#34;event.param_number_pax&#34;,
        &#34;number_rooms&#34;: &#34;event.param_number_rooms&#34;,
        &#34;travel_origin&#34;: &#34;event.param_origin&#34;,
        &#34;score&#34;: &#34;event.param_score&#34;,
        &#34;search_keyword&#34;: &#34;event.param_search_term&#34;,
        &#34;order_shipping_amount&#34;: &#34;event.param_shipping&#34;,
        &#34;signup_method&#34;: &#34;event.param_signup_method&#34;,
        &#34;campaign_source&#34;: &#34;event.param_source&#34;,
        &#34;start_date&#34;: &#34;event.param_start_date&#34;,
        &#34;order_tax_amount&#34;: &#34;event.param_tax&#34;,
        &#34;product_term&#34;: &#34;event.param_term&#34;,
        &#34;order_id&#34;: &#34;event.param_transaction_id&#34;,
        &#34;travel_class&#34;: &#34;event.param_travel_class&#34;,
        &#34;order_total&#34;: &#34;event.param_value&#34;,
        &#34;currency_type&#34;: &#34;event.param_virtual_currency_name&#34;,
        &#34;user_signup_method&#34;: &#34;event.param_user_signup_method&#34;,
        &#34;event_title&#34;: &#34;firebase_event_name&#34;,
        &#34;screen_name&#34;: &#34;firebase_screen_name&#34;,
        &#34;screen_class&#34;: &#34;firebase_screen_class&#34;,
        &#34;customer_property&#34;: &#34;firebase_property_name&#34;,
        &#34;customer_value&#34;: &#34;firebase_property_value&#34;,
        &#34;customer_id&#34;: &#34;firebase_user_id&#34;,
        &#34;consent_ad_storage&#34;: &#34;firebase_consent_settings.ad_storage&#34;,
        &#34;consent_analytics_storage&#34;: &#34;firebase_consent_settings.analytics_storage&#34;,
        &#34;consent_ad_user_data&#34;: &#34;firebase_consent_settings.ad_user_data&#34;,
        &#34;consent_ad_personalization&#34;: &#34;firebase_consent_settings.ad_personalization&#34;
    },
    &#34;commands&#34;: {
        &#34;launch&#34;: &#34;config&#34;,
        &#34;user_login&#34;: &#34;logevent&#34;,
        &#34;user_register&#34;: &#34;logevent,setuserproperty&#34;,
        &#34;share&#34;: &#34;logevent&#34;,
        &#34;show_offers&#34;: &#34;logevent&#34;,
        &#34;join_group&#34;: &#34;logevent&#34;,
        &#34;travel_order&#34;: &#34;logevent&#34;,
        &#34;earn_currency&#34;: &#34;logevent&#34;,
        &#34;spend_currency&#34;: &#34;logevent&#34;,
        &#34;unlock_achievement&#34;: &#34;logevent&#34;,
        &#34;level_up&#34;: &#34;logevent&#34;,
        &#34;start_tutorial&#34;: &#34;logevent&#34;,
        &#34;stop_tutorial&#34;: &#34;logevent&#34;,
        &#34;record_score&#34;: &#34;logevent&#34;,
        &#34;category&#34;: &#34;logevent,setscreenname&#34;,
        &#34;product&#34;: &#34;logevent,setscreenname&#34;,
        &#34;cart_add&#34;: &#34;logevent&#34;,
        &#34;wishlist_add&#34;: &#34;logevent&#34;,
        &#34;checkout&#34;: &#34;logevent,setscreenname&#34;,
        &#34;checkout_progress&#34;: &#34;logevent&#34;,
        &#34;email_signup&#34;: &#34;logevent&#34;,
        &#34;order&#34;: &#34;logevent,setscreenname&#34;,
        &#34;setconsent&#34;: &#34;setconsent&#34;,
        &#34;initiateconversionmeasurement&#34;: &#34;initiateconversionmeasurement&#34;,
        &#34;resetanalyticsdata&#34;: &#34;resetdata&#34;
    }
}
```

## サポートされているメソッド

Firebaseメソッドに対応するコマンドをマッピングします。Firebaseメソッドをトリガーするには、指定された形式で対応するコマンドを渡します。

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

### SDKの構成

### 構成

| リモートコマンド | Firebaseメソッド |
|---|---|
| `config` | `configure()` |

SDKを構成するために使用されるパラメータは次のとおりです：

| パラメータ | タイプ | 説明 |
|---|---|---|
| `firebase_session_timeout_seconds` |  `String` | セッションの長さを秒単位で表した文字列です。 |
| `firebase_analytics_enabled` |  `String` | 分析を有効または無効にするためのブール値を表す文字列（デフォルトは `true`）。 |
| `firebase_log_level` (iOS) |  `String` | ログレベル min|max|error|debug|notice|warning|info (デフォルトは `min`)。 |

### トラック

アプリとの基本的なやり取りによってトリガーされるイベントは自動的に追跡されます。詳細については、[GA4: 自動収集されるイベント](https://support.google.com/firebase/answer/6317485?hl=ja)を参照してください。

#### イベントログ

パラメータと、オプションでアイテムの配列を使用してイベントをログします。

| リモートコマンド | Firebaseメソッド |
|---|---|
| `logevent` | `logEvent(name, parameters)` |

| パラメータ | タイプ | 説明 |
|---|---|---|
| `firebase_event_name` |  `String` | 必須。イベント名で、Firebaseイベント名のリストにマッピングされます。 |
| `event` (JSON) |  `[String:Any]` | このイベントのすべてのパラメータを含むオブジェクトで、Firebaseパラメータのリストにマッピングされます。 |
| `firebase_event_params` (Tag) | `[String:Any]` | このイベントのすべてのパラメータを含むオブジェクト（タグによって使用されます）、Firebaseパラメータのリストにマッピングされます。 |
| `items` (JSON) |  `[String:[Any]]` | このイベントのアイテムの配列を含むオブジェクト。すべての配列には同じ数の要素が含まれ、すべての要素は単一のアイテム配列に正規化できます。 |
| `param_items` (Tag) | `[[String:Any]]` | このイベントのアイテムの配列（タグによって使用されます）。 |

#### スクリーン名の構成

このコマンドは、ユーティリティとして追加された特定のログイベントです。

| リモートコマンド | Firebaseメソッド (iOS) | Firebaseメソッド (Android) |
|---|---|---|
| `setscreenname` | `logEvent(name (AnalyticsEventScreenView), parameters)` | `setCurrentScreen(currentActivity, screenName, screenClass)` |

| パラメータ | タイプ | 説明 |
|---|---|---|
| `firebase_screen_name` |  `String` | 必須。現在のスクリーンの名前です。 |
| `firebase_screen_class` |  `String` | 現在のスクリーンのクラスです。 |

#### デフォルトパラメータの構成

このコマンドは、すべてのログイベントで送信されるパラメータを構成します。

| リモートコマンド | Firebaseメソッド |
|---|---|
| `setdefaultparameters` | `setDefaultEventParameters(parameters)` |

| パラメータ | タイプ | 説明 |
|---|---|---|
| `default` (JSON) |  `[String:Any]` | キーと値のデフォルトパラメータを含むオブジェクトです。 |
| `firebase_default_params` (Tag) |  `String` | キーと値のデフォルトパラメータを含むオブジェクト（タグによって使用されます）。 |


### マッピング

`logEvent` メソッドで送信されるパラメータとイベントは、Tealiumの値からFirebaseの定数名にマッピングされます。

以下の表は、iOSとAndroidで利用可能なキーを定数にマッピングしたものです。Tealiumのマッピングからパラメータが欠けている場合は、Firebaseの定数値を直接使用できます。

#### イベントマッピング

| Tealium Key | Firebase Event (iOS) | Firebase Event (Android) |
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

#### パラメータマッピング

| Tealium Key | Firebase Parameter (iOS) | Firebase Parameter (Android) |
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

### ユーザー構成


#### ユーザープロパティの構成

このコマンドは、1つまたは複数のユーザープロパティ名と値を構成します。

| リモートコマンド | Firebase メソッド |
|---|---|
| `setuserproperty` | `setUserProperty(value, name)` |

| パラメータ | タイプ | 説明 |
|---|---|---|
| `firebase_property_name` |  `String\|[String]` | 必須。プロパティ名またはプロパティ名の配列 |
| `firebase_property_value` |  `String\|[String]` | 必須。プロパティ値またはプロパティ値の配列。このパラメータが配列の場合、`firebase_property_name` 配列の長さと項目の順序と一致する必要があります。 |

#### ユーザーIDの構成

このコマンドはユーザーIDを構成します。

| リモートコマンド | Firebase メソッド |
|---|---|
| `setuserid` | `setUserId(id)` |

| パラメータ | タイプ | 説明 |
|---|---|---|
| `firebase_user_id`|  `String` | 必須。構成するユーザーID |

### コンバージョン測定（iOS）

このコマンドはコンバージョン測定を開始します。

| リモートコマンド | Firebase メソッド |
|---|---|
| `initiateconversionmeasurement` | `initiateOnDeviceConversionMeasurement()` |

| パラメータ | タイプ | 説明 |
|---|---|---|
| `param_hashed_email_address` | `String` | ハッシュ化されたユーザーのメールアドレス |
| `param_hashed_phone_number` | `String` | ハッシュ化されたユーザーの電話番号 |
| `param_email_address` | `String` | ユーザーのメールアドレス |
| `param_phone_number` | `String` | ユーザーの電話番号 |

 パラメータをハッシュ化して送信する場合は、[Firebase ドキュメントの iOS 広告のコンバージョン測定](https://firebase.google.com/docs/tutorials/ads-ios-on-device-measurement/step-3)に従って正規化およびハッシュ化する必要があります。Tealiumはパラメータを `String` として受け取る必要があります。これは最終的に `Firebase` に渡す前に `Data` に変換されます。

### 同意

このコマンドは同意モードを構成します。

| リモートコマンド | Firebase メソッド |
|---|---|
| `setconsent` | `setConsent(consentSettings)` |

| パラメータ | タイプ | 説明 |
|---|---|---|
| `firebase_consent_settings` |  `[String:String]` | 必須。同意構成を含むオブジェクト。キーは同意タイプ、値は `granted` または `denied` |

#### サポートされる同意タイプ

| 同意タイプ | 最小 Firebase iOS バージョン | 最小 Firebase Android バージョン |
|---|---|---|
| `ad_storage`| 10.7.0 | 18.0.0 |
| `analytics_storage` | 10.7.0 | 18.0.0 |
| `ad_personalization`| 10.17.0 | 21.5.0 |
| `ad_user_data` | 10.17.0 | 21.5.0 |

詳細については、[Firebase: Mobile Remote Command Tag setup]()を参照してください。

### アナリティクスデータのリセット

このデバイスのすべてのアナリティクスデータをクリアし、アプリインスタンスIDをリセットします。

| リモートコマンド | Firebase メソッド |
|---|---|
| `resetdata` | `resetAnalyticsData()` |
