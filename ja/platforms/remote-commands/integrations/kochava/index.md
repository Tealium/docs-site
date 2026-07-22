---
title: リモートコマンド：Kochava
description: AndroidおよびSwift/iOS用KochavaのTealiumリモートコマンド統合。
url: https://docs.tealium.com/ja/platforms/remote-commands/integrations/kochava/
---
## 要件

* [KochavaアプリGUID](https://support.kochava.com/reference-information/locating-an-app-guid/)
* 以下のいずれかのモバイルライブラリ：
  * [Tealium for Android-Kotlin](https://docs.tealium.com/ja/platforms/android-kotlin/) (1.0.0+)
  * [Tealium for Android-Java](https://docs.tealium.com/ja/platforms/android-java/) (5.9.0+)
  * [Tealium for iOS-Swift](https://docs.tealium.com/ja/platforms/ios-swift/) (2.1.0+)
* 以下のいずれかのリモートコマンド統合：
  * [Kochava Remote Command JSON File](https://docs.tealium.com/ja/platforms/remote-commands/integrations/kochava/#json-template) (Android-Kotlin 1.0.0+またはiOS-Swift 2.1.0+が必要)
  * Tealium iQタグ管理の[Kochava Remote Command tag](https://docs.tealium.com/kochava-mobile-remote-command-tag/)

## 動作原理

Kochava統合は3つのアイテムを使用します：

1. KochavaネイティブSDK
2. Kochavaメソッドをラップするリモートコマンドモジュール
3. イベントトラッキングをネイティブKochavaコールに変換するJSON構成ファイルまたはリモートコマンドタグ

アプリにKochavaリモートコマンドモジュールを追加すると、アプリにベンダー固有のコードを追加することなく、必要なKochavaライブラリが自動的にインストールされてビルドされます。依存関係マネージャーのインストールを使用している場合、Kochava SDKを別途インストールする必要はありません。

リモートコマンドオプションには2つあります：JSON構成ファイル、またはiQタグ管理を使用してマッピングを構成します。JSON構成ファイルは、ベンダー統合のためにリモートまたはアプリ内にローカルでホストされることを推奨されるオプションです。iQタグ管理を使用する場合は、ベンダー統合のためのリモートコマンドタグを追加します。[ベンダー統合についての詳細](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/#vendor-integrations)を学びましょう。

## インストール

### 依存関係マネージャ




1. Xcodeプロジェクトで、**File > Add Packages... > Add Package Dependency**を選択します。
2. リポジトリURLを入力します：`https://github.com/tealium/tealium-ios-kochava-remote-command`。
3. バージョンルールを構成します。通常は`Up to next major`が推奨されます。現在の`TealiumKochava`バージョンがリストに表示されない場合は、Swiftパッケージキャッシュをリセットしてください。
4. インストールする`TealiumKochava`モジュールを選択し、そのモジュールをインストールしたいアプリターゲットを選択します。

プロジェクトに複数のアプリターゲットがあり、複数のアプリターゲットに`TealiumKochava`モジュールが必要な場合は、**Frameworks, Libraries, and Embedded Content**セクションで手動で追加する必要があります。

追加のアプリターゲットに`TealiumKochava`をインストールするには：

1. **Project Navigator**でXcodeプロジェクトを選択します。
2. Xcodeプロジェクトで、**TARGETS**セクションのアプリターゲットを選択します。
3. **General > Frameworks, Libraries & Embedded Content**に移動し、`TealiumKochava`モジュールをアプリターゲットに追加します。

Tealium Swiftライブラリから追加のモジュールを追加するには、[Swift Package Manager](https://docs.tealium.com/ja/platforms/ios-swift/install/#swift-package-manager-recommended)の指示に従ってください。




1. Podfileから`tealium-swift`と`pod "KochavaTrackeriOS"`を削除します。`tealium-swift`の依存関係はすでに`TealiumKochava`フレームワークに含まれています。

2. Podfileに次の依存関係を追加します：
      ```ruby
      pod "TealiumKochava"
      ```
      `TealiumKochava`ポッドには次の`TealiumSwift`依存関係が含まれています：
      ```bash
      'tealium-swift/Core'
      'tealium-swift/RemoteCommands'
      'tealium-swift/TagManagement'
      ```

3. `TealiumHelper`ファイルおよび`Tealium`クラスまたはKochavaリモートコマンドにアクセスする他のファイルで`TealiumSwift`および`TealiumKochava`モジュールをインポートします。




1. Cartfileから`tealium-swift`を削除します。`tealium-swift`の依存関係はすでに`TealiumKochava`フレームワークに含まれています。

2. Cartfileに次の依存関係を追加します：
      ```bash
      github "tealium/tealium-ios-kochava-remote-command"
      ```


<blockquote>
Tealium for Swift SDK (バージョン1.6.5+)は、インストール時に`TealiumDelegate`モジュールを含める必要があります。
</blockquote>





1. まだ行っていない場合は、[Tealium for Android (Kotlin)](https://docs.tealium.com/ja/platforms/android-kotlin/install/)または[Tealium for Android (Java)](https://docs.tealium.com/ja/platforms/android-java/install/)をインストールし、プロジェクトのトップレベルの`build.gradle`ファイルにTealium Maven URLを追加します。

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

2. アプリプロジェクトの`build.gradle`ファイルに次の依存関係を追加して、Kochava SDKとTealium-Kochavaリモートコマンドをインポートします：
      ```groovy
      dependencies {
            implementation 'com.tealium.remotecommands:kochava:1.0.0'
      }
      ```





### 手動インストール




Kochavaリモートコマンドの手動インストールには、[Tealium for Swift](https://docs.tealium.com/ja/platforms/ios-swift/)ライブラリのインストールが必要です。iOSプロジェクト用のKochavaリモートコマンドをインストールするには：

1. まだ行っていない場合は、[Kochava SDK](https://support.kochava.com/sdk-integration/ios-sdk-integration/)をインストールします。

2. [Tealium iOS Kochavaリモートコマンド](https://github.com/tealium/tealium-ios-kochava-remote-command)リポジトリをクローンし、`Sources`フォルダ内のファイルをプロジェクトにドラッグします。

3. [`remoteAPIEnabled`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#remoteapienabled)構成フラグを`true`に構成します。




Kochavaリモートコマンドの手動インストールには、[Tealium for Android (Kotlin)](https://docs.tealium.com/ja/platforms/android-kotlin/install/)または[Tealium for Android (Java)](https://docs.tealium.com/ja/platforms/android-java/install/)のインストールが必要です。

Androidプロジェクト用のKochavaリモートコマンドをインストールするには：

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

2. `<PROJECT_ROOT>/<MODULE>/libs`に`tealium-kochava.aar`を追加します。

3. `build.gradle`ファイルにTealiumライブラリの依存関係を追加します：

      ```groovy
      dependencies {
            implementation(name:'tealium-kochava', ext:'aar')
      }
      ```


## 初期化

すべてのTealiumライブラリで、初期化時にKochavaモバイルリモートコマンドを登録します。




TealiumのiOS（Swift）ライブラリ用のJSON構成ファイルまたはリモートコマンドタグでリモートコマンドを初期化します：
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
    let kochava = KochavaRemoteCommand() 

    // ローカルJSON
    //let kochava = KochavaRemoteCommand(type: .local(file: "kochava"))

    // リモートJSON 
    //let kochava = KochavaRemoteCommand(type: .remote(url: "https://some.domain.com/kochava.json")) 

    remoteCommands.add(kochava)
}
```




TealiumのKotlinライブラリ用のJSON構成ファイルまたはリモートコマンドタグでリモートコマンドを初期化します：
```kotlin
val config = TealiumConfig(application,
        "ACCOUNT",
        "PROFILE",
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands, Dispatchers.TagManagement));
val kochava = KochavaRemoteCommand(application);

var tealium = Tealium.create(TEALIUM_MAIN, config) {

    // Webviewタグ
    remoteCommands?.add(kochava); 

    // ローカルJSON
    //remoteCommands?.add(kochava, filename = "kochava.json"); 

    // リモートJSON
    //remoteCommands?.add(kochava, remoteUrl = "https://some.domain.com/kochava.json"); 
}
```




TealiumのAndroid（Java）ライブラリ用のリモートコマンドタグでリモートコマンドを初期化します：

```java
RemoteCommand kochava = new KochavaRemoteCommand(application);
teal.addRemoteCommand(kochava);
```



## JSONテンプレート

[JSON構成ファイル](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/#json-configuration-file)を使用してリモートコマンドを構成する場合は、以下のテンプレートを参考にしてください。このテンプレートには、標準的なインストールで使用される一般的なマッピングが含まれています。必要に応じてマッピングを編集してください。

```json
{
  "config": {
    "app_guid": "test app guid",
    "log_level": "debug",
    "app_tracking_transparency_enabled": false,
    "limit_ad_tracking": true,
    "identity_link_ids": {
        "userID": "CUST123",
        "userName": "Bob"
    }
  },
  "mappings": {
      "event_title": "custom_event_name",
      "achievement_id": "custom.achievement_id",
      "ad_network_name": "custom.ad_network_name",
      "campaign_id": "event.ad_campaign_id",
      "campaign": "event.ad_campaign_name",
      "cart_add_location": "event.item_added_from",
      "checkout_option": "custom.checkout_option",
      "checkout_step": "custom.checkout_step",
      "content": "event.content_id",
      "content_type": "event.content_type",
      "coupon": "custom.coupon",
      "currency_code": "event.currency",
      "customer_id": "event.user_id,identity_link_ids.userID",
      "device_type": "event.ad_device_type",
      "end_date": "event.end_date",
      "flight_number": "custom.flight_number",
      "game_character": "custom.character",
      "group_name": "event.ad_group_name",
      "guest_checkout": "event.checkout_as_guest",
      "level": "event.level",
      "number_nights": "custom.number_nights",
      "number_pax": "custom.number_passengers",
      "number_rooms": "custom.number_rooms",
      "order_id": "event.order_id",
      "order_shipping_amount": "custom.shipping",
      "order_tax_amount": "custom.tax",
      "order_total": "custom.total",
      "product_brand": "custom.brand",
      "product_category": "custom.category",
      "product_id": "custom.product_id",
      "product_name": "event.name",
      "product_quantity": "event.quantity",
      "product_unit_price": "event.price",
      "rating": "event.rating_value",
      "score": "event.score",
      "search_keyword": "event.search_term",
      "search_results": "event.results",
      "signup_method": "event.registration_method",
      "start_date": "event.start_date",
      "travel_destination": "event.destination",
      "travel_class": "custom.travel_class",
      "travel_origin": "event.origin",
      "username": "event.user_name,identity_link_ids.userName"
    },
  "commands": {
      "launch": "initialize",
      "user_login": "custom,sendidentitylink",
      "user_register": "registrationcomplete",
      "share": "custom",
      "show_offers": "adclick,adview",
      "join_group": "custom",
      "travel_order": "purchase",
      "unlock_achievement": "achievement",
      "level_up": "levelcomplete",
      "stop_tutorial": "tutorialcomplete",
      "record_score": "custom",
      "category": "view",
      "product": "view",
      "cart_add": "addtocart",
      "wishlist_add": "addtowishlist",
      "checkout": "checkoutstart",
      "rating": "rating",
      "search": "search",
      "screen_veiw": "view",
      "email_signup": "subscribe",
      "order": "purchase",
      "disable_analytics": "sleeptracker,invalidate"
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


<blockquote>
iOSでは、`KVAEvent.deepLink`イベントは、ネイティブの`KVAEvent.send()`メソッドまたは[`TealiumDeepLinkable`プロトコル](https://docs.tealium.com/ja/platforms/remote-commands/integrations/kochava/#enhanced-deeplinking-ios)を使用して`AppDelegate`で送信する必要があります。
</blockquote>


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
| アトリビューションデータの取得 | `retrieve_attribution_data`  | アトリビューションデータが準備できたときにデリゲート/リスナーを構成するためのブール値。`TealiumKochava`では、`attributionDictionary`が[Volatile Storage](https://docs.tealium.com/ja/platforms/getting-started-mobile/mobile-concepts/#volatile-storage)に構成され、`tealium_event`の`track`コールとして送信されます。デリゲート/リスナーメソッドは`TealiumKochavaTracker`に追加されるかもしれません ([アトリビューションの取得についてもっと学ぶ](https://support.kochava.com/sdk-integration/ios-sdk-integration/ios-using-the-sdk/?scrollto=marker_6))| `Bool` |
| Identity Link ID | `identity_link_ids`  | キーと値のペアの形で異なるアイデンティティをリンクします ([アイデンティティリンキングについてもっと学ぶ](https://support.kochava.com/sdk-integration/ios-sdk-integration/ios-using-the-sdk/?scrollto=marker_5)) | `Int` |
| 広告追跡の制限 | `limit_ad_tracking`  | 有効にされている場合、アプリケーションレベルで広告追跡を制限します (デフォルト：`false`) | `Bool` |
| アプリ追跡透明性の有効化 (iOS 14+) | `app_tracking_transparency_enabled`  | 有効にされている場合、KochavaのApp Tracking Transparencyの自動実装を有効にします (iOS 14+) (デフォルト：`false`) | `Bool` |

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
