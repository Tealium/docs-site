---
title: リモートコマンド：Kochava
description: AndroidおよびSwift/iOS用KochavaのTealiumリモートコマンド統合。
url: https://docs.tealium.com/ja/platforms/remote-commands/integrations/kochava/
---
## 要件

* [KochavaアプリGUID](https://support.kochava.com/reference-information/locating-an-app-guid/)
* 以下のいずれかのモバイルライブラリ：
  * [Tealium for Android-Kotlin](/ja/platforms/android-kotlin/) (1.0.0&#43;)
  * [Tealium for Android-Java](/ja/platforms/android-java/) (5.9.0&#43;)
  * [Tealium for iOS-Swift](/ja/platforms/ios-swift/) (2.1.0&#43;)
* 以下のいずれかのリモートコマンド統合：
  * [Kochava Remote Command JSON File](/ja/platforms/remote-commands/integrations/kochava/#json-template) (Android-Kotlin 1.0.0&#43;またはiOS-Swift 2.1.0&#43;が必要)
  * Tealium iQタグ管理の[Kochava Remote Command tag]()

## 動作原理

Kochava統合は3つのアイテムを使用します：

1. KochavaネイティブSDK
2. Kochavaメソッドをラップするリモートコマンドモジュール
3. イベントトラッキングをネイティブKochavaコールに変換するJSON構成ファイルまたはリモートコマンドタグ

アプリにKochavaリモートコマンドモジュールを追加すると、アプリにベンダー固有のコードを追加することなく、必要なKochavaライブラリが自動的にインストールされてビルドされます。依存関係マネージャーのインストールを使用している場合、Kochava SDKを別途インストールする必要はありません。

リモートコマンドオプションには2つあります：JSON構成ファイル、またはiQタグ管理を使用してマッピングを構成します。JSON構成ファイルは、ベンダー統合のためにリモートまたはアプリ内にローカルでホストされることを推奨されるオプションです。iQタグ管理を使用する場合は、ベンダー統合のためのリモートコマンドタグを追加します。[ベンダー統合についての詳細](/ja/platforms/remote-commands/how-it-works/#vendor-integrations)を学びましょう。

## インストール

### 依存関係マネージャ




1. Xcodeプロジェクトで、**File &gt; Add Packages... &gt; Add Package Dependency**を選択します。
2. リポジトリURLを入力します：`https://github.com/tealium/tealium-ios-kochava-remote-command`。
3. バージョンルールを構成します。通常は`Up to next major`が推奨されます。現在の`TealiumKochava`バージョンがリストに表示されない場合は、Swiftパッケージキャッシュをリセットしてください。
4. インストールする`TealiumKochava`モジュールを選択し、そのモジュールをインストールしたいアプリターゲットを選択します。

プロジェクトに複数のアプリターゲットがあり、複数のアプリターゲットに`TealiumKochava`モジュールが必要な場合は、**Frameworks, Libraries, and Embedded Content**セクションで手動で追加する必要があります。

追加のアプリターゲットに`TealiumKochava`をインストールするには：

1. **Project Navigator**でXcodeプロジェクトを選択します。
2. Xcodeプロジェクトで、**TARGETS**セクションのアプリターゲットを選択します。
3. **General &gt; Frameworks, Libraries &amp; Embedded Content**に移動し、`TealiumKochava`モジュールをアプリターゲットに追加します。

Tealium Swiftライブラリから追加のモジュールを追加するには、[Swift Package Manager](/ja/platforms/ios-swift/install/#swift-package-manager-recommended)の指示に従ってください。




1. Podfileから`tealium-swift`と`pod &#34;KochavaTrackeriOS&#34;`を削除します。`tealium-swift`の依存関係はすでに`TealiumKochava`フレームワークに含まれています。

2. Podfileに次の依存関係を追加します：
      ```ruby
      pod &#34;TealiumKochava&#34;
      ```
      `TealiumKochava`ポッドには次の`TealiumSwift`依存関係が含まれています：
      ```bash
      &#39;tealium-swift/Core&#39;
      &#39;tealium-swift/RemoteCommands&#39;
      &#39;tealium-swift/TagManagement&#39;
      ```

3. `TealiumHelper`ファイルおよび`Tealium`クラスまたはKochavaリモートコマンドにアクセスする他のファイルで`TealiumSwift`および`TealiumKochava`モジュールをインポートします。




1. Cartfileから`tealium-swift`を削除します。`tealium-swift`の依存関係はすでに`TealiumKochava`フレームワークに含まれています。

2. Cartfileに次の依存関係を追加します：
      ```bash
      github &#34;tealium/tealium-ios-kochava-remote-command&#34;
      ```

Tealium for Swift SDK (バージョン1.6.5&#43;)は、インストール時に`TealiumDelegate`モジュールを含める必要があります。




1. まだ行っていない場合は、[Tealium for Android (Kotlin)](/ja/platforms/android-kotlin/install/)または[Tealium for Android (Java)](/ja/platforms/android-java/install/)をインストールし、プロジェクトのトップレベルの`build.gradle`ファイルにTealium Maven URLを追加します。

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

2. アプリプロジェクトの`build.gradle`ファイルに次の依存関係を追加して、Kochava SDKとTealium-Kochavaリモートコマンドをインポートします：
      ```groovy
      dependencies {
            implementation &#39;com.tealium.remotecommands:kochava:1.0.0&#39;
      }
      ```





### 手動インストール




Kochavaリモートコマンドの手動インストールには、[Tealium for Swift](/ja/platforms/ios-swift/)ライブラリのインストールが必要です。iOSプロジェクト用のKochavaリモートコマンドをインストールするには：

1. まだ行っていない場合は、[Kochava SDK](https://support.kochava.com/sdk-integration/ios-sdk-integration/)をインストールします。

2. [Tealium iOS Kochavaリモートコマンド](https://github.com/tealium/tealium-ios-kochava-remote-command)リポジトリをクローンし、`Sources`フォルダ内のファイルをプロジェクトにドラッグします。

3. [`remoteAPIEnabled`](/ja/platforms/ios-swift/api/tealium-config/#remoteapienabled)構成フラグを`true`に構成します。




Kochavaリモートコマンドの手動インストールには、[Tealium for Android (Kotlin)](/ja/platforms/android-kotlin/install/)または[Tealium for Android (Java)](/ja/platforms/android-java/install/)のインストールが必要です。

Androidプロジェクト用のKochavaリモートコマンドをインストールするには：

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

2. `&lt;PROJECT_ROOT&gt;/&lt;MODULE&gt;/libs`に`tealium-kochava.aar`を追加します。

3. `build.gradle`ファイルにTealiumライブラリの依存関係を追加します：

      ```groovy
      dependencies {
            implementation(name:&#39;tealium-kochava&#39;, ext:&#39;aar&#39;)
      }
      ```


## 初期化

すべてのTealiumライブラリで、初期化時にKochavaモバイルリモートコマンドを登録します。




TealiumのiOS（Swift）ライブラリ用のJSON構成ファイルまたはリモートコマンドタグでリモートコマンドを初期化します：
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
    let kochava = KochavaRemoteCommand() 

    // ローカルJSON
    //let kochava = KochavaRemoteCommand(type: .local(file: &#34;kochava&#34;))

    // リモートJSON 
    //let kochava = KochavaRemoteCommand(type: .remote(url: &#34;https://some.domain.com/kochava.json&#34;)) 

    remoteCommands.add(kochava)
}
```




TealiumのKotlinライブラリ用のJSON構成ファイルまたはリモートコマンドタグでリモートコマンドを初期化します：
```kotlin
val config = TealiumConfig(application,
        &#34;ACCOUNT&#34;,
        &#34;PROFILE&#34;,
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands, Dispatchers.TagManagement));
val kochava = KochavaRemoteCommand(application);

var tealium = Tealium.create(TEALIUM_MAIN, config) {

    // Webviewタグ
    remoteCommands?.add(kochava); 

    // ローカルJSON
    //remoteCommands?.add(kochava, filename = &#34;kochava.json&#34;); 

    // リモートJSON
    //remoteCommands?.add(kochava, remoteUrl = &#34;https://some.domain.com/kochava.json&#34;); 
}
```




TealiumのAndroid（Java）ライブラリ用のリモートコマンドタグでリモートコマンドを初期化します：

```java
RemoteCommand kochava = new KochavaRemoteCommand(application);
teal.addRemoteCommand(kochava);
```



## JSONテンプレート

[JSON構成ファイル](/ja/platforms/remote-commands/how-it-works/#json-configuration-file)を使用してリモートコマンドを構成する場合は、以下のテンプレートを参考にしてください。このテンプレートには、標準的なインストールで使用される一般的なマッピングが含まれています。必要に応じてマッピングを編集してください。

```json
{
  &#34;config&#34;: {
    &#34;app_guid&#34;: &#34;test app guid&#34;,
    &#34;log_level&#34;: &#34;debug&#34;,
    &#34;app_tracking_transparency_enabled&#34;: false,
    &#34;limit_ad_tracking&#34;: true,
    &#34;identity_link_ids&#34;: {
        &#34;userID&#34;: &#34;CUST123&#34;,
        &#34;userName&#34;: &#34;Bob&#34;
    }
  },
  &#34;mappings&#34;: {
      &#34;event_title&#34;: &#34;custom_event_name&#34;,
      &#34;achievement_id&#34;: &#34;custom.achievement_id&#34;,
      &#34;ad_network_name&#34;: &#34;custom.ad_network_name&#34;,
      &#34;campaign_id&#34;: &#34;event.ad_campaign_id&#34;,
      &#34;campaign&#34;: &#34;event.ad_campaign_name&#34;,
      &#34;cart_add_location&#34;: &#34;event.item_added_from&#34;,
      &#34;checkout_option&#34;: &#34;custom.checkout_option&#34;,
      &#34;checkout_step&#34;: &#34;custom.checkout_step&#34;,
      &#34;content&#34;: &#34;event.content_id&#34;,
      &#34;content_type&#34;: &#34;event.content_type&#34;,
      &#34;coupon&#34;: &#34;custom.coupon&#34;,
      &#34;currency_code&#34;: &#34;event.currency&#34;,
      &#34;customer_id&#34;: &#34;event.user_id,identity_link_ids.userID&#34;,
      &#34;device_type&#34;: &#34;event.ad_device_type&#34;,
      &#34;end_date&#34;: &#34;event.end_date&#34;,
      &#34;flight_number&#34;: &#34;custom.flight_number&#34;,
      &#34;game_character&#34;: &#34;custom.character&#34;,
      &#34;group_name&#34;: &#34;event.ad_group_name&#34;,
      &#34;guest_checkout&#34;: &#34;event.checkout_as_guest&#34;,
      &#34;level&#34;: &#34;event.level&#34;,
      &#34;number_nights&#34;: &#34;custom.number_nights&#34;,
      &#34;number_pax&#34;: &#34;custom.number_passengers&#34;,
      &#34;number_rooms&#34;: &#34;custom.number_rooms&#34;,
      &#34;order_id&#34;: &#34;event.order_id&#34;,
      &#34;order_shipping_amount&#34;: &#34;custom.shipping&#34;,
      &#34;order_tax_amount&#34;: &#34;custom.tax&#34;,
      &#34;order_total&#34;: &#34;custom.total&#34;,
      &#34;product_brand&#34;: &#34;custom.brand&#34;,
      &#34;product_category&#34;: &#34;custom.category&#34;,
      &#34;product_id&#34;: &#34;custom.product_id&#34;,
      &#34;product_name&#34;: &#34;event.name&#34;,
      &#34;product_quantity&#34;: &#34;event.quantity&#34;,
      &#34;product_unit_price&#34;: &#34;event.price&#34;,
      &#34;rating&#34;: &#34;event.rating_value&#34;,
      &#34;score&#34;: &#34;event.score&#34;,
      &#34;search_keyword&#34;: &#34;event.search_term&#34;,
      &#34;search_results&#34;: &#34;event.results&#34;,
      &#34;signup_method&#34;: &#34;event.registration_method&#34;,
      &#34;start_date&#34;: &#34;event.start_date&#34;,
      &#34;travel_destination&#34;: &#34;event.destination&#34;,
      &#34;travel_class&#34;: &#34;custom.travel_class&#34;,
      &#34;travel_origin&#34;: &#34;event.origin&#34;,
      &#34;username&#34;: &#34;event.user_name,identity_link_ids.userName&#34;
    },
  &#34;commands&#34;: {
      &#34;launch&#34;: &#34;initialize&#34;,
      &#34;user_login&#34;: &#34;custom,sendidentitylink&#34;,
      &#34;user_register&#34;: &#34;registrationcomplete&#34;,
      &#34;share&#34;: &#34;custom&#34;,
      &#34;show_offers&#34;: &#34;adclick,adview&#34;,
      &#34;join_group&#34;: &#34;custom&#34;,
      &#34;travel_order&#34;: &#34;purchase&#34;,
      &#34;unlock_achievement&#34;: &#34;achievement&#34;,
      &#34;level_up&#34;: &#34;levelcomplete&#34;,
      &#34;stop_tutorial&#34;: &#34;tutorialcomplete&#34;,
      &#34;record_score&#34;: &#34;custom&#34;,
      &#34;category&#34;: &#34;view&#34;,
      &#34;product&#34;: &#34;view&#34;,
      &#34;cart_add&#34;: &#34;addtocart&#34;,
      &#34;wishlist_add&#34;: &#34;addtowishlist&#34;,
      &#34;checkout&#34;: &#34;checkoutstart&#34;,
      &#34;rating&#34;: &#34;rating&#34;,
      &#34;search&#34;: &#34;search&#34;,
      &#34;screen_veiw&#34;: &#34;view&#34;,
      &#34;email_signup&#34;: &#34;subscribe&#34;,
      &#34;order&#34;: &#34;purchase&#34;,
      &#34;disable_analytics&#34;: &#34;sleeptracker,invalidate&#34;
  }
}
```

## プッシュメッセージトラッキング（iOS）

Tealium Swiftライブラリには、TealiumおよびKochavaリモートコマンドを介してプッシュメッセージトラッキングを処理するための`TealiumRegistration`プロトコルが含まれています。このプロトコルに準拠するラッパークラス`KochavaInstance`を使用して、プッシュメッセージ認証イベント、プッシュメッセージオープンイベント、およびアンインストールトラッキングを送信します。プッシュメッセージトラッキング機能を活用することをお勧めします。

iOSプロジェクトでプッシュメッセージトラッキングを統合するための手順は次のとおりです：

1. `TealiumHelper.swift`ファイルで、`TealiumRegistration`プロトコルに準拠するオブジェクトの空の配列を初期化します。例えば：
      ```swift
      var pushMessagingHelpers = [TealiumRegistration]()
      ```
2. `KochavaRemoteCommand`の前に`KochavaInstance`を初期化します
3. 上記の配列に`KochavaInstance`を追加します

以下はプッシュメッセージトラッキング統合の例です：

```swift
var pushMessagingHelpers = [TealiumRegistration]()

//...

teal = Tealium(config: config) { responses in
  guard let remoteCommands = self.tealium?.remoteCommands() else {
        return
  }
  let kochavaInstance = KochavaInstance()
  let kochavaRemoteCommand = KochavaRemoteCommand(kochavaInstance: kochavaInstance)
  remoteCommands.add(kochavaRemoteCommand)
  self.pushMessagingHelpers.append(kochavaInstance)
}
```

`TealiumHelper.swift`ファイル全体を見るには、[Kochava Remote Command Example App](https://github.com/Tealium/tealium-ios-kochava-remote-command/tree/master/TealiumKochavaExample)をご覧ください。ユーザーが通知に登録した後、プッシュメッセージを開いた後、またはアプリをアンインストールした後にKochavaにイベントを送信するには、ファイル[`AppDelegate.swift`](https://github.com/Tealium/tealium-ios-kochava-remote-command/blob/master/TealiumKochavaExample/TealiumKochavaExample/AppDelegate.swift)を参照してください。

Kochavaのプッシュメッセージトラッキングについての詳細は、[Kochava iOS push notification](https://support.kochava.com/sdk-integration/ios-sdk-integration/ios-push-notification/)ドキュメントをご覧ください。
## iOS向けエンリッチメントディープリンキング

Tealium Swiftライブラリには、TealiumおよびKochavaリモートコマンドを介してディープリンクを処理するための`TealiumDeepLinkable`プロトコルが含まれています。このプロトコルに準拠するラッパークラス`KochavaInstance`を使用して、ユーザーを希望の場所にリダイレクトする前に`.deepLink`イベントを送信します。

以下は、iOSプロジェクトにエンリッチメントディープリンキングを統合する手順です：

1. `TealiumHelper.swift`ファイルで、`TealiumDeepLinkable`プロトコルに準拠するオブジェクトの空の配列を初期化します。例えば：
      ```swift
      var deepLinkHelpers = [TealiumDeepLinkable]()
      ```
2. `KochavaRemoteCommand`の前に`KochavaInstance`を初期化します。
3. 上記の配列に`KochavaInstance`を追加します。

以下は、エンリッチメントディープリンキング統合の完全な例です：
      ```swift
      var deepLinkHelpers = [TealiumDeepLinkable]()

      //...

      teal = Tealium(config: config) { responses in
        guard let remoteCommands = self.tealium?.remoteCommands() else {
          return
        }
        let kochavaInstance = KochavaInstance()
        let kochavaRemoteCommand = KochavaRemoteCommand(kochavaInstance: kochavaInstance)
        remoteCommands.add(kochavaRemoteCommand)
        self.deepLinkHelpers.append(kochavaInstance)
      }
      ```

`TealiumHelper.swift`ファイル全体を見るには、[Kochava Remote Command Example App](https://github.com/Tealium/tealium-ios-kochava-remote-command/tree/master/TealiumKochavaExample)を参照してください。

通知の登録、プッシュメッセージの開封、またはアプリのアンインストール後にKochavaにイベントを送信するには、[`AppDelegate.swift`](https://github.com/Tealium/tealium-ios-kochava-remote-command/blob/master/TealiumKochavaExample/TealiumKochavaExample/AppDelegate.swift)ファイルを参照してください。

Kochavaのエンリッチメントディープリンキングについての詳細は、[Kochava iOS](http://support.kochava.com/sdk-integration/ios-sdk-integration/ios-using-the-sdk/)ドキュメントを参照してください。

## サポートされているメソッド

各Kochavaメソッドに対応するコマンドをマッピングします。Kochavaメソッドをトリガーするには、指定された形式で対応するコマンドを渡します。

#### iOSリモートコマンド

| iOSリモートコマンド | Kochavaメソッド |
| :-- | :-- |
| `initialize` | `start()` |
| `sleepTracker` | `sleepTracker (KochavaTracker.sharedオブジェクトのプロパティ)` |
| `invalidate` | `invalidate()` |
| 下記のいずれかのイベント名 | `sendEvent()` |
| `sendIdentityLink` | `sendIdentityLink()` |
| `AppDelegate`内の`didReceiveRemoteNotification`で手動で呼び出される | `sendEvent() - イベントタイプ: .pushOpened` |
| `AppDelegate`内の`didRegisterForRemoteNotificationsWithDeviceToken`で`TealiumRegistration`プロトコル(`registerPushToken()`メソッド)を使用して手動で呼び出される | `addRemoteNotificationsDeviceToken()` |
| `AppDelegate`内の`continue userActivity`で`TealiumDeeplinkable`プロトコルを使用して手動で呼び出される | `KVADeeplink.process()`および/または`sendEvent() - イベントタイプ: .deepLink` |

#### Androidリモートコマンド

| Androidリモートコマンド | Kochavaメソッド |
| :-- | :-- |
| `configure` | `configure()` |
| `setsleep` | `setSleep()` |
| 下記のいずれかのイベント名 | `sendEvent()` |

### 標準イベント名

`trackEvent`メソッドでサポートされる以下の標準イベントコマンド名があります。コマンドが送信され、イベントに必要なすべての変数がマッピングされ定義されている場合、コマンドは自動的にKochava SDKでトリガーされます。

| リモートコマンド | Kochavaイベント名 (iOS)| Kochavaイベント名 (Android) |
| :-- | :-- | :-- |
|`achievement`| `KVAEventType.achievement`| `Commands.ACHIEVEMENT` |
|`addToCart`| `KVAEventType.addToCart`| `Commands.ADD_TO_CART` |
|`addToWishlist`| `KVAEventType.addToWishList`| `Commands.ADD_TO_WISH_LIST` |
|`registrationComplete`| `KVAEventType.registrationComplete`| `Commands.REGISTRATION_COMPLETE` |
|`tutorialComplete`| `KVAEventType.tutorialComplete`| `Commands.TUTORIAL_COMPLETE` |
|`levelComplete`| `KVAEventType.levelComplete`| `Commands.LEVEL_COMPLETE` |
|`checkoutStart`| `KVAEventType.checkoutStart`| `Commands.CHECKOUT_START` |
|`purchase`| `KVAEventType.purchase`| `Commands.PURCHASE` |
|`subscribe`| `KVAEventType.subscribe`| `Commands.SUBSCRIBE` |
|`startTrial`| `KVAEventType.startTrial`| `Commands.START_TRIAL` |
|`rating`| `KVAEventType.rating`| `Commands.RATING` |
|`search`| `KVAEventType.search`| `Commands.SEARCH` |
|`adView`| `KVAEventType.adView`| `Commands.AD_VIEW` |
|`view`| `KVAEventType.view`| `Commands.VIEW` |
|`pushOpened`| `KVAEventType.pushOpened`| `customEventNameString`がマッピングで必要です |
|`pushRecieved`| `KVAEventType.pushReceived`| `customEventNameString`がマッピングで必要です |
|`consentGranted`| `KochavaEventTypeEnumConsentGranted`| `customEventNameString`がマッピングで必要です |
|`adClick`| `KVAEventType.adClick`| `customEventNameString`がマッピングで必要です |
|`custom`| `KVAEventType.custom` (`customEventNameString`がマッピングで必要です)| `customEventNameString`がマッピングで必要です |

iOSでは、`KVAEvent.deepLink`イベントは、ネイティブの`KVAEvent.send()`メソッドまたは[`TealiumDeepLinkable`プロトコル](/ja/platforms/remote-commands/integrations/kochava/#enhanced-deeplinking-ios)を使用して`AppDelegate`で送信する必要があります。

### SDKセットアップ

Kochava SDKセットアップについてもっと学びましょう：

  - [Kochava iOS SDK](https://support.kochava.com/sdk-integration/ios-sdk-integration/)
  - [Kochava Android SDK](https://support.kochava.com/sdk-integration/android-sdk-integration/)

#### 初期化

Kochava SDKは起動時に自動的に初期化されます。Kochava App GUIDはTealiumリモートコマンド構成で構成されます。

| リモートコマンド | Kochavaメソッド |
|---|---|
| `initialize`  | `start()` |

起動時に以下のいずれかが構成されている場合、それらは`configure()`メソッド中に送信されます。

##### 構成オプション

| 名前 | TiQ変数マッピング | 説明 | タイプ |
|---|---|---|---|
| ログレベル  | `log_level` | コンソールでのKochava出力のログレベル：`none`, `error`, `warn`, `info`, `debug`, `trace` ([ログレベルについてもっと学ぶ](https://support.kochava.com/sdk-integration/ios-sdk-integration/ios-using-the-sdk/?scrollto=marker_10)) | `String` |
| アトリビューションデータの取得 | `retrieve_attribution_data`  | アトリビューションデータが準備できたときにデリゲート/リスナーを構成するためのブール値。`TealiumKochava`では、`attributionDictionary`が[Volatile Storage](/ja/platforms/getting-started-mobile/mobile-concepts/#volatile-storage)に構成され、`tealium_event`の`track`コールとして送信されます。デリゲート/リスナーメソッドは`TealiumKochavaTracker`に追加されるかもしれません ([アトリビューションの取得についてもっと学ぶ](https://support.kochava.com/sdk-integration/ios-sdk-integration/ios-using-the-sdk/?scrollto=marker_6))| `Bool` |
| Identity Link ID | `identity_link_ids`  | キーと値のペアの形で異なるアイデンティティをリンクします ([アイデンティティリンキングについてもっと学ぶ](https://support.kochava.com/sdk-integration/ios-sdk-integration/ios-using-the-sdk/?scrollto=marker_5)) | `Int` |
| 広告追跡の制限 | `limit_ad_tracking`  | 有効にされている場合、アプリケーションレベルで広告追跡を制限します (デフォルト：`false`) | `Bool` |
| アプリ追跡透明性の有効化 (iOS 14&#43;) | `app_tracking_transparency_enabled`  | 有効にされている場合、KochavaのApp Tracking Transparencyの自動実装を有効にします (iOS 14&#43;) (デフォルト：`false`) | `Bool` |

#### スリープトラッカー

| リモートコマンド | Kochavaメソッド |
|---|---|
| `sleeptracker` (iOS) | `sleepTracker` (`KochavaTracker.shared`オブジェクトのプロパティ) |
| `setsleep` (Android) | `setSleep()` |

|  パラメータ | タイプ |
|---|---|
|  `sleep` (必須) | `Bool` |


#### 無効化 (iOS)

| リモートコマンド | Kochavaメソッド |
| :--- | :---|
| `invalidate`  | `invalidate()` |


#### アイデンティティリンクの送信 (iOS)

|  リモートコマンド | Kochavaメソッド |
|---|---|
| `sendidentitylink`  | `sendIdentityLink()` |

|  パラメータ | タイプ |
|---|---|
|  `identityLinkIds` (必須) | キー値ペア |
#### カスタムイベントの送信 (iOS)

|  リモートコマンド | Kochavaメソッド |
|---|---|
| [標準イベント名](#standard-event-names) | `send()` |

|  パラメータ | タイプ |
|---|---|
|  `event_parameters` (オプション) | キー値ペア |

#### カスタムイベントの送信 (iOS)

|  リモートコマンド | Kochavaメソッド |
|---|---|
| `custom`  | `sendCustom()` |

|  パラメータ | タイプ |
|---|---|
|  `custom_event_name` (必須) | `String` |
|  `info_dictionary` (オプション) | キー値ペア |
