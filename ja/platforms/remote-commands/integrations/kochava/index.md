---
title: リモートコマンド：Kochava
description: AndroidおよびSwift/iOS向けのTealiumリモートコマンドとKochavaの連携。
url: https://docs.tealium.com/ja/platforms/remote-commands/integrations/kochava/
---
## 要件

* [Kochava App GUID](https://support.kochava.com/reference-information/locating-an-app-guid/)
* 以下のいずれかのモバイルライブラリ：
  * [Tealium for Android-Kotlin](https://docs.tealium.com/ja/platforms/android-kotlin/)（1.0.0以降）
  * [Tealium for Android-Java](https://docs.tealium.com/ja/platforms/android-java/)（5.9.0以降）
  * [Tealium for iOS-Swift](https://docs.tealium.com/ja/platforms/ios-swift/)（2.1.0以降）
* 以下のいずれかのリモートコマンド連携：
  * [KochavaリモートコマンドJSONファイル](https://docs.tealium.com/ja/platforms/remote-commands/integrations/kochava/#json-template)（Android-Kotlin 1.0.0以降またはiOS-Swift 2.1.0以降が必要）
  * タグ管理の[Kochavaリモートコマンドタグ](https://docs.tealium.com/kochava-mobile-remote-command-tag/)

## 仕組み

Kochava連携では、次の3つの項目を使用します。

1. KochavaネイティブSDK
2. Kochavaのメソッドをラップするリモートコマンドモジュール
3. イベントトラッキングをKochavaのネイティブ呼び出しに変換するJSON構成ファイルまたはリモートコマンドタグ

Kochavaリモートコマンドモジュールをアプリに追加すると、必要なKochavaライブラリが自動的にインストールおよびビルドされるため、ベンダー固有のコードをアプリに追加する必要はありません。依存関係マネージャーを使用してインストールする場合は、Kochava SDKを別途インストールする必要はありません。

リモートコマンドには、JSON構成ファイルを使用する方法と、タグ管理を使用してマッピングを構成する方法の2つがあります。ベンダー連携には、リモートでホストするかアプリ内にローカルに配置したJSON構成ファイルの使用を推奨します。タグ管理を使用する場合は、ベンダー連携用のリモートコマンドタグを追加します。[ベンダー連携](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/#vendor-integrations)の詳細をご覧ください。

## インストール

### 依存関係マネージャー




1. Xcodeプロジェクトで、**File > Add Packages... > Add Package Dependency**を選択します。
2. リポジトリのURLとして`https://github.com/tealium/tealium-ios-kochava-remote-command`を入力します。
3. バージョンルールを構成します。通常は`Up to next major`を推奨します。現在の`TealiumKochava`バージョンがリストに表示されない場合は、Swiftパッケージのキャッシュをリセットしてください。
4. インストールする`TealiumKochava`モジュールを選択し、そのモジュールをインストールするアプリターゲットを選択します。

プロジェクトに複数のアプリターゲットがあり、追加のアプリターゲットでも`TealiumKochava`モジュールが必要な場合は、**Frameworks, Libraries, and Embedded Content**セクションで手動で追加する必要があります。

追加のアプリターゲットに`TealiumKochava`をインストールするには、次の手順を実行します。

1. **Project Navigator**でXcodeプロジェクトを選択します。
2. Xcodeプロジェクトの**TARGETS**セクションでアプリターゲットを選択します。
3. **General > Frameworks, Libraries & Embedded Content**に移動し、アプリターゲットに追加する`TealiumKochava`モジュールを選択します。

Tealium Swiftライブラリから追加のモジュールをインストールするには、[Swift Package Manager](https://docs.tealium.com/ja/platforms/ios-swift/install/#swift-package-manager-recommended)の手順に従ってください。




1. Podfileに`tealium-swift`および`pod "KochavaTrackeriOS"`がすでに存在する場合は、それらを削除します。`tealium-swift`の依存関係は、すでに`TealiumKochava`フレームワークに含まれています。

2. Podfileに次の依存関係を追加します。
      ```ruby
      pod "TealiumKochava"
      ```
      `TealiumKochava` Podには、次の`TealiumSwift`依存関係が含まれています。  
      ```bash
      'tealium-swift/Core'
      'tealium-swift/RemoteCommands'
      'tealium-swift/TagManagement'
      ```

3. `TealiumHelper`ファイル、および`Tealium`クラスまたはKochavaリモートコマンドにアクセスするその他のファイルに、`TealiumSwift`モジュールと`TealiumKochava`モジュールをインポートします。




1. Cartfileから`tealium-swift`を削除します。`tealium-swift`の依存関係は、すでに`TealiumKochava`フレームワークに含まれています。

2. Cartfileに次の依存関係を追加します。  
      ```bash
      github "tealium/tealium-ios-kochava-remote-command"
      ```


<blockquote>
Tealium for Swift SDK（バージョン1.6.5以降）では、インストールに`TealiumDelegate`モジュールを含める必要があります。
</blockquote>






1. まだ実行していない場合は、[Tealium for Android（Kotlin）](https://docs.tealium.com/ja/platforms/android-kotlin/install/)または[Tealium for Android（Java）](https://docs.tealium.com/ja/platforms/android-java/install/)をインストールし、プロジェクトのトップレベルの`build.gradle`ファイルにTealium Maven URLを追加します。

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

2. アプリプロジェクトの`build.gradle`ファイルに次の依存関係を追加して、Kochava SDKとTealium-Kochavaリモートコマンドの両方をインポートします。  
      ```groovy
      dependencies {
            implementation 'com.tealium.remotecommands:kochava:1.0.0'
      }
      ```





### 手動インストール




Kochavaリモートコマンドを手動でインストールするには、[Tealium for Swift](https://docs.tealium.com/ja/platforms/ios-swift/)ライブラリがインストールされている必要があります。iOSプロジェクトにKochavaリモートコマンドをインストールするには、次の手順を実行します。

1. まだインストールしていない場合は、[Kochava SDK](https://support.kochava.com/sdk-integration/ios-sdk-integration/)をインストールします。

2. [Tealium iOS Kochavaリモートコマンド](https://github.com/tealium/tealium-ios-kochava-remote-command)リポジトリをクローンし、`Sources`フォルダー内のファイルをプロジェクトにドラッグします。

3. [`remoteAPIEnabled`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#remoteapienabled)構成フラグを`true.`に構成します。




Kochavaリモートコマンドを手動でインストールするには、[Tealium for Android（Kotlin）](https://docs.tealium.com/ja/platforms/android-kotlin/install/)または[Tealium for Android（Java）](https://docs.tealium.com/ja/platforms/android-java/install/)がインストールされている必要があります。

AndroidプロジェクトにKochavaリモートコマンドをインストールするには、次の手順を実行します。

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

2. `tealium-kochava.aar`を`<PROJECT_ROOT>/<MODULE>/libs`に追加します。

3. `build.gradle`ファイルにTealiumライブラリの依存関係を追加します。

      ```groovy
      dependencies {
            implementation(name:'tealium-kochava', ext:'aar')
      }
      ```


## 初期化

すべての Tealium ライブラリで、初期化時に Kochava モバイルリモートコマンドを登録します。




JSON 構成ファイルまたは Remote Command タグを使用して、Tealium の iOS（Swift）ライブラリ向けにリモートコマンドを初期化します。
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
    let kochava = KochavaRemoteCommand() 

    // Local JSON
    //let kochava = KochavaRemoteCommand(type: .local(file: "kochava"))

    // Remote JSON 
    //let kochava = KochavaRemoteCommand(type: .remote(url: "https://some.domain.com/kochava.json")) 

    remoteCommands.add(kochava)
}
```




JSON 構成ファイルまたは Remote Command タグを使用して、Tealium の Kotlin ライブラリ向けにリモートコマンドを初期化します。
```kotlin
val config = TealiumConfig(application,
        "ACCOUNT",
        "PROFILE",
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands, Dispatchers.TagManagement));
val kochava = KochavaRemoteCommand(application);

var tealium = Tealium.create(TEALIUM_MAIN, config) {

    // Webview Tag
    remoteCommands?.add(kochava); 

    // Local JSON
    //remoteCommands?.add(kochava, filename = "kochava.json"); 

    // Remote JSON
    //remoteCommands?.add(kochava, remoteUrl = "https://some.domain.com/kochava.json"); 
}
```




Remote Command タグを使用して、Tealium の Android（Java）ライブラリ向けにリモートコマンドを初期化します。

```java
RemoteCommand kochava = new KochavaRemoteCommand(application);
teal.addRemoteCommand(kochava);
```



## JSON テンプレート

[JSON 構成ファイル](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/#json-configuration-file)を使用してリモートコマンドを構成する場合は、以下のテンプレートを参考にしてください。このテンプレートには、標準インストールで使用される一般的なマッピングが含まれています。必要に応じてマッピングを編集してください。

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

Tealium Swift ライブラリには、Tealium および Kochava Remote Command を介したプッシュメッセージトラッキングを処理するための `TealiumRegistration` プロトコルが含まれています。プッシュメッセージの認証イベント、プッシュメッセージの開封イベント、およびアンインストールトラッキングの送信に使用するラッパークラス `KochavaInstance` で、このプロトコルに準拠しています。プッシュメッセージトラッキング機能を利用することをお勧めします。

以下の手順で、iOS プロジェクトにプッシュメッセージトラッキングを統合します。

1. `TealiumHelper.swift` ファイルで、`TealiumRegistration` プロトコルに準拠するオブジェクトの空の配列を初期化します。例：  
      ```swift
      var pushMessagingHelpers = [TealiumRegistration]()
      ```
2. `KochavaRemoteCommand` より前に `KochavaInstance` を初期化します。
3. 上記の配列に `KochavaInstance` を追加します。

以下は、プッシュメッセージトラッキングを統合する例です。  

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

`TealiumHelper.swift` ファイル全体を確認するには、[Kochava Remote Command サンプルアプリ](https://github.com/Tealium/tealium-ios-kochava-remote-command/tree/master/TealiumKochavaExample)を参照してください。ユーザーが通知を登録したとき、プッシュメッセージを開いたとき、またはアプリをアンインストールしたときに Kochava へイベントを送信する方法については、[`AppDelegate.swift`](https://github.com/Tealium/tealium-ios-kochava-remote-command/blob/master/TealiumKochavaExample/TealiumKochavaExample/AppDelegate.swift) ファイルを参照してください。

Kochava のプッシュメッセージトラッキングの詳細については、[Kochava iOS プッシュ通知](https://support.kochava.com/sdk-integration/ios-sdk-integration/ios-push-notification/)のドキュメントを参照してください。
## エンリッチメントされたディープリンク（iOS）

Tealium Swift ライブラリには、Tealium および Kochava Remote Command を介してディープリンクを処理するための `TealiumDeepLinkable` プロトコルが含まれています。このプロトコルは、ユーザーを目的の場所へリダイレクトする前に `.deepLink` イベントを送信するために使用されるラッパークラス `KochavaInstance` に実装されています。

iOS プロジェクトにエンリッチメントされたディープリンクを統合する手順は次のとおりです。

1. `TealiumHelper.swift` ファイルで、`TealiumDeepLinkable ` プロトコルに準拠するオブジェクトの空の配列を初期化します。例：  
      ```swift
      var deepLinkHelpers = [TealiumDeepLinkable]()
      ```
2. `KochavaRemoteCommand` より前に `KochavaInstance` を初期化します。
3. 上記の配列に `KochavaInstance` を追加します。

以下は、エンリッチメントされたディープリンク統合の完全な例です。  
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

`TealiumHelper.swift` ファイル全体については、[Kochava Remote Command サンプルアプリ](https://github.com/Tealium/tealium-ios-kochava-remote-command/tree/master/TealiumKochavaExample)を参照してください。

ユーザーが通知に登録したとき、プッシュメッセージを開いたとき、またはアプリをアンインストールしたときに Kochava へイベントを送信する方法については、[`AppDelegate.swift`](https://github.com/Tealium/tealium-ios-kochava-remote-command/blob/master/TealiumKochavaExample/TealiumKochavaExample/AppDelegate.swift) ファイルを参照してください。

Kochava のエンリッチメントされたディープリンクの詳細については、[Kochava iOS](http://support.kochava.com/sdk-integration/ios-sdk-integration/ios-using-the-sdk/) のドキュメントを参照してください。

## サポートされているメソッド

各 Kochava メソッドにコマンドをマッピングします。Kochava メソッドをトリガーするには、対応するコマンドを指定された形式で渡します。

#### iOS Remote Command

| iOS Remote Command | Kochava メソッド |
| :-- | :-- |
| `initialize` | `start()` |
| `sleepTracker` | `sleepTracker (property on the KochavaTracker.shared object)` |
| `invalidate` | `invalidate()` |
| 以下のいずれかのイベント名 | `sendEvent()` |
| `sendIdentityLink` | `sendIdentityLink()` |
| `AppDelegate` の `didReceiveRemoteNotification` 内で手動で呼び出す | `sendEvent() - event type: .pushOpened` |
| `TealiumRegistration` プロトコル（`registerPushToken()` メソッド）を使用して、`AppDelegate` の `didRegisterForRemoteNotificationsWithDeviceToken` 内で手動で呼び出す | `addRemoteNotificationsDeviceToken()` |
| `TealiumDeeplinkable` プロトコルを使用して、`AppDelegate` の `continue userActivity` 内で手動で呼び出す | `KVADeeplink.process()` and/or `sendEvent() - event type: .deepLink` |

#### Android Remote Command

| Android Remote Command | Kochava メソッド |
| :-- | :-- |
| `configure` | `configure()` |
| `setsleep` | `setSleep()` |
| 以下のいずれかのイベント名 | `sendEvent()` |

### 標準イベント名

`trackEvent` メソッドでは、以下の標準イベントコマンド名がサポートされています。コマンドが送信され、そのイベントに必要なすべての変数がマッピングおよび定義されている場合、Kochava SDK でコマンドが自動的にトリガーされます。

| Remote Command | Kochava イベント名（iOS）| Kochava イベント名（Android）
| :-- | :-- | :-- |
|`achievement`| `KVAEventType.achievement`| `Commands.ACHIEVEMENT` |
|`addToCart`| `KVAEventType.addToCart`| `Commands.ADD_TO_CART` |
|`addToWishlist`| `KVAEventType.addToWishList`| `Commands.Add_TO_WISH_LIST` |
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
|`pushOpened`| `KVAEventType.pushOpened`| マッピングに `customEventNameString` が必要 |
|`pushRecieved`| `KVAEventType.pushReceived`| マッピングに `customEventNameString` が必要 |
|`consentGranted`| `KochavaEventTypeEnumConsentGranted`| マッピングに `customEventNameString` が必要 |
|`adClick`| `KVAEventType.adClick`| マッピングに `customEventNameString` が必要 |
|`custom`| `KVAEventType.custom`（マッピングに `customEventNameString` が必要）| マッピングに `customEventNameString` が必要 |


<blockquote>
iOS では、ネイティブの `KVAEvent.send()` メソッドまたは [`TealiumDeepLinkable` プロトコル](https://docs.tealium.com/ja/platforms/remote-commands/integrations/kochava/#enhanced-deeplinking-ios)のいずれかを使用し、`AppDelegate` で `KVAEvent.deepLink` イベントを送信する必要があります。
</blockquote>


### SDK のセットアップ

Kochava SDK のセットアップについて詳しくは、以下を参照してください。

  - [Kochava iOS SDK](https://support.kochava.com/sdk-integration/ios-sdk-integration/)
  - [Kochava Android SDK](https://support.kochava.com/sdk-integration/android-sdk-integration/)

#### 初期化

Kochava SDK は、起動時に自動的に初期化されます。Kochava App GUID は、Tealium Remote Command の構成で構成されます。

| Remote Command | Kochava メソッド |
|---|---|
| `initialize`  | `start()` |

Kochava Remote Command タグでは、複数の構成オプションを使用できます。以下のいずれかが起動時に構成されている場合、`configure()` メソッドの実行時に送信されます。

##### 構成オプション

| 名前 | TiQ 変数マッピング | 説明 | 型 |
|---|---|---|---|
| ログレベル | `log_level` | コンソールへの Kochava 出力に使用するログレベル：`none`、`error`、`warn`、`info`、`debug`、`trace`（[ログレベル](https://support.kochava.com/sdk-integration/ios-sdk-integration/ios-using-the-sdk/?scrollto=marker_10)の詳細） | `String` |
| アトリビューションデータの取得 | `retrieve_attribution_data` | アトリビューションデータの準備が整ったときにそのデータを取得するデリゲート／リスナーを構成するためのブール値です。`TealiumKochava` では、`attributionDictionary` が[揮発性保存](https://docs.tealium.com/ja/platforms/getting-started-mobile/mobile-concepts/#volatile-storage)に構成され、`tealium_event` が `attribution` の `track` 呼び出しが送信されます。デリゲート／リスナーメソッドは `TealiumKochavaTracker` に追加できます（[アトリビューションの取得](https://support.kochava.com/sdk-integration/ios-sdk-integration/ios-using-the-sdk/?scrollto=marker_6)の詳細）| `Bool` |
| Identity Link ID | `identity_link_ids` | キーと値のペアの形式で異なる ID を関連付けます（[ID の関連付け](https://support.kochava.com/sdk-integration/ios-sdk-integration/ios-using-the-sdk/?scrollto=marker_5)の詳細） | `Int` |
| 広告トラッキングの制限 | `limit_ad_tracking` | 有効にすると、アプリケーションレベルで広告トラッキングを制限します（デフォルト：`false`） | `Bool` |
| App Tracking Transparency の有効化（iOS 14 以降） | `app_tracking_transparency_enabled` | 有効にすると、Kochava による App Tracking Transparency（iOS 14 以降）の自動実装を有効にします。（デフォルト：`false`） | `Bool` |

#### トラッカーのスリープ

| Remote Command | Kochava メソッド |
|---|---|
| `sleeptracker`（iOS） | `sleepTracker`（`KochavaTracker.shared` オブジェクトのプロパティ） |
| `setsleep`（Android） | `setSleep()` |

| パラメータ | 型 |
|---|---|
| `sleep`（必須） | `Bool` |


#### 無効化（iOS）

| Remote Command | Kochava メソッド |
| :--- | :---|
| `invalidate`  | `invalidate()` |


#### Identity Link の送信（iOS）

| Remote Command | Kochava メソッド |
|---|---|
| `sendidentitylink`  | `sendIdentityLink()` |

| パラメータ | 型 |
|---|---|
| `identityLinkIds`（必須） | キーと値のペア |
#### カスタムイベントの送信（iOS）

| リモートコマンド | Kochavaメソッド |
|---|---|
| [標準イベント名](#standard-event-names) | `send()` |

| パラメータ | 型 |
|---|---|
| `event_parameters`（任意） | キーと値のペア |

#### カスタムイベントの送信（iOS）

| リモートコマンド | Kochavaメソッド |
|---|---|
| `custom` | `sendCustom()` |

| パラメータ | 型 |
|---|---|
| `custom_event_name`（必須） | `String` |
| `info_dictionary`（任意） | キーと値のペア |