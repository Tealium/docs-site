---
title: リモートコマンド：Facebook
description: AndroidおよびSwift/iOS向けのTealiumリモートコマンドによるFacebook連携。
url: https://docs.tealium.com/ja/platforms/remote-commands/integrations/facebook/
---
## 要件

* 以下のいずれかのモバイルライブラリ：
  * [Tealium for Android（Kotlin）](https://docs.tealium.com/ja/platforms/android-kotlin/)（1.0.0以降）。
  * [Tealium for Android（Java）](https://docs.tealium.com/ja/platforms/android-java/)（Facebook 1.0.0以降の場合は5.9.0以降、それより前のバージョンの場合は5.9.0未満）。
  * [Tealium for iOS（Swift）](https://docs.tealium.com/ja/platforms/ios-swift/)。
* 以下のいずれかのリモートコマンド連携：
  * [FacebookリモートコマンドJSONファイル](https://docs.tealium.com/ja/platforms/remote-commands/integrations/facebook/.#json-template)（Android-Kotlin 1.0.0以降またはiOS-Swift 2.1.0以降が必要）。
  * タグ管理のFacebookリモートコマンドタグ。

iOSおよびAndroidの要件は次のとおりです。  




次のキーを`app/src/main/res/values/strings.xml`ファイルに追加します。`[APP_ID]`をFacebookアプリIDに、`[CLIENT_TOKEN]`をFacebookクライアントトークンに置き換えます。
```xml
<string name="facebook_app_id">[APP_ID]</string>
<string name="fb_login_protocol_scheme">fb[APP_ID]</string>
<string name="facebook_client_token">[CLIENT_TOKEN]</string>
```

`AndroidManifest.xml`ファイルには、次の`meta-data`要素が必要です。
```xml
<application android:label="@string/app_name" ...>
    ...
    <meta-data
      android:name="com.facebook.sdk.ApplicationId"
      android:value="@string/facebook_app_id" />
    <meta-data 
        android:name="com.facebook.sdk.ClientToken"
        android:value="@string/facebook_client_token" />
    ...
</application>
```

詳細については、[Facebook Androidスタートガイド - AndroidアプリへのFacebook SDKの統合](https://developers.facebook.com/docs/app-events/getting-started-app-events-android)を参照してください。




次のキーを`Info.plist`ファイルに追加します。`[APP_ID]`をFacebookアプリIDに、`[APP_NAME]`をアプリ名に、`[CLIENT_TOKEN]`をFacebookクライアントトークンに置き換えます。  
```xml
<key>CFBundleURLTypes</key>
<array>
  <dict>
  <key>CFBundleURLSchemes</key>
  <array>
    <string>fb[APP_ID]</string>
  </array>
  </dict>
</array>
<key>FacebookAppID</key>
<string>[APP_ID]</string>
<key>FacebookDisplayName</key>
<string>[APP_NAME]</string>
<key>FacebookClientToken</key>
<string>[CLIENT_TOKEN]</string>
```
詳細については、[Facebook iOSスタートガイド - プロパティリストの構成](https://developers.facebook.com/docs/app-events/getting-started-app-events-ios/#plist-config)を参照してください。

`AppDelegate`のコードを次のように更新します。

1. `FBSDKCoreKit`をインポートします。
2. `didFinishLaunchingWithOptions`メソッドに次のコードを追加します。  
      ```swift
      ApplicationDelegate.shared.application(
            application, 
            didFinishLaunchingWithOptions: launchOptions)
      ```
3. `AppDelegate.swift`（または同等のObjective-Cコード）に次の関数を追加します。
      ```swift
      func application(
            _ app: UIApplication,
            open url: URL,
            options: [UIApplicationOpenURLOptionsKey : Any] = [:]) -> Bool {
        let handled = ApplicationDelegate.shared.application(
            app,
            open: url,
            options: options)
      }
      ```
詳細については、[Facebook iOSスタートガイド - 開発環境の構成](https://developers.facebook.com/docs/app-events/getting-started-app-events-ios/#dev-env-setup)を参照してください。




## 仕組み

Facebook連携では、次の3つの項目を使用します。

1. FacebookネイティブSDK。
2. Facebookのメソッドをラップするリモートコマンドモジュール。
3. イベントトラッキングをFacebookのネイティブ呼び出しに変換するJSON構成ファイルまたはリモートコマンドタグ。

Facebookリモートコマンドモジュールをアプリに追加すると、アプリにベンダー固有のコードを追加することなく、必要なFacebookライブラリが自動的にインストールおよびビルドされます。依存関係マネージャーを使用してインストールする場合、Facebook SDKを個別にインストールする必要はありません。

リモートコマンドには、JSON構成ファイルを使用する方法と、タグ管理を使用してマッピングを構成する方法の2つがあります。ベンダー連携には、リモートまたはアプリ内のローカルでホストされるJSON構成ファイルの使用を推奨します。タグ管理を使用する場合は、ベンダー連携用のリモートコマンドタグを追加します。詳しくは、[ベンダー連携](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/#vendor-integrations)を参照してください。

## インストール

### 依存関係マネージャー




1. Xcodeプロジェクトで、**File > Add Packages... > Add Package Dependency**を選択します。
2. リポジトリURLとして`https://github.com/tealium/tealium-ios-facebook-remote-command`を入力します。
3. バージョンルールを構成します。通常は`Up to next major`を推奨します。現在の`TealiumFacebook`バージョンがリストに表示されない場合は、Swiftパッケージのキャッシュをリセットしてください。
4. インストールする`TealiumFacebook`モジュールを選択し、モジュールのインストール先となるアプリターゲットを選択します。

プロジェクトに複数のアプリターゲットがあり、追加のアプリターゲットでも`TealiumFacebook`モジュールが必要な場合は、**Frameworks, Libraries, and Embedded Content**セクションで手動で追加する必要があります。

追加のアプリターゲットに`TealiumFacebook`をインストールするには、次の手順を実行します。

1. **Project Navigator**でXcodeプロジェクトを選択します。
2. Xcodeプロジェクトの**TARGETS**セクションでアプリターゲットを選択します。
3. **General > Frameworks, Libraries & Embedded Content**に移動し、アプリターゲットに追加する`TealiumFacebook`モジュールを選択します。

Tealium Swiftライブラリから追加のモジュールを追加するには、[Swift Package Manager](https://docs.tealium.com/ja/platforms/ios-swift/install/#swift-package-manager-recommended)の手順に従ってください。




1. Podfileに`tealium-swift`と`pod "FBSDKCoreKit"`がすでに存在する場合は削除します。`tealium-swift`への依存関係は、`TealiumFacebook`フレームワークにすでに含まれています。

2. Podfileに次の依存関係を追加します。
      ```ruby
      pod "TealiumFacebook"
      ```
      `TealiumFacebook` Podには、次の`TealiumSwift`依存関係が含まれています。  
      ```bash
      'tealium-swift/Core'
      'tealium-swift/RemoteCommands'
      'tealium-swift/TagManagement'
      ```

3. `TealiumHelper`ファイル、および`Tealium`クラスまたはFacebookリモートコマンドにアクセスするその他のファイルで、`TealiumSwift`モジュールと`TealiumFacebook`モジュールをインポートします。




1. Cartfileから`tealium-swift`を削除します。`tealium-swift`への依存関係は、`TealiumFacebook`フレームワークにすでに含まれています。

2. Cartfileに次の行が存在する場合は削除します。  
      ```bash
      github "facebook/facebook-ios-sdk"
      ```

3. Cartfileに次の依存関係を追加します。  
      ```bash
      github "tealium/tealium-ios-facebook-remote-command"
      ```


<blockquote>
最新のFacebookリモートコマンド連携には、Tealium for Swift SDK（バージョン2.12以降）が必要です。
</blockquote>






1. まだ実行していない場合は、[Tealium for Android（Kotlin）](https://docs.tealium.com/ja/platforms/android-kotlin/install/)または[Tealium for Android（Java）](https://docs.tealium.com/ja/platforms/android-java/install/)をインストールし、プロジェクトの最上位`build.gradle`ファイルにTealium Maven URLを追加します。


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

2. アプリプロジェクトの`build.gradle`ファイルに次の依存関係を追加し、Facebook SDKとTealium-Facebookリモートコマンドの両方をインポートします。  
      ```groovy
      dependencies {
            implementation 'com.tealium.remotecommands:facebook:3.0.0'
      }
      ```


### 手動インストール




Facebookリモートコマンドを手動でインストールするには、[Tealium for Swift](https://docs.tealium.com/ja/platforms/ios-swift/)ライブラリがインストールされている必要があります。iOSプロジェクトにFacebookリモートコマンドをインストールするには、次の手順を実行します。

1. まだインストールしていない場合は、[Facebook SDK](https://github.com/facebook/facebook-ios-sdk/tree/master/FBSDKCoreKit)をインストールします。

2. [Tealium iOS Facebookリモートコマンド](https://github.com/tealium/tealium-ios-facebook-remote-command)リポジトリをクローンし、`Sources`フォルダー内のファイルをプロジェクトにドラッグします。

3. ディスパッチャーとして`Dispatchers.RemoteCommands`を追加します。

4. [`remoteAPIEnabled`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#remoteapienabled)構成フラグを`true.`に構成します。




Facebookリモートコマンドを手動でインストールするには、[Tealium for Android（Kotlin）](https://docs.tealium.com/ja/platforms/android-kotlin/install/)または[Tealium for Android（Java）](https://docs.tealium.com/ja/platforms/android-java/install/)がインストールされている必要があります。

AndroidプロジェクトにFacebookリモートコマンドをインストールするには、次の手順を実行します。

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

2. `tealium-facebook.aar`を`<PROJECT_ROOT>/<MODULE>/libs`に追加します。

3. `build.gradle`ファイルにTealiumライブラリの依存関係を追加します。  
      ```groovy
      dependencies {
            implementation(name:'tealium-facebook', ext:'aar')
      }
      ```



## 初期化

すべてのTealiumライブラリで、初期化時にFacebookリモートコマンドを登録します。





JSON構成ファイルまたはリモートコマンドタグを使用して、TealiumのiOS（Swift）ライブラリ用のリモートコマンドを初期化します。
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
    let facebook = FacebookRemoteCommand(launchOptions: launchOptions) 

    // Local JSON
    //let facebook = FacebookRemoteCommand(type: .local(file: "facebook"), launchOptions: launchOptions) 

    // Remote JSON
    //let facebook = FacebookRemoteCommand(type: .remote(url: "https://some.domain.com/facebook.json"), launchOptions: launchOptions) 

    remoteCommands.add(facebook)
}
```



JSON構成ファイルまたはリモートコマンドタグを使用して、TealiumのKotlinライブラリ用のリモートコマンドを初期化します。
```kotlin
val config = TealiumConfig(application,
        "ACCOUNT",
        "PROFILE",
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands, Dispatchers.TagManagement));
val facebook = FacebookRemoteCommand(application);

var tealium = Tealium.create(TEALIUM_MAIN, config) {
    // Webview Tag
    remoteCommands?.add(facebook); 

    // Local JSON
    //remoteCommands?.add(facebook, filename = "facebook.json"); 

    // Remote JSON
    //remoteCommands?.add(facebook, remoteUrl = "https://some.domain.com/facebook.json"); 
}
```



リモートコマンドタグを使用して、TealiumのAndroid（Java）ライブラリ用のリモートコマンドを初期化します。   
```java
import com.tealium.remotecommands.facebook.FacebookRemoteCommand;

Tealium.Config config = Tealium.Config.create(application, "ACCOUNT", "PROFILE", "ENVIRONMENT");
Tealium teal = Tealium.createInstance(TEALIUM_MAIN, config);

FacebookRemoteCommand facebook = new FacebookRemoteCommand(this);

// register the command
teal.addRemoteCommand(facebook);
```




## JSONテンプレート

[JSON構成ファイル](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/#json-configuration-file)を使用してリモートコマンドを構成する場合は、以下のテンプレートを参照して作業を開始してください。このテンプレートには、標準的なEコマース実装で使用される一般的なマッピングが含まれています。必要に応じてマッピングを編集してください。

```json
{
  "config": {
    "applicationid": "YOUR_APP_ID",
    "clienttoken": "YOUR_CLIENT_TOKEN",
    "accesstoken": "YOUR_ACCESS_TOKEN",
    "userid": "YOUR_USER_ID",
    "auto_log": true,
    "auto_log_events_enabled": true,
    "auto_initialized": true,
    "advertiser_id_collection_enabled": true,
    "advertiser_collection": true,
    "debug": true
  },
  "mappings": {
    "achievement_type": "event.fb_description",
    "ad_type": "event.ad_type",
    "content": "event.fb_content",
    "content_type": "event.fb_content_type",
    "currency_code": "event.fb_currency",
    "event_name": "event.fb_description",
    "current_level": "event.fb_level",
    "pet_count": "event.fb_max_rating_value",
    "number_of_items": "event.fb_num_items",
    "order_id": "event.fb_order_id",
    "payment_info_available": "event.fb_payment_info_available",
    "signup_method": "event.fb_registration_method",
    "search_keyword": "event.fb_search_string",
    "success": "event.fb_success",
    "customer_email": "user.em",
    "customer_first_name": "user.fn",
    "customer_last_name": "user.ln",
    "customer_phone": "user.ph",
    "customer_dob": "user.dob",
    "customer_gender": "user.ge",
    "customer_city": "user.ct",
    "customer_state": "user.st",
    "customer_zip": "user.zp",
    "customer_country": "user.country",
    "customer_id": "fb_user_id",
    "user_value": "fb_user_value",
    "user_key": "fb_user_key",
    "product_id": "product.fb_product_item_id,event.fb_content_id",
    "product_availability": "product.fb_product_availability",
    "product_condition": "product.fb_product_condition",
    "product_description": "product.fb_product_description,event.fb_product_description",
    "product_image_link": "product.fb_product_image_link",
    "product_link": "product.fb_product_link",
    "product_name": "product.fb_product_title",
    "product_variant": "product.fb_product_gtin",
    "product_brand": "product.fb_product_brand",
    "product_price": "product.fb_product_price_amount,event.fb_value_to_sum",
    "product_currency": "product.fb_product_price_currency",
    "product_alias": "product_parameters.product_alias",
    "product_color": "product_parameters.product_color",
    "order_total": "purchase.fb_purchase_amount",
    "order_currency": "purchase.fb_purchase_currency",
    "customer_status": "purchase_parameters.customer_status",
    "coupon": "purchase_parameters.coupon",
    "push_action": "push.fb_push_action",
    "push_payload": "push.fb_push_payload",
    "tealium_event": "command_name"
  },
  "commands": {
    "launch": "initialize,setautologappeventsenabled,setautoinitenabled,enableadvertiseridcollection",
    "user_login": "setuser,setuserid",
    "email_signup": "updateuservalue",
    "level_up": "achievedlevel",
    "user_register": "completedregistration",
    "unlock_achievement": "unlockedachievement",
    "cart_add": "addedtocart",
    "custom_attribute": "rated",
    "wishlist_add": "addedtowishlist",
    "payment": "initiatedcheckout",
    "product": "logproductitem",
    "order": "logpurchase",
    "flush": "flush",
    "customfbevent": "customfbevent"
  }
}
```
## プッシュメッセージトラッキング（iOS）

Tealium Swift ライブラリには、Tealium および Facebook リモートコマンドを通じてプッシュメッセージトラッキングを処理するための `TealiumRegistration` プロトコルが含まれています。ラッパークラス `FacebookInstance` でこのプロトコルに準拠しており、プッシュメッセージの許可イベント、プッシュメッセージの開封イベント、およびアンインストールのトラッキングを送信するために使用されます。プッシュメッセージトラッキング機能を活用することを推奨します。

iOS プロジェクトにプッシュメッセージトラッキングを統合するには、次の手順を実行します。

1. `TealiumHelper.swift` ファイルで、`TealiumRegistration` プロトコルに準拠するオブジェクトの空の配列を初期化します。例：  
      ```swift
      var pushMessagingHelpers = [TealiumRegistration]()
      ```
2. `FacebookRemoteCommand` より先に `FacebookInstance` を初期化します。
3. 上記の配列に `FacebookInstance` を追加します。

次に、プッシュメッセージトラッキングの統合例を示します。
```swift
var pushMessagingHelpers = [TealiumRegistration]()

//...

teal = Tealium(config: config) { responses in
      guard let remoteCommands = self.tealium?.remoteCommands() else {
            return
      }
      let facebookInstance = FacebookInstance()
      let facebookRemoteCommand = FacebookRemoteCommand(facebookInstance: facebookInstance)
      remoteCommands.add(facebookRemoteCommand)
      self.pushMessagingHelpers.append(facebookInstance)
}
```

`TealiumHelper.swift` ファイル全体を確認するには、[Facebook リモートコマンドのサンプルアプリ](https://github.com/Tealium/tealium-ios-facebook-remote-command/tree/master/Examples)を参照してください。ユーザーが通知に登録したとき、プッシュメッセージを開いたとき、またはアプリをアンインストールしたときに Facebook へイベントを送信する方法については、`AppDelegate.swift` ファイルを参照してください。

## サポートされているメソッド

各 Facebook メソッドにコマンドをマッピングします。Facebook メソッドをトリガーするには、対応するコマンドを指定された形式で渡します。

| リモートコマンド | Facebook メソッド | サポートされているプラットフォーム |
| -------------- | --------------- | ------------------- |
| `clearuser`(ios)/`clearuserdata`(android) | `clearUserData()` | iOS、Android |
| `clearuserid` | `clearUserId()` | iOS、Android |
| `enableadvertiseridcollection` | `setAdvertiserIDCollectionEnabled()` | iOS、Android |
| `flush` | `flush()` | iOS、Android |
| `initialize` | `initialize()` | iOS、Android |
| `logproductitem` | `logProductItem()` | iOS、Android |
| `logpurchase` | `logPurchase()` | iOS、Android |
| `setautoinitenabled` | `setAutoInitEnabled()` | Android |
| `setautologappeventsenabled` | `setAutoLogAppEventsEnabled()` | iOS、Android |
| `setflushbehavior` | `setFlushBehavior()` | iOS、Android |
| `setpushregistrationid` | `setPushNotificationsRegistrationId()` | Android のみ |
| `setuser`(ios, android)/`updateUserValue`(ios) | `setUserData()` | iOS、Android |
| `setuserid` | `setUserId()` | iOS、Android |
| 以下のいずれかのイベント名 | `logEvent()` | iOS、Android |

### 標準イベント名

次に、`logEvent` メソッドでサポートされている標準イベント名の一覧を示します。以下のいずれかのコマンド名が送信されると、Facebook SDK で自動的にトリガーされます。これは、該当するイベントに必要なすべての変数がマッピングおよび定義されていることを前提としています。[アプリ内イベントの記録](https://developers.facebook.com/docs/app-events/getting-started-app-events-ios/#manually-log-events)について詳しく確認してください。

| リモートコマンド               | Facebook イベント名                                |
| :--------------------------- | :------------------------------------------------ |
| `activatedapp`               | `FBSDKAppEventNameActivatedApp`                   |
| `achievedlevel`              | `FBSDKAppEventNameAchievedLevel`                  |
| `adclick`                    | `FBSDKAppEventNameAdClick`                        |
| `adimpression`               | `FBSDKAppEventNameAdImpression`                   |
| `addedpaymentinfo`           | `FBSDKAppEventNameAddedPaymentInfo`               |
| `addedtocart`                | `FBSDKAppEventNameAddedToCart`                    |
| `addedtowishlist`            | `FBSDKAppEventNameAddedToWishlist`                |
| `completedregistration`      | `FBSDKAppEventNameCompletedRegistration`          |
| `completedtutorial`          | `FBSDKAppEventNameCompletedTutorial`              |
| `contact`                    | `FBSDKAppEventNameContact`                        |
| `customizeproduct`           | `FBSDKAppEventNameCustomizeProduct`               |
| `deactivatedapp`             | `FBSDKAppEventNameDeactivatedApp`                 |
| `donate`                     | `FBSDKAppEventNameDonate`                         |
| `findlocation`               | `FBSDKAppEventNameFindLocation`                   |
| `initiatedcheckout`          | `FBSDKAppEventNameInitiatedCheckout`              |
| `livestreamingstart`         | `FBSDKAppEventNameLiveStreamingStart`             |
| `livestreamingstop`          | `FBSDKAppEventNameLiveStreamingStop`              |
| `livestreamingpause`         | `FBSDKAppEventNameLiveStreamingPause`             |
| `livestreamingresume`        | `FBSDKAppEventNameLiveStreamingResume`            |
| `livestreamingerror`         | `FBSDKAppEventNameLiveStreamingError`             |
| `livestreamingupdatestatus`  | `FBSDKAppEventNameLiveStreamingUpdateStatus`      |
| `productcatalogupdate`       | `FBSDKAppEventNameProductCatalogUpdate`           |
| `pushtokenobtained`          | `FBSDKAppEventNamePushTokenObtained`              |
| `rated`                      | `FBSDKAppEventNameRated`                          |
| `schedule`                   | `FBSDKAppEventNameSchedule`                       |
| `searched`                   | `FBSDKAppEventNameSearched`                       |
| `sessioninterruptions`       | `FBSDKAppEventNameSessionInterruptions`           |
| `spentcredits`               | `FBSDKAppEventNameSpentCredits`                   |
| `starttrial`                 | `FBSDKAppEventNameStartTrial`                     |
| `submitapplication`          | `FBSDKAppEventNameSubmitApplication`              |
| `subscribe`                  | `FBSDKAppEventNameSubscribe`                      |
| `timebetweensessions`        | `FBSDKAppEventNameTimeBetweenSessions`            |
| `unlockedachievement`        | `FBSDKAppEventNameUnlockedAchievement`            |
| `viewedcontent`              | `FBSDKAppEventNameViewedContent`                  |



<blockquote>
Since the Facebook SDK is installed alongside the Tealium SDK, you are able to trigger any native Facebook functionality given the corresponding tag configuration.
</blockquote>


### ユーザーのクリア

現在のユーザーデータをクリアします。

| イベント名  | 必須 | 任意 | 型 |
| ----------- | -------- | -------- | ---- |
| `clearuser` |          |          |      |

- [Facebook iOS SDK の統合 - clearUserData](https://github.com/facebook/facebook-ios-sdk/blob/1a223fd53b96c6a9078dacb1005e03035db3a0ff/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L800)
- [Facebook Android SDK の統合 - clearUserData](https://github.com/facebook/facebook-android-sdk/blob/8cc5dbb133d49f736845f999a30bfb30cf39e282/facebook-core/src/main/java/com/facebook/appevents/AppEventsLogger.java#L708)

### ユーザー ID のクリア

現在構成されているユーザー ID をクリアします。

| イベント名     | 必須 | 任意 | 型 |
| -------------- | -------- | -------- | ---- |
| `clearuserid`  |          |          |      |

- [Facebook iOS SDK の統合 - clearUserId](https://github.com/facebook/facebook-ios-sdk/blob/1a223fd53b96c6a9078dacb1005e03035db3a0ff/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L761)
- [Facebook Android SDK の統合 - clearUserId](https://github.com/facebook/facebook-android-sdk/blob/8cc5dbb133d49f736845f999a30bfb30cf39e282/facebook-core/src/main/java/com/facebook/appevents/AppEventsLogger.java#L629)
### 広告主 ID の収集構成

アプリケーションの advertiserID 収集フラグを構成します。

| イベント名                     | 必須                                    | 任意 | 型     |
| ------------------------------ | --------------------------------------- | ---- | ------ |
| `enableadvertiseridcollection` | `advertiser_collection`（Android）      |      | `bool` |
|                                | `advertiser_id_collection_enabled`（iOS） |    |        |

- [Facebook iOS SDK インテグレーション - setAdvertiserIDCollectionEnabled](https://github.com/facebook/facebook-ios-sdk/blob/ae94c9c7489fd8b080a965d9551758eadf419a06/FBSDKCoreKit/FBSDKCoreKit/Settings.swift#L155)
- [Facebook Android SDK インテグレーション - setAdvertiserIDCollectionEnabled](https://github.com/facebook/facebook-android-sdk/blob/ade6cec4c97be018302f1ba3da5a8ccae1118c3c/facebook-core/src/main/java/com/facebook/FacebookSdk.kt#L1011)

### フラッシュ

Facebook へのイベントのフラッシュを明示的に開始します。これは非同期メソッドですが、即座に処理を開始します。サーバーエラーは、通知 ID `FBSDKAppEventsLoggingResultNotification` を使用して NotificationCenter 経由で報告されます。

| イベント名 | 必須 | 任意 | 型 |
| ---------- | ---- | ---- | -- |
| `flush`    |      |      |    |

- [Facebook iOS SDK インテグレーション - flush](https://github.com/facebook/facebook-objc-sdk/blob/1a223fd53b96c6a9078dacb1005e03035db3a0ff/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L730)
- [Facebook Android SDK インテグレーション - flush](https://github.com/facebook/facebook-android-sdk/blob/8cc5dbb133d49f736845f999a30bfb30cf39e282/facebook-core/src/main/java/com/facebook/appevents/AppEventsLogger.java#L560)

### 初期化

アプリケーションの認証情報を使用して Facebook SDK を初期化します。

| イベント名   | 必須            | 任意          | 型        |
| ------------ | --------------- | ------------- | --------- |
| `initialize` | `applicationid` |               | `String`  |
|              |                 | `clienttoken` | `String`  |
|              |                 | `debug`       | `Boolean` |

### 商品アイテムのログ記録

商品カタログの商品アイテムをアプリイベントとしてアップロードします。

| イベント名       | 必須                        | 任意                 | 型                                             |
| ---------------- | --------------------------- | -------------------- | ---------------------------------------------- |
| `logProductItem` | `fb_product_item_id`        |                      | `String`                                       |
|                  | `fb_product_availability`   |                      | `Int`（以下の対応表を参照）                    |
|                  | `fb_product_condition`      |                      | `Int`（以下の対応表を参照）                    |
|                  | `fb_product_description`    |                      | `String`                                       |
|                  | `fb_product_image_link`     |                      | `String`                                       |
|                  | `fb_product_link`           |                      | `String`                                       |
|                  | `fb_product_title`          |                      | `String`                                       |
|                  | `fb_product_price_amount`   |                      | `Double/Decimal`                               |
|                  | `fb_product_price_currency` |                      | `String`                                       |
|                  | `fb_product_parameters`     |                      | `[String: Any]` - iQ では JavaScript オブジェクト |
|                  |                             | `fb_product_gtin`    | `String`                                       |
|                  |                             | `fb_product_mpn`     | `String`                                       |
|                  |                             | `fb_product_brand`   | `String`                                       |


<blockquote>
`gtin`、`mpn`、`brand` のいずれかが必須です。商品パラメーターは、ディープリンクを指定するための任意フィールドです。
</blockquote>


| 商品の在庫状況の入力値 | 商品の在庫状況の対応表                     |
| ---------------------- | ------------------------------------------ |
| `0`                    | 在庫あり - 商品はすぐに発送されます        |
| `1`                    | 在庫切れ - 再入荷の予定はありません        |
| `2`                    | 予約注文 - 今後入手可能になります          |
| `3`                    | 注文可能 - 1～2 週間以内に発送されます      |
| `4`                    | 販売終了 - 販売は終了しています            |

| 商品状態の入力値 | 商品状態の対応表 |
| ---------------- | ---------------- |
| `0`              | 新品             |
| `1`              | 再生品           |
| `2`              | 中古品           |

- [Facebook iOS SDK インテグレーション - logProductItem](https://github.com/facebook/facebook-objc-sdk/blob/1a223fd53b96c6a9078dacb1005e03035db3a0ff/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L642)
- [Facebook Android SDK インテグレーション - logProductItem](https://github.com/facebook/facebook-android-sdk/blob/8cc5dbb133d49f736845f999a30bfb30cf39e282/facebook-core/src/main/java/com/facebook/appevents/AppEventsLogger.java#L524)

### 購入のログ記録

指定された金額および通貨での購入をログに記録します。必要に応じて、購入を説明する追加の特性セットも指定できます。

特性を格納する任意のパラメーター辞書です。この辞書のキーは `NSString` である必要があり、値には `NSString` または `NSNumber` を指定します。パラメーター数および名前の構成に関する制限については、[FBSDKAppEvents](https://developers.facebook.com/docs/app-events/getting-started-app-events-ios#event-names) のドキュメントを参照してください。よく使用されるパラメーター名は、[FBSDKAppEventParameterName](https://developers.facebook.com/docs/app-events/getting-started-app-events-ios#event-params) 定数で提供されています。

| イベント名    | 必須                   | 任意                     | 型                                           |
| ------------- | ---------------------- | ------------------------ | -------------------------------------------- |
| `logPurchase` | `fb_purchase_amount`   |                          | `Decimal/Double`（iOS）/ `Double`（Android） |
|               | `fb_purchase_currency` |                          | `String`                                     |
|               |                        | `fb_purchase_parameters` | `[String: Any]` - iQ では Javascript オブジェクト |

- [Facebook iOS SDK インテグレーション - logPurchase](https://github.com/facebook/facebook-objc-sdk/blob/1a223fd53b96c6a9078dacb1005e03035db3a0ff/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L547)
- [Facebook Android SDK インテグレーション - logPurchase](https://github.com/facebook/facebook-android-sdk/blob/8cc5dbb133d49f736845f999a30bfb30cf39e282/facebook-core/src/main/java/com/facebook/appevents/AppEventsLogger.java#L440)

### 自動初期化の有効化構成

アプリケーションの SDK 自動初期化フラグを構成します。

| イベント名            | 必須               | 任意 | 型        |
| --------------------- | ------------------ | ---- | --------- |
| `setautoinitenabled`  | `auto_initialized` |      | `Boolean` |

- [Facebook Android SDK インテグレーション - setAutoInitEnabled](https://github.com/facebook/facebook-android-sdk/blob/ade6cec4c97be018302f1ba3da5a8ccae1118c3c/facebook-core/src/main/java/com/facebook/FacebookSdk.kt#L957)
### アプリイベントの自動ログを有効に構成

アプリケーションのイベント自動ログ記録フラグを構成します。

| イベント名                  | 必須                           | 任意 | 型        |
| --------------------------- | ------------------------------ | ---- | --------- |
| `setautologappeventsenabled` | `auto_log`（Android）          |      | `Boolean` |

- [Facebook iOS SDK インテグレーション - setAutoLogAppEventsEnabled](https://github.com/facebook/facebook-ios-sdk/blob/ae94c9c7489fd8b080a965d9551758eadf419a06/FBSDKCoreKit/FBSDKCoreKit/Settings.swift#L83)
- [Facebook Android SDK インテグレーション - setAutoLogAppEventsEnabled](https://github.com/facebook/facebook-android-sdk/blob/ade6cec4c97be018302f1ba3da5a8ccae1118c3c/facebook-core/src/main/java/com/facebook/FacebookSdk.kt#L981)

### フラッシュ動作を構成

Facebook SDK がアプリイベントをサーバーにフラッシュするタイミングを構成します。

| イベント名         | 必須             | 任意 | 型       |
| ------------------ | ---------------- | ---- | -------- |
| `setFlushBehavior` | `flush_behavior` |      | `String` |

- [Facebook iOS SDK インテグレーション - setFlushBehavior](https://github.com/facebook/facebook-ios-sdk/blob/ae94c9c7489fd8b080a965d9551758eadf419a06/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.m#L1752)
- [Facebook Android SDK インテグレーション - setFlushBehavior](https://github.com/facebook/facebook-android-sdk/blob/8cc5dbb133d49f736845f999a30bfb30cf39e282/facebook-core/src/main/java/com/facebook/appevents/AppEventsLogger.java#L348)

### プッシュ通知登録 ID を構成（Android）

Android プラットフォームで利用可能な追加のプッシュ通知メソッドです。

| イベント名                | 必須              | 任意 | 型       |
| ------------------------- | ----------------- | ---- | -------- |
| `setPushRegistrationId`   | `registration_id` |      | `String` |

利用可能なフラッシュ動作の値：

- `auto` - イベントは自動的にフラッシュされます（デフォルト）
- `explicit_only` - 明示的に呼び出された場合にのみイベントがフラッシュされます

- [Facebook Android SDK インテグレーション - setPushNotificationsRegistrationId](https://github.com/facebook/facebook-android-sdk/blob/ade6cec4c97be018302f1ba3da5a8ccae1118c3c/facebook-core/src/main/java/com/facebook/appevents/AppEventsLogger.kt#L453)

### ユーザーを構成

すべてのアプリイベントに関連付けるカスタムユーザーデータを構成します。すべてのユーザーデータはハッシュ化され、このアプリケーションのインスタンスから Facebook ユーザーを照合するために使用されます。ユーザーデータはアプリケーションのインスタンス間で保持されます。

| イベント名 | 必須   | 任意 | 型              |
| ---------- | ------ | ---- | --------------- |
| `setUser`  | `user` |      | `[String: Any]` |

| ユーザー辞書のプロパティ | 任意     |
| ------------------------ | -------- |
| `em`                     | `String` |
| `fn`                     | `String` |
| `ln`                     | `String` |
| `dob`                    | `String` |
| `ge`                     | `String` |
| `ct`                     | `String` |
| `st`                     | `String` |
| `zp`                     | `String` |
| `country`                | `String` |

- [Facebook iOS SDK setUser](https://github.com/facebook/facebook-objc-sdk/blob/1a223fd53b96c6a9078dacb1005e03035db3a0ff/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L764)
- [Facebook Android SDK インテグレーション - setUserData](https://github.com/facebook/facebook-android-sdk/blob/8cc5dbb133d49f736845f999a30bfb30cf39e282/facebook-core/src/main/java/com/facebook/appevents/AppEventsLogger.java#L674)

### ユーザー ID を構成

すべてのアプリイベントに関連付けるユーザー ID を構成します。この ID は、クロスデバイスコンバージョンの測定とカスタムオーディエンスの構成に使用されます。

| イベント名  | 必須         | 任意 | 型       |
| ----------- | ------------ | ---- | -------- |
| `setUserId` | `fb_user_id` |      | `String` |

### ユーザー値を更新

指定されたタイプ／キーのユーザー値を更新します。すべてのユーザーデータはハッシュ化され、このアプリケーションのインスタンスから Facebook ユーザーを照合するために使用されます。ユーザーデータはアプリケーションのインスタンス間で保持されます。

| イベント名        | 必須            | 任意 | 型       |
| ----------------- | --------------- | ---- | -------- |
| `updateUserValue` | `fb_user_value` |      | `String` |
|                   | `fb_user_key`   |      | `String` |

- [Facebook iOS SDK インテグレーション - setUserData](https://github.com/facebook/facebook-objc-sdk/blob/1a223fd53b96c6a9078dacb1005e03035db3a0ff/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L803)
- [Facebook Android SDK インテグレーション - updateUserProperties](https://github.com/facebook/facebook-android-sdk/blob/8cc5dbb133d49f736845f999a30bfb30cf39e282/facebook-core/src/main/java/com/facebook/appevents/AppEventsLogger.java#L712)
### イベントのログ記録

以下は [Facebook 標準イベント](https://github.com/facebook/facebook-ios-sdk/blob/9909ff8215c2ca41b2b1985563a4edd057111017/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L118)であり、ペイロードで任意の[パラメータ](https://github.com/facebook/facebook-ios-sdk/blob/9909ff8215c2ca41b2b1985563a4edd057111017/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L195)を複数指定できます。

- `activatedapp`
- `achievedlevel`
- `adclick`
- `adimpression`
- `addedpaymentinfo`
- `addedtocart`
- `addedtowishlist`
- `completedregistration`
- `completedtutorial`
- `contact`
- `customizeproduct`
- `deactivatedapp`
- `donate`
- `findlocation`
- `initiatedcheckout`
- `livestreamingstart`
- `livestreamingstop`
- `livestreamingpause`
- `livestreamingresume`
- `livestreamingerror`
- `livestreamingupdatestatus`
- `productcatalogupdate`
- `pushtokenobtained`
- `rated`
- `schedule`
- `searched`
- `sessioninterruptions`
- `spentcredits`
- `starttrial`
- `submitapplication`
- `subscribe`
- `timebetweensessions`
- `unlockedachievement`
- `viewedcontent`


<blockquote>
Facebook SDK は Tealium SDK と併せてインストールされるため、Facebook のすべてのネイティブ機能を利用できます。
</blockquote>


特性を表す任意のパラメータディクショナリです。このディクショナリのキーは `NSString` である必要があり、値には `NSString` または `NSNumber` が想定されています。パラメータ数と名前の構成に関する制限については、[FBSDKAppEvents](https://github.com/facebook/facebook-ios-sdk/blob/9909ff8215c2ca41b2b1985563a4edd057111017/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L118s) のドキュメントを参照してください。一般的に使用されるパラメータ名は、[FBSDKAppEventParameterName](https://github.com/facebook/facebook-ios-sdk/blob/9909ff8215c2ca41b2b1985563a4edd057111017/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L195) 定数で提供されています。

| イベント名 | 必須 | 任意 | 型 |
| ----------------------------------- | -------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------- |
|                                     | `command_name`（上記のイベント名のいずれか） |                                                                                                                                                                                   |                                         |
| 上記のイベント名のいずれか |                                                    | [パラメータ一覧を参照](https://github.com/facebook/facebook-ios-sdk/blob/9909ff8215c2ca41b2b1985563a4edd057111017/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L195) | 複数 |
|                                     |                                                    | `fb_value_to_sum`                                                                                                                                                                   | `Double/Decimal`（iOS）/ `Double`（Android） |

- [Facebook iOS SDK インテグレーション - logEvent](https://github.com/facebook/facebook-objc-sdk/blob/1a223fd53b96c6a9078dacb1005e03035db3a0ff/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L456)
- [Facebook Android SDK インテグレーション - logEvent](https://github.com/facebook/facebook-android-sdk/blob/8cc5dbb133d49f736845f999a30bfb30cf39e282/facebook-core/src/main/java/com/facebook/appevents/AppEventsLogger.java#L362)