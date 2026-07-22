---
title: リモートコマンド：エアシップ
description: AndroidおよびSwift/iOSのエアシップに対するTealiumリモートコマンド統合。
url: https://docs.tealium.com/ja/platforms/remote-commands/integrations/airship/
---

## 必要条件

- [エアシップの資格情報](https://docs.airship.com/guides/messaging/user-guide/admin/security/app-keys-secrets/)
- 以下のいずれかのモバイルライブラリ：
  - [Android用Tealium](https://docs.tealium.com/ja/platforms/android-java/)
  - [iOS-Swift用Tealium](https://docs.tealium.com/ja/platforms/ios-swift/)
- Tealium iQタグ管理でのエアシップリモートコマンドタグ

## 動作方法

エアシップ統合には3つのアイテムが使用されます：

1. エアシップネイティブSDK
2. エアシップメソッドをラップするTealiumエアシップリモートコマンドモジュール
3. イベントトラッキングをネイティブのエアシップコールに変換するエアシップリモートコマンドタグ

エアシップリモートコマンドモジュールをアプリに追加すると、必要なエアシップライブラリが自動的にインストールされ、ベンダー固有のコードをアプリに追加する必要はありません。エアシップSDKを別途インストールする必要はありません。

## インストール
### 依存関係マネージャー




Swiftパッケージマネージャーは、TealiumAirshipパッケージをインストールするための推奨される最も簡単な方法です。Swiftパッケージマネージャーを使用してiOS向けのエアシップリモートコマンドをインストールするには、次の手順を実行します。

1. Xcodeプロジェクトで、「ファイル」>「パッケージの追加...」>「パッケージの依存関係を追加」を選択します。

2. リポジトリのURLを入力します：`https://github.com/tealium/tealium-ios-airship-remote-command`

3. バージョンルールを構成します。通常は、「次のメジャーバージョンまで」が推奨されます。現在の`TealiumAirship`バージョンがリストに表示されない場合は、Swiftパッケージキャッシュをリセットします。

4. インストールする`TealiumAirship`モジュールを選択し、モジュールをインストールするアプリのターゲットを選択します。
5. Tealium Swiftライブラリから追加のモジュールを使用している場合は、[Swiftパッケージマネージャーの手順](https://docs.tealium.com/ja/platforms/ios-swift/install/#swift-package-manager-recommended)に従って追加します。

プロジェクトに複数のアプリターゲットがある場合で、`TealiumAirship`モジュールを他のアプリターゲットに追加する必要がある場合は、**フレームワーク、ライブラリ、および埋め込みコンテンツ**セクションに手動で追加する必要があります。

追加のアプリターゲットに`TealiumAirship`をインストールするには：

1. **プロジェクトナビゲーター**でXcodeプロジェクトを選択します。
2. Xcodeプロジェクトで、**TARGETS**セクションのアプリターゲットを選択します。
3. **一般 > フレームワーク、ライブラリ、および埋め込みコンテンツ**に移動し、`TealiumAirship`モジュールをアプリターゲットに追加します。




1. Podfileに`pod "tealium-swift"`と`pod "Airship"`が存在する場合は、削除します。`tealium-swift`の依存関係は、`TealiumAirship`フレームワークにすでに含まれています。

2. Podfileに次の依存関係を追加します：  
      ```ruby
      pod "TealiumAirship"
      ```
      `TealiumAirship`ポッドには、次の`TealiumSwift`の依存関係が含まれています：  
      ```bash
      "tealium-swift/Core"
      "tealium-swift/RemoteCommands"
      "tealium-swift/TagManagement"
      ```

3. その他の必要なモジュールを手動でPodfileに追加します。以下は例です：   
      ```ruby
      pod "tealium-swift/Lifecycle"
      pod "tealium-swift/VisitorService"
      ```
      iOS向けの[推奨モジュール](https://docs.tealium.com/ja/platforms/ios-swift/modules/)について詳しくは、ドキュメントを参照してください。

4. `TealiumSwift`および`TealiumAirship`モジュールを`TealiumHelper`ファイルおよび`Tealium`クラスにアクセスする他のファイルにインポートします。




1. Cartfileから`tealium-swift`を削除します。`tealium-swift`の依存関係は、`TealiumAirship`フレームワークにすでに含まれています。

2. Cartfileに次の依存関係を追加します：  
      ```bash
      github "tealium/tealium-ios-airship-remote-command"
      ```






1. [Android用Tealium](https://docs.tealium.com/ja/platforms/android-java/install/)をインストールし、プロジェクトのトップレベルの`build.gradle`ファイルにTealium Maven URLを追加します。

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

2. アプリプロジェクトの`build.gradle`ファイルに、Tealium-Airshipリモートコマンドをインポートするために次の依存関係を追加します：  
      ```groovy
      dependencies {
            implementation 'com.tealium.remotecommands:airship:1.1.0'
      }
      ```



### 手動インストール




エアシップリモートコマンドの手動インストールには、[Swift用Tealium](https://docs.tealium.com/ja/platforms/ios-swift/)ライブラリのインストールが必要です。iOSプロジェクトにエアシップリモートコマンドをインストールするには、次の手順を実行します。

1. [エアシップSDK](https://github.com/urbanairship/ios-library)をインストールします（まだインストールしていない場合）。

2. [Tealium iOS Airshipリモートコマンド](https://github.com/tealium/tealium-ios-airship-remote-command)リポジトリをクローンし、`Sources`フォルダ内のファイルをプロジェクトにドラッグします。

3. `Dispatchers.RemoteCommands`をディスパッチャーとして追加します。

4. [`remoteAPIEnabled`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#remoteapienabled)構成フラグを`true`に構成します。




エアシップリモートコマンドの手動インストールには、[Android（Kotlin）用Tealium](https://docs.tealium.com/ja/platforms/android-kotlin/install/)または[Android（Java）用Tealium](https://docs.tealium.com/ja/platforms/android-java/install/)のインストールが必要です。Androidプロジェクトにエアシップリモートコマンドをインストールするには、次の手順を実行します。

1. プロジェクトのルート`build.gradle`ファイルに`flatDir`を追加します：  
      ```groovy
      repositories {
          flatDir {
              dirs ('/src/main/libs')
          }
      }
      ```

2. `<PROJECT_ROOT>/<MODULE>/libs`に`tealium-airship.aar`を追加します。

3. `build.gradle`ファイルにTealiumライブラリの依存関係を追加します：  
      ```groovy
      dependencies {
            implementation(name:'tealium-airship', ext:'aar')
      }
      ```



## 初期化

JSON構成ファイルまたはTealiumのAndroidまたはSwiftライブラリのリモートコマンドタグを使用して、リモートコマンドを初期化します。




以下の例では、Tealiumインスタンスを作成し、TealiumのSwiftライブラリ用にエアシップリモートコマンドを登録しています。

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
    let airship = AirshipRemoteCommand() 

    // ローカルJSON
    //let airship = AirshipRemoteCommand(type: .local(file: "airship"))

    // リモートJSON
    //let airship = AirshipRemoteCommand(type: .remote(url: "https://some.domain.com/airship.json"))
    remoteCommands.add(airship)
}
```




以下の例では、Tealiumインスタンスを作成し、Android（Kotlin）用のエアシップリモートコマンドを登録しています。

```kotlin
val config = TealiumConfig(application,
        "ACCOUNT",
        "PROFILE",
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands, Dispatchers.TagManagement));
val airship = AirshipRemoteCommand(application);

var tealium = Tealium.create(TEALIUM_MAIN, config) {

    // Webviewタグ
    remoteCommands?.add(airship);

    // ローカルJSON
    //remoteCommands?.add(airship, filename = "airship.json");

    // リモートJSON
    //remoteCommands?.add(airship, remoteUrl = "https://some.domain.com/airship.json"); 
}
```




## サポートされているメソッド

次のAirshipメソッドは、Airshipリモートコマンドタグ内のデータマッピングを使用して、これらのTealiumコマンドをトリガーします。

| リモートコマンド | Airshipメソッド |
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
エアシップSDKはTealiumSDKと統合されているため、Tealiumエアシップリモートコマンドタグで提供されていない機能でも、SDKを直接呼び出すことでネイティブのAirship機能をトリガーすることができます。
</blockquote>


### SDKのセットアップ

#### 初期化

Airship SDKは、起動時に自動的に初期化されます。AirshipのAPIキーは、タグの構成で構成されます。

| リモートコマンド | Airshipメソッド |
|---|---|
| `initialize`  | `takeOff()` |

**可能なUAConfigパラメーター**

| パラメーター | タイプ | 例 |
| :-- | :-- | :-- |
| `productionAppKey`（必須） | `String` | `MyProdKey` |
| `productionAppSecret`（必須） | `String|MyProdSecret` |
| `developmentAppKey`（必須） | `String` | `MyDevKey` |
| `developmentAppSecret`（必須） | `String` | `MyDevSecret` |
| `site`（オプション） | `String` | `eu/us` |
| `isDataCollectionOptInEnabled`（オプション） | `Boolean` | `true` |
| `isInProduction`（オプション） | `Boolean` | `true` |
| `developmentLogLevel`（オプション） | `String` | `debug/error/info/none/trace/undefined/warn` |
| `productionLogLevel`（オプション） | `String` | `debug/error/info/none/trace/undefined/warn` |
| `isAnalyticsEnabled`（オプション） | `Boolean` | `true` |

Airship Developer Guide: Initial SDK Setup

- [iOS](https://docs.airship.com/platform/ios/getting-started/#takeoff)
- [Android](https://docs.airship.com/platform/android/getting-started/#takeoff)

#### trackEvent

カスタムイベントをAirshipに送信します。

| リモートコマンド | Airshipメソッド |
|---|---|
| `trackEvent`  | `UACustomEvent.track()` |

| パラメーター | タイプ | 例 |
| :-- | :-- | :-- |
| `event_name`（必須） | `String` | `Purchase` |
| `event`（オプション） | `JSONオブジェクト` | `{"my_numeric_property": 1}` |
| `event_value`（オプション） | `Number` | `1.5` |

Airship Developer Guide: Event Tracking

- [iOS](https://docs.airship.com/platform/ios/analytics-and-reporting/#ios-custom-events)
- [Android](https://docs.airship.com/platform/android/analytics-and-reporting/#android-custom-events)

#### trackScreenView

画面ビューをトラッキングします。

| リモートコマンド | Airshipメソッド |
| :-- | :-- |
| `trackScreenView` | `UAirship.analytics()?.trackScreen` |


| パラメーター | タイプ | 例 |
| :-- | :-- | :-- |
| `screen_name`（必須） | `String` | `Home Screen` |

Airship Developer Guide: Event Tracking

- [iOS](https://docs.airship.com/platform/ios/analytics-and-reporting/#ios-screen-tracking)
- [Android](https://docs.airship.com/platform/android/analytics-and-reporting/#android-screen-tracking)

#### enableAnalytics

以前に無効になっていた場合、Airship Analyticsを有効にします（デフォルトは有効）。

| リモートコマンド | Airshipメソッド |
| :-- | :-- |
| `enableAnalytics` | `UAirship.analytics()?.isEnabled` |

Airship Developer Guide: Enable Analytics

- [iOS](https://docs.airship.com/platform/ios/analytics-and-reporting/#disabling-analytics)
- [Android](https://docs.airship.com/platform/android/analytics-and-reporting/#disabling-analytics)

#### disableAnalytics

以前に有効になっていた場合、Airship Analyticsを無効にします（デフォルトは有効）。

| リモートコマンド | Airshipメソッド |
| :-- | :-- |
| `disableAnalytics` | `UAirship.analytics()?.isEnabled` |

Airship Developer Guide: Disable Analytics

- [iOS](https://docs.airship.com/platform/ios/analytics-and-reporting/#disabling-analytics)
- [Android](https://docs.airship.com/platform/android/analytics-and-reporting/#disabling-analytics)

#### setNamedUser

現在のアプリユーザーの既知のユーザー識別子を構成します。

| リモートコマンド | Airshipメソッド |
| :-- | :-- |
| `setNamedUser` | `UAirship.namedUser()?.identifier` |


| パラメーター | タイプ | 例 |
| :-- | :-- | :-- |
| `named_user_identifier`（必須） | `String` | `email@tealium.com` |

Airship Developer Guide: Event Tracking

- [iOS](https://docs.airship.com/platform/ios/segmentation/#named-users-ios)
- [Android](https://docs.airship.com/platform/android/segmentation/#named-users-android)

#### setCustomIdentifiers

ユーザーにとって重要と思われる追加のカスタム識別子を構成します。

| リモートコマンド | Airshipメソッド |
| :-- | :-- |
| `setCustomIdentifiers` | `UAirship.analytics()?.associateDeviceIdentifiers` |


| パラメーター | タイプ | 例 |
| :-- | :-- | :-- |
| `custom`（必須） | `JSONオブジェクト`（文字列のみ） | `{"my_custom_identifier":"user@email.com"}` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/analytics-and-reporting/#ios-custom-identifiers)
- [Android](https://docs.airship.com/platform/android/analytics-and-reporting/#android-custom-identifiers)

#### enableAdvertisingIdentifiers

広告識別子をカスタム識別子の辞書に追加します（IDFV、IDFA、Ad Tracking Enabled）。

| リモートコマンド | Airshipメソッド |
| :-- | :-- |
| `setCustomIdentifiers` | `UAirship.analytics()?.associateDeviceIdentifiers` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/analytics-and-reporting/#ios-custom-identifiers)
- [Android](https://docs.airship.com/platform/android/analytics-and-reporting/#android-custom-identifiers)

#### enableInAppMessaging

インアプメッセージング機能を有効にします。

| リモートコマンド | Airshipメソッド |
| :-- | :-- |
| `enableInAppMessaging` | `UAInAppMessageManager.shared()?.isEnabled` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/in-app-automation/#component-enablement)
- [Android](https://docs.airship.com/platform/android/in-app-automation/#feature-enablement)

#### disableInAppMessaging

インアプメッセージング機能を無効にします。

| リモートコマンド | Airshipメソッド |
| :-- | :-- |
| `disableInAppMessaging` | `UAInAppMessageManager.shared()?.isEnabled` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/in-app-automation/#component-enablement)
- [Android](https://docs.airship.com/platform/android/in-app-automation/#feature-enablement)

#### pauseInAppMessaging

インアプメッセージング機能を一時停止します。

| リモートコマンド | Airshipメソッド |
| :-- | :-- |
| `pauseInAppMessaging` | `UAInAppMessageManager.shared()?.isPaused` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/in-app-automation/#pausing-message-display)
- [Android](https://docs.airship.com/platform/android/in-app-automation/#pausing-message-display)

#### unPauseInAppMessaging

インアプメッセージング機能を再開します。

| リモートコマンド | Airshipメソッド |
| :-- | :-- |
| `unPauseInAppMessaging` | `UAInAppMessageManager.shared()?.isPaused` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/in-app-automation/#pausing-message-display)
- [Android](https://docs.airship.com/platform/android/in-app-automation/#pausing-message-display)

#### setInAppMessagingDisplayInterval

新しいインアプメッセージを表示するまでの待機時間（秒単位）。

| リモートコマンド | Airshipメソッド |
| :-- | :-- |
| `setInAppMessagingDisplayInterval` | `UAInAppMessageManager.shared()?.displayInterval` |

| パラメーター | タイプ | 例 |
| :-- | :-- | :-- |
| `in_app_messaging_display_interval`（必須） | `String` | `"10"` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/in-app-automation/#pausing-message-display)
- [Android](https://docs.airship.com/platform/android/in-app-automation/#pausing-message-display)

#### enableUserPushNotifications

ユーザープッシュ通知を有効にします。

| リモートコマンド | Airshipメソッド |
| :-- | :-- |
| `enableUserPushNotifications` | `UAirship.push()?.userPushNotificationsEnabled` |

| パラメーター | タイプ | 例 |
| :-- | :-- | :-- |
| `push_notification_options`（オプション） | `Stringの配列` | `["badge", "sound", "announcement"]` |
可能なプッシュメッセージオプション：`"badge"`、`"sound"`、`"alert"`、`"carplay"`、`"announcement"`、`"critical"`、`"app_notification_settings"`

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/push-notifications/#enabling-user-notifications)
- [Android](https://docs.airship.com/platform/android/push-notifications/#enabling-user-notifications)

#### disableUserPushNotifications

ユーザープッシュ通知を無効にします。

| リモートコマンド | Airshipメソッド |
| :-- | :-- |
| `enableUserPushNotifications` | `UAirship.push()?.userPushNotificationsEnabled` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/push-notifications/#enabling-user-notifications)
- [Android](https://docs.airship.com/platform/android/push-notifications/#enabling-user-notifications)

#### enableBackgroundPushNotifications

バックグラウンドプッシュ通知を有効にします。

| リモートコマンド | Airshipメソッド |
| :-- | :-- |
| `enableUserPushNotifications` | `UAirship.push()?. backgroundPushNotificationsEnabled` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/push-notifications/#enabling-user-notifications)
- [Android](https://docs.airship.com/platform/android/push-notifications/#enabling-user-notifications)

#### disableBackgroundPushNotifications

バックグラウンドプッシュ通知を無効にします。

| リモートコマンド | Airshipメソッド |
| :-- | :-- |
| `disableBackgroundPushNotifications` | `UAirship.push()?.backgroundPushNotificationsEnabled` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/push-notifications/#enabling-user-notifications)
- [Android](https://docs.airship.com/platform/android/push-notifications/#enabling-user-notifications)

#### setPushNotificationOptions

プッシュ通知オプションを構成します。iOSのみ。

| リモートコマンド | Airshipメソッド |
| :-- | :-- |
| `setPushNotificationOptions` | `UAirship.push()?.notificationOptions` |

| パラメーター | タイプ | 例 |
| :-- | :-- | :-- |
| `push_notification_options`（必須） | `Stringの配列` | `["badge", "sound", "announcement"]` |

可能なプッシュメッセージオプション：`"badge"`、`"sound"`、`"alert"`、`"carplay"`、`"announcement"`、`"critical"`、`"app_notification_settings"`

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/push-notifications/#notification-options)

#### setForegroundPresentationOptions

プッシュ通知の表示オプションを構成します。iOSのみ。

| リモートコマンド | Airshipメソッド |
| :-- | :-- |
| `setForegroundPresentationOptions` | `UAirship.push()?.defaultPresentationOptions` |

| パラメーター | タイプ | 例 |
| :-- | :-- | :-- |
| `foreground_presentation_options`（必須） | `Stringの配列` | `["badge", "sound", "alert"]` |

可能なフォアグラウンドプレゼンテーションオプション：`"badge"`、`"sound"`、`"alert"`

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/push-notifications/#foreground-presentation-options)

#### setBadgeNumber

アプリのアイコンのバッジ番号を指定の番号に構成します。iOSのみ。

| リモートコマンド | Airshipメソッド |
| :-- | :-- |
| `setBadgeNumber` | `UAirship.push()?.badgeNumber` |

| パラメーター | タイプ | 例 |
| :-- | :-- | :-- |
| `badge_number`（必須） | `Number` | `3` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/push-notifications/#ios-feature-badges)

#### resetBadgeNumber

バッジ番号をリセットします。iOSのみ。

| リモートコマンド | Airshipメソッド |
| :-- | :-- |
| `setBadgeNumber` | `UAirship.push()?.badgeNumber` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/push-notifications/#ios-feature-badges)

#### enableAutoBadge

自動バッジ機能を有効にします。iOSのみ。

| リモートコマンド | Airshipメソッド |
| :-- | :-- |
| `enableAutoBadge` | `UAirship.push()?.isAutobadgeEnabled` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/push-notifications/#ios-feature-badges)

#### disableAutoBadge

自動バッジ機能を無効にします。iOSのみ。

| リモートコマンド | Airshipメソッド |
| :-- | :-- |
| `disableAutoBadge` | `UAirship.push()?.isAutobadgeEnabled` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/push-notifications/#ios-feature-badges)

#### enableQuietTime

静音時間機能を有効にします。iOSのみ。

| リモートコマンド | Airshipメソッド |
| :-- | :-- |
| `enableAutoBadge` | `UAirship.push()?.isQuietTimeEnabled` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/push-notifications/#quiet-time)

#### disableQuietTime

静音時間機能を無効にします。iOSのみ。

| リモートコマンド | Airshipメソッド |
| :-- | :-- |
| `disableAutoBadge` | `UAirship.push()?.isQuietTimeEnabled` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/push-notifications/#quiet-time)

#### setQuietTimeStart

静音時間機能の時間制約を構成します。iOSのみ。

| リモートコマンド | Airshipメソッド |
| :-- | :-- |
| `setQuietTimeStart` | `UAirship.push()?.isQuietTimeEnabled` |

| パラメーター | タイプ | 例 |
| :-- | :-- | :-- |
| `quiet`（必須） | `JSONオブジェクト` | `{'start_hour': 3, 'start_minute': 30, 'end_hour': 4, 'end_minute': 30` |
quietオブジェクト内で必要なもの：

| パラメーター | タイプ | 例 |
| :-- | :-- | :-- |
| `start_hour`（必須） | `Number` | `3` |
| `start_minute`（必須） | `Number` | `30` |
| `end_hour`（必須） | `Number` | `4` |
| `end_minute`（必須） | `Number` | `30` |

Airship Developer Guide:

- [iOS](https://docs.airship.com/platform/ios/push-not