---
title: リモートコマンド：調整
description: AndroidおよびSwift/iOSでのAdjustのTealiumリモートコマンド統合。
url: https://docs.tealium.com/ja/platforms/remote-commands/integrations/adjust/
---
## 要件

* Adjust [アプリトークン](https://help.adjust.com/en/article/app-settings#view-your-app-token)
* 以下のいずれかのモバイルライブラリ：
  * [Tealium for Android-Kotlin](https://docs.tealium.com/ja/platforms/android-kotlin/) (1.0.0+)
  * [Tealium for Android-Java](https://docs.tealium.com/ja/platforms/android-java/) (5.9.0+)
  * [Tealium for iOS-Swift](https://docs.tealium.com/ja/platforms/ios-swift/)
* 以下のいずれかのリモートコマンド統合：
  * [Adjust Remote Command JSONファイル](https://docs.tealium.com/ja/platforms/remote-commands/integrations/adjust/#json-template) (Android-Kotlin 1.0.0+またはiOS-Swift 2.1.0+が必要)
  * [Tealium iQタグ管理内のAdjust Remote Commandタグ](https://docs.tealium.com/adjust-mobile-remote-command-tag/)

## 動作原理

Adjust統合は3つのアイテムを使用します：

1. AdjustネイティブSDK
2. Adjustメソッドをラップするリモートコマンドモジュール
3. イベントトラッキングをネイティブのAdjustコールに変換するJSON構成ファイルまたはリモートコマンドタグ

アプリにAdjustリモートコマンドモジュールを追加すると、アプリにベンダー固有のコードを追加することなく、必要なAdjustライブラリが自動的にインストールされてビルドされます。依存関係マネージャーのインストールを使用している場合、Adjust SDKを別途インストールする必要はありません。

リモートコマンドオプションには2つのタイプがあります：JSON構成ファイル、またはiQタグ管理を使用してマッピングを構成します。JSON構成ファイルは、ベンダー統合に推奨されるオプションで、アプリ内またはリモートでホストされます。iQタグ管理を使用する場合は、ベンダー統合のリモートコマンドタグを追加します。[ベンダー統合についての詳細はこちら](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/#vendor-integrations)。


<blockquote>
iOS：Adjustバージョン4.23.0以降、SDKは自動的に以下のネイティブフレームワークを追加します：`AdSupport.framework`、`iAd.framework`、`AppTrackingTransparaceny.framework`。[Adjust iOS SKAdNetwork統合ガイド](https://help.adjust.com/en/article/app-tracking-transparency-att-framework)で詳細を確認してください。
</blockquote>


## インストール

### 依存関係マネージャ




1. Xcodeプロジェクトで、**File > Add Packages... > Add Package Dependency**を選択します。
2. リポジトリURLを入力します：`https://github.com/tealium/tealium-ios-adjust-remote-command`
3. バージョンルールを構成します。通常は`Up to next major`が推奨されます。現在の`TealiumAdjust`バージョンがリストに表示されない場合は、Swiftパッケージキャッシュをリセットしてください。
4. インストールする`TealiumAdjust`モジュールを選択し、モジュールをインストールするアプリターゲットを選択します。
5. Tealium Swiftライブラリから追加のモジュールを使用している場合は、[Swift Package Managerの指示](https://docs.tealium.com/ja/platforms/ios-swift/install/#swift-package-manager-recommended)に従って追加してください。

プロジェクトに複数のアプリターゲットがあり、`TealiumAdjust`モジュールを複数のアプリターゲットに追加する必要がある場合は、**Frameworks, Libraries, and Embedded Content**セクションで手動で追加する必要があります。

追加のアプリターゲットに`TealiumAdjust`をインストールするには：

1. **Project Navigator**でXcodeプロジェクトを選択します。
2. Xcodeプロジェクトで、**TARGETS**セクションのアプリターゲットを選択します。
3. **General > Frameworks, Libraries & Embedded Content**に移動し、`TealiumAdjust`モジュールをアプリターゲットに追加します。




1. Podfileから`pod "tealium-swift"`と`pod "Adjust"`を削除します。`tealium-swift`の依存関係はすでに`TealiumAdjust`フレームワークに含まれています。

2. Podfileに次の依存関係を追加します：
      ```ruby
      pod "TealiumAdjust"
      ```  
      `TealiumAdjust`ポッドには次の`TealiumSwift`依存関係が含まれています：
      ```bash
      "tealium-swift/Core"
      "tealium-swift/RemoteCommands"
      ```

3. インストールにディスパッチャーポッドを含めます。`tealium-swift/Collect`または`tealium-swift/TagManagement`のいずれかを選択し、Podfileに他の個々のサブモジュールを含めます。例：
      ```ruby
      pod "TealiumAdjust"
      pod "tealium-swift/Collect"
      pod "tealium-swift/Lifecycle"
      pod "tealium-swift/Attribution"
      ```

4. `TealiumHelper`ファイルおよび`Tealium`クラスまたはAdjustリモートコマンドにアクセスする他のファイルで`TealiumSwift`と`TealiumAdjust`モジュールをインポートします。




1. Cartfileから`tealium-swift`を削除します。`tealium-swift`の依存関係はすでに`TealiumAdjust`フレームワークに含まれています。

2. Cartfileに存在する場合は次の行を削除します：
      ```bash
      github "adjust/ios_sdk"
      ```

3. Cartfileに次の依存関係を追加します：
      ```bash
      github "tealium/tealium-ios-adjust-remote-command"
      ```






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

2. アプリプロジェクトの`build.gradle`ファイルにAdjust SDKとTealium-Adjustリモートコマンドの依存関係を追加します：
      ```groovy
      dependencies {
            implementation 'com.tealium.remotecommands:adjust:1.0.0'
      }
      ```



1. React Nativeプロジェクトのルートに移動します。

2. 次のコマンドで`tealium-react-adjust`パッケージをダウンロードしてインストールします：
    ```bash
    yarn add tealium-react-adjust
    ```
3. React Native AutolinkingはNPMパッケージのバージョン1.0.7で有効になっており、React Nativeのバージョン0.60+を使用している場合、`react-native link`を実行する必要はありません。




### 手動インストール




Adjustリモートコマンドの手動インストールには、[Tealium for Swift](https://docs.tealium.com/ja/platforms/ios-swift/)ライブラリがインストールされている必要があります。iOSプロジェクトのAdjustリモートコマンドをインストールするには：

1. まだ行っていない場合は、[Adjust SDK](https://github.com/adjust/ios_sdk)をインストールします。

2. [Tealium iOS Adjustリモートコマンド](https://github.com/tealium/tealium-ios-adjust-remote-command)リポジトリをクローンし、`Sources`フォルダ内のファイルをプロジェクトにドラッグします。

3. [`remoteAPIEnabled`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#remoteapienabled)構成フラグを`true`に構成します。





Adjustリモートコマンドの手動インストールには、[Tealium for Android (Kotlin)](https://docs.tealium.com/ja/platforms/android-kotlin/install/)または[Tealium for Android (Java)](https://docs.tealium.com/ja/platforms/android-java/install/)がインストールされている必要があります。AndroidプロジェクトのAdjustリモートコマンドをインストールするには：

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

2. `<PROJECT_ROOT>/<MODULE>/libs`に`tealium-adjust.aar`を追加します。

3. `build.gradle`ファイルにTealiumライブラリの依存関係を追加します：
      ```groovy
      dependencies {
            implementation(name:'tealium-adjust', ext:'aar')
      }
      ```


## 初期化

Tealiumのすべてのライブラリで、初期化時にAdjust Remote Commandを登録します。




TealiumのiOS（Swift）ライブラリ用にJSON構成ファイルまたはRemote Commandタグでリモートコマンドを初期化します：
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
    let adjust = AdjustRemoteCommand()

    // ローカルJSON
    //let adjust = AdjustRemoteCommand(type: .local(file: "adjust")) 

    // リモートJSON
    //let adjust = AdjustRemoteCommand(type: .remote(url: "https://some.domain.com/adjust.json"))

    remoteCommands.add(adjust)
}
```



TealiumのAndroid（Kotlin）ライブラリ用にJSON構成ファイルまたはRemote Commandタグでリモートコマンドを初期化します：
```kotlin
val config = TealiumConfig(application,
        "ACCOUNT",
        "PROFILE",
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands, Dispatchers.TagManagement));
val adjust = AdjustRemoteCommand(application);

var tealium = Tealium.create(TEALIUM_MAIN, config) {

    // Webviewタグ
    remoteCommands?.add(adjust); 

    // ローカルJSON
    //remoteCommands?.add(adjust, filename = "adjust.json");

    // リモートJSON
    //remoteCommands?.add(adjust, remoteUrl = "https://some.domain.com/adjust.json"); 
}
```



TealiumのAndroid（Java）ライブラリ用にJSON構成ファイルまたはRemote Commandタグでリモートコマンドを初期化します：
```java
Tealium.Config config = Tealium.Config.create(application, "ACCOUNT", "PROFILE", "ENVIRONMENT");
Tealium teal = Tealium.createInstance(TEALIUM_MAIN, config);

// Adjust Remote Commandを追加する新しいコード
AdjustRemoteCommand adjustRemoteCommand = new AdjustRemoteCommand(application)
teal.addRemoteCommand(adjustRemoteCommand);
```




React Native用にJSON構成ファイルまたはRemote Commandタグでリモートコマンドを初期化します：
```javascript
import AdjustRemoteCommand from 'tealium-react-adjust';
AdjustRemoteCommand.initialize();

// Webviewタグ
let adjust = { id: AdjustRemoteCommand.name } 

// ローカルJSON
//let adjust = { id: AdjustRemoteCommand.name, path: "adjust.json" }

// リモートJSON
//let adjust = { id: AdjustRemoteCommand.name, url: "https://some.domain.com/adjust.json" }

let config = TealiumConfig {
    // ...
    remoteCommands: [adjust]
}
```




## JSONテンプレート

リモートコマンドを[JSON構成ファイル](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/#json-configuration-file)を使用して構成する場合は、以下のテンプレートを参照してください。このテンプレートには、標準的なeコマースインストールで使用される一般的なマッピングが含まれています。必要に応じてマッピングを編集してください。

```json
{
  "config": {
    "api_token": "YOUR_API_TOKEN",
    "sandbox": true,
    "settings": {
      "log_level": "verbose",
      "allow_iad": true,
      "allow_ad_services": true,
      "allow_idfa": true,
      "event_buffering_enabled": false,
      "send_in_background": true
    }
  },
  "mappings": {
    "event_token": "event_token",
    "order_total": "revenue,callback.orderTotal",
    "order_currency": "currency",
    "order_id": "order_id,callback.orderId",
    "conversion_value": "conversion_value",
    "sales_region": "sales_region",
    "callback_id": "callback_id",
    "ad_revenue_source": "ad_revenue_source",
    "campaign": "ad_revenue_payload.campaignId",
    "ad_uuid": "ad_revenue_payload.adId",
    "appstore_receipt_data": "receipt",
    "purchase_timestamp": "purchase_time",
    "product_sku": "sku",
    "purchase_signature": "signature",
    "purchase_token": "purchase_token",
    "deeplink_url": "deeplink_open_url",
    "push_token": "push_token",
    "favorite_color": "callback.color,session_callback.color",
    "num_of_pets": "partner.pets,session_partner.pets",
    "customer_id": "callback.customerId",
    "customer_is_member": "partner.isMember",
    "global_params": "global_callback,global_partner",
    "remove_global_params": "remove_global_callback_params,remove_global_partner_params",
    "reset_global_params": "reset_global_callback_params,reset_global_partner_params",
    "consent_granted": "measurement_consent",
    "enabled": "enabled"
  },
  "commands": {
    "launch": "initialize",
    "track_deeplink": "appwillopenurl",
    "purchase": "trackevent,updateconversionvalue",
    "event": "trackevent",
    "contact": "trackevent,addglobalcallbackparams,addglobalpartnerparams",
    "ad_revenue": "trackadrevenue",
    "subscribe": "trackevent,tracksubscription",
    "received_push_token": "setpushtoken",
    "add_global_parameters": "addglobalcallbackparams,addglobalpartnerparams",
    "remove_global_parameters": "removeglobalcallbackparams,removeglobalpartnerparams",
    "reset_global_parameters": "resetglobalcallbackparams,resetglobalpartnerparams",
    "consent_revoked": "gdprforgetme,trackmeasurementconsent",
    "consent_granted": "trackmeasurementconsent",
    "set_enabled": "setenabled",
    "offline": "setofflinemode"
  }
}

```

## サポートされているメソッド

各Adjustメソッドに対応するコマンドをマッピングします。Adjustメソッドをトリガーするには、指定された形式で対応するコマンドを渡します。

| リモートコマンド | Adjustメソッド |
| :-- | :-- |
| `initialize` | `initialize()` |
| `sendEvent` | `trackEvent()` |
| `trackSubscription` | `trackSubscription()` |
| `requestTrackingAuthorization`* | `requestTrackingAuthorization()` |
| `updateConversionValue`* | `updateConversionValue()`|
| `appWillOpen` | `appWillOpen()` |
| `trackAdRevenue` | `trackAdRevenue()` |
| `setPushToken` | `setPushToken()` |
| `setEnabled` | `enable()`/`disable()` |
| `setOfflineMode` | `switchToOfflineMode()`/`switchBackToOnlineMode()` |
| `gdprForgetMe` | `gdprForgetMe()` |
| `trackThirdPartySharing` | `trackThirdPartySharing()` |
| `trackMeasurementConsent` | `trackMeasurementConsent()` |
| `addSessionCallbackParams` (非推奨) | `addSessionCallbackParams()` |
| `removeSessionCallbackParams` (非推奨) | `removeSessionCallbackParams()` |
| `resetSessionCallbackParams` (非推奨) | `resetSessionCallbackParams()` |
| `addSessionPartnerParams` (非推奨) | `addSessionPartnerParams()` |
| `removeSessionPartnerParams` (非推奨) | `removeSessionPartnerParams()` |
| `resetSessionPartnerParams` (非推奨) | `resetSessionPartnerParams()` |
| `addGlobalCallbackParams` | `addGlobalCallbackParams()` |
| `removeGlobalCallbackParams` | `removeGlobalCallbackParams()` |
| `resetGlobalCallbackParams` | `resetGlobalCallbackParams()` |
| `addGlobalPartnerParams` | `addGlobalPartnerParams()` |
| `removeGlobalPartnerParams` | `removeGlobalPartnerParams()` |
| `resetGlobalPartnerParams` | `resetGlobalPartnerParams()` |


<blockquote>
iOSの`AppTrackingTransparency.framework`の一部としてのみサポートされています。[Adjust iOS SKAdNetwork統合](https://help.adjust.com/en/article/app-tracking-transparency-att-framework)ガイドで詳細を学びましょう。
</blockquote>


### SDKセットアップ

#### 初期化

Adjust SDKは起動時に自動的に初期化されます。Adjust APIキーはタグ構成で構成されます。

| リモートコマンド | Adjustメソッド |
|---|---|
| `initialize`  | `initialize()` |

Adjust開発者ガイド：初期SDKセットアップ

- [iOS](https://dev.adjust.com/en/sdk/ios/configuration)
- [Android](https://dev.adjust.com/en/sdk/android/configuration)

Adjust Remote Commandタグにはいくつかの構成オプションがあります。これらのいずれかが起動時に構成されている場合、`initialize()`メソッド中に送信されます。
##### 構成オプション

| 名前 | iQ変数マッピング | タイプ |
|---|---|---|
| `environment`  | `sandbox` | `Bool` |
| `logLevel`| `logLevel`  | `String` |
| `delayStart` (非推奨) | `delay_start` | `Double` |
| `allowiAdInfoReading`* | `allow_iad` | `Bool` |
| `allowAdServicesInfoReading`* | `allow_ad_services` | `Bool` |
| `allowIdfaReading`* | `allow_idfa` | `Bool` |
| `appSecret` (非推奨) | `app_secret` | `String` |
| `appSecretInfo1` (非推奨) | `app_secret_info_1` | `String` |
| `appSecretInfo2` (非推奨) | `app_secret_info_2` | `String` |
| `appSecretInfo3` (非推奨) | `app_secret_info_3` | `String` |
| `appSecretInfo4` (非推奨) | `app_secret_info_4` | `String` |
| `defaultTracker`| `default_tracker` | `String` |
| `externalDeviceId`| `external_device_id` | `String` |
| `eventBufferingEnabled`| `event_buffering_enabled` | `String` |
| `sendInBackground`| `send_in_background` | `String` |
| `setPreinstallTrackingEnabled`** | `preinstall_tracking` | `String` |
| `eventDeduplicationIdsMaxSize`| `deduplication_id_max_size` | `Int` |
| `urlStrategy`| `url_strategy` | `String` |
| `domains`| `url_strategy_domains` | `[String]` |
| `useSubdomains`| `url_strategy_use_subdomains` | `Bool` |
| `isResidency`| `url_strategy_is_residency` | `Bool` |

`url_strategy`はv4 URL戦略のいずれかでなければならず、または、domains/useSubdomains/isResidencyの3つのパラメータを提供して将来追加される別の戦略を作成することができます。


<blockquote>
iOSとAndroidのみ
</blockquote>


#### イベントトラッキング

| リモートコマンド | Adjustメソッド |
|---|---|
| `sendevent`  | `trackEvent()` |

|  パラメータ | タイプ |
|---|---|
|  `event_token` (必須) | `String` |
|  `order_id` | `String` |
|  `deduplication_id` | `String` |
|  `revenue` | `Double` |
|  `currency` | `String` |
|  `callback` | `Dictionary` または `Map` |
|  `partner` | `Dictionary` または `Map` |
|  `callback_id` | `String` |

Adjust 開発者ガイド: イベントトラッキング

- [iOS](https://dev.adjust.com/en/sdk/ios/features/events)
- [Android](https://dev.adjust.com/en/sdk/android/features/events)

#### サブスクリプショントラッキング

| リモートコマンド | Adjustメソッド |
| :--- | :---|
| `tracksubscription`  | `trackAppStoreSubscription()` |

|  パラメータ | タイプ |
|---|---|
|  `revenue` (必須) | `Double` |
|  `currency` (必須) | `String ` |
|  `order_id` (必須) | `String` |
|  `deduplication_id` | `String` |
|  `receipt` (非推奨) | `Data` |
|  `sku` (Androidのみ必須) | `String` |
|  `signature` (Androidのみ必須) | `String` |
|  `purchase_token` (Androidのみ必須) | `String` |
|  `purchase_time` | `Date` |
|  `sales_region` | `String` |
|  `callback` | `Dictionary` または `Map` |
|  `partner` | `Dictionary` または `Map` |

Adjust APIリファレンス: サブスクリプショントラッキング

- [iOS](https://dev.adjust.com/en/sdk/ios/features/subscriptions)
- [Android](https://dev.adjust.com/en/sdk/android/features/subscriptions)

#### トラッキング認証のリクエスト (iOS)

Adjust SDKは自動的にユーザーからのトラッキング認証をリクエストします。完了を構成するには、`Adjust.trackingAuthorizationCompletion()`メソッドを使用し、リモートコマンドを追加します。

例:

```swift
tealium = Tealium(config: config) { _ in
    guard let remoteCommands = self.tealium?.remoteCommands else {
        return
    }

	let adjustRemoteCommand = AdjustRemoteCommand()
	adjustRemoteCommand.trackingAuthorizationCompletion = { status in
            switch status {
            case 0: print("ATTrackingManagerAuthorizationStatusNotDetermined")
            case 1: print("ATTrackingManagerAuthorizationStatusRestricted")
            case 2: print("ATTrackingManagerAuthorizationStatusDenied")
            case 3: print("ATTrackingManagerAuthorizationStatusAuthorized")
            default:
                break;
            }
        }
	remoteCommands.add(adjustRemoteCommand)
}
```

Adjust APIリファレンス: アプリトラッキング認証ラッパー

- [iOS](https://dev.adjust.com/en/sdk/ios/features/att)

#### コンバージョン値の更新 (iOSのみ)

| リモートコマンド | Adjustメソッド |
|---|---|
| `updateconversionvalue`  | `updateConversionValue()` |

|  パラメータ | タイプ |
|---|---|
|  `conversion_value` (必須) | `Int` |
|  `coarse_value` | `low`, `medium`, `high` |
|  `lock_window` | `Bool` |

Adjust APIリファレンス: SKAdNetworkコンバージョン値の更新

- [iOS](https://dev.adjust.com/en/sdk/ios/features/skad)


#### アプリが開かれる

|  リモートコマンド | Adjustメソッド |
|---|---|
| `appwillopen`  | `appWillOpen()` |

|  パラメータ | タイプ |
|----|---|
| `deeplink_open_url` (必須) | `String` |


Adjust APIリファレンス: ディープリンク経由の再帰属

- [iOS](https://dev.adjust.com/en/sdk/ios/features/deep-links/)
- [Android](https://dev.adjust.com/en/sdk/android/features/deep-links/)

#### 広告収益のトラッキング

|  リモートコマンド | Adjustメソッド |
|---|---|
| `trackadrevenue`  | `trackAdRevenue()` |

|  パラメータ | タイプ |
|----|---|
| `ad_revenue_source` (必須) | `String` |
| `ad_revenue_payload` | `Dictionary` または `Map` |

ペイロードは以下のパラメータで構成されます:

|  パラメータ | タイプ |
|----|---|
|  `unit` | `String` |
|  `network` | `String` |
|  `amount` | `Double` |
|  `currency` | `String` |
|  `placement` | `String` |
|  `impression_count` | `Int32` |
|  `callback` | `Dictionary` または `Map` |
|  `partner` | `Dictionary` または `Map` |

Adjust APIリファレンス: 広告収益のトラッキング

- [iOS](https://dev.adjust.com/en/sdk/ios/features/ad-revenue)
- [Android](https://dev.adjust.com/en/sdk/android/features/ad-revenue)

#### プッシュトークンの構成

|  リモートコマンド | Adjustメソッド |
|---|---|
| `setpushtoken`  | `setPushToken()` |

|  パラメータ | タイプ |
|----|---|
| `push_token` (必須) | `String` |

Adjust追加API: プッシュトークンの構成

- [iOS](https://dev.adjust.com/en/sdk/ios/configuration/#set-push-tokens)
- [Android](https://dev.adjust.com/en/sdk/android/configuration/#set-push-tokens)

#### オフラインモードの構成

|  リモートコマンド | Adjustメソッド |
|---|---|
| `setofflinemode`  | `switchToOfflineMode()`/`switchBackToOnlineMode()` |


|  パラメータ | タイプ |
|----|---|
| `offline` (必須) | Bool |

Adjust追加API: オフラインモードの構成

- [iOS](https://dev.adjust.com/en/sdk/ios/configuration/#activate-offline-mode)
- [Android](https://dev.adjust.com/en/sdk/android/configuration/#activate-offline-mode)

### コールバックパラメータ

Adjust追加API: コールバックパラメータ

- [iOS](https://dev.adjust.com/en/sdk/ios/features/session-parameters)
- [Android](https://dev.adjust.com/en/sdk/android/features/session-parameter)

#### グローバルコールバックパラメータの追加

|  リモートコマンド | Adjustメソッド |
|---|---|
| `addsessioncallbackparams` (非推奨) | `addGlobalCallbackParams()` |
| `addglobalcallbackparams` | `addGlobalCallbackParams()` |

|  パラメータ | タイプ |
|----|---|
| `session_callback` (非推奨) | `Dictionary` または `Map` |
| `global_callback` (必須) | `Dictionary` または `Map` |


#### グローバルパートナーパラメータの追加

|  リモートコマンド | Adjustメソッド |
|---|---|
| `addsessionpartnerparams` (非推奨) | `addGlobalPartnerParams()` |
| `addglobalpartnerparams` | `addGlobalPartnerParams()` |

|  パラメータ | タイプ |
|----|---|
| `session_partner` (非推奨) | `Dictionary` または `Map` |
| `global_partner` (必須) | `Dictionary` または `Map` |


#### グローバルコールバックパラメータの削除

|  リモートコマンド | Adjustメソッド |
|---|---|
| `removesessioncallbackparams` (非推奨) | `removeGlobalCallbackParams()` |
| `removeglobalcallbackparams` | `removeGlobalCallbackParams()` |

|  パラメータ | タイプ |
|----|---|
| `remove_session_callback_params` (非推奨) | `[String]` |
| `remove_global_callback_params` (必須) | `[String]` |


#### グローバルパートナーパラメータの削除

|  リモートコマンド | Adjustメソッド |
|---|---|
| `removesessionpartnerparams` (非推奨) | `removeGlobalPartnerParams()` |
| `removeglobalpartnerparams` | `removeGlobalPartnerParams()` |

|  パラメータ | タイプ |
|----|---|
| `remove_session_partner_params` (非推奨) | `[String]` |
| `remove_global_partner_params` (必須) | `[String]` |



#### セッションコールバックパラメータのリセット

|  リモートコマンド | 調整メソッド |
|---|---|
| `resetsessioncallbackparams` (非推奨) | `resetGlobalCallbackParams()` |
| `resetglobalcallbackparams` | `resetGlobalCallbackParams()` |

#### セッションパートナーパラメータのリセット

|  リモートコマンド | 調整メソッド |
|---|---|
| `resetsessionpartnerparams` (非推奨) | `resetGlobalPartnerParams()` |
| `resetglobalpartnerparams` | `resetGlobalPartnerParams()` |

### 同意オプション

#### 私を忘れてください

|  リモートコマンド | 調整メソッド |
|---|---|
| `gdprforgetme`  | `gdprForgetMe()` |

Adjust 追加API: GDPR 忘れられる権利

- [iOS](https://dev.adjust.com/en/sdk/ios/features/privacy/#send-erasure-request)
- [Android](https://dev.adjust.com/en/sdk/android/features/privacy/#send-erasure-request)

#### 有効化構成

| リモートコマンド | 調整プロパティ |
|---|---|
| `setenabled`  | `enable()`/`disable()` |

|  パラメータ | タイプ |
|---|---|
|  `enabled` (必須) | `Bool` |

Adjust API リファレンス: トラッキング無効化

- [iOS](https://dev.adjust.com/en/sdk/ios/configuration#disable-the-sdk)
- [Android](https://dev.adjust.com/en/sdk/android/configuration#disable-the-sdk)

#### 測定同意の追跡

|  リモートコマンド | 調整メソッド |
|---|---|
| `trackmeasurementconsent`  | `trackMeasurementConsent()` |

|  パラメータ | タイプ |
|----|---|
| `measurement_consent` (必須) | Bool |

Adjust 追加API: 特定ユーザーの測定同意

- [iOS](https://dev.adjust.com/en/sdk/ios/features/privacy#consent-measurement-for-specific-users)
- [Android](https://dev.adjust.com/en/sdk/android/features/privacy#consent-measurement-for-specific-users)

#### 第三者共有の追跡

|  リモートコマンド | 調整メソッド |
|---|---|
| `trackthirdpartysharing`  | `trackThirdPartySharing()` |

|  パラメータ | タイプ |
|----|---|
| `enabled` (必須) | Bool |

Adjust 追加API: 第三者共有の有効化

- [iOS](https://dev.adjust.com/en/sdk/ios/features/privacy#third-party-sharing-for-specific-users)
- [Android](https://dev.adjust.com/en/sdk/android/features/privacy#third-party-sharing-for-specific-users)
