---
title: リモートコマンド：Braze
description: AndroidおよびSwift/iOS向けのTealiumリモートコマンドによるBraze連携。
url: https://docs.tealium.com/ja/platforms/remote-commands/integrations/braze/
---
## 要件

* Braze APIキー
* 次のいずれかのモバイルライブラリ：
  * [Tealium for Android-Kotlin](https://docs.tealium.com/ja/platforms/android-kotlin/)（1.0.0以降）
  * [Tealium for Android-Java](https://docs.tealium.com/ja/platforms/android-java/)（Braze 1.0.0以降の場合は5.9.0以降、以前のバージョンの場合は5.9.0未満）
  * [Tealium for iOS-Swift](https://docs.tealium.com/ja/platforms/ios-swift/)（2.8.0以降）
* 次のいずれかのリモートコマンド連携：
  * [BrazeリモートコマンドJSONファイル](https://docs.tealium.com/ja/platforms/remote-commands/integrations/braze/#json-template)（Android-Kotlin 1.0.0以降またはiOS-Swift 2.1.0以降が必要）
  * タグ管理のBrazeリモートコマンドタグ

## 仕組み

Braze連携では、次の項目を使用します。

1. BrazeネイティブSDK。
2. Brazeメソッドをラップするリモートコマンドモジュール。
3. イベントトラッキングをBrazeのネイティブ呼び出しに変換するJSON構成ファイルまたはリモートコマンドタグ。

Brazeリモートコマンドモジュールをアプリに追加すると、必要なBrazeライブラリが自動的にインストールおよびビルドされるため、ベンダー固有のコードをアプリに追加する必要はありません。依存関係マネージャーを使用してインストールする場合、Braze SDKを別途インストールする必要はありません。

リモートコマンドには、JSON構成ファイルを使用する方法と、タグ管理を使用してマッピングを構成する方法の2つがあります。ベンダー連携には、リモートでホストするかアプリ内にローカルで配置したJSON構成ファイルの使用をお勧めします。タグ管理を使用する場合は、ベンダー連携用のリモートコマンドタグを追加します。[ベンダー連携](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/#vendor-integrations)の詳細をご確認ください。


## インストール

### 依存関係マネージャー




1. Xcodeプロジェクトで、**File > Add Packages... > Add Package Dependency**を選択します。
2. リポジトリURLとして`https://github.com/tealium/tealium-ios-braze-remote-command`を入力します。
3. バージョンルールを構成します。通常は`Up to next major`をお勧めします。現在の`TealiumBraze`バージョンがリストに表示されない場合は、Swiftパッケージのキャッシュをリセットします。
4. インストールする`TealiumBraze`モジュールを選択し、そのモジュールをインストールするアプリターゲットを選択します。

プロジェクトに複数のアプリターゲットがあり、追加のアプリターゲットでも`TealiumBraze`モジュールが必要な場合は、**Frameworks, Libraries, and Embedded Content**セクションでそれらを手動で追加する必要があります。

追加のアプリターゲットに`TealiumBraze`をインストールするには、次の手順を実行します。

1. **Project Navigator**でXcodeプロジェクトを選択します。
2. Xcodeプロジェクトの**TARGETS**セクションでアプリターゲットを選択します。
3. **General > Frameworks, Libraries & Embedded Content**に移動し、`TealiumBraze`モジュールを選択してアプリターゲットに追加します。

Tealium Swiftライブラリから追加のモジュールを追加するには、[Swift Package Manager](https://docs.tealium.com/ja/platforms/ios-swift/install/#swift-package-manager-recommended)の手順に従ってください。




1. Podfileに`tealium-swift`および`pod "BrazeKit"`が存在する場合は削除します。`tealium-swift`の依存関係は、すでに`TealiumBraze`フレームワークに含まれています。

2. 次の依存関係をPodfileに追加します。  
      ```ruby
      pod "TealiumBraze"
      ```  
      `TealiumBraze` Podには、次の`TealiumSwift`依存関係が含まれています。  
      ```bash
      'tealium-swift/Core'
      'tealium-swift/RemoteCommands'
      ```

3. `TealiumHelper`ファイル、および`Tealium`クラスまたはBrazeリモートコマンドにアクセスするその他のファイルに、`TealiumSwift`モジュールと`TealiumBraze`モジュールをインポートします。





1. Cartfileから`tealium-swift`を削除します。`tealium-swift`の依存関係は、すでに`TealiumBraze`フレームワークに含まれています。

2. Cartfileに次の依存関係を追加します。  
      ```bash
      github "tealium/tealium-ios-braze-remote-command"
      ```





1. [Tealium for Android（Kotlin）](https://docs.tealium.com/ja/platforms/android-kotlin/install/)または[Tealium for Android（Java）](https://docs.tealium.com/ja/platforms/android-java/install/)をインストールし、まだ追加していない場合は、プロジェクトのトップレベルの`build.gradle`ファイルにTealium Maven URLを追加します。

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

2. アプリプロジェクトの`build.gradle`ファイルに次の依存関係を追加して、Braze SDKとTealium-Brazeリモートコマンドの両方をインポートします。  
      ```groovy
      dependencies {
            implementation 'com.tealium.remotecommands:braze:3.0.0'
            implementation 'com.braze:android-sdk-ui:29.0.1'
      }
      ```



1. React Nativeプロジェクトのルートに移動します。

2. 次のコマンドを使用して、`tealium-react-braze`パッケージをダウンロードしてインストールします。  
    ```bash
    yarn add tealium-react-braze
    ```
3. React Nativeの自動リンクはNPMパッケージのバージョン1.0.7で有効になっています。React Nativeバージョン0.60以降を使用している場合、`react-native link`を実行する必要はありません。



### 手動インストール




Brazeリモートコマンドを手動でインストールするには、[Tealium for Swift](https://docs.tealium.com/ja/platforms/ios-swift/)ライブラリがインストールされている必要があります。iOSプロジェクトにBrazeリモートコマンドをインストールするには、次の手順を実行します。

1. まだインストールしていない場合は、[Braze SDK](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/initial_sdk_setup/initial_sdk_setup/)をインストールします。

2. [Tealium iOS Brazeリモートコマンド](https://github.com/tealium/tealium-ios-braze-remote-command)リポジトリをクローンし、`Sources`フォルダー内のファイルをプロジェクトにドラッグします。

3. [`remoteAPIEnabled`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#remoteapienabled)構成フラグを`true`に構成します。




Brazeリモートコマンドを手動でインストールするには、[Tealium for Android（Kotlin）](https://docs.tealium.com/ja/platforms/android-kotlin/install/)または[Tealium for Android（Java）](https://docs.tealium.com/ja/platforms/android-java/install/)がインストールされている必要があります。

AndroidプロジェクトにBrazeリモートコマンドをインストールするには、次の手順を実行します。

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

2. `tealium-braze.aar`を`<PROJECT_ROOT>/<MODULE>/libs`に追加します。

3. `build.gradle`ファイルにTealiumライブラリの依存関係を追加します。

      ```groovy
      dependencies {
            implementation(name:'tealium-braze', ext:'aar')
      }
      ```



## 初期化



JSON 構成ファイルまたは Remote Command タグを使用して、Tealium の iOS（Swift）ライブラリ向けリモートコマンドを初期化します。  
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
    let braze = BrazeRemoteCommand(brazeLocation: BrazeLocationProvider()) 

    // Local JSON
    //let braze = BrazeRemoteCommand(type: .local(file: "braze"), brazeLocation: BrazeLocationProvider()) 

    // Remote JSON
    //let braze = BrazeRemoteCommand(type: .remote(url: "https://some.domain.com/braze.json"), brazeLocation: BrazeLocationProvider()) 

    remoteCommands.add(braze)
}
```


JSON 構成ファイルまたは Remote Command タグを使用して、Tealium の Kotlin ライブラリ向けリモートコマンドを初期化します。
```kotlin
val config = TealiumConfig(application,
        "ACCOUNT",
        "PROFILE",
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands, Dispatchers.TagManagement));
// New code to add the Braze Remote Command
val braze = BrazeRemoteCommand(application,
                            true,
                            sessionHandlingBlacklist,
                            true,
                            inAppMessageBlacklist)

var tealium = Tealium.create(TEALIUM_MAIN, config) {
    // Optional: Set config options that may not be supported yet by the Tag in Tag Management
    //              or simply to override settings locally.
    braze.registerConfigOverride { builder ->
        // builder.setIsLocationCollectionEnabled(true);
        // builder.setGeofencesEnabled(true);
        // builder.setPushDeepLinkBackStackActivityEnabled(true);
        // builder.setPushDeepLinkBackStackActivityClass(UserActivity.class);
    }

    // register the command

    // Webview Tag
    remoteCommands?.add(braze); 

    // Local JSON
    //remoteCommands?.add(braze, filename = "braze.json"); 

    // Remote JSON
    //remoteCommands?.add(braze, remoteUrl = "https://some.domain.com/braze.json"); 
}
```


Remote Command タグを使用して、Tealium の Android（Java）ライブラリ向けリモートコマンドを初期化します。  
```java
import com.tealium.remotecommands.BrazeRemoteCommand;

Tealium.Config config = Tealium.Config.create(application, "ACCOUNT", "PROFILE", "ENVIRONMENT");
Tealium teal = Tealium.createInstance(TEALIUM_MAIN, config);

BrazeRemoteCommand braze;
// Initialize with default configuration options.
braze = new BrazeRemoteCommand(config);

// Or alternatively initialize with some additional config options:
Set<Class> sessionHandlingBlacklist = new HashSet<>();
Set<Class> inAppMessageBlacklist = new HashSet<>();
// sessionHandlingBlacklist.add(MainActivity.class);
// inAppMessageBlacklist.add(UserActivity.class);
braze = new BrazeRemoteCommand(config,
        true,                     // sessiongHandlingEnabled
        sessionHandlingBlacklist, // sessionHandlingBlacklist
        true,                     // registerInAppMessageManager
        inAppMessageBlacklist);   // inAppMessageBlackList

// Optional: Set config options that may not be supported yet by the Tag in Tag Management
//              or simply to override settings locally.
braze.registerConfigOverride(new BrazeRemoteCommand.ConfigOverrider() {
    @Override
    public void onOverride(AppboyConfig.Builder b) {
        b.setPushDeepLinkBackStackActivityEnabled(true);
        b.setPushDeepLinkBackStackActivityClass(UserActivity.class);
    }
});

// register the command
teal.addRemoteCommand(braze);
```

 

JSON 構成ファイルまたは Remote Command タグを使用して、React Native 向けリモートコマンドを初期化します。
```javascript
import BrazeRemoteCommand from 'tealium-react-braze';
BrazeRemoteCommand.initialize();

// Webview Tag
let braze = { id: BrazeRemoteCommand.name } 

// Local JSON
//let braze = { id: BrazeRemoteCommand.name, path: "braze.json" } 

// Remote JSON
//let braze = { id: BrazeRemoteCommand.name, url: "https://some.domain.com/braze.json" } 

let config = TealiumConfig {
    // ...
    remoteCommands: [braze]
}
```





## JSON テンプレート

[JSON 構成ファイル](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/#json-configuration-file)を使用してリモートコマンドを構成する場合は、以下のテンプレートを参照して作業を開始してください。このテンプレートには、標準的な e コマース実装で使用される一般的なマッピングが含まれています。必要に応じてマッピングを編集してください。

```json
{
    "config": {
        "api_key": "YOUR_API_KEY",
        "custom_endpoint": "sdk.iad-01.braze.com",
        "session_timeout": 30,
        "trigger_interval_seconds": 100,
        "enable_geofences": true,
        "enable_automatic_geofences": true,
        "enable_automatic_location": true,
        "push_story_identifier": "YOUR_IDENTIFIER",
        "use_uuid_as_device_id": true,
        "forward_universal_links": true
    },
    "mappings": {
        "customer_id": "user_id",
        "customer_first_name": "first_name",
        "customer_last_name": "last_name",
        "customer_gender": "gender",
        "customer_language": "language",
        "customer_email": "email",
        "customer_home_city": "home_city",
        "customer_dob": "date_of_birth",
        "customer_alias": "user_alias",
        "customer_alias_label": "alias_label",
        "pet": "set_custom_attribute.pet",
        "pet_count": "set_custom_attribute.pet_count",
        "pet_count_unset": "unset_custom_attribute.pet_count_unset",
        "pet_count_increment": "increment_custom_attribute.pet_count_increment",
        "pet_names": "set_custom_array_attribute.pet_names",
        "pet_names_append": "append_custom_array_attribute.pet_names_append",
        "pet_names_remove": "remove_custom_array_attribute.pet_names_remove",
        "screen_name": "screen_name",
        "email_notification": "email_notification",
        "push_notification": "push_notification",
        "event_name": "event_name",
        "current_level": "event.current_level",
        "start_date": "event.start_date",
        "high_score": "event.high_score",
        "product_id": "product_id",
        "product_quantity": "product_qty",
        "product_unit_price": "product_unit_price",
        "currency_code": "product_currency",
        "rewards_member": "purchase.rewards_member",
        "rewards_points_earned": "purchase.rewards_points_earned",
        "date_joined_program": "purchase.date_joined_program",
        "latitude": "location_latitude",
        "longitude": "location_longitude",
        "horizontal_accuracy": "location_horizontal_accuracy",
        "vertical_accuracy": "location_vertical_accuracy"
    },
    "commands": {
        "launch": "initialize",
        "setengagement": "emailnotification,pushnotification",
        "log_custom_event": "logcustomevent",
        "set_location": "setlastknownlocation",
        "custom_attribute": "setcustomattribute",
        "unset_custom_attribute": "unsetcustomattribute",
        "custom_array_attribute": "appendcustomarrayattribute",
        "append_custom_array_attribute": "appendcustomarrayattribute",
        "remove_custom_array_attribute": "removecustomarrayattribute",
        "increment_custom_attribute": "incrementcustomattribute",
        "log_purchase": "logpurchase",
        "user_attribute": "userattribute,useridentifier,useralias",
        "user_login": "useridentifier,useralias",
        "user_alias": "useralias",
    }
}
```
## サポートされているメソッド

各 Braze メソッドにコマンドを対応付けます。Braze メソッドをトリガーするには、対応するコマンドを指定された形式で渡します。

|リモートコマンド|Braze メソッド|
|--------------|------------|
| `addtosubscriptiongroup` | `user.addToSubscriptionGroup(id:)` |
| `appendcustomarrayattribute` | `user.addToCustomAttributeArray()` |
| `emailnotification` | `user.set(emailSubscriptionState:)` |
| `enablesdk` | `enabled = true/false` |
| `flush`| `requestImmediateDataFlush()` |
| `incrementcustomattribute` | `user.incrementCustomUserAttribute()` |
| `initialize` | `Braze(configuration:)` |
| `logcustomevent` | `logCustomEvent()` |
| `logpurchase` | `logPurchase()` |
| `pushnotification` | `user.set(pushNotificationSubscriptionState:)` |
| `removefromsubscriptiongroup` | `user.removeFromSubscriptionGroup(id:)` |
| `removecustomarrayattribute` | `user.removeFromCustomAttributeArray()` |
| `setadtrackingenabled` | `set(adTrackingEnabled:)` |
| `setcustomattribute` | `user.setCustomAttribute())` |
| `setcustomarrayattribute` | `user.setCustomAttributeArray()` |
| `setlastknownlocation` | `user.setLastKnownLocation()` |
| `setsdkauthsignature`| `set(sdkAuthenticationSignature:)` |
| `useralias` | `user.add(alias:)` |
| `unsetcustomattribute` | `user.unsetCustomAttribute()` |
| `userattribute` | `user.set()` |
| `useridentifier` | `changeUser()` |
| `wipedata` | `wipeData()` |



<blockquote>
Braze SDK は Tealium SDK とともにインストールされるため、対応するタグ構成を指定することで、Braze のネイティブ機能をトリガーできます。
</blockquote>


### SDK のセットアップ

#### 初期化

Braze API キーとカスタムエンドポイントは必須であり、タグ構成で指定する必要があります。

| リモートコマンド | Braze メソッド（iOS） | Braze メソッド（Android） |
|---|---|---|
| `initialize` | `Braze(configuration:)` | `configure()` |

起動オプションの構成には、以下のマッピングを使用します。

| パラメータ | 型 | 説明 |
|---|---|---|
| `api_key`（必須） |  `String` | API キーを構成します |
| `custom_endpoint`（必須） |  `String` | カスタム API エンドポイントを構成します。これは `sdk.api.braze.eu` 形式で送信されます |
| `device_options` |  `[String]` | Braze SDK が収集するデバイスフィールドの許可リストです（デフォルトでは、すべてのフィールドが収集されます）。 |
| `enable_automatic_geofences` | `Bool` | ジオフェンスの自動収集を有効にします（`true` または `false`）。 |
| `enable_automatic_location` | `Bool` | 位置情報の収集を有効にします（`true` または `false`）。 |
| `enable_geofences` | `Bool` | ジオフェンスの収集を有効にします（`true` または `false`）。 |
| `flush_interval` |  `Double` | データのフラッシュ間隔を秒単位で構成します。値は NSTimeInterval に変換され、`1.0` より大きくなければなりません。 |
| `is_sdk_authentication_enabled` | `Bool` | SDK 認証を有効にします。デフォルトは `false` です。 |
| `push_story_identifier` |  `String` | Push Story Notification Content 拡張機能のアプリグループ名を表す文字列値を、このキーに構成します。 |
| `request_processing_policy` |  `String` | SDK のリクエスト処理に指定できる値です（`manual` または `automatic`）。デフォルトは `automatic` です。 |
| `session_timeout` |  `Int`（秒） | セッションタイムアウトの秒数です（デフォルトは `30` 秒）。 |
| `trigger_interval_seconds` | `Int`（秒） | アプリ内メッセージのトリガー間の最小間隔を上書きします（デフォルトは `30` 秒）。 |
| `use_uuid_as_device_id` | `Bool` | （iOS）ランダムに生成された UUID をデバイス ID として使用するかどうかを決定します（デフォルトは `true`）。 |
| `forward_universal_links` | `Bool` | SDK がユニバーサルリンクを自動的に認識し、システムメソッドに転送するかどうかを指定します（デフォルトは `false`）。 |

Android  

- [Braze 開発者ガイド：SDK の初期セットアップ](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/initial_sdk_setup/android_sdk_integration/)

iOS  

- [Braze 開発者ガイド：SDK 起動時の Braze のカスタマイズ](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/initial_sdk_setup/#customizing-braze-on-startup)   
- [Braze 開発者ガイド：ネットワークトラフィックの詳細な制御](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/advanced_use_cases/fine_network_traffic_control/)  
- [Braze 開発者ガイド：位置情報とジオフェンス](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/advanced_use_cases/locations_and_geofences/)  
- [Braze 開発者ガイド：Push Story のセットアップ](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/push_story/)  
- [Braze 開発者ガイド：セッションの追跡](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/tracking_sessions/)


#### SDK 認証署名の構成

| リモートコマンド | Braze メソッド（iOS） | Braze メソッド（Android）
|---|---|---|
| `setsdkauthsignature`| `set(sdkAuthenticationSignature:)` | `setSdkAuthenticationSignature` |

| パラメータ | 型 |
|---|---|
| `sdk_authentication_signature` | `String` |

#### フラッシュ

| リモートコマンド | Braze メソッド |
|---|---|
| `flush`| `requestImmediateDataFlush` |


- Braze 開発者ガイド：分析の無効化  
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/advanced_use_cases/fine_network_traffic_control/)

### ユーザーの追跡

#### ユーザー ID の割り当て

| リモートコマンド | Braze メソッド |
|---|---|
| `useridentifier`  | `changeUser` |

| パラメータ | 型 |
|---|---|
| `user_id`（必須） | `String` |
| `sdk_authentication_signature` | `String` |


- Braze 開発者ガイド：分析用ユーザー ID  
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/setting_user_ids/)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/setting_user_ids/#assigning-a-user-id)

#### ユーザーのエイリアス構成

| リモートコマンド | Braze メソッド |
|---|---|
| `useralias` | `user.add(alias:)` |

| パラメータ | 型 |
|----|---|
| `user_alias`（必須） | `String` |
| `alias_label`（必須） | `String` |

- Braze 開発者ガイド：分析用ユーザーのエイリアス     
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/setting_user_ids/#aliasing-users)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/setting_user_ids/#aliasing-users)

### ユーザー属性

#### 標準属性

| イベント | Braze メソッド |
|---|---|
| userattribute  | `Braze.User` オブジェクトのフィールドを構成 |

| パラメータ | 型 |
|---|---|
| `first_name` | `String` |
| `last_name` | `String` |
| `email` | `String` |
| `date_of_birth` | `String` |
| `country` | `String` |
| `language` | `String` |
| `home_city` | `String` |
| `phone` | `String` |
| `gender` | `String` |

- Braze 開発者ガイド：分析用ユーザー属性
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/setting_custom_attributes/#assigning-standard-user-attributes)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/setting_custom_attributes/#assigning-standard-user-attributes)
- [Braze 開発者ガイド：ユーザーデータ API](https://www.braze.com/docs/api/endpoints/user_data/?redirected=true#user-attributes-object-specification)

#### カスタム属性の構成

| リモートコマンド | Braze メソッド |
|---|---|
| `setcustomattribute` | `user.setCustomAttribute` |


| パラメータ | 型 |
|---|---|
| `set_custom_attribute.PROPERTY` | `[String: Any]` / `JSONObject` |

- Braze 開発者ガイド：分析用カスタム属性  
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/setting_custom_attributes/#assigning-custom-user-attributes)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/setting_custom_attributes/#assigning-custom-user-attributes)
#### カスタム属性の構成解除

| リモートコマンド | Brazeメソッド |
|---|---|
| `setcustomattribute` | `user.unsetCustomAttribute` |

| パラメーター | 型 |
|---|---|
| `set_custom_attribute.PROPERTY` | `String` |

- Braze開発者ガイド：分析用カスタム属性  
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/setting_custom_attributes/#unsetting-a-custom-attribute)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/setting_custom_attributes/#assigning-custom-user-attributes)

#### カスタム属性のインクリメント

| リモートコマンド | Brazeメソッド |
|---|---|
| `incrementcustomattribute` | `user.incrementCustomUserAttribute`|

| パラメーター | 型 |
|---|---|
| `increment_custom_attribute.PROPERTY` | `String` |

- Braze開発者ガイド：分析用属性のインクリメント
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/setting_custom_attributes/#incrementingdecrementing-custom-attributes)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/setting_custom_attributes/#assigning-custom-user-attributes)

#### カスタム配列属性の構成

| リモートコマンド | Brazeメソッド |
|---|---|
| `setcustomarrayattribute` | `user.setCustomAttributeArray` |

| パラメーター | 型 |
|---|---|
| `set_custom_array_attribute.PROPERTY` | `[String: [Any]]` / `JSONObject` |

- Braze開発者ガイド：分析用配列属性  
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/setting_custom_attributes/#custom-attribute-with-an-array-value)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/setting_custom_attributes/#assigning-custom-user-attributes)

#### カスタム配列属性への追加

| リモートコマンド | Brazeメソッド |
|---|---|
| `appendcustomarrayattribute` | `user.addToCustomAttributeArray` |

| パラメーター | 型 |
|---|---|
| `append_custom_array_attribute.PROPERTY` | `[String: String]` / `JSONObject` |

- Braze開発者ガイド：分析用配列属性  
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/setting_custom_attributes/#custom-attribute-with-an-array-value)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/setting_custom_attributes/#assigning-custom-user-attributes)

#### カスタム配列属性からの削除

| リモートコマンド | Brazeメソッド |
|---|---|
| `removecustomarrayattribute`| `user.removeFromCustomAttributeArray`|

| パラメーター | 型 |
|---|---|
| `remove_custom_array_attribute.PROPERTY` | `[String: String]` / `JSONObject` |

- Braze開発者ガイド：分析用配列属性  
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/setting_custom_attributes/#custom-attribute-with-an-array-value)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/setting_custom_attributes/#assigning-custom-user-attributes)

### カスタムイベントのトラッキング

#### カスタムイベント

| リモートコマンド | Brazeメソッド |
| --- | --- |
| `logcustomevent`  | `logCustomEvent` |

| パラメーター | 型 |
|--- | --- |
|  `event_name`（必須） | `String` |
|  `event_properties` | `[String: Any]` / `JSONObject` |

- Braze開発者ガイド：分析用カスタムイベント
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/tracking_custom_events/)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/tracking_custom_events/)

### 通知

#### メール通知

| リモートコマンド | Brazeメソッド |
|---|---|
| `emailnotification` | `setEmailNotificationSubscriptionType` |

| パラメーター | 型 | 例 |
|---|---|---|
| `email_notification` | `String`| [`"optedin"`, `"subscribed"`, `"unsubscribed"`]|

- Braze開発者ガイド：分析用メールサブスクリプション   
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/setting_custom_attributes/#setting-email-subscriptions)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/setting_custom_attributes/#setting-up-user-subscriptions)

#### サブスクリプショングループへの追加

| リモートコマンド | Brazeメソッド |
|---|---|
| `addtosubscriptiongroup` | `user.addToSubscriptionGroup(id:)` |

| パラメーター | 型 |
|---|---|
| `subscription_group_id`（必須） | `String` |

- [Braze開発者ガイド：サブスクリプショングループ](https://www.braze.com/docs/user_guide/message_building_by_channel/email/managing_user_subscriptions/#updating-email-subscription-states)

#### サブスクリプショングループからの削除

| リモートコマンド | Brazeメソッド |
|---|---|
| `removefromsubscriptiongroup` | `user.removeFromSubscriptionGroup(id:)` |

| パラメーター | 型 |
|---|---|
| `subscription_group_id`（必須） | `String` |

- [Braze開発者ガイド：サブスクリプショングループ](https://www.braze.com/docs/user_guide/message_building_by_channel/email/managing_user_subscriptions/#updating-email-subscription-states)

#### プッシュ通知

| リモートコマンド | Brazeメソッド |
|---|---|
| `pushnotification` | `setPushNotificationSubscriptionType` |

| パラメーター | 型 | 例 |
|---|---|---|
| `push_notification` | `String`| [`"optedin"`, `"subscribed"`, `"unsubscribed"`]|


- Braze開発者ガイド：分析用プッシュ通知  
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/setting_custom_attributes/#setting-up-user-subscriptions)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/setting_custom_attributes/#setting-up-user-subscriptions)

### 購入のトラッキング

#### 購入の記録

| リモートコマンド | Brazeメソッド |
|--- | ---|
| `logpurchase` | `logPurchase`|

| パラメーター | 型 |
|---|---|
| `product_id`（必須）| `[String]` / `String[]` |
| `product_currency`（必須） | `String` / `String` |
| `price`（必須） | `[Double]` / `Double[]`|
| `product_qty`  | `[Int]` / `Int[]` |
| `purchase_properties` | `[AnyHashable: Any]` / `JSONObject` |


- Braze開発者ガイド：分析用購入イベント  
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/logging_purchases/)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/logging_purchases/)

### 位置情報のトラッキング

#### ユーザーの最終既知位置の構成

| リモートコマンド | Brazeメソッド |
|---|---|
| `setlastknownlocation` | `user.setLastKnownLocation` |

| パラメーター | 型 |
|---|---|
| `latitude`（必須） | `Double` |
| `longitude`（必須） | `Double` |
| `horizontalAccuracy`（必須） | `Double` |
| `altitude`  | `Double` |
| `verticalAccuracy` | `Double` |


- [Braze開発者ガイド：分析用位置情報トラッキング](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/location_tracking/#enabling-automatic-location-tracking)


### データプライバシー（同意オプション）

#### SDKの有効化

| リモートコマンド | Brazeメソッド（iOS） | Brazeメソッド（Android） |
|---|---|---|
| `enablesdk` | `enabled` | `enableSdk` |

- Braze開発者ガイド：分析の無効化  
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/disabling_tracking/)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/disabling_tracking/)

#### SDKの無効化

| リモートコマンド | Brazeメソッド（iOS） | Brazeメソッド（Android） |
|---|---|---|
| `disablesdk` | `enabled` | `disableSdk` |

- Braze開発者ガイド：分析の無効化  
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/disabling_tracking/)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/disabling_tracking/)
#### データの消去

| リモートコマンド | Brazeメソッド |
|---|---|
| `wipedata` | `wipeData` |

- Braze開発者ガイド：分析の無効化  
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/disabling_tracking/)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/disabling_tracking/)

#### 広告トラッキングの有効化構成

| リモートコマンド | Brazeメソッド |
|---|---|
| `setadtrackingenabled` | `set(adTrackingEnabled:)` |

| パラメータ | 型 |
|---|---|
| `ad_tracking_enabled`（必須）| `Bool` |

## Brazeインスタンスへのアクセス（iOS）

リモートコマンドを使用すると、イベントや購入の記録など、Brazeが提供する一部の機能をアプリに簡単にマッピングできます。  
ただし、コンテンツカード、機能フラグ、通知など、一部のBraze機能については、Brazeインスタンスを使用してアプリに統合する必要があります。

Brazeインスタンスに直接アクセスするには、`onReady`メソッドを使用します。`onReady`メソッドは、Brazeインスタンスが正しく構成されると、完了ブロックでそのインスタンスを返します。

```swift
brazeRemoteCommand.onReady { braze in
    // use the Braze instance here
}
```

Brazeインスタンスへの参照を取得したら、Brazeのドキュメントに記載されているとおりに使用してください。

### プッシュ通知の自動統合

最新バージョンのBrazeでは、リモート通知の処理を自動化できます。詳細については、[Braze開発者ガイド：プッシュ通知の自動統合](https://www.braze.com/docs/developer_guide/platform_integration_guides/swift/push_notifications/integration/#automatic-push-integration)を参照してください。

この機能を使用するには、アプリデリゲートの`didFinishLaunchingWithOptions`メソッド内で、メインスレッド上でBrazeインスタンスを同期的に初期化する必要があります。そのため、リモートコマンド構成を使用する代わりに、Brazeインスタンスを直接構成する必要があります。

Brazeインスタンスを直接構成するには、次のコードを使用します。

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    let brazeConfig = Braze.Configuration(apiKey: "YOUR_API_KEY", endpoint: "YOUR_ENDPOINT")
    brazeConfig.push.automation = true
    // ...
    // add all your other configuration here
    // ...
    let brazeInstanceWrapper = BrazeInstance()
    brazeInstanceWrapper.initializeBraze(brazeConfig: brazeConfig)
    let brazeCommand = BrazeRemoteCommand(brazeInstance: brazeInstanceWrapper)
    let tealiumConfig = TealiumConfig(...)
    tealiumConfig.remoteCommands = [brazeCommand]
    // ... 
    // complete tealium initialization
    return true
}
```

### プッシュ通知の手動統合

プッシュ通知の手動統合を実装するには、リモートコマンド構成を維持したまま、Brazeインスタンスに直接アクセスしてプッシュ通知の統合を有効にします。

詳細については、[Braze開発者ガイド：プッシュ通知の手動統合](https://www.braze.com/docs/developer_guide/platform_integration_guides/swift/push_notifications/integration/#manual-push-integration)を参照してください。