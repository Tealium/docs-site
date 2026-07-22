---
title: リモートコマンド：Facebook
description: AndroidおよびSwift/iOS用FacebookのTealiumリモートコマンド統合。
url: https://docs.tealium.com/ja/platforms/remote-commands/integrations/facebook/
---
## 要件

* 以下のモバイルライブラリのいずれか：
  * [Tealium for Android (Kotlin)](https://docs.tealium.com/ja/platforms/android-kotlin/) (1.0.0+).
  * [Tealium for Android (Java)](https://docs.tealium.com/ja/platforms/android-java/) (Facebook 1.0.0+の場合は5.9.0+、それ以前のバージョンの場合は<5.9.0).
  * [Tealium for iOS (Swift)](https://docs.tealium.com/ja/platforms/ios-swift/).
* 以下のリモートコマンド統合のいずれか：
  * [Facebook Remote Command JSON File](https://docs.tealium.com/ja/platforms/remote-commands/integrations/facebook/.#json-template) (Android-Kotlin 1.0.0+またはiOS-Swift 2.1.0+が必要).
  * Tealium Tag ManagementのFacebook Remote Commandタグ。

iOSおよびAndroidに必要な要件は以下の通りです：




`app/src/main/res/values/strings.xml`ファイルに以下のキーを追加します。`[APP_ID]`をあなたのFacebookアプリID、`[CLIENT_TOKEN]`をあなたのFacebookクライアントトークンに置き換えてください：
```xml
<string name="facebook_app_id">[APP_ID]</string>
<string name="fb_login_protocol_scheme">fb[APP_ID]</string>
<string name="facebook_client_token">[CLIENT_TOKEN]</string>
```

`AndroidManifest.xml`ファイルには以下の`meta-data`要素が必要です：
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

詳細はこちら：[Facebook Android Getting Started - Integrate the Facebook SDK in Your Android App](https://developers.facebook.com/docs/app-events/getting-started-app-events-android).




`Info.plist`ファイルに以下のキーを追加します。`[APP_ID]`をあなたのFacebookアプリID、`[APP_NAME]`をあなたのアプリ名、`[CLIENT_TOKEN]`をあなたのFacebookクライアントトークンに置き換えてください：
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
詳細はこちら：[Facebook iOS Getting Started - Configure Your Property List](https://developers.facebook.com/docs/app-events/getting-started-app-events-ios/#plist-config).

`AppDelegate`コードを以下のように更新します：

1. `FBSDKCoreKit`をインポートします。
2. `didFinishLaunchingWithOptions`メソッドに以下を追加します：
      ```swift
      ApplicationDelegate.shared.application(
            application, 
            didFinishLaunchingWithOptions: launchOptions)
      ```
3. `AppDelegate.swift`（またはObjective-Cの同等物）に以下の関数を追加します：
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
詳細はこちら：[Facebook iOS Getting Started - Set Up Your Development Environment](https://developers.facebook.com/docs/app-events/getting-started-app-events-ios/#dev-env-setup).




## 動作原理

Facebook統合は3つの要素を使用します：

1. FacebookネイティブSDK。
2. Facebookメソッドをラップするリモートコマンドモジュール。
3. イベントトラッキングをネイティブのFacebookコールに変換するJSON構成ファイルまたはRemote Commandタグのいずれか。

Facebookリモートコマンドモジュールをアプリに追加すると、ベンダー固有のコードをアプリに追加することなく、必要なFacebookライブラリが自動的にインストールされビルドされます。依存関係マネージャーのインストールを使用している場合、Facebook SDKを別途インストールする必要はありません。

リモートコマンドのオプションは2つあります：JSON構成ファイル、またはTag Managementを使用してマッピングを構成します。ベンダー統合には、リモートまたはアプリ内にローカルでホストされたJSON構成ファイルが推奨されます。Tag Managementを使用する場合は、ベンダー統合のためのRemote Commandタグを追加します。[ベンダー統合についての詳細](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/#vendor-integrations)を学びましょう。

## インストール

### 依存関係マネージャ




1. Xcodeプロジェクトで、**File > Add Packages... > Add Package Dependency**を選択します。
2. リポジトリURLを入力します：`https://github.com/tealium/tealium-ios-facebook-remote-command`.
3. バージョンルールを構成します。通常は`Up to next major`が推奨されます。現在の`TealiumFacebook`バージョンがリストに表示されない場合は、Swiftパッケージキャッシュをリセットしてください。
4. インストールする`TealiumFacebook`モジュールを選択し、そのモジュールをインストールするアプリターゲットを選択します。

プロジェクトに複数のアプリターゲットがあり、`TealiumFacebook`モジュールを複数のアプリターゲットに追加する必要がある場合は、**Frameworks, Libraries, and Embedded Content**セクションで手動で追加する必要があります。

追加のアプリターゲットに`TealiumFacebook`をインストールするには：

1. **Project Navigator**でXcodeプロジェクトを選択します。
2. Xcodeプロジェクトで、**TARGETS**セクションのアプリターゲットを選択します。
3. **General > Frameworks, Libraries & Embedded Content**に移動し、`TealiumFacebook`モジュールをアプリターゲットに追加するために選択します。

Tealium Swiftライブラリから追加のモジュールを追加するには、[Swift Package Manager](https://docs.tealium.com/ja/platforms/ios-swift/install/#swift-package-manager-recommended)の指示に従ってください。




1. Podfileから`tealium-swift`と`pod "FBSDKCoreKit"`を削除します。`TealiumFacebook`フレームワークには`tealium-swift`の依存関係がすでに含まれています。

2. Podfileに以下の依存関係を追加します：
      ```ruby
      pod "TealiumFacebook"
      ```
      `TealiumFacebook`ポッドには以下の`TealiumSwift`依存関係が含まれています：
      ```bash
      'tealium-swift/Core'
      'tealium-swift/RemoteCommands'
      'tealium-swift/TagManagement'
      ```

3. `TealiumHelper`ファイルおよび`Tealium`クラスまたはFacebook Remote Commandにアクセスする他のファイルで`TealiumSwift`および`TealiumFacebook`モジュールをインポートします。




1. Cartfileから`tealium-swift`を削除します。`TealiumFacebook`フレームワークには`tealium-swift`の依存関係がすでに含まれています。

2. Cartfileに存在する場合は以下の行を削除します：
      ```bash
      github "facebook/facebook-ios-sdk"
      ```

3. Cartfileに以下の依存関係を追加します：
      ```bash
      github "tealium/tealium-ios-facebook-remote-command"
      ```


<blockquote>
最新のFacebook Remote Command統合にはTealium for Swift SDK（バージョン2.12+）が必要です。
</blockquote>





1. [Tealium for Android (Kotlin)](https://docs.tealium.com/ja/platforms/android-kotlin/install/)または[Tealium for Android (Java)](https://docs.tealium.com/ja/platforms/android-java/install/)をインストールし、まだ行っていない場合はプロジェクトのトップレベルの`build.gradle`ファイルにTealium Maven URLを追加します。


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

2. アプリプロジェクトの`build.gradle`ファイルに以下の依存関係を追加して、Facebook SDKとTealium-Facebookリモートコマンドをインポートします：
      ```groovy
      dependencies {
            implementation 'com.tealium.remotecommands:facebook:3.0.0'
      }
      ```


### マニュアルインストール




Facebookリモートコマンドの手動インストールには、[Tealium for Swift](https://docs.tealium.com/ja/platforms/ios-swift/)ライブラリのインストールが必要です。iOSプロジェクトのFacebookリモートコマンドをインストールするには：

1. まだインストールしていない場合は、[Facebook SDK](https://github.com/facebook/facebook-ios-sdk/tree/master/FBSDKCoreKit)をインストールします。

2. [Tealium iOS Facebookリモートコマンド](https://github.com/tealium/tealium-ios-facebook-remote-command)リポジトリをクローンし、`Sources`フォルダ内のファイルをプロジェクトにドラッグします。

3. ディスパッチャーとして`Dispatchers.RemoteCommands`を追加します。

4. [`remoteAPIEnabled`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#remoteapienabled)構成フラグを`true`に構成します。




Facebookリモートコマンドの手動インストールには、[Tealium for Android (Kotlin)](https://docs.tealium.com/ja/platforms/android-kotlin/install/)または[Tealium for Android (Java)](https://docs.tealium.com/ja/platforms/android-java/install/)のインストールが必要です。

AndroidプロジェクトのFacebookリモートコマンドをインストールするには：

1. プロジェクトルートの`build.gradle`ファイルに`flatDir`を追加します：
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

2. `<PROJECT_ROOT>/<MODULE>/libs`に`tealium-facebook.aar`を追加します。

3. `build.gradle`ファイルにTealiumライブラリの依存関係を追加します：
      ```groovy
      dependencies {
            implementation(name:'tealium-facebook', ext:'aar')
      }
      ```



## 初期化

すべてのTealiumライブラリで、初期化時にFacebookリモートコマンドを登録します。





TealiumのiOS（Swift）ライブラリ用にJSON構成ファイルまたはリモートコマンドタグでリモートコマンドを初期化します：
```swift
var tealium : Tealium?
let config = TealiumConfig(account: "ACCOUNT",
                           profile: "PROFILE",
                           environment: "ENVIRONMENT",
                           dataSource: "DATASOURCE")
config.dispatchers = [Dispatchers.TagManagement, Dispatchers.RemoteCommands]
config.remoteAPIEnabled = true // リモートコマンドを使用するために必要

tealium = Tealium(config: config) { _ in
    guard let remoteCommands = self.tealium?.remoteCommands else {
        return
    }

    // Webviewタグ
    let facebook = FacebookRemoteCommand(launchOptions: launchOptions) 

    // ローカルJSON
    //let facebook = FacebookRemoteCommand(type: .local(file: "facebook"), launchOptions: launchOptions) 

    // リモートJSON
    //let facebook = FacebookRemoteCommand(type: .remote(url: "https://some.domain.com/facebook.json"), launchOptions: launchOptions) 

    remoteCommands.add(facebook)
}
```



TealiumのKotlinライブラリ用にJSON構成ファイルまたはリモートコマンドタグでリモートコマンドを初期化します：
```kotlin
val config = TealiumConfig(application,
        "ACCOUNT",
        "PROFILE",
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands, Dispatchers.TagManagement));
val facebook = FacebookRemoteCommand(application);

var tealium = Tealium.create(TEALIUM_MAIN, config) {
    // Webviewタグ
    remoteCommands?.add(facebook); 

    // ローカルJSON
    //remoteCommands?.add(facebook, filename = "facebook.json"); 

    // リモートJSON
    //remoteCommands?.add(facebook, remoteUrl = "https://some.domain.com/facebook.json"); 
}
```



TealiumのAndroid（Java）ライブラリ用にリモートコマンドタグでリモートコマンドを初期化します：
```java
import com.tealium.remotecommands.facebook.FacebookRemoteCommand;

Tealium.Config config = Tealium.Config.create(application, "ACCOUNT", "PROFILE", "ENVIRONMENT");
Tealium teal = Tealium.createInstance(TEALIUM_MAIN, config);

FacebookRemoteCommand facebook = new FacebookRemoteCommand(this);

// コマンドを登録
teal.addRemoteCommand(facebook);
```




## JSONテンプレート

[JSON構成ファイル](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/#json-configuration-file)を使用してリモートコマンドを構成する場合は、以下のテンプレートを参照してください。このテンプレートには、標準的なeコマースインストールで使用される一般的なマッピングが含まれています。必要に応じてマッピングを編集してください。

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
## Pushメッセージ追跡（iOS）

Tealium Swiftライブラリには、TealiumおよびFacebook Remote Commandを通じてプッシュメッセージ追跡を処理するための`TealiumRegistration`プロトコルが含まれています。このプロトコルに準拠するラッパークラス`FacebookInstance`を使用して、プッシュメッセージ認証イベント、プッシュメッセージオープンイベント、およびアンインストール追跡を送信します。プッシュメッセージ追跡機能を活用することをお勧めします。

以下は、iOSプロジェクトにプッシュメッセージ追跡を統合する手順です：

1. `TealiumHelper.swift`ファイルで、`TealiumRegistration`プロトコルに準拠するオブジェクトの空の配列を初期化します。例：
      ```swift
      var pushMessagingHelpers = [TealiumRegistration]()
      ```
2. `FacebookRemoteCommand`の前に`FacebookInstance`を初期化します。
3. 上記の配列に`FacebookInstance`を追加します。

以下は、プッシュメッセージ追跡統合の例です：
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

`TealiumHelper.swift`ファイル全体を見るには、[Facebook Remote Commandサンプルアプリ](https://github.com/Tealium/tealium-ios-facebook-remote-command/tree/master/Examples)を参照してください。ユーザーが通知に登録した後、プッシュメッセージを開いたり、アプリをアンインストールしたりした場合にFacebookにイベントを送信するには、`AppDelegate.swift`ファイルを参照してください。

## サポートされているメソッド

各Facebookメソッドにコマンドをマッピングします。Facebookメソッドをトリガーするには、指定された形式で対応するコマンドを渡します。

| リモートコマンド | Facebookメソッド | サポートプラットフォーム |
| -------------- | --------------- | ------------------- |
| `clearuser`(ios)/`clearuserdata`(android) | `clearUserData()` | iOS, Android |
| `clearuserid` | `clearUserId()` | iOS, Android |
| `enableadvertiseridcollection` | `setAdvertiserIDCollectionEnabled()` | iOS, Android |
| `flush` | `flush()` | iOS, Android |
| `initialize` | `initialize()` | iOS, Android |
| `logproductitem` | `logProductItem()` | iOS, Android |
| `logpurchase` | `logPurchase()` | iOS, Android |
| `setautoinitenabled` | `setAutoInitEnabled()` | Android |
| `setautologappeventsenabled` | `setAutoLogAppEventsEnabled()` | iOS, Android |
| `setflushbehavior` | `setFlushBehavior()` | iOS, Android |
| `setpushregistrationid` | `setPushNotificationsRegistrationId()` | Androidのみ |
| `setuser`(ios, android)/`updateUserValue`(ios) | `setUserData()` | iOS, Android |
| `setuserid` | `setUserId()` | iOS, Android |
| 以下のいずれかのイベント名 | `logEvent()` | iOS, Android |

### 標準イベント名

以下は、`logEvent`メソッドでサポートされている標準イベント名のリストです。以下のコマンド名が送信された場合、それに対応するFacebook SDKで自動的にトリガーされます。これは、その特定のイベントに対して必要な変数もマッピングおよび定義されていると仮定しています。[アプリ内イベントの記録について学ぶ](https://developers.facebook.com/docs/app-events/getting-started-app-events-ios/#manually-log-events)。

| リモートコマンド               | Facebookイベント名                                |
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
Facebook SDKがTealium SDKと一緒にインストールされているため、対応するタグ構成が与えられた場合、任意のネイティブFacebook機能をトリガーできます。
</blockquote>


### ユーザークリア

現在のユーザーデータをクリアします。

| イベント名  | 必須 | オプション | タイプ |
| ----------- | -------- | -------- | ---- |
| `clearuser` |          |          |      |

- [Facebook iOS SDK統合 - clearUserData](https://github.com/facebook/facebook-ios-sdk/blob/1a223fd53b96c6a9078dacb1005e03035db3a0ff/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L800)
- [Facebook Android SDK統合 - clearUserData](https://github.com/facebook/facebook-android-sdk/blob/8cc5dbb133d49f736845f999a30bfb30cf39e282/facebook-core/src/main/java/com/facebook/appevents/AppEventsLogger.java#L708)

### ユーザーIDクリア

現在構成されているユーザーIDをクリアします。

| イベント名     | 必須 | オプション | タイプ |
| -------------- | -------- | -------- | ---- |
| `clearuserid`  |          |          |      |

- [Facebook iOS SDK統合 - clearUserId](https://github.com/facebook/facebook-ios-sdk/blob/1a223fd53b96c6a9078dacb1005e03035db3a0ff/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L761)
- [Facebook Android SDK統合 - clearUserId](https://github.com/facebook/facebook-android-sdk/blob/8cc5dbb133d49f736845f999a30bfb30cf39e282/facebook-core/src/main/java/com/facebook/appevents/AppEventsLogger.java#L629)
### 広告主IDコレクションの構成

アプリケーションの広告主IDコレクションフラグを構成します。

| イベント名                         | 必須                                      | 任意 | 型     |
| ---------------------------------- | ----------------------------------------- | ---- | ------ |
| `enableadvertiseridcollection`     | `advertiser_collection`(android)          |      | `bool` |
|                                    | `advertiser_id_collection_enabled`(ios)   |      |        |

- [Facebook iOS SDK統合 - setAdvertiserIDCollectionEnabled](https://github.com/facebook/facebook-ios-sdk/blob/ae94c9c7489fd8b080a965d9551758eadf419a06/FBSDKCoreKit/FBSDKCoreKit/Settings.swift#L155)
- [Facebook Android SDK統合 - setAdvertiserIDCollectionEnabled](https://github.com/facebook/facebook-android-sdk/blob/ade6cec4c97be018302f1ba3da5a8ccae1118c3c/facebook-core/src/main/java/com/facebook/FacebookSdk.kt#L1011)

### フラッシュ

Facebookにイベントのフラッシュを明示的に開始します。これは非同期メソッドですが、即時に開始されます。サーバーの障害はNotificationCenterを通じて通知ID `FBSDKAppEventsLoggingResultNotification`で報告されます。

| イベント名 | 必須 | 任意 | 型 |
| ---------- | ---- | ---- | --- |
| `flush`    |      |      |     |

- [Facebook iOS SDK統合 - flush](https://github.com/facebook/facebook-objc-sdk/blob/1a223fd53b96c6a9078dacb1005e03035db3a0ff/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L730)
- [Facebook Android SDK統合 - flush](https://github.com/facebook/facebook-android-sdk/blob/8cc5dbb133d49f736845f999a30bfb30cf39e282/facebook-core/src/main/java/com/facebook/appevents/AppEventsLogger.java#L560)

### 初期化

アプリケーションの認証情報を使用してFacebook SDKを初期化します。

| イベント名   | 必須              | 任意            | 型        |
| ------------ | ----------------- | --------------- | --------- |
| `initialize` | `applicationid`   |                 | `String`  |
|              |                   | `clienttoken`   | `String`  |
|              |                   | `debug`         | `Boolean` |

### 商品アイテムのログ

商品カタログの商品アイテムをアプリイベントとしてアップロードします。

| イベント名           | 必須                        | 任意                 | 型                                           |
| -------------------- | --------------------------- | -------------------- | -------------------------------------------- |
| `logProductItem`     | `fb_product_item_id`        |                      | `String`                                     |
|                      | `fb_product_availability`   |                      | `Int` (下記参照)                              |
|                      | `fb_product_condition`      |                      | `Int` (下記参照)                              |
|                      | `fb_product_description`    |                      | `String`                                     |
|                      | `fb_product_image_link`     |                      | `String`                                     |
|                      | `fb_product_link`           |                      | `String`                                     |
|                      | `fb_product_title`          |                      | `String`                                     |
|                      | `fb_product_price_amount`   |                      | `Double/Decimal`                             |
|                      | `fb_product_price_currency` |                      | `String`                                     |
|                      | `fb_product_parameters`     |                      | `[String: Any]` - JavaScriptオブジェクト（iQ内） |
|                      |                             | `fb_product_gtin`    | `String`                                     |
|                      |                             | `fb_product_mpn`     | `String`                                     |
|                      |                             | `fb_product_brand`   | `String`                                     |


<blockquote>
`gtin`、`mpn`、または`brand`のいずれかが必要です。商品パラメーターはディープリンク仕様のための任意フィールドです。
</blockquote>


| 商品在庫入力 | 商品在庫参照                                 |
| ------------ | ------------------------------------------- |
| `0`          | 在庫あり - 即時出荷                         |
| `1`          | 在庫なし - 再入荷予定なし                   |
| `2`          | 予約注文 - 将来入荷予定                     |
| `3`          | 注文可能 - 1-2週間で出荷                    |
| `4`          | 販売終了 - 販売終了                         |

| 商品状態入力 | 商品状態参照 |
| ------------ | ------------ |
| `0`          | 新品         |
| `1`          | 再生品       |
| `2`          | 中古         |

- [Facebook iOS SDK統合 - logProductItem](https://github.com/facebook/facebook-objc-sdk/blob/1a223fd53b96c6a9078dacb1005e03035db3a0ff/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L642)
- [Facebook Android SDK統合 - logProductItem](https://github.com/facebook/facebook-android-sdk/blob/8cc5dbb133d49f736845f999a30bfb30cf39e282/facebook-core/src/main/java/com/facebook/appevents/AppEventsLogger.java#L524)

### 購入のログ

指定された金額と通貨で購入を記録し、オプションで購入の追加特性を提供します。

特性の任意パラメーター辞書。この辞書のキーは`NSString`でなければならず、値は`NSString`または`NSNumber`であることが期待されます。パラメーターの数と名前の構造に関する制限は[FBSDKAppEvents](https://developers.facebook.com/docs/app-events/getting-started-app-events-ios#event-names)のドキュメントに記載されています。一般的に使用されるパラメーター名は[FBSDKAppEventParameterName](https://developers.facebook.com/docs/app-events/getting-started-app-events-ios#event-params)の定数で提供されています。

| イベント名     | 必須                   | 任意                     | 型                                             |
| -------------- | ---------------------- | ------------------------ | ---------------------------------------------- |
| `logPurchase`  | `fb_purchase_amount`   |                          | `Decimal/Double` (iOS) / `Double` (Android)    |
|                | `fb_purchase_currency` |                          | `String`                                       |
|                |                        | `fb_purchase_parameters` | `[String: Any]` - JavaScriptオブジェクト（iQ内） |

- [Facebook iOS SDK統合 - logPurchase](https://github.com/facebook/facebook-objc-sdk/blob/1a223fd53b96c6a9078dacb1005e03035db3a0ff/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L547)
- [Facebook Android SDK統合 - logPurchase](https://github.com/facebook/facebook-android-sdk/blob/8cc5dbb133d49f736845f999a30bfb30cf39e282/facebook-core/src/main/java/com/facebook/appevents/AppEventsLogger.java#L440)

### 自動初期化有効化の構成

アプリケーションの自動初期化SDKフラグを構成します。

| イベント名             | 必須               | 任意 | 型        |
| ---------------------- | ------------------ | ---- | --------- |
| `setautoinitenabled`   | `auto_initialized` |      | `Boolean` |

- [Facebook Android SDK統合 - setAutoInitEnabled](https://github.com/facebook/facebook-android-sdk/blob/ade6cec4c97be018302f1ba3da5a8ccae1118c3c/facebook-core/src/main/java/com/facebook/FacebookSdk.kt#L957)
### 自動ログアプリイベント有効構成

アプリケーションの自動ログイベントフラグを構成します。

| イベント名                     | 必須                           | 任意 | 型        |
| ----------------------------- | ------------------------------ | ---- | --------- |
| `setautologappeventsenabled` | `auto_log`(android)            |      | `Boolean` |

- [Facebook iOS SDK 統合 - setAutoLogAppEventsEnabled](https://github.com/facebook/facebook-ios-sdk/blob/ae94c9c7489fd8b080a965d9551758eadf419a06/FBSDKCoreKit/FBSDKCoreKit/Settings.swift#L83)
- [Facebook Android SDK 統合 - setAutoLogAppEventsEnabled](https://github.com/facebook/facebook-android-sdk/blob/ade6cec4c97be018302f1ba3da5a8ccae1118c3c/facebook-core/src/main/java/com/facebook/FacebookSdk.kt#L981)

### フラッシュ動作構成

Facebook SDKがアプリイベントをサーバーにフラッシュするタイミングを構成します。

| イベント名          | 必須              | 任意 | 型       |
| ----------------- | ----------------- | ---- | -------- |
| `setFlushBehavior` | `flush_behavior` |      | `String` |

- [Facebook iOS SDK 統合 - setFlushBehavior](https://github.com/facebook/facebook-ios-sdk/blob/ae94c9c7489fd8b080a965d9551758eadf419a06/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.m#L1752)
- [Facebook Android SDK 統合 - setFlushBehavior](https://github.com/facebook/facebook-android-sdk/blob/8cc5dbb133d49f736845f999a30bfb30cf39e282/facebook-core/src/main/java/com/facebook/appevents/AppEventsLogger.java#L348)

### プッシュ通知登録ID構成（Android）

Androidプラットフォームで利用可能な追加のプッシュ通知方法。

| イベント名                  | 必須              | 任意 | 型       |
| --------------------------- | ----------------- | ---- | -------- |
| `setPushRegistrationId`     | `registration_id` |      | `String` |

利用可能なフラッシュ動作値:
- `auto` - イベントは自動的にフラッシュされます（デフォルト）
- `explicit_only` - イベントは明示的に呼び出されたときのみフラッシュされます

- [Facebook Android SDK 統合 - setPushNotificationsRegistrationId](https://github.com/facebook/facebook-android-sdk/blob/ade6cec4c97be018302f1ba3da5a8ccae1118c3c/facebook-core/src/main/java/com/facebook/appevents/AppEventsLogger.kt#L453)

### ユーザー構成

すべてのアプリイベントに関連付けるカスタムユーザーデータを構成します。すべてのユーザーデータはハッシュ化され、このアプリケーションのインスタンスからFacebookユーザーを照合するために使用されます。ユーザーデータはアプリケーションインスタンス間で保持されます。

| イベント名 | 必須   | 任意 | 型              |
| ---------- | ------ | ---- | --------------- |
| `setUser`    | `user` |      | `[String: Any]` |

| ユーザー辞書のプロパティ | 任意 |
| -------------------------- | ---- |
| `em`                         | `String`   |
| `fn`                         | `String`   |
| `ln`                         | `String`   |
| `dob`                        | `String`   |
| `ge`                         | `String`   |
| `ct`                         | `String`   |
| `st`                         | `String`   |
| `zp`                         | `String`   |
| `country`                    | `String`   |

- [Facebook iOS SDK ユーザー構成](https://github.com/facebook/facebook-objc-sdk/blob/1a223fd53b96c6a9078dacb1005e03035db3a0ff/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L764)
- [Facebook Android SDK 統合 - setUserData](https://github.com/facebook/facebook-android-sdk/blob/8cc5dbb133d49f736845f999a30bfb30cf39e282/facebook-core/src/main/java/com/facebook/appevents/AppEventsLogger.java#L674)

### ユーザーID構成

すべてのアプリイベントに関連付けるユーザーIDを構成します。このIDは、デバイス間のコンバージョン測定およびカスタムオーディエンスの構成に使用されます。

| イベント名  | 必須         | 任意 | 型       |
| ----------- | ------------ | ---- | -------- |
| `setUserId` | `fb_user_id` |      | `String` |

### ユーザー値の更新

タイプ/キーに対するユーザー値を更新します。すべてのユーザーデータはハッシュ化され、このアプリケーションのインスタンスからFacebookユーザーを照合するために使用されます。ユーザーデータはアプリケーションインスタンス間で保持されます。

| イベント名          | 必須              | 任意 | 型       |
| --------------- | ------------- | ---- | ------ |
| `updateUserValue` | `fb_user_value` |      | `String` |
|                 | `fb_user_key`   |      | `String` |

- [Facebook iOS SDK 統合 - setUserData](https://github.com/facebook/facebook-objc-sdk/blob/1a223fd53b96c6a9078dacb1005e03035db3a0ff/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L803)
- [Facebook Android SDK 統合 - updateUserProperties](https://github.com/facebook/facebook-android-sdk/blob/8cc5dbb133d49f736845f999a30bfb30cf39e282/facebook-core/src/main/java/com/facebook/appevents/AppEventsLogger.java#L712)
### ログイベント

以下は[Facebook標準イベント](https://github.com/facebook/facebook-ios-sdk/blob/9909ff8215c2ca41b2b1985563a4edd057111017/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L118)で、ペイロード内のオプショナルな[パラメータ](https://github.com/facebook/facebook-ios-sdk/blob/9909ff8215c2ca41b2b1985563a4edd057111017/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L195)を数多く受け入れます。

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
Facebook SDKはTealium SDKと一緒にインストールされているため、すべてのネイティブFacebook機能が利用可能です。
</blockquote>


特性の任意のパラメータ辞書。この辞書のキーは`NSString`でなければならず、値は`NSString`または`NSNumber`であることが期待されます。パラメータの数と名前の構造に関する制限は、[FBSDKAppEvents](https://github.com/facebook/facebook-ios-sdk/blob/9909ff8215c2ca41b2b1985563a4edd057111017/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L118s)のドキュメントで与えられています。一般的に使用されるパラメータ名は[FBSDKAppEventParameterName](https://github.com/facebook/facebook-ios-sdk/blob/9909ff8215c2ca41b2b1985563a4edd057111017/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L195)定数で提供されています。

| イベント名                          | 必須                                           | オプショナル                                                                                                                                                                          | タイプ                                    |
| ----------------------------------- | -------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------- |
|                                     | `command_name` (上記リストのイベント名のいずれか) |                                                                                                                                                                                   |                                         |
| 上記リストのイベント名のいずれか |                                                    | [パラメータリストを参照](https://github.com/facebook/facebook-ios-sdk/blob/9909ff8215c2ca41b2b1985563a4edd057111017/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L195) | 複数                                |
|                                     |                                                    | `fb_value_to_sum`                                                                                                                                                                   | `Double/Decimal` (iOS) / `Double` (Android) |

- [Facebook iOS SDK統合 - logEvent](https://github.com/facebook/facebook-objc-sdk/blob/1a223fd53b96c6a9078dacb1005e03035db3a0ff/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L456)
- [Facebook Android SDK統合 - logEvent](https://github.com/facebook/facebook-android-sdk/blob/8cc5dbb133d49f736845f999a30bfb30cf39e282/facebook-core/src/main/java/com/facebook/appevents/AppEventsLogger.java#L362)