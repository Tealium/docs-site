---
title: リモートコマンド：Airship
description: AndroidおよびSwift/iOS向けのTealiumリモートコマンドとAirshipの統合。
url: https://docs.tealium.com/ja/platforms/remote-commands/integrations/airship/
---

## 要件

* [Airshipの認証情報](https://docs.airship.com/guides/messaging/user-guide/admin/security/app-keys-secrets/)
* 次のいずれかのモバイルライブラリ：
  * [Tealium for Android](https://docs.tealium.com/ja/platforms/android-java/)
  * [Tealium for iOS-Swift](https://docs.tealium.com/ja/platforms/ios-swift/)
* タグ管理のAirshipリモートコマンドタグ

## 仕組み

Airship統合では、次の3つの項目を使用します。

1. AirshipネイティブSDK
2. AirshipのメソッドをラップするTealium Airshipリモートコマンドモジュール
3. イベントトラッキングをAirshipのネイティブ呼び出しに変換するAirshipリモートコマンドタグ

Airshipリモートコマンドモジュールをアプリに追加すると、ベンダー固有のコードをアプリに追加することなく、必要なAirshipライブラリが自動的にインストールされます。Airship SDKを個別にインストールする必要はありません。

## インストール
### 依存関係マネージャー




Swift Package Managerは、TealiumAirshipパッケージをインストールするための推奨される最も簡単な方法です。Swift Package Managerを使用してiOS向けAirshipリモートコマンドをインストールするには、次の手順を実行します。

1. Xcodeプロジェクトで、**File > Add Packages... > Add Package Dependency**を選択します。

2. リポジトリURLとして`https://github.com/tealium/tealium-ios-airship-remote-command`を入力します。

3. バージョンルールを構成します。通常は`Up to next major`を推奨します。現在の`TealiumAirship`バージョンがリストに表示されない場合は、Swiftパッケージのキャッシュをリセットしてください。

4. インストールする`TealiumAirship`モジュールを選択し、モジュールのインストール先となるアプリターゲットを選択します。
5. Tealium Swiftライブラリの追加モジュールを使用する場合は、[Swift Package Managerの手順](https://docs.tealium.com/ja/platforms/ios-swift/install/#swift-package-manager-recommended)に従って追加してください。

プロジェクトに複数のアプリターゲットがあり、複数のターゲットで`TealiumAirship`モジュールが必要な場合は、**Frameworks, Libraries, and Embedded Content**セクションで手動で追加する必要があります。

追加のアプリターゲットに`TealiumAirship`をインストールするには、次の手順を実行します。

1. **Project Navigator**でXcodeプロジェクトを選択します。
2. Xcodeプロジェクトの**TARGETS**セクションで、アプリターゲットを選択します。
3. **General > Frameworks, Libraries & Embedded Content**に移動し、`TealiumAirship`モジュールを選択してアプリターゲットに追加します。




1. Podfileに`pod "tealium-swift"`および`pod "Airship"`が存在する場合は削除します。`tealium-swift`の依存関係は、すでに`TealiumAirship`フレームワークに含まれています。

2. 次の依存関係をPodfileに追加します。  
      ```ruby
      pod "TealiumAirship"
      ```
      `TealiumAirship` Podには、次の`TealiumSwift`依存関係が含まれています。  
      ```bash
      "tealium-swift/Core"
      "tealium-swift/RemoteCommands"
      "tealium-swift/TagManagement"
      ```

3. 次のようなその他の必要なモジュールをPodfileに手動で追加します。   
      ```ruby
      pod "tealium-swift/Lifecycle"
      pod "tealium-swift/VisitorService"
      ```
      詳細については、[iOS向けの推奨モジュール](https://docs.tealium.com/ja/platforms/ios-swift/modules/)を参照してください。

4. `TealiumHelper`ファイル、および`Tealium`クラスまたはAirshipリモートコマンドにアクセスするその他のファイルで、`TealiumSwift`モジュールと`TealiumAirship`モジュールをインポートします。




1. Cartfileから`tealium-swift`を削除します。`tealium-swift`の依存関係は、すでに`TealiumAirship`フレームワークに含まれています。

2. Cartfileに次の行が存在する場合は削除します。  
      ```bash
      github "urbanairship/ios-library"
      ```

3. 次の依存関係をCartfileに追加します。  
      ```bash
      github "tealium/tealium-ios-airship-remote-command"
      ```






1. まだ実行していない場合は、[Tealium for Android](https://docs.tealium.com/ja/platforms/android-java/install/)をインストールし、Tealium Maven URLをプロジェクトの最上位`build.gradle`ファイルに追加します。

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

2. アプリプロジェクトの`build.gradle`ファイルに次の依存関係を追加して、Tealium-Airshipリモートコマンドをインポートします。  
      ```groovy
      dependencies {
            implementation 'com.tealium.remotecommands:airship:1.1.0'
      }
      ```



### 手動インストール




Airshipリモートコマンドを手動でインストールするには、[Tealium for Swift](https://docs.tealium.com/ja/platforms/ios-swift/)ライブラリがインストールされている必要があります。iOSプロジェクトにAirshipリモートコマンドをインストールするには、次の手順を実行します。

1. まだインストールしていない場合は、[Airship SDK](https://github.com/urbanairship/ios-library)をインストールします。

2. [Tealium iOS Airshipリモートコマンド](https://github.com/tealium/tealium-ios-airship-remote-command)リポジトリをクローンし、`Sources`フォルダー内のファイルをプロジェクトにドラッグします。

3. `Dispatchers.RemoteCommands`をディスパッチャーとして追加します。

4. [`remoteAPIEnabled`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#remoteapienabled)構成フラグを`true`に構成します。




Airshipリモートコマンドを手動でインストールするには、[Tealium for Android（Kotlin）](https://docs.tealium.com/ja/platforms/android-kotlin/install/)または[Tealium for Android（Java）](https://docs.tealium.com/ja/platforms/android-java/install/)がインストールされている必要があります。AndroidプロジェクトにAirshipリモートコマンドをインストールするには、次の手順を実行します。

1. プロジェクトルートの`build.gradle`ファイルに`flatDir`を追加します。  
      ```groovy
      repositories {
          flatDir {
              dirs ('/src/main/libs')
          }
      }
      ```

2. `tealium-airship.aar`を`<PROJECT_ROOT>/<MODULE>/libs`に追加します。

3. Tealiumライブラリの依存関係を`build.gradle`ファイルに追加します。  
      ```groovy
      dependencies {
            implementation(name:'tealium-airship', ext:'aar')
      }
      ```



## 初期化

JSON構成ファイル、またはTealiumのAndroidライブラリまたはSwiftライブラリ用のリモートコマンドタグを使用して、リモートコマンドを初期化します。




次の例では、Tealiumインスタンスを作成し、iOS向けTealium SwiftライブラリにAirshipリモートコマンドを登録します。

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
    let airship = AirshipRemoteCommand() 

    // Local JSON
    //let airship = AirshipRemoteCommand(type: .local(file: "airship"))

    // Remote JSON
    //let airship = AirshipRemoteCommand(type: .remote(url: "https://some.domain.com/airship.json"))
    remoteCommands.add(airship)
}
```




次の例では、Tealiumインスタンスを作成し、Android（Kotlin）向けのAirshipリモートコマンドを登録します。

```kotlin
val config = TealiumConfig(application,
        "ACCOUNT",
        "PROFILE",
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands, Dispatchers.TagManagement));
val airship = AirshipRemoteCommand(application);

var tealium = Tealium.create(TEALIUM_MAIN, config) {

    // Webview Tag
    remoteCommands?.add(airship);

    // Local JSON
    //remoteCommands?.add(airship, filename = "airship.json");

    // Remote JSON
    //remoteCommands?.add(airship, remoteUrl = "https://some.domain.com/airship.json"); 
}
```



## サポートされているメソッド

各 Airship メソッドにコマンドをマッピングします。Airship メソッドをトリガーするには、対応するコマンドを指定された形式で渡します。

| リモートコマンド | Airship メソッド |
| :-- | :-- |
| `initialize` | `takeOff()` |
| `trackevent` | `UACustomEvent.track()` |
| `trackscreenview` | `trackScreen` |
| `enableanalytics` | `analytics()?.isEnabled` |
| `disableanalytics` | `analytics()?.isEnabled` |
| `setnameduser` | `UAirship.namedUser()?.identifier` |
| `setcustomidentifiers` | `analytics()?.associateDeviceIdentifiers` |
| `enableadvertisingidentifiers` | `analytics()?.associateDeviceIdentifiers` |
| `enableinappmessaging` | `UAInAppMessageManager.shared()?.isEnabled` |
| `disableinappmessaging` | `UAInAppMessageManager.shared()?.isEnabled` |
| `pauseinappmessaging` | `UAInAppMessageManager.shared()?.isPaused` |
| `unpauseinappmessaging` | `UAInAppMessageManager.shared()?.isPaused` |
| `setinappmessagingdisplayinterval` | `UAInAppMessageManager.shared()?.displayInterval` |
| `enableuserpushnotifications` | `UAirship.push()?.userPushNotificationsEnabled` |
| `disableuserpushnotifications` | `UAirship.push()?.userPushNotificationsEnabled` |
| `enablebackgroundpushnotifications` | `UAirship.push()?.backgroundPushNotificationsEnabled` |
| `disablebackgroundpushnotifications` | `UAirship.push()?.backgroundPushNotificationsEnabled` |
| `setpushnotificationoptions` | `UAirship.push()?.notificationOptions` |
| `setforegroundpresentationoptions` | `UAirship.push()?.defaultPresentationOptions` |
| `setbadgenumber` | `UAirship.push()?.badgeNumber` |
| `resetbadgenumber` | `UAirship.push()?.resetBadge()` |
| `enableautobadge` | `UAirship.push()?.isAutobadgeEnabled` |
| `disableautobadge` | `UAirship.push()?.isAutobadgeEnabled` |
| `enablequiettime` | `UAirship.push()?.isQuietTimeEnabled` |
| `disablequiettime` | `UAirship.push()?.isQuietTimeEnabled` |
| `setquiettimestart` | `UAirship.push()?.setQuietTimeStartHour` |
| `setchanneltags` | `UAirship.channel()?.tags` |
| `setnamedusertags` | `UAirship.namedUser()?.setTags()` |
| `addtag` | `UAirship.channel()?.addTag()` |
| `removetag` | `UAirship.channel()?.removeTag` |
| `addtaggroup` | `UAirship.channel()?.addTags, UAirship.namedUser()?.addTags` |
| `removetaggroup` | `UAirship.channel()?.removeTags, UAirship.namedUser()?.removeTags` |
| `setattributes` | `UAirship.channel()?.apply` |
| `displaymessagecenter` | `UAMessageCenter.shared().display()` |
| `setmessagecentertitle` | `UAMessageCenter.shared()?.defaultUI.title` |
| `setmessagecenterstyle` | `UAMessageCenter.shared().defaultUI.style` |
| `enablelocation` | `UALocation.shared().isLocationUpdatesEnabled` |
| `disablelocation` | `UALocation.shared().isLocationUpdatesEnabled` |
| `enablebackgroundlocation` | `UALocation.shared().isBackgroundLocationUpdatesAllowed` |
| `disablebackgroundlocation` | `UALocation.shared().isBackgroundLocationUpdatesAllowed` |


<blockquote>
Airship SDK は Tealium SDK と統合されているため、Tealium Airship リモートコマンドタグで提供されていない機能であっても、SDK を直接呼び出すことで、Airship の任意のネイティブ機能をトリガーできます。
</blockquote>


### SDK のセットアップ

#### 初期化

Airship SDK は起動時に自動的に初期化されます。Airship API キーはタグ構成で指定します。

| リモートコマンド | Airship メソッド |
|---|---|
| `initialize`  | `takeOff()` |

**使用可能な UAConfig パラメータ**

| パラメータ | 型 | 例 |
| :-- | :-- | :-- |
| `productionAppKey`（必須） | `String` | `MyProdKey` |
| `productionAppSecret`（必須） | `String|MyProdSecret` |
| `developmentAppKey`（必須） | `String` | `MyDevKey` |
| `developmentAppSecret`（必須） | `String` | `MyDevSecret` |
| `site`（任意） | `String` | `eu/us` |
| `isDataCollectionOptInEnabled`（任意） | `Boolean` | `true` |
| `isInProduction`（任意） | `Boolean` | `true` |
| `developmentLogLevel`（任意） | `String` | `debug/error/info/none/trace/undefined/warn` |
| `productionLogLevel`（任意） | `String` | `debug/error/info/none/trace/undefined/warn` |
| `isAnalyticsEnabled`（任意） | `Boolean` | `true` |

Airship 開発者ガイド：SDK の初期セットアップ

- [iOS](https://docs.airship.com/platform/ios/getting-started/#takeoff)
- [Android](https://docs.airship.com/platform/android/getting-started/#takeoff)

#### trackEvent

カスタムイベントを Airship に送信します。

| リモートコマンド | Airship メソッド |
|---|---|
| `trackEvent`  | `UACustomEvent.track()` |

| パラメータ | 型 | 例 |
| :-- | :-- | :-- |
| `event_name`（必須） | `String` | `Purchase` |
| `event`（任意） | `JSON object` | `{"my_numeric_property": 1}` |
| `event_value`（任意） | `Number` | `1.5` |

Airship 開発者ガイド：イベントトラッキング

- [iOS](https://docs.airship.com/platform/ios/analytics-and-reporting/#ios-custom-events)
- [Android](https://docs.airship.com/platform/android/analytics-and-reporting/#android-custom-events)

#### trackScreenView

画面表示をトラッキングします。

| リモートコマンド | Airship メソッド |
| :-- | :-- |
| `trackScreenView` | `UAirship.analytics()?.trackScreen` |


| パラメータ | 型 | 例 |
| :-- | :-- | :-- |
| `screen_name`（必須） | `String` | `Home Screen` |

Airship 開発者ガイド：イベントトラッキング

- [iOS](https://docs.airship.com/platform/ios/analytics-and-reporting/#ios-screen-tracking)
- [Android](https://docs.airship.com/platform/android/analytics-and-reporting/#android-screen-tracking)

#### enableAnalytics

以前に無効化された Airship Analytics を有効化します（デフォルトでは有効です）。

| リモートコマンド | Airship メソッド |
| :-- | :-- |
| `enableAnalytics` | `UAirship.analytics()?.isEnabled` |

Airship 開発者ガイド：Analytics の有効化

- [iOS](https://docs.airship.com/platform/ios/analytics-and-reporting/#disabling-analytics)
- [Android](https://docs.airship.com/platform/android/analytics-and-reporting/#disabling-analytics)

#### disableAnalytics

以前に有効化された Airship Analytics を無効化します（デフォルトでは有効です）。

| リモートコマンド | Airship メソッド |
| :-- | :-- |
| `disableAnalytics` | `UAirship.analytics()?.isEnabled` |

Airship 開発者ガイド：Analytics の無効化

- [iOS](https://docs.airship.com/platform/ios/analytics-and-reporting/#disabling-analytics)
- [Android](https://docs.airship.com/platform/android/analytics-and-reporting/#disabling-analytics)

#### setNamedUser

現在のアプリユーザーに既知のユーザー識別子を構成します。

| リモートコマンド | Airship メソッド |
| :-- | :-- |
| `setNamedUser` | `UAirship.namedUser()?.identifier` |


| パラメータ | 型 | 例 |
| :-- | :-- | :-- |
| `named_user_identifier`（必須） | `String` | `email@tealium.com` |

Airship 開発者ガイド：イベントトラッキング

- [iOS](https://docs.airship.com/platform/ios/segmentation/#named-users-ios)
- [Android](https://docs.airship.com/platform/android/segmentation/#named-users-android)

#### setCustomIdentifiers

ユーザーにとって重要と判断した追加のカスタム識別子を構成します。

| リモートコマンド | Airship メソッド |
| :-- | :-- |
| `setCustomIdentifiers` | `UAirship.analytics()?.associateDeviceIdentifiers` |


| パラメータ | 型 | 例 |
| :-- | :-- | :-- |
| `custom`（必須） | `JSON Object`（文字列のみ） | `{"my_custom_identifier":"user@email.com"}` |

Airship 開発者ガイド：

- [iOS](https://docs.airship.com/platform/ios/analytics-and-reporting/#ios-custom-identifiers)
- [Android](https://docs.airship.com/platform/android/analytics-and-reporting/#android-custom-identifiers)

#### enableAdvertisingIdentifiers

広告識別子をカスタム識別子のディクショナリに追加します（IDFV、IDFA、広告トラッキングの有効化）。

| リモートコマンド | Airship メソッド |
| :-- | :-- |
| `setCustomIdentifiers` | `UAirship.analytics()?.associateDeviceIdentifiers` |

Airship 開発者ガイド：

- [iOS](https://docs.airship.com/platform/ios/analytics-and-reporting/#ios-custom-identifiers)
- [Android](https://docs.airship.com/platform/android/analytics-and-reporting/#android-custom-identifiers)
#### enableInAppMessaging

アプリ内メッセージング機能を有効にします。

| リモートコマンド | Airship メソッド |
| :-- | :-- |
| `enableInAppMessaging` | `UAInAppMessageManager.shared()?.isEnabled` |

Airship 開発者ガイド：

- [iOS](https://docs.airship.com/platform/ios/in-app-automation/#component-enablement)
- [Android](https://docs.airship.com/platform/android/in-app-automation/#feature-enablement)

#### disableInAppMessaging

アプリ内メッセージング機能を無効にします。

| リモートコマンド | Airship メソッド |
| :-- | :-- |
| `disableInAppMessaging` | `UAInAppMessageManager.shared()?.isEnabled` |

Airship 開発者ガイド：

- [iOS](https://docs.airship.com/platform/ios/in-app-automation/#component-enablement)
- [Android](https://docs.airship.com/platform/android/in-app-automation/#feature-enablement)

#### pauseInAppMessaging

アプリ内メッセージング機能を有効にします。

| リモートコマンド | Airship メソッド |
| :-- | :-- |
| `pauseInAppMessaging` | `UAInAppMessageManager.shared()?.isPaused` |

Airship 開発者ガイド：

- [iOS](https://docs.airship.com/platform/ios/in-app-automation/#pausing-message-display)
- [Android](https://docs.airship.com/platform/android/in-app-automation/#pausing-message-display)

#### unPauseInAppMessaging

アプリ内メッセージング機能を有効にします。

| リモートコマンド | Airship メソッド |
| :-- | :-- |
| `unPauseInAppMessaging` | `UAInAppMessageManager.shared()?.isPaused` |

Airship 開発者ガイド：

- [iOS](https://docs.airship.com/platform/ios/in-app-automation/#pausing-message-display)
- [Android](https://docs.airship.com/platform/android/in-app-automation/#pausing-message-display)

#### setInAppMessagingDisplayInterval

Airship が新しいアプリ内メッセージを表示するまで待機する時間を、*秒単位*で指定します。

| リモートコマンド | Airship メソッド |
| :-- | :-- |
| `setInAppMessagingDisplayInterval` | `UAInAppMessageManager.shared()?.displayInterval` |

| パラメーター | 型 | 例 |
| :-- | :-- | :-- |
| `in_app_messaging_display_interval`（必須） | `String` | `"10"` |

Airship 開発者ガイド：

- [iOS](https://docs.airship.com/platform/ios/in-app-automation/#pausing-message-display)
- [Android](https://docs.airship.com/platform/android/in-app-automation/#pausing-message-display)

#### enableUserPushNotifications

ユーザー向けプッシュ通知を有効にします。

| リモートコマンド | Airship メソッド |
| :-- | :-- |
| `enableUserPushNotifications` | `UAirship.push()?.userPushNotificationsEnabled` |

| パラメーター | 型 | 例 |
| :-- | :-- | :-- |
| `push_notification_options`（任意） | `Array of Strings` | `["badge", "sound", "announcement"]` |

指定可能なプッシュメッセージングオプション：`"badge"`、`"sound"`、`"alert"`、`"carplay"`、`"announcement"`、`"critical"`、`"app_notification_settings"`

Airship 開発者ガイド：

- [iOS](https://docs.airship.com/platform/ios/push-notifications/#enabling-user-notifications)
- [Android](https://docs.airship.com/platform/android/push-notifications/#enabling-user-notifications)

#### disableUserPushNotifications

ユーザー向けプッシュ通知を無効にします。

| リモートコマンド | Airship メソッド |
| :-- | :-- |
| `enableUserPushNotifications` | `UAirship.push()?.userPushNotificationsEnabled` |

Airship 開発者ガイド：

- [iOS](https://docs.airship.com/platform/ios/push-notifications/#enabling-user-notifications)
- [Android](https://docs.airship.com/platform/android/push-notifications/#enabling-user-notifications)

#### enableBackgroundPushNotifications

バックグラウンドプッシュ通知を有効にします。

| リモートコマンド | Airship メソッド |
| :-- | :-- |
| `enableUserPushNotifications` | `UAirship.push()?. backgroundPushNotificationsEnabled` |

Airship 開発者ガイド：

- [iOS](https://docs.airship.com/platform/ios/push-notifications/#enabling-user-notifications)
- [Android](https://docs.airship.com/platform/android/push-notifications/#enabling-user-notifications)

#### disableBackgroundPushNotifications

バックグラウンドプッシュ通知を無効にします。

| リモートコマンド | Airship メソッド |
| :-- | :-- |
| `disableBackgroundPushNotifications` | `UAirship.push()?.backgroundPushNotificationsEnabled` |

Airship 開発者ガイド：

- [iOS](https://docs.airship.com/platform/ios/push-notifications/#enabling-user-notifications)
- [Android](https://docs.airship.com/platform/android/push-notifications/#enabling-user-notifications)

#### setPushNotificationOptions

プッシュ通知オプションを構成します。iOS のみ。

| リモートコマンド | Airship メソッド |
| :-- | :-- |
| `setPushNotificationOptions` | `UAirship.push()?.notificationOptions` |

| パラメーター | 型 | 例 |
| :-- | :-- | :-- |
| `push_notification_options`（必須） | `Array of Strings` | `["badge", "sound", "announcement"]` |

指定可能なプッシュメッセージングオプション：`"badge"`、`"sound"`、`"alert"`、`"carplay"`、`"announcement"`、`"critical"`、`"app_notification_settings"`

Airship 開発者ガイド：

- [iOS](https://docs.airship.com/platform/ios/push-notifications/#notification-options)

#### setForegroundPresentationOptions

プッシュ通知の表示オプションを構成します。iOS のみ。

| リモートコマンド | Airship メソッド |
| :-- | :-- |
| `setForegroundPresentationOptions` | `UAirship.push()?.defaultPresentationOptions` |

| パラメーター | 型 | 例 |
| :-- | :-- | :-- |
| `foreground_presentation_options`（必須） | `Array of Strings` | `["badge", "sound", "alert"]` |

指定可能なフォアグラウンド表示オプション：`"badge"`、`"sound"`、`"alert"`

Airship 開発者ガイド：

- [iOS](https://docs.airship.com/platform/ios/push-notifications/#foreground-presentation-options)

#### setBadgeNumber

アプリアイコンのバッジ番号を指定した数値に構成します。iOS のみ。

| リモートコマンド | Airship メソッド |
| :-- | :-- |
| `setBadgeNumber` | `UAirship.push()?.badgeNumber` |

| パラメーター | 型 | 例 |
| :-- | :-- | :-- |
| `badge_number`（必須） | `Number` | `3` |

Airship 開発者ガイド：

- [iOS](https://docs.airship.com/platform/ios/push-notifications/#ios-feature-badges)

#### resetBadgeNumber

バッジ番号をリセットします。iOS のみ。

| リモートコマンド | Airship メソッド |
| :-- | :-- |
| `setBadgeNumber` | `UAirship.push()?.badgeNumber` |

Airship 開発者ガイド：

- [iOS](https://docs.airship.com/platform/ios/push-notifications/#ios-feature-badges)

#### enableAutoBadge

自動バッジ機能を有効にします。iOS のみ。

| リモートコマンド | Airship メソッド |
| :-- | :-- |
| `enableAutoBadge` | `UAirship.push()?.isAutobadgeEnabled` |

Airship 開発者ガイド：

- [iOS](https://docs.airship.com/platform/ios/push-notifications/#ios-feature-badges)

#### disableAutoBadge

自動バッジ機能を無効にします。iOS のみ。

| リモートコマンド | Airship メソッド |
| :-- | :-- |
| `disableAutoBadge` | `UAirship.push()?.isAutobadgeEnabled` |

Airship 開発者ガイド：

- [iOS](https://docs.airship.com/platform/ios/push-notifications/#ios-feature-badges)

#### enableQuietTime

Quiet Time 機能を有効にします。iOS のみ。

| リモートコマンド | Airship メソッド |
| :-- | :-- |
| `enableAutoBadge` | `UAirship.push()?.isQuietTimeEnabled` |

Airship 開発者ガイド：

- [iOS](https://docs.airship.com/platform/ios/push-notifications/#quiet-time)

#### disableQuietTime

Quiet Time 機能を無効にします。iOS のみ。

| リモートコマンド | Airship メソッド |
| :-- | :-- |
| `disableAutoBadge` | `UAirship.push()?.isQuietTimeEnabled` |

Airship 開発者ガイド：

- [iOS](https://docs.airship.com/platform/ios/push-notifications/#quiet-time)

#### setQuietTimeStart

Quiet Time 機能の時間制約を構成します。iOS のみ。

| リモートコマンド | Airship メソッド |
| :-- | :-- |
| `setQuietTimeStart` | `UAirship.push()?.isQuietTimeEnabled` |

| パラメーター | 型 | 例 |
| :-- | :-- | :-- |
| `quiet`（必須） | `JSON Object` | `{'start_hour': 3, 'start_minute': 30, 'end_hour': 4, 'end_minute': 30` |

quiet オブジェクト内で必須の項目：

| パラメーター | 型 | 例 |
| :-- | :-- | :-- |
| `start_hour`（必須） | `Number` | `3` |
| `start_minute`（必須） | `Number` | `30` |
| `end_hour`（必須） | `Number` | `4` |
| `end_minute`（必須） | `Number` | `30` |

Airship 開発者ガイド：

- [iOS](https://docs.airship.com/platform/ios/push-notifications/#quiet-time)
#### setChannelTags

`updateRegistration` 関数を呼び出します。通知オプションを変更した後に呼び出す必要があります。iOS のみ。

| リモートコマンド | Airship メソッド |
| :-- | :-- |
| `updateRegistration` | `UAirship.push()?.updateRegistration` |

Airship 開発者ガイド：

- [iOS](https://docs.airship.com/platform/ios/push-notifications/#quiet-time)

#### setNamedUserTags

指定ユーザーのタグを構成し、以前に構成されたタグを上書きします。

| リモートコマンド | Airship メソッド |
| :-- | :-- |
| `setNamedUserTags` | `UAirship.channel()?.addTags` | `UAirship.namedUser()?.addTags` |

| パラメーター | 型 | 例 |
| :-- | :-- | :-- |
| `named_user_tags`（必須） | `String Array` | `["silver-member", "gold-member"]` |
| `tag_group`（必須） | `String` | `loyalty` |

Airship 開発者ガイド：

- [iOS](https://docs.airship.com/platform/ios/segmentation/#ios-tag-groups)
- [Android](https://docs.airship.com/platform/android/segmentation/#android-tag-groups)

#### addTag

チャネルタグを追加します。

| リモートコマンド | Airship メソッド |
| :-- | :-- |
| `addTag` | `UAirship.channel()?.addTag` |

| パラメーター | 型 | 例 |
| :-- | :-- | :-- |
| `channel_tag`（必須） | `String` | `"a_tag"` |

Airship 開発者ガイド：

- [iOS](https://docs.airship.com/platform/ios/segmentation/#tags)
- [Android](https://docs.airship.com/platform/android/segmentation/#tags)

#### removeTag

チャネルタグを削除します。

| リモートコマンド | Airship メソッド |
| :-- | :-- |
| `removeTag` | `UAirship.channel()?.removeTag` |

| パラメーター | 型 | 例 |
| :-- | :-- | :-- |
| `channel_tag`（必須） | `String` | `"a_tag"` |

Airship 開発者ガイド：

- [iOS](https://docs.airship.com/platform/ios/segmentation/#tags)
- [Android](https://docs.airship.com/platform/android/segmentation/#tags)

#### addTagGroup

指定ユーザーまたはチャネルにタググループを追加します。

| リモートコマンド | Airship メソッド |
| :-- | :-- |
| `addTagGroup` | `UAirship.channel()?.addTags` | `UAirship.namedUser()?.addTags` |

| パラメーター | 型 | 例 |
| :-- | :-- | :-- |
| `named_user_tags` | `channel_tags`（必須） | `String Array` | `["silver-member", "gold-member"]` |
| `tag_group`（必須） | `String` | `loyalty` |
| `tag_type`（必須） | `String` | `channel|named_user` |

Airship 開発者ガイド：

- [iOS](https://docs.airship.com/platform/ios/segmentation/#ios-tag-groups)
- [Android](https://docs.airship.com/platform/android/segmentation/#android-tag-groups)

#### removeTagGroup

指定ユーザーまたはチャネルからタググループを削除します。

| リモートコマンド | Airship メソッド |
| :-- | :-- |
| `removeTagGroup` | `UAirship.channel()?.removeTags` | `UAirship.namedUser()?.removeTags` |

| パラメーター | 型 | 例 |
| :-- | :-- | :-- |
| `named_user_tags` | `channel_tags`（必須） | `String Array` | `["silver-member", "gold-member"]` |
| `tag_group`（必須） | `String` | `loyalty` |
| `tag_type`（必須） | `String` | `channel` | `named_user` |

Airship 開発者ガイド：

- [iOS](https://docs.airship.com/platform/ios/segmentation/#ios-tag-groups)
- [Android](https://docs.airship.com/platform/android/segmentation/#android-tag-groups)

#### setAttributes

カスタム属性を構成します。

| リモートコマンド | Airship メソッド |
| :-- | :-- |
| `setAttributes` | `UAirship.channel()?.apply` |


| パラメーター | 型 | 例 |
| :-- | :-- | :-- |
| `attributes`（必須） | `JSON object` | `{"last\_product\_purchased": "A1234567"}` |

属性値には文字列または数値のみを指定できます。

Airship 開発者ガイド：

- [iOS](https://docs.airship.com/platform/ios/segmentation/#attributes)
- [Android](https://docs.airship.com/platform/android/segmentation/#attributes)

#### displayMessageCenter

メッセージセンターを表示します。

| リモートコマンド | Airship メソッド |
| :-- | :-- |
| `displayMessageCenter` | `UAMessageCenter.shared().display` |

Airship 開発者ガイド：

- [iOS](https://docs.airship.com/platform/ios/message-center/#displaying-the-message-center)
- [Android](https://docs.airship.com/platform/android/message-center/#android-rich-push-inbox-intents)

#### setMessageCenterTitle

メッセージセンターのタイトルを構成します。iOS のみ。

| リモートコマンド | Airship メソッド |
| :-- | :-- |
| `setMessageCenterTitle` | `UAMessageCenter.shared().defaultUI.title` |


| パラメーター | 型 | 例 |
| :-- | :-- | :-- |
| `message_center_title`（必須） | `String` | `"Custom Message Center"` |

Airship 開発者ガイド：

- [iOS](https://docs.airship.com/platform/ios/message-center/#title)

#### setMessageCenterStyle

メッセージセンターのスタイルを構成します。iOS のみ。

| リモートコマンド | Airship メソッド |
| :-- | :-- |
| `setMessageCenterStyle` | `UAMessageCenter.shared().defaultUI.style` |

| パラメーター | 型 | 例 |
| :-- | :-- | :-- |
| `message_center_style`（必須） | `JSON object` | 以下の例を参照 |

```
{"titleFont": {"size": Double, "name":"fontname"},
 "cellTitleFont": {"size": Double, "name":"fontname"},
 "cellDateFont": {"size": Double, "name":"fontname"},
 "navigationBarColor": {"red": Double, "green": Double, "blue": Double, "alpha": Double}
 "titleColor": {"red": Double, "green": Double, "blue": Double, "alpha": Double}
 "tintColor": {"red": Double, "green": Double, "blue": Double, "alpha": Double}
 }
```

Airship 開発者ガイド：

- [iOS](https://docs.airship.com/platform/ios/message-center/#styling-ios-mc)

#### enableLocation

位置情報を有効にします。

| リモートコマンド | Airship メソッド |
| :-- | :-- |
| `enableLocation` | `UALocation.shared().isLocationUpdatesEnabled` |

Airship 開発者ガイド：

- [iOS](https://docs.airship.com/platform/ios/location/#enabling-location)
- [Android](https://docs.airship.com/platform/android/location-targeting/#continuous-location-updates)

#### disableLocation

位置情報を無効にします。

| リモートコマンド | Airship メソッド |
| :-- | :-- |
| `disableLocation` | `UALocation.shared().isLocationUpdatesEnabled` |

Airship 開発者ガイド：

- [iOS](https://docs.airship.com/platform/ios/location/#allow-background-location)
- [Android](https://docs.airship.com/platform/android/location-targeting/#using-airship-location)

#### enableBackgroundLocation

バックグラウンドでの位置情報取得を有効にします。

| リモートコマンド | Airship メソッド |
| :-- | :-- |
| `enableBackgroundLocation` | `UALocation.shared().isBackgroundLocationUpdatesAllowed` |

Airship 開発者ガイド：

- [iOS](https://docs.airship.com/platform/ios/location/#allow-background-location)
- [Android](https://docs.airship.com/platform/android/location-targeting/#continuous-location-updates)

#### disableBackgroundLocation

バックグラウンドでの位置情報取得を無効にします。

| リモートコマンド | Airship メソッド |
| :-- | :-- |
| `disableBackgroundLocation` | `UALocation.shared().isBackgroundLocationUpdatesAllowed` |

Airship 開発者ガイド：

- [iOS](https://docs.airship.com/platform/ios/location/#allow-background-location)
- [Android](https://docs.airship.com/platform/android/location-targeting/#continuous-location-updates)