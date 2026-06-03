---
title: リモートコマンド：調整
description: AndroidおよびSwift/iOSでのAdjustのTealiumリモートコマンド統合。
url: https://docs.tealium.com/ja/platforms/remote-commands/integrations/adjust/
---
## 要件

* Adjust [アプリトークン](https://help.adjust.com/en/article/app-settings#view-your-app-token)
* 以下のいずれかのモバイルライブラリ：
  * [Tealium for Android-Kotlin](/ja/platforms/android-kotlin/) (1.0.0&#43;)
  * [Tealium for Android-Java](/ja/platforms/android-java/) (5.9.0&#43;)
  * [Tealium for iOS-Swift](/ja/platforms/ios-swift/)
* 以下のいずれかのリモートコマンド統合：
  * [Adjust Remote Command JSONファイル](/ja/platforms/remote-commands/integrations/adjust/#json-template) (Android-Kotlin 1.0.0&#43;またはiOS-Swift 2.1.0&#43;が必要)
  * [Tealium iQタグ管理内のAdjust Remote Commandタグ]()

## 動作原理

Adjust統合は3つのアイテムを使用します：

1. AdjustネイティブSDK
2. Adjustメソッドをラップするリモートコマンドモジュール
3. イベントトラッキングをネイティブのAdjustコールに変換するJSON構成ファイルまたはリモートコマンドタグ

アプリにAdjustリモートコマンドモジュールを追加すると、アプリにベンダー固有のコードを追加することなく、必要なAdjustライブラリが自動的にインストールされてビルドされます。依存関係マネージャーのインストールを使用している場合、Adjust SDKを別途インストールする必要はありません。

リモートコマンドオプションには2つのタイプがあります：JSON構成ファイル、またはiQタグ管理を使用してマッピングを構成します。JSON構成ファイルは、ベンダー統合に推奨されるオプションで、アプリ内またはリモートでホストされます。iQタグ管理を使用する場合は、ベンダー統合のリモートコマンドタグを追加します。[ベンダー統合についての詳細はこちら](/ja/platforms/remote-commands/how-it-works/#vendor-integrations)。

iOS：Adjustバージョン4.23.0以降、SDKは自動的に以下のネイティブフレームワークを追加します：`AdSupport.framework`、`iAd.framework`、`AppTrackingTransparaceny.framework`。[Adjust iOS SKAdNetwork統合ガイド](https://help.adjust.com/en/article/app-tracking-transparency-att-framework)で詳細を確認してください。

## インストール

### 依存関係マネージャ




1. Xcodeプロジェクトで、**File &gt; Add Packages... &gt; Add Package Dependency**を選択します。
2. リポジトリURLを入力します：`https://github.com/tealium/tealium-ios-adjust-remote-command`
3. バージョンルールを構成します。通常は`Up to next major`が推奨されます。現在の`TealiumAdjust`バージョンがリストに表示されない場合は、Swiftパッケージキャッシュをリセットしてください。
4. インストールする`TealiumAdjust`モジュールを選択し、モジュールをインストールするアプリターゲットを選択します。
5. Tealium Swiftライブラリから追加のモジュールを使用している場合は、[Swift Package Managerの指示](/ja/platforms/ios-swift/install/#swift-package-manager-recommended)に従って追加してください。

プロジェクトに複数のアプリターゲットがあり、`TealiumAdjust`モジュールを複数のアプリターゲットに追加する必要がある場合は、**Frameworks, Libraries, and Embedded Content**セクションで手動で追加する必要があります。

追加のアプリターゲットに`TealiumAdjust`をインストールするには：

1. **Project Navigator**でXcodeプロジェクトを選択します。
2. Xcodeプロジェクトで、**TARGETS**セクションのアプリターゲットを選択します。
3. **General &gt; Frameworks, Libraries &amp; Embedded Content**に移動し、`TealiumAdjust`モジュールをアプリターゲットに追加します。




1. Podfileから`pod &#34;tealium-swift&#34;`と`pod &#34;Adjust&#34;`を削除します。`tealium-swift`の依存関係はすでに`TealiumAdjust`フレームワークに含まれています。

2. Podfileに次の依存関係を追加します：
      ```ruby
      pod &#34;TealiumAdjust&#34;
      ```  
      `TealiumAdjust`ポッドには次の`TealiumSwift`依存関係が含まれています：
      ```bash
      &#34;tealium-swift/Core&#34;
      &#34;tealium-swift/RemoteCommands&#34;
      ```

3. インストールにディスパッチャーポッドを含めます。`tealium-swift/Collect`または`tealium-swift/TagManagement`のいずれかを選択し、Podfileに他の個々のサブモジュールを含めます。例：
      ```ruby
      pod &#34;TealiumAdjust&#34;
      pod &#34;tealium-swift/Collect&#34;
      pod &#34;tealium-swift/Lifecycle&#34;
      pod &#34;tealium-swift/Attribution&#34;
      ```

4. `TealiumHelper`ファイルおよび`Tealium`クラスまたはAdjustリモートコマンドにアクセスする他のファイルで`TealiumSwift`と`TealiumAdjust`モジュールをインポートします。




1. Cartfileから`tealium-swift`を削除します。`tealium-swift`の依存関係はすでに`TealiumAdjust`フレームワークに含まれています。

2. Cartfileに存在する場合は次の行を削除します：
      ```bash
      github &#34;adjust/ios_sdk&#34;
      ```

3. Cartfileに次の依存関係を追加します：
      ```bash
      github &#34;tealium/tealium-ios-adjust-remote-command&#34;
      ```






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

2. アプリプロジェクトの`build.gradle`ファイルにAdjust SDKとTealium-Adjustリモートコマンドの依存関係を追加します：
      ```groovy
      dependencies {
            implementation &#39;com.tealium.remotecommands:adjust:1.0.0&#39;
      }
      ```



1. React Nativeプロジェクトのルートに移動します。

2. 次のコマンドで`tealium-react-adjust`パッケージをダウンロードしてインストールします：
    ```bash
    yarn add tealium-react-adjust
    ```
3. React Native AutolinkingはNPMパッケージのバージョン1.0.7で有効になっており、React Nativeのバージョン0.60&#43;を使用している場合、`react-native link`を実行する必要はありません。




### 手動インストール




Adjustリモートコマンドの手動インストールには、[Tealium for Swift](/ja/platforms/ios-swift/)ライブラリがインストールされている必要があります。iOSプロジェクトのAdjustリモートコマンドをインストールするには：

1. まだ行っていない場合は、[Adjust SDK](https://github.com/adjust/ios_sdk)をインストールします。

2. [Tealium iOS Adjustリモートコマンド](https://github.com/tealium/tealium-ios-adjust-remote-command)リポジトリをクローンし、`Sources`フォルダ内のファイルをプロジェクトにドラッグします。

3. [`remoteAPIEnabled`](/ja/platforms/ios-swift/api/tealium-config/#remoteapienabled)構成フラグを`true`に構成します。





Adjustリモートコマンドの手動インストールには、[Tealium for Android (Kotlin)](/ja/platforms/android-kotlin/install/)または[Tealium for Android (Java)](/ja/platforms/android-java/install/)がインストールされている必要があります。AndroidプロジェクトのAdjustリモートコマンドをインストールするには：

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

2. `&lt;PROJECT_ROOT&gt;/&lt;MODULE&gt;/libs`に`tealium-adjust.aar`を追加します。

3. `build.gradle`ファイルにTealiumライブラリの依存関係を追加します：
      ```groovy
      dependencies {
            implementation(name:&#39;tealium-adjust&#39;, ext:&#39;aar&#39;)
      }
      ```


## 初期化

Tealiumのすべてのライブラリで、初期化時にAdjust Remote Commandを登録します。




TealiumのiOS（Swift）ライブラリ用にJSON構成ファイルまたはRemote Commandタグでリモートコマンドを初期化します：
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
    let adjust = AdjustRemoteCommand()

    // ローカルJSON
    //let adjust = AdjustRemoteCommand(type: .local(file: &#34;adjust&#34;)) 

    // リモートJSON
    //let adjust = AdjustRemoteCommand(type: .remote(url: &#34;https://some.domain.com/adjust.json&#34;))

    remoteCommands.add(adjust)
}
```



TealiumのAndroid（Kotlin）ライブラリ用にJSON構成ファイルまたはRemote Commandタグでリモートコマンドを初期化します：
```kotlin
val config = TealiumConfig(application,
        &#34;ACCOUNT&#34;,
        &#34;PROFILE&#34;,
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands, Dispatchers.TagManagement));
val adjust = AdjustRemoteCommand(application);

var tealium = Tealium.create(TEALIUM_MAIN, config) {

    // Webviewタグ
    remoteCommands?.add(adjust); 

    // ローカルJSON
    //remoteCommands?.add(adjust, filename = &#34;adjust.json&#34;);

    // リモートJSON
    //remoteCommands?.add(adjust, remoteUrl = &#34;https://some.domain.com/adjust.json&#34;); 
}
```



TealiumのAndroid（Java）ライブラリ用にJSON構成ファイルまたはRemote Commandタグでリモートコマンドを初期化します：
```java
Tealium.Config config = Tealium.Config.create(application, &#34;ACCOUNT&#34;, &#34;PROFILE&#34;, &#34;ENVIRONMENT&#34;);
Tealium teal = Tealium.createInstance(TEALIUM_MAIN, config);

// Adjust Remote Commandを追加する新しいコード
AdjustRemoteCommand adjustRemoteCommand = new AdjustRemoteCommand(application)
teal.addRemoteCommand(adjustRemoteCommand);
```




React Native用にJSON構成ファイルまたはRemote Commandタグでリモートコマンドを初期化します：
```javascript
import AdjustRemoteCommand from &#39;tealium-react-adjust&#39;;
AdjustRemoteCommand.initialize();

// Webviewタグ
let adjust = { id: AdjustRemoteCommand.name } 

// ローカルJSON
//let adjust = { id: AdjustRemoteCommand.name, path: &#34;adjust.json&#34; }

// リモートJSON
//let adjust = { id: AdjustRemoteCommand.name, url: &#34;https://some.domain.com/adjust.json&#34; }

let config = TealiumConfig {
    // ...
    remoteCommands: [adjust]
}
```




## JSONテンプレート

リモートコマンドを[JSON構成ファイル](/ja/platforms/remote-commands/how-it-works/#json-configuration-file)を使用して構成する場合は、以下のテンプレートを参照してください。このテンプレートには、標準的なeコマースインストールで使用される一般的なマッピングが含まれています。必要に応じてマッピングを編集してください。

```json
{
  &#34;config&#34;: {
    &#34;api_token&#34;: &#34;YOUR_API_TOKEN&#34;,
    &#34;sandbox&#34;: true,
    &#34;settings&#34;: {
      &#34;log_level&#34;: &#34;verbose&#34;,
      &#34;allow_iad&#34;: true,
      &#34;allow_ad_services&#34;: true,
      &#34;allow_idfa&#34;: true,
      &#34;event_buffering_enabled&#34;: false,
      &#34;send_in_background&#34;: true
    }
  },
  &#34;mappings&#34;: {
    &#34;event_token&#34;: &#34;event_token&#34;,
    &#34;order_total&#34;: &#34;revenue,callback.orderTotal&#34;,
    &#34;order_currency&#34;: &#34;currency&#34;,
    &#34;order_id&#34;: &#34;order_id,callback.orderId&#34;,
    &#34;conversion_value&#34;: &#34;conversion_value&#34;,
    &#34;sales_region&#34;: &#34;sales_region&#34;,
    &#34;callback_id&#34;: &#34;callback_id&#34;,
    &#34;ad_revenue_source&#34;: &#34;ad_revenue_source&#34;,
    &#34;campaign&#34;: &#34;ad_revenue_payload.campaignId&#34;,
    &#34;ad_uuid&#34;: &#34;ad_revenue_payload.adId&#34;,
    &#34;appstore_receipt_data&#34;: &#34;receipt&#34;,
    &#34;purchase_timestamp&#34;: &#34;purchase_time&#34;,
    &#34;product_sku&#34;: &#34;sku&#34;,
    &#34;purchase_signature&#34;: &#34;signature&#34;,
    &#34;purchase_token&#34;: &#34;purchase_token&#34;,
    &#34;deeplink_url&#34;: &#34;deeplink_open_url&#34;,
    &#34;push_token&#34;: &#34;push_token&#34;,
    &#34;favorite_color&#34;: &#34;callback.color,session_callback.color&#34;,
    &#34;num_of_pets&#34;: &#34;partner.pets,session_partner.pets&#34;,
    &#34;customer_id&#34;: &#34;callback.customerId&#34;,
    &#34;customer_is_member&#34;: &#34;partner.isMember&#34;,
    &#34;global_params&#34;: &#34;global_callback,global_partner&#34;,
    &#34;remove_global_params&#34;: &#34;remove_global_callback_params,remove_global_partner_params&#34;,
    &#34;reset_global_params&#34;: &#34;reset_global_callback_params,reset_global_partner_params&#34;,
    &#34;consent_granted&#34;: &#34;measurement_consent&#34;,
    &#34;enabled&#34;: &#34;enabled&#34;
  },
  &#34;commands&#34;: {
    &#34;launch&#34;: &#34;initialize&#34;,
    &#34;track_deeplink&#34;: &#34;appwillopenurl&#34;,
    &#34;purchase&#34;: &#34;trackevent,updateconversionvalue&#34;,
    &#34;event&#34;: &#34;trackevent&#34;,
    &#34;contact&#34;: &#34;trackevent,addglobalcallbackparams,addglobalpartnerparams&#34;,
    &#34;ad_revenue&#34;: &#34;trackadrevenue&#34;,
    &#34;subscribe&#34;: &#34;trackevent,tracksubscription&#34;,
    &#34;received_push_token&#34;: &#34;setpushtoken&#34;,
    &#34;add_global_parameters&#34;: &#34;addglobalcallbackparams,addglobalpartnerparams&#34;,
    &#34;remove_global_parameters&#34;: &#34;removeglobalcallbackparams,removeglobalpartnerparams&#34;,
    &#34;reset_global_parameters&#34;: &#34;resetglobalcallbackparams,resetglobalpartnerparams&#34;,
    &#34;consent_revoked&#34;: &#34;gdprforgetme,trackmeasurementconsent&#34;,
    &#34;consent_granted&#34;: &#34;trackmeasurementconsent&#34;,
    &#34;set_enabled&#34;: &#34;setenabled&#34;,
    &#34;offline&#34;: &#34;setofflinemode&#34;
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

 iOSの`AppTrackingTransparency.framework`の一部としてのみサポートされています。[Adjust iOS SKAdNetwork統合](https://help.adjust.com/en/article/app-tracking-transparency-att-framework)ガイドで詳細を学びましょう。


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

 iOSとAndroidのみ

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
            case 0: print(&#34;ATTrackingManagerAuthorizationStatusNotDetermined&#34;)
            case 1: print(&#34;ATTrackingManagerAuthorizationStatusRestricted&#34;)
            case 2: print(&#34;ATTrackingManagerAuthorizationStatusDenied&#34;)
            case 3: print(&#34;ATTrackingManagerAuthorizationStatusAuthorized&#34;)
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
