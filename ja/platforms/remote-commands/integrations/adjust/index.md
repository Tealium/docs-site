---
title: リモートコマンド：Adjust
description: AndroidおよびSwift/iOS向けのTealiumリモートコマンドによるAdjust連携。
url: https://docs.tealium.com/ja/platforms/remote-commands/integrations/adjust/
---
## 要件

* Adjustの[アプリトークン](https://help.adjust.com/en/article/app-settings#view-your-app-token)
* 以下のモバイルライブラリのいずれか：
  * [Tealium for Android-Kotlin](https://docs.tealium.com/ja/platforms/android-kotlin/)（1.0.0以降）
  * [Tealium for Android-Java](https://docs.tealium.com/ja/platforms/android-java/)（5.9.0以降）
  * [Tealium for iOS-Swift](https://docs.tealium.com/ja/platforms/ios-swift/)
* 以下のリモートコマンド連携のいずれか：
  * [AdjustリモートコマンドJSONファイル](https://docs.tealium.com/ja/platforms/remote-commands/integrations/adjust/#json-template)（Android-Kotlin 1.0.0以降またはiOS-Swift 2.1.0以降が必要）
  * [タグ管理のAdjustリモートコマンドタグ](https://docs.tealium.com/adjust-mobile-remote-command-tag/)

## 仕組み

Adjust連携では、次の3つの項目を使用します。

1. AdjustネイティブSDK
2. Adjustのメソッドをラップするリモートコマンドモジュール
3. イベントトラッキングをAdjustのネイティブ呼び出しに変換するJSON構成ファイルまたはリモートコマンドタグ

Adjustリモートコマンドモジュールをアプリに追加すると、アプリにベンダー固有のコードを追加することなく、必要なAdjustライブラリが自動的にインストールおよびビルドされます。依存関係マネージャーを使用してインストールする場合、Adjust SDKを個別にインストールする必要はありません。

リモートコマンドには、JSON構成ファイルを使用する方法と、タグ管理を使用してマッピングを構成する方法の2つがあります。ベンダー連携では、リモートまたはアプリ内のローカルにホストしたJSON構成ファイルを使用することを推奨します。タグ管理を使用する場合は、ベンダー連携用のリモートコマンドタグを追加します。詳しくは、[ベンダー連携](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/#vendor-integrations)を参照してください。


<blockquote>
iOS：Adjustバージョン4.23.0以降では、SDKによって次のネイティブフレームワークが自動的に追加されます：`AdSupport.framework`、`iAd.framework`、`AppTrackingTransparaceny.framework`。詳しくは、[Adjust iOS SKAdNetwork連携](https://help.adjust.com/en/article/app-tracking-transparency-att-framework)ガイドを参照してください。
</blockquote>


## インストール

### 依存関係マネージャー




1. Xcodeプロジェクトで、**File > Add Packages... > Add Package Dependency**を選択します。
2. リポジトリのURLとして`https://github.com/tealium/tealium-ios-adjust-remote-command`を入力します。
3. バージョンルールを構成します。通常は`Up to next major`を推奨します。現在の`TealiumAdjust`バージョンがリストに表示されない場合は、Swiftパッケージのキャッシュをリセットしてください。
4. インストールする`TealiumAdjust`モジュールを選択し、そのモジュールをインストールするアプリターゲットを選択します。
5. Tealium Swiftライブラリの追加モジュールを使用する場合は、[Swift Package Managerの手順](https://docs.tealium.com/ja/platforms/ios-swift/install/#swift-package-manager-recommended)に従って追加します。

プロジェクトに複数のアプリターゲットがあり、複数のターゲットで`TealiumAdjust`モジュールが必要な場合は、**Frameworks, Libraries, and Embedded Content**セクションで手動で追加する必要があります。

追加のアプリターゲットに`TealiumAdjust`をインストールするには、次の手順を実行します。

1. **Project Navigator**でXcodeプロジェクトを選択します。
2. Xcodeプロジェクトの**TARGETS**セクションでアプリターゲットを選択します。
3. **General > Frameworks, Libraries & Embedded Content**に移動し、`TealiumAdjust`モジュールを選択してアプリターゲットに追加します。




1. Podfileに`pod "tealium-swift"`および`pod "Adjust"`が存在する場合は削除します。`tealium-swift`への依存関係は、すでに`TealiumAdjust`フレームワークに含まれています。

2. 次の依存関係をPodfileに追加します。  
      ```ruby
      pod "TealiumAdjust"
      ```  
      `TealiumAdjust` Podには、次の`TealiumSwift`依存関係が含まれています。  
      ```bash
      "tealium-swift/Core"
      "tealium-swift/RemoteCommands"
      ```

3. `tealium-swift/Collect`または`tealium-swift/TagManagement`のいずれかのディスパッチャーPodをインストールに含め、その他の個別のサブモジュールもPodfileに追加します。例：   
      ```ruby
      pod "TealiumAdjust"
      pod "tealium-swift/Collect"
      pod "tealium-swift/Lifecycle"
      pod "tealium-swift/Attribution"
      ```

4. `TealiumHelper`ファイル、および`Tealium`クラスまたはAdjustリモートコマンドにアクセスするその他のファイルで、`TealiumSwift`モジュールと`TealiumAdjust`モジュールをインポートします。




1. Cartfileから`tealium-swift`を削除します。`tealium-swift`への依存関係は、すでに`TealiumAdjust`フレームワークに含まれています。

2. Cartfileに次の行が存在する場合は削除します。  
      ```bash
      github "adjust/ios_sdk"
      ```

3. 次の依存関係をCartfileに追加します。  
      ```bash
      github "tealium/tealium-ios-adjust-remote-command"
      ```






1. まだ実行していない場合は、[Tealium for Android（Kotlin）](https://docs.tealium.com/ja/platforms/android-kotlin/install/)または[Tealium for Android（Java）](https://docs.tealium.com/ja/platforms/android-java/install/)をインストールし、プロジェクトの最上位の`build.gradle`ファイルにTealium Maven URLを追加します。

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

2. アプリプロジェクトの`build.gradle`ファイルに次の依存関係を追加して、Adjust SDKとTealium-Adjustリモートコマンドの両方をインポートします。  
      ```groovy
      dependencies {
            implementation 'com.tealium.remotecommands:adjust:1.0.0'
      }
      ```



1. React Nativeプロジェクトのルートに移動します。

2. 次のコマンドを使用して`tealium-react-adjust`パッケージをダウンロードし、インストールします。  
    ```bash
    yarn add tealium-react-adjust
    ```
3. NPMパッケージのバージョン1.0.7ではReact Native Autolinkingが有効になっているため、React Native 0.60以降を使用している場合は`react-native link`を実行する必要はありません。




### 手動インストール




Adjustリモートコマンドを手動でインストールするには、[Tealium for Swift](https://docs.tealium.com/ja/platforms/ios-swift/)ライブラリがインストールされている必要があります。iOSプロジェクトにAdjustリモートコマンドをインストールするには、次の手順を実行します。

1. まだインストールしていない場合は、[Adjust SDK](https://github.com/adjust/ios_sdk)をインストールします。

2. [Tealium iOS Adjustリモートコマンド](https://github.com/tealium/tealium-ios-adjust-remote-command)リポジトリをクローンし、`Sources`フォルダー内のファイルをプロジェクトにドラッグします。

3. [`remoteAPIEnabled`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#remoteapienabled)構成フラグを`true`に構成します。





Adjustリモートコマンドを手動でインストールするには、[Tealium for Android（Kotlin）](https://docs.tealium.com/ja/platforms/android-kotlin/install/)または[Tealium for Android（Java）](https://docs.tealium.com/ja/platforms/android-java/install/)がインストールされている必要があります。AndroidプロジェクトにAdjustリモートコマンドをインストールするには、次の手順を実行します。

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

2. `tealium-adjust.aar`を`<PROJECT_ROOT>/<MODULE>/libs`に追加します。

3. Tealiumライブラリの依存関係を`build.gradle`ファイルに追加します。  
      ```groovy
      dependencies {
            implementation(name:'tealium-adjust', ext:'aar')
      }
      ```


## 初期化

すべての Tealium ライブラリで、初期化時に Adjust Remote Command を登録します。




Tealium の iOS（Swift）ライブラリ向けに、JSON 構成ファイルまたは Remote Command タグを使用して Remote Command を初期化します。
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
    let adjust = AdjustRemoteCommand()

    // Local JSON
    //let adjust = AdjustRemoteCommand(type: .local(file: "adjust")) 

    // Remote JSON
    //let adjust = AdjustRemoteCommand(type: .remote(url: "https://some.domain.com/adjust.json"))

    remoteCommands.add(adjust)
}
```



Tealium の Android（Kotlin）ライブラリ向けに、JSON 構成ファイルまたは Remote Command タグを使用して Remote Command を初期化します。
```kotlin
val config = TealiumConfig(application,
        "ACCOUNT",
        "PROFILE",
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands, Dispatchers.TagManagement));
val adjust = AdjustRemoteCommand(application);

var tealium = Tealium.create(TEALIUM_MAIN, config) {

    // Webview Tag
    remoteCommands?.add(adjust); 

    // Local JSON
    //remoteCommands?.add(adjust, filename = "adjust.json");

    // Remote JSON
    //remoteCommands?.add(adjust, remoteUrl = "https://some.domain.com/adjust.json"); 
}
```



Tealium の Android（Java）ライブラリ向けに、JSON 構成ファイルまたは Remote Command タグを使用して Remote Command を初期化します。
```java
Tealium.Config config = Tealium.Config.create(application, "ACCOUNT", "PROFILE", "ENVIRONMENT");
Tealium teal = Tealium.createInstance(TEALIUM_MAIN, config);

// New code to add the Adjust Remote Command
AdjustRemoteCommand adjustRemoteCommand = new AdjustRemoteCommand(application)
teal.addRemoteCommand(adjustRemoteCommand);
```




React Native 向けに、JSON 構成ファイルまたは Remote Command タグを使用して Remote Command を初期化します。
```javascript
import AdjustRemoteCommand from 'tealium-react-adjust';
AdjustRemoteCommand.initialize();

// Webview Tag
let adjust = { id: AdjustRemoteCommand.name } 

// Local JSON
//let adjust = { id: AdjustRemoteCommand.name, path: "adjust.json" }

// Remote JSON
//let adjust = { id: AdjustRemoteCommand.name, url: "https://some.domain.com/adjust.json" }

let config = TealiumConfig {
    // ...
    remoteCommands: [adjust]
}
```




## JSON テンプレート

[JSON 構成ファイル](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/#json-configuration-file)を使用して Remote Command を構成する場合は、以下のテンプレートを使用して構成を開始してください。このテンプレートには、標準的な e コマース実装で使用される一般的なマッピングが含まれています。必要に応じてマッピングを編集してください。

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

各 Adjust メソッドにコマンドをマッピングします。Adjust メソッドをトリガーするには、対応するコマンドを指定された形式で渡します。

| Remote Command | Adjust メソッド |
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
| `addSessionCallbackParams`（非推奨） | `addSessionCallbackParams()` |
| `removeSessionCallbackParams`（非推奨） | `removeSessionCallbackParams()` |
| `resetSessionCallbackParams`（非推奨） | `resetSessionCallbackParams()` |
| `addSessionPartnerParams`（非推奨） | `addSessionPartnerParams()` |
| `removeSessionPartnerParams`（非推奨） | `removeSessionPartnerParams()` |
| `resetSessionPartnerParams`（非推奨） | `resetSessionPartnerParams()` |
| `addGlobalCallbackParams` | `addGlobalCallbackParams()` |
| `removeGlobalCallbackParams` | `removeGlobalCallbackParams()` |
| `resetGlobalCallbackParams` | `resetGlobalCallbackParams()` |
| `addGlobalPartnerParams` | `addGlobalPartnerParams()` |
| `removeGlobalPartnerParams` | `removeGlobalPartnerParams()` |
| `resetGlobalPartnerParams` | `resetGlobalPartnerParams()` |


<blockquote>
`AppTrackingTransparency.framework` の一部として、iOS でのみサポートされています。詳しくは、[Adjust iOS SKAdNetwork インテグレーション](https://help.adjust.com/en/article/app-tracking-transparency-att-framework)ガイドを参照してください。
</blockquote>


### SDK のセットアップ

#### 初期化

Adjust SDK は起動時に自動的に初期化されます。Adjust API キーはタグ構成で指定します。

| Remote Command | Adjust メソッド |
|---|---|
| `initialize`  | `initialize()` |

Adjust 開発者ガイド：SDK の初期セットアップ

- [iOS](https://dev.adjust.com/en/sdk/ios/configuration)
- [Android](https://dev.adjust.com/en/sdk/android/configuration)

Adjust Remote Command タグでは、複数の構成オプションを利用できます。以下のいずれかを起動時に構成すると、`initialize()` メソッドの実行時に送信されます。
##### 構成オプション

| 名前 | iQ変数のマッピング | 型 |
|---|---|---|
| `environment`  | `sandbox` | `Bool` |
| `logLevel`| `logLevel`  | `String` |
| `delayStart`（非推奨） | `delay_start` | `Double` |
| `allowiAdInfoReading`* | `allow_iad` | `Bool` |
| `allowAdServicesInfoReading`* | `allow_ad_services` | `Bool` |
| `allowIdfaReading`* | `allow_idfa` | `Bool` |
| `appSecret`（非推奨） | `app_secret` | `String` |
| `appSecretInfo1`（非推奨） | `app_secret_info_1` | `String` |
| `appSecretInfo2`（非推奨） | `app_secret_info_2` | `String` |
| `appSecretInfo3`（非推奨） | `app_secret_info_3` | `String` |
| `appSecretInfo4`（非推奨） | `app_secret_info_4` | `String` |
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

`url_strategy`には、v4 URLストラテジーのいずれかを指定する必要があります。または、代わりにdomains/useSubdomains/isResidencyの3つのパラメータをすべて指定し、今後追加される別のストラテジーを作成できます。


<blockquote>
iOSおよびAndroidのみ
</blockquote>


#### イベントのトラッキング

| リモートコマンド | Adjustメソッド |
|---|---|
| `sendevent`  | `trackEvent()` |

| パラメータ | 型 |
|---|---|
| `event_token`（必須） | `String` |
| `order_id` | `String` |
| `deduplication_id` | `String` |
| `revenue` | `Double` |
| `currency` | `String` |
| `callback` | `Dictionary`または`Map` |
| `partner` | `Dictionary`または`Map` |
| `callback_id` | `String` |


Adjust開発者ガイド：イベントのトラッキング

- [iOS](https://dev.adjust.com/en/sdk/ios/features/events)
- [Android](https://dev.adjust.com/en/sdk/android/features/events)

#### サブスクリプションのトラッキング

| リモートコマンド | Adjustメソッド |
| :--- | :---|
| `tracksubscription`  | `trackAppStoreSubscription()` |

| パラメータ | 型 |
|---|---|
| `revenue`（必須） | `Double` |
| `currency`（必須） | `String ` |
| `order_id`（必須） | `String` |
| `deduplication_id` | `String` |
| `receipt`（非推奨） | `Data` |
| `sku`（Androidのみ必須） | `String` |
| `signature`（Androidのみ必須） | `String` |
| `purchase_token`（Androidのみ必須） | `String` |
| `purchase_time` | `Date` |
| `sales_region` | `String` |
| `callback` | `Dictionary`または`Map` |
| `partner` | `Dictionary`または`Map` |

Adjust APIリファレンス：サブスクリプションのトラッキング

- [iOS](https://dev.adjust.com/en/sdk/ios/features/subscriptions)
- [Android](https://dev.adjust.com/en/sdk/android/features/subscriptions)

#### トラッキング認証のリクエスト（iOS）

Adjust SDKは、ユーザーにトラッキング認証を自動的にリクエストします。完了ハンドラーを構成するには、`Adjust.trackingAuthorizationCompletion()`メソッドを使用してから、リモートコマンドを追加します。

例：

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

Adjust APIリファレンス：アプリトラッキング認証ラッパー

- [iOS](https://dev.adjust.com/en/sdk/ios/features/att)

#### コンバージョン値の更新（iOSのみ）

| リモートコマンド | Adjustメソッド |
|---|---|
| `updateconversionvalue`  | `updateConversionValue()` |

| パラメータ | 型 |
|---|---|
| `conversion_value`（必須） | `Int` |
| `coarse_value` | `low`、`medium`、`high` |
| `lock_window` | `Bool` |

Adjust APIリファレンス：SKAdNetworkコンバージョン値の更新

- [iOS](https://dev.adjust.com/en/sdk/ios/features/skad)


#### アプリの起動

| リモートコマンド | Adjustメソッド |
|---|---|
| `appwillopen`  | `appWillOpen()` |

| パラメータ | 型 |
|----|---|
| `deeplink_open_url`（必須） | `String` |


Adjust APIリファレンス：ディープリンク経由のリアトリビューション

- [iOS](https://dev.adjust.com/en/sdk/ios/features/deep-links/)
- [Android](https://dev.adjust.com/en/sdk/android/features/deep-links/)

#### 広告収益のトラッキング

| リモートコマンド | Adjustメソッド |
|---|---|
| `trackadrevenue`  | `trackAdRevenue()` |

| パラメータ | 型 |
|----|---|
| `ad_revenue_source`（必須） | `String` |
| `ad_revenue_payload` | `Dictionary`または`Map` |

ペイロードは、以下のパラメータで構成されます。

| パラメータ | 型 |
|----|---|
| `unit` | `String` |
| `network` | `String` |
| `amount` | `Double` |
| `currency` | `String` |
| `placement` | `String` |
| `impression_count` | `Int32` |
| `callback` | `Dictionary`または`Map` |
| `partner` | `Dictionary`または`Map` |

Adjust APIリファレンス：広告収益のトラッキング

- [iOS](https://dev.adjust.com/en/sdk/ios/features/ad-revenue)
- [Android](https://dev.adjust.com/en/sdk/android/features/ad-revenue)

#### プッシュトークンの構成

| リモートコマンド | Adjustメソッド |
|---|---|
| `setpushtoken`  | `setPushToken()` |

| パラメータ | 型 |
|----|---|
| `push_token`（必須） | `String` |

Adjust追加API：プッシュトークンの構成

- [iOS](https://dev.adjust.com/en/sdk/ios/configuration/#set-push-tokens)
- [Android](https://dev.adjust.com/en/sdk/android/configuration/#set-push-tokens)

#### オフラインモードの構成

| リモートコマンド | Adjustメソッド |
|---|---|
| `setofflinemode`  | `switchToOfflineMode()`/`switchBackToOnlineMode()` |


| パラメータ | 型 |
|----|---|
| `offline`（必須） | Bool |

Adjust追加API：オフラインモードの構成

- [iOS](https://dev.adjust.com/en/sdk/ios/configuration/#activate-offline-mode)
- [Android](https://dev.adjust.com/en/sdk/android/configuration/#activate-offline-mode)

### コールバックパラメータ

Adjust追加API：コールバックパラメータ

- [iOS](https://dev.adjust.com/en/sdk/ios/features/session-parameters)
- [Android](https://dev.adjust.com/en/sdk/android/features/session-parameter)

#### グローバルコールバックパラメータの追加

| リモートコマンド | Adjustメソッド |
|---|---|
| `addsessioncallbackparams`（非推奨） | `addGlobalCallbackParams()` |
| `addglobalcallbackparams` | `addGlobalCallbackParams()` |

| パラメータ | 型 |
|----|---|
| `session_callback`（非推奨） | `Dictionary`または`Map` |
| `global_callback`（必須） | `Dictionary`または`Map` |


#### グローバルパートナーパラメータの追加

| リモートコマンド | Adjustメソッド |
|---|---|
| `addsessionpartnerparams`（非推奨） | `addGlobalPartnerParams()` |
| `addglobalpartnerparams` | `addGlobalPartnerParams()` |

| パラメータ | 型 |
|----|---|
| `session_partner`（非推奨） | `Dictionary`または`Map` |
| `global_partner`（必須） | `Dictionary`または`Map` |


#### グローバルコールバックパラメータの削除

| リモートコマンド | Adjustメソッド |
|---|---|
| `removesessioncallbackparams`（非推奨） | `removeGlobalCallbackParams()` |
| `removeglobalcallbackparams` | `removeGlobalCallbackParams()` |

| パラメータ | 型 |
|----|---|
| `remove_session_callback_params`（非推奨） | `[String]` |
| `remove_global_callback_params`（必須） | `[String]` |


#### グローバルパートナーパラメータの削除

| リモートコマンド | Adjustメソッド |
|---|---|
| `removesessionpartnerparams`（非推奨） | `removeGlobalPartnerParams()` |
| `removeglobalpartnerparams` | `removeGlobalPartnerParams()` |

| パラメータ | 型 |
|----|---|
| `remove_session_partner_params`（非推奨） | `[String]` |
| `remove_global_partner_params`（必須） | `[String]` |
#### セッションコールバックパラメーターのリセット

| リモートコマンド | Adjustメソッド |
|---|---|
| `resetsessioncallbackparams`（非推奨） | `resetGlobalCallbackParams()` |
| `resetglobalcallbackparams` | `resetGlobalCallbackParams()` |


#### セッションパートナーパラメーターのリセット

| リモートコマンド | Adjustメソッド |
|---|---|
| `resetsessionpartnerparams`（非推奨） | `resetGlobalPartnerParams()` |
| `resetglobalpartnerparams` | `resetGlobalPartnerParams()` |

### 同意オプション

#### ユーザー情報の消去

| リモートコマンド | Adjustメソッド |
|---|---|
| `gdprforgetme` | `gdprForgetMe()` |

Adjust追加API：GDPRに基づく忘れられる権利

- [iOS](https://dev.adjust.com/en/sdk/ios/features/privacy/#send-erasure-request)
- [Android](https://dev.adjust.com/en/sdk/android/features/privacy/#send-erasure-request)

#### 有効化状態の構成

| リモートコマンド | Adjustプロパティ |
|---|---|
| `setenabled` | `enable()`/`disable()` |

| パラメーター | 型 |
|---|---|
| `enabled`（必須） | `Bool` |

Adjust APIリファレンス：トラッキングの無効化

- [iOS](https://dev.adjust.com/en/sdk/ios/configuration#disable-the-sdk)
- [Android](https://dev.adjust.com/en/sdk/android/configuration#disable-the-sdk)

#### 計測への同意の記録

| リモートコマンド | Adjustメソッド |
|---|---|
| `trackmeasurementconsent` | `trackMeasurementConsent()` |


| パラメーター | 型 |
|----|---|
| `measurement_consent`（必須） | Bool |

Adjust追加API：計測への同意

- [iOS](https://dev.adjust.com/en/sdk/ios/features/privacy#consent-measurement-for-specific-users)
- [Android](https://dev.adjust.com/en/sdk/android/features/privacy#consent-measurement-for-specific-users)

#### サードパーティ共有の記録

| リモートコマンド | Adjustメソッド |
|---|---|
| `trackthirdpartysharing` | `trackThirdPartySharing()` |

| パラメーター | 型 |
|----|---|
| `enabled`（必須） | Bool |

Adjust追加API：サードパーティ共有の有効化

- [iOS](https://dev.adjust.com/en/sdk/ios/features/privacy#third-party-sharing-for-specific-users)
- [Android](https://dev.adjust.com/en/sdk/android/features/privacy#third-party-sharing-for-specific-users)