---
title: リモートコマンド：Facebook
description: AndroidおよびSwift/iOS用FacebookのTealiumリモートコマンド統合。
url: https://docs.tealium.com/ja/platforms/remote-commands/integrations/facebook/
---
## 要件

* 以下のモバイルライブラリのいずれか：
  * [Tealium for Android (Kotlin)](/ja/platforms/android-kotlin/) (1.0.0&#43;).
  * [Tealium for Android (Java)](/ja/platforms/android-java/) (Facebook 1.0.0&#43;の場合は5.9.0&#43;、それ以前のバージョンの場合は&lt;5.9.0).
  * [Tealium for iOS (Swift)](/ja/platforms/ios-swift/).
* 以下のリモートコマンド統合のいずれか：
  * [Facebook Remote Command JSON File](/ja/platforms/remote-commands/integrations/facebook/.#json-template) (Android-Kotlin 1.0.0&#43;またはiOS-Swift 2.1.0&#43;が必要).
  * Tealium iQ Tag ManagementのFacebook Remote Commandタグ。

iOSおよびAndroidに必要な要件は以下の通りです：




`app/src/main/res/values/strings.xml`ファイルに以下のキーを追加します。`[APP_ID]`をあなたのFacebookアプリID、`[CLIENT_TOKEN]`をあなたのFacebookクライアントトークンに置き換えてください：
```xml
&lt;string name=&#34;facebook_app_id&#34;&gt;[APP_ID]&lt;/string&gt;
&lt;string name=&#34;fb_login_protocol_scheme&#34;&gt;fb[APP_ID]&lt;/string&gt;
&lt;string name=&#34;facebook_client_token&#34;&gt;[CLIENT_TOKEN]&lt;/string&gt;
```

`AndroidManifest.xml`ファイルには以下の`meta-data`要素が必要です：
```xml
&lt;application android:label=&#34;@string/app_name&#34; ...&gt;
    ...
    &lt;meta-data
      android:name=&#34;com.facebook.sdk.ApplicationId&#34;
      android:value=&#34;@string/facebook_app_id&#34; /&gt;
    &lt;meta-data 
        android:name=&#34;com.facebook.sdk.ClientToken&#34;
        android:value=&#34;@string/facebook_client_token&#34; /&gt;
    ...
&lt;/application&gt;
```

詳細はこちら：[Facebook Android Getting Started - Integrate the Facebook SDK in Your Android App](https://developers.facebook.com/docs/app-events/getting-started-app-events-android).




`Info.plist`ファイルに以下のキーを追加します。`[APP_ID]`をあなたのFacebookアプリID、`[APP_NAME]`をあなたのアプリ名、`[CLIENT_TOKEN]`をあなたのFacebookクライアントトークンに置き換えてください：
```xml
&lt;key&gt;CFBundleURLTypes&lt;/key&gt;
&lt;array&gt;
  &lt;dict&gt;
  &lt;key&gt;CFBundleURLSchemes&lt;/key&gt;
  &lt;array&gt;
    &lt;string&gt;fb[APP_ID]&lt;/string&gt;
  &lt;/array&gt;
  &lt;/dict&gt;
&lt;/array&gt;
&lt;key&gt;FacebookAppID&lt;/key&gt;
&lt;string&gt;[APP_ID]&lt;/string&gt;
&lt;key&gt;FacebookDisplayName&lt;/key&gt;
&lt;string&gt;[APP_NAME]&lt;/string&gt;
&lt;key&gt;FacebookClientToken&lt;/key&gt;
&lt;string&gt;[CLIENT_TOKEN]&lt;/string&gt;
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
            options: [UIApplicationOpenURLOptionsKey : Any] = [:]) -&gt; Bool {
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

リモートコマンドのオプションは2つあります：JSON構成ファイル、またはiQ Tag Managementを使用してマッピングを構成します。ベンダー統合には、リモートまたはアプリ内にローカルでホストされたJSON構成ファイルが推奨されます。iQ Tag Managementを使用する場合は、ベンダー統合のためのRemote Commandタグを追加します。[ベンダー統合についての詳細](/ja/platforms/remote-commands/how-it-works/#vendor-integrations)を学びましょう。

## インストール

### 依存関係マネージャ




1. Xcodeプロジェクトで、**File &gt; Add Packages... &gt; Add Package Dependency**を選択します。
2. リポジトリURLを入力します：`https://github.com/tealium/tealium-ios-facebook-remote-command`.
3. バージョンルールを構成します。通常は`Up to next major`が推奨されます。現在の`TealiumFacebook`バージョンがリストに表示されない場合は、Swiftパッケージキャッシュをリセットしてください。
4. インストールする`TealiumFacebook`モジュールを選択し、そのモジュールをインストールするアプリターゲットを選択します。

プロジェクトに複数のアプリターゲットがあり、`TealiumFacebook`モジュールを複数のアプリターゲットに追加する必要がある場合は、**Frameworks, Libraries, and Embedded Content**セクションで手動で追加する必要があります。

追加のアプリターゲットに`TealiumFacebook`をインストールするには：

1. **Project Navigator**でXcodeプロジェクトを選択します。
2. Xcodeプロジェクトで、**TARGETS**セクションのアプリターゲットを選択します。
3. **General &gt; Frameworks, Libraries &amp; Embedded Content**に移動し、`TealiumFacebook`モジュールをアプリターゲットに追加するために選択します。

Tealium Swiftライブラリから追加のモジュールを追加するには、[Swift Package Manager](/ja/platforms/ios-swift/install/#swift-package-manager-recommended)の指示に従ってください。




1. Podfileから`tealium-swift`と`pod &#34;FBSDKCoreKit&#34;`を削除します。`TealiumFacebook`フレームワークには`tealium-swift`の依存関係がすでに含まれています。

2. Podfileに以下の依存関係を追加します：
      ```ruby
      pod &#34;TealiumFacebook&#34;
      ```
      `TealiumFacebook`ポッドには以下の`TealiumSwift`依存関係が含まれています：
      ```bash
      &#39;tealium-swift/Core&#39;
      &#39;tealium-swift/RemoteCommands&#39;
      &#39;tealium-swift/TagManagement&#39;
      ```

3. `TealiumHelper`ファイルおよび`Tealium`クラスまたはFacebook Remote Commandにアクセスする他のファイルで`TealiumSwift`および`TealiumFacebook`モジュールをインポートします。




1. Cartfileから`tealium-swift`を削除します。`TealiumFacebook`フレームワークには`tealium-swift`の依存関係がすでに含まれています。

2. Cartfileに存在する場合は以下の行を削除します：
      ```bash
      github &#34;facebook/facebook-ios-sdk&#34;
      ```

3. Cartfileに以下の依存関係を追加します：
      ```bash
      github &#34;tealium/tealium-ios-facebook-remote-command&#34;
      ```

最新のFacebook Remote Command統合にはTealium for Swift SDK（バージョン2.12&#43;）が必要です。




1. [Tealium for Android (Kotlin)](/ja/platforms/android-kotlin/install/)または[Tealium for Android (Java)](/ja/platforms/android-java/install/)をインストールし、まだ行っていない場合はプロジェクトのトップレベルの`build.gradle`ファイルにTealium Maven URLを追加します。


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

2. アプリプロジェクトの`build.gradle`ファイルに以下の依存関係を追加して、Facebook SDKとTealium-Facebookリモートコマンドをインポートします：
      ```groovy
      dependencies {
            implementation &#39;com.tealium.remotecommands:facebook:3.0.0&#39;
      }
      ```


### マニュアルインストール




Facebookリモートコマンドの手動インストールには、[Tealium for Swift](/ja/platforms/ios-swift/)ライブラリのインストールが必要です。iOSプロジェクトのFacebookリモートコマンドをインストールするには：

1. まだインストールしていない場合は、[Facebook SDK](https://github.com/facebook/facebook-ios-sdk/tree/master/FBSDKCoreKit)をインストールします。

2. [Tealium iOS Facebookリモートコマンド](https://github.com/tealium/tealium-ios-facebook-remote-command)リポジトリをクローンし、`Sources`フォルダ内のファイルをプロジェクトにドラッグします。

3. ディスパッチャーとして`Dispatchers.RemoteCommands`を追加します。

4. [`remoteAPIEnabled`](/ja/platforms/ios-swift/api/tealium-config/#remoteapienabled)構成フラグを`true`に構成します。




Facebookリモートコマンドの手動インストールには、[Tealium for Android (Kotlin)](/ja/platforms/android-kotlin/install/)または[Tealium for Android (Java)](/ja/platforms/android-java/install/)のインストールが必要です。

AndroidプロジェクトのFacebookリモートコマンドをインストールするには：

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

2. `&lt;PROJECT_ROOT&gt;/&lt;MODULE&gt;/libs`に`tealium-facebook.aar`を追加します。

3. `build.gradle`ファイルにTealiumライブラリの依存関係を追加します：
      ```groovy
      dependencies {
            implementation(name:&#39;tealium-facebook&#39;, ext:&#39;aar&#39;)
      }
      ```



## 初期化

すべてのTealiumライブラリで、初期化時にFacebookリモートコマンドを登録します。





TealiumのiOS（Swift）ライブラリ用にJSON構成ファイルまたはリモートコマンドタグでリモートコマンドを初期化します：
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
    let facebook = FacebookRemoteCommand(launchOptions: launchOptions) 

    // ローカルJSON
    //let facebook = FacebookRemoteCommand(type: .local(file: &#34;facebook&#34;), launchOptions: launchOptions) 

    // リモートJSON
    //let facebook = FacebookRemoteCommand(type: .remote(url: &#34;https://some.domain.com/facebook.json&#34;), launchOptions: launchOptions) 

    remoteCommands.add(facebook)
}
```



TealiumのKotlinライブラリ用にJSON構成ファイルまたはリモートコマンドタグでリモートコマンドを初期化します：
```kotlin
val config = TealiumConfig(application,
        &#34;ACCOUNT&#34;,
        &#34;PROFILE&#34;,
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands, Dispatchers.TagManagement));
val facebook = FacebookRemoteCommand(application);

var tealium = Tealium.create(TEALIUM_MAIN, config) {
    // Webviewタグ
    remoteCommands?.add(facebook); 

    // ローカルJSON
    //remoteCommands?.add(facebook, filename = &#34;facebook.json&#34;); 

    // リモートJSON
    //remoteCommands?.add(facebook, remoteUrl = &#34;https://some.domain.com/facebook.json&#34;); 
}
```



TealiumのAndroid（Java）ライブラリ用にリモートコマンドタグでリモートコマンドを初期化します：
```java
import com.tealium.remotecommands.facebook.FacebookRemoteCommand;

Tealium.Config config = Tealium.Config.create(application, &#34;ACCOUNT&#34;, &#34;PROFILE&#34;, &#34;ENVIRONMENT&#34;);
Tealium teal = Tealium.createInstance(TEALIUM_MAIN, config);

FacebookRemoteCommand facebook = new FacebookRemoteCommand(this);

// コマンドを登録
teal.addRemoteCommand(facebook);
```




## JSONテンプレート

[JSON構成ファイル](/ja/platforms/remote-commands/how-it-works/#json-configuration-file)を使用してリモートコマンドを構成する場合は、以下のテンプレートを参照してください。このテンプレートには、標準的なeコマースインストールで使用される一般的なマッピングが含まれています。必要に応じてマッピングを編集してください。

```json
{
  &#34;config&#34;: {
    &#34;applicationid&#34;: &#34;YOUR_APP_ID&#34;,
    &#34;clienttoken&#34;: &#34;YOUR_CLIENT_TOKEN&#34;,
    &#34;accesstoken&#34;: &#34;YOUR_ACCESS_TOKEN&#34;,
    &#34;userid&#34;: &#34;YOUR_USER_ID&#34;,
    &#34;auto_log&#34;: true,
    &#34;auto_log_events_enabled&#34;: true,
    &#34;auto_initialized&#34;: true,
    &#34;advertiser_id_collection_enabled&#34;: true,
    &#34;advertiser_collection&#34;: true,
    &#34;debug&#34;: true
  },
  &#34;mappings&#34;: {
    &#34;achievement_type&#34;: &#34;event.fb_description&#34;,
    &#34;ad_type&#34;: &#34;event.ad_type&#34;,
    &#34;content&#34;: &#34;event.fb_content&#34;,
    &#34;content_type&#34;: &#34;event.fb_content_type&#34;,
    &#34;currency_code&#34;: &#34;event.fb_currency&#34;,
    &#34;event_name&#34;: &#34;event.fb_description&#34;,
    &#34;current_level&#34;: &#34;event.fb_level&#34;,
    &#34;pet_count&#34;: &#34;event.fb_max_rating_value&#34;,
    &#34;number_of_items&#34;: &#34;event.fb_num_items&#34;,
    &#34;order_id&#34;: &#34;event.fb_order_id&#34;,
    &#34;payment_info_available&#34;: &#34;event.fb_payment_info_available&#34;,
    &#34;signup_method&#34;: &#34;event.fb_registration_method&#34;,
    &#34;search_keyword&#34;: &#34;event.fb_search_string&#34;,
    &#34;success&#34;: &#34;event.fb_success&#34;,
    &#34;customer_email&#34;: &#34;user.em&#34;,
    &#34;customer_first_name&#34;: &#34;user.fn&#34;,
    &#34;customer_last_name&#34;: &#34;user.ln&#34;,
    &#34;customer_phone&#34;: &#34;user.ph&#34;,
    &#34;customer_dob&#34;: &#34;user.dob&#34;,
    &#34;customer_gender&#34;: &#34;user.ge&#34;,
    &#34;customer_city&#34;: &#34;user.ct&#34;,
    &#34;customer_state&#34;: &#34;user.st&#34;,
    &#34;customer_zip&#34;: &#34;user.zp&#34;,
    &#34;customer_country&#34;: &#34;user.country&#34;,
    &#34;customer_id&#34;: &#34;fb_user_id&#34;,
    &#34;user_value&#34;: &#34;fb_user_value&#34;,
    &#34;user_key&#34;: &#34;fb_user_key&#34;,
    &#34;product_id&#34;: &#34;product.fb_product_item_id,event.fb_content_id&#34;,
    &#34;product_availability&#34;: &#34;product.fb_product_availability&#34;,
    &#34;product_condition&#34;: &#34;product.fb_product_condition&#34;,
    &#34;product_description&#34;: &#34;product.fb_product_description,event.fb_product_description&#34;,
    &#34;product_image_link&#34;: &#34;product.fb_product_image_link&#34;,
    &#34;product_link&#34;: &#34;product.fb_product_link&#34;,
    &#34;product_name&#34;: &#34;product.fb_product_title&#34;,
    &#34;product_variant&#34;: &#34;product.fb_product_gtin&#34;,
    &#34;product_brand&#34;: &#34;product.fb_product_brand&#34;,
    &#34;product_price&#34;: &#34;product.fb_product_price_amount,event.fb_value_to_sum&#34;,
    &#34;product_currency&#34;: &#34;product.fb_product_price_currency&#34;,
    &#34;product_alias&#34;: &#34;product_parameters.product_alias&#34;,
    &#34;product_color&#34;: &#34;product_parameters.product_color&#34;,
    &#34;order_total&#34;: &#34;purchase.fb_purchase_amount&#34;,
    &#34;order_currency&#34;: &#34;purchase.fb_purchase_currency&#34;,
    &#34;customer_status&#34;: &#34;purchase_parameters.customer_status&#34;,
    &#34;coupon&#34;: &#34;purchase_parameters.coupon&#34;,
    &#34;push_action&#34;: &#34;push.fb_push_action&#34;,
    &#34;push_payload&#34;: &#34;push.fb_push_payload&#34;,
    &#34;tealium_event&#34;: &#34;command_name&#34;
  },
  &#34;commands&#34;: {
    &#34;launch&#34;: &#34;initialize,setautologappeventsenabled,setautoinitenabled,enableadvertiseridcollection&#34;,
    &#34;user_login&#34;: &#34;setuser,setuserid&#34;,
    &#34;email_signup&#34;: &#34;updateuservalue&#34;,
    &#34;level_up&#34;: &#34;achievedlevel&#34;,
    &#34;user_register&#34;: &#34;completedregistration&#34;,
    &#34;unlock_achievement&#34;: &#34;unlockedachievement&#34;,
    &#34;cart_add&#34;: &#34;addedtocart&#34;,
    &#34;custom_attribute&#34;: &#34;rated&#34;,
    &#34;wishlist_add&#34;: &#34;addedtowishlist&#34;,
    &#34;payment&#34;: &#34;initiatedcheckout&#34;,
    &#34;product&#34;: &#34;logproductitem&#34;,
    &#34;order&#34;: &#34;logpurchase&#34;,
    &#34;flush&#34;: &#34;flush&#34;,
    &#34;customfbevent&#34;: &#34;customfbevent&#34;
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


Facebook SDKがTealium SDKと一緒にインストールされているため、対応するタグ構成が与えられた場合、任意のネイティブFacebook機能をトリガーできます。

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

`gtin`、`mpn`、または`brand`のいずれかが必要です。商品パラメーターはディープリンク仕様のための任意フィールドです。

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

Facebook SDKはTealium SDKと一緒にインストールされているため、すべてのネイティブFacebook機能が利用可能です。

特性の任意のパラメータ辞書。この辞書のキーは`NSString`でなければならず、値は`NSString`または`NSNumber`であることが期待されます。パラメータの数と名前の構造に関する制限は、[FBSDKAppEvents](https://github.com/facebook/facebook-ios-sdk/blob/9909ff8215c2ca41b2b1985563a4edd057111017/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L118s)のドキュメントで与えられています。一般的に使用されるパラメータ名は[FBSDKAppEventParameterName](https://github.com/facebook/facebook-ios-sdk/blob/9909ff8215c2ca41b2b1985563a4edd057111017/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L195)定数で提供されています。

| イベント名                          | 必須                                           | オプショナル                                                                                                                                                                          | タイプ                                    |
| ----------------------------------- | -------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------- |
|                                     | `command_name` (上記リストのイベント名のいずれか) |                                                                                                                                                                                   |                                         |
| 上記リストのイベント名のいずれか |                                                    | [パラメータリストを参照](https://github.com/facebook/facebook-ios-sdk/blob/9909ff8215c2ca41b2b1985563a4edd057111017/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L195) | 複数                                |
|                                     |                                                    | `fb_value_to_sum`                                                                                                                                                                   | `Double/Decimal` (iOS) / `Double` (Android) |

- [Facebook iOS SDK統合 - logEvent](https://github.com/facebook/facebook-objc-sdk/blob/1a223fd53b96c6a9078dacb1005e03035db3a0ff/FBSDKCoreKit/FBSDKCoreKit/AppEvents/FBSDKAppEvents.h#L456)
- [Facebook Android SDK統合 - logEvent](https://github.com/facebook/facebook-android-sdk/blob/8cc5dbb133d49f736845f999a30bfb30cf39e282/facebook-core/src/main/java/com/facebook/appevents/AppEventsLogger.java#L362)