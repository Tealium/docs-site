---
title: リモートコマンド：Braze
description: AndroidおよびSwift/iOS用BrazeのTealiumリモートコマンド統合。
url: https://docs.tealium.com/ja/platforms/remote-commands/integrations/braze/
---
## 必要条件

* Braze APIキー
* 以下のいずれかのモバイルライブラリ：
  * [Tealium for Android-Kotlin](https://docs.tealium.com/ja/platforms/android-kotlin/) (1.0.0+)
  * [Tealium for Android-Java](https://docs.tealium.com/ja/platforms/android-java/) (Braze 1.0.0+用は5.9.0+、それ以前のバージョン用は<5.9.0)
  * [Tealium for iOS-Swift](https://docs.tealium.com/ja/platforms/ios-swift/) (2.8.0+)
* 以下のいずれかのリモートコマンド統合：
  * [Braze Remote Command JSON File](https://docs.tealium.com/ja/platforms/remote-commands/integrations/braze/#json-template) (Android-Kotlin 1.0.0+またはiOS-Swift 2.1.0+が必要)
  * Tealium Tag Management内のBraze Remote Commandタグ

## 動作原理

Braze統合は以下の項目を使用します：

1. BrazeネイティブSDK。
2. Brazeメソッドをラップするリモートコマンドモジュール。
3. JSON構成ファイルまたはイベントトラッキングをネイティブのBrazeコールに変換するRemote Commandタグのいずれか。

アプリにBrazeリモートコマンドモジュールを追加すると、アプリにベンダー固有のコードを追加することなく、必要なBrazeライブラリが自動的にインストールされてビルドされます。依存関係マネージャーのインストールを使用している場合、Braze SDKを別途インストールする必要はありません。

リモートコマンドオプションには、JSON構成ファイルを使用するか、Tag Managementを使用してマッピングを構成するかの2つがあります。ベンダー統合には、アプリ内またはリモートでホストされるJSON構成ファイルの使用を推奨します。Tag Managementを使用する場合は、ベンダー統合のためのRemote Commandタグを追加します。[ベンダー統合についての詳細はこちら](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/#vendor-integrations)をご覧ください。


## インストール

### 依存関係マネージャ




1. Xcodeプロジェクトで、**File > Add Packages... > Add Package Dependency**を選択します。
2. リポジトリURLを入力します：`https://github.com/tealium/tealium-ios-braze-remote-command`。
3. バージョンルールを構成します。通常は`Up to next major`が推奨されます。現在の`TealiumBraze`バージョンがリストに表示されない場合は、Swiftパッケージキャッシュをリセットしてください。
4. インストールする`TealiumBraze`モジュールを選択し、そのモジュールをインストールしたいアプリターゲットを選択します。

プロジェクトに複数のアプリターゲットがあり、それらのターゲットに`TealiumBraze`モジュールが必要な場合は、**Frameworks, Libraries, and Embedded Content**セクションで手動で追加する必要があります。

追加のアプリターゲットに`TealiumBraze`をインストールするには：

1. **Project Navigator**でXcodeプロジェクトを選択します。
2. Xcodeプロジェクトで、**TARGETS**セクションのアプリターゲットを選択します。
3. **General > Frameworks, Libraries & Embedded Content**に移動し、アプリターゲットに`TealiumBraze`モジュールを追加します。

Tealium Swiftライブラリから追加のモジュールを追加するには、[Swift Package Manager](https://docs.tealium.com/ja/platforms/ios-swift/install/#swift-package-manager-recommended)の指示に従ってください。




1. Podfileから`tealium-swift`と`pod "BrazeKit"`を削除します。`tealium-swift`の依存関係はすでに`TealiumBraze`フレームワークに含まれています。

2. Podfileに次の依存関係を追加します：
      ```ruby
      pod "TealiumBraze"
      ```  
      `TealiumBraze`ポッドには次の`TealiumSwift`依存関係が含まれています：
      ```bash
      'tealium-swift/Core'
      'tealium-swift/RemoteCommands'
      ```

3. `TealiumHelper`ファイルおよび`Tealium`クラスまたはBrazeリモートコマンドにアクセスするその他のファイルで`TealiumSwift`および`TealiumBraze`モジュールをインポートします。





1. Cartfileから`tealium-swift`を削除します。`tealium-swift`の依存関係はすでに`TealiumBraze`フレームワークに含まれています。

2. Cartfileに次の依存関係を追加します：
      ```bash
      github "tealium/tealium-ios-braze-remote-command"
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

2. アプリプロジェクトの`build.gradle`ファイルにBraze SDKとTealium-Brazeリモートコマンドの依存関係を追加します：
      ```groovy
      dependencies {
            implementation 'com.tealium.remotecommands:braze:3.0.0'
            implementation 'com.braze:android-sdk-ui:29.0.1'
      }
      ```



1. React Nativeプロジェクトのルートに移動します。

2. 次のコマンドで`tealium-react-braze`パッケージをダウンロードしてインストールします：
    ```bash
    yarn add tealium-react-braze
    ```
3. NPMパッケージのバージョン1.0.7でReact Native Autolinkingが有効になっており、React Nativeのバージョン0.60+を使用している場合、`react-native link`を実行する必要はありません。



### 手動インストール




Brazeリモートコマンドの手動インストールには、[Tealium for Swift](https://docs.tealium.com/ja/platforms/ios-swift/)ライブラリのインストールが必要です。iOSプロジェクト用のBrazeリモートコマンドをインストールするには：

1. まだ行っていない場合は、[Braze SDK](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/initial_sdk_setup/initial_sdk_setup/)をインストールします。

2. [Tealium iOS Brazeリモートコマンド](https://github.com/tealium/tealium-ios-braze-remote-command)リポジトリをクローンし、`Sources`フォルダ内のファイルをプロジェクトにドラッグします。

3. [`remoteAPIEnabled`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#remoteapienabled)構成フラグを`true`に構成します。




Brazeリモートコマンドの手動インストールには、[Tealium for Android (Kotlin)](https://docs.tealium.com/ja/platforms/android-kotlin/install/)または[Tealium for Android (Java)](https://docs.tealium.com/ja/platforms/android-java/install/)のインストールが必要です。

Androidプロジェクト用のBrazeリモートコマンドをインストールするには：

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

2. `<PROJECT_ROOT>/<MODULE>/libs`に`tealium-braze.aar`を追加します。

3. `build.gradle`ファイルにTealiumライブラリの依存関係を追加します：

      ```groovy
      dependencies {
            implementation(name:'tealium-braze', ext:'aar')
      }
      ```



## 初期化



TealiumのiOS（Swift）ライブラリ用のJSON構成ファイルまたはRemote Commandタグでリモートコマンドを初期化します：
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
    let braze = BrazeRemoteCommand(brazeLocation: BrazeLocationProvider()) 

    // ローカルJSON
    //let braze = BrazeRemoteCommand(type: .local(file: "braze"), brazeLocation: BrazeLocationProvider()) 

    // リモートJSON
    //let braze = BrazeRemoteCommand(type: .remote(url: "https://some.domain.com/braze.json"), brazeLocation: BrazeLocationProvider()) 

    remoteCommands.add(braze)
}
```


TealiumのKotlinライブラリ用のJSON構成ファイルまたはRemote Commandタグでリモートコマンドを初期化します：
```kotlin
val config = TealiumConfig(application,
        "ACCOUNT",
        "PROFILE",
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands, Dispatchers.TagManagement));
// Braze Remote Commandを追加する新しいコード
val braze = BrazeRemoteCommand(application,
                            true,
                            sessionHandlingBlacklist,
                            true,
                            inAppMessageBlacklist)

var tealium = Tealium.create(TEALIUM_MAIN, config) {
    // オプション：Tealium IQのタグでまだサポートされていない構成オプションを構成するか、
    //              ローカルで構成を上書きする。
    braze.registerConfigOverride { builder ->
        // builder.setIsLocationCollectionEnabled(true);
        // builder.setGeofencesEnabled(true);
        // builder.setPushDeepLinkBackStackActivityEnabled(true);
        // builder.setPushDeepLinkBackStackActivityClass(UserActivity.class);
    }

    // コマンドを登録

    // Webviewタグ
    remoteCommands?.add(braze); 

    // ローカルJSON
    //remoteCommands?.add(braze, filename = "braze.json"); 

    // リモートJSON
    //remoteCommands?.add(braze, remoteUrl = "https://some.domain.com/braze.json"); 
}
```


TealiumのAndroid（Java）ライブラリ用のRemote Commandタグでリモートコマンドを初期化します：
```java
import com.tealium.remotecommands.BrazeRemoteCommand;

Tealium.Config config = Tealium.Config.create(application, "ACCOUNT", "PROFILE", "ENVIRONMENT");
Tealium teal = Tealium.createInstance(TEALIUM_MAIN, config);

BrazeRemoteCommand braze;
// デフォルトの構成オプションで初期化。
braze = new BrazeRemoteCommand(config);

// または追加の構成オプションで初期化する場合：
Set<Class> sessionHandlingBlacklist = new HashSet<>();
Set<Class> inAppMessageBlacklist = new HashSet<>();
// sessionHandlingBlacklist.add(MainActivity.class);
// inAppMessageBlacklist.add(UserActivity.class);
braze = new BrazeRemoteCommand(config,
        true,                     // sessionHandlingEnabled
        sessionHandlingBlacklist, // sessionHandlingBlacklist
        true,                     // registerInAppMessageManager
        inAppMessageBlacklist);   // inAppMessageBlackList

// オプション：Tealium IQのタグでまだサポートされていない構成オプションを構成するか、
//              ローカルで構成を上書きする。
braze.registerConfigOverride(new BrazeRemoteCommand.ConfigOverrider() {
    @Override
    public void onOverride(AppboyConfig.Builder b) {
        b.setPushDeepLinkBackStackActivityEnabled(true);
        b.setPushDeepLinkBackStackActivityClass(UserActivity.class);
    }
});

// コマンドを登録
teal.addRemoteCommand(braze);
```

 

React Native用のJSON構成ファイルまたはRemote Commandタグでリモートコマンドを初期化します：
```javascript
import BrazeRemoteCommand from 'tealium-react-braze';
BrazeRemoteCommand.initialize();

// Webviewタグ
let braze = { id: BrazeRemoteCommand.name } 

// ローカルJSON
//let braze = { id: BrazeRemoteCommand.name, path: "braze.json" } 

// リモートJSON
//let braze = { id: BrazeRemoteCommand.name, url: "https://some.domain.com/braze.json" } 

let config = TealiumConfig {
    // ...
    remoteCommands: [braze]
}
```





## JSONテンプレート

[JSON構成ファイル](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/#json-configuration-file)を使用してリモートコマンドを構成する場合は、以下のテンプレートを参照してください。このテンプレートには、標準的なeコマースインストールで使用される一般的なマッピングが含まれています。必要に応じてマッピングを編集してください。

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

各Brazeメソッドにコマンドをマッピングします。Brazeメソッドをトリガーするには、指定された形式で対応するコマンドを渡します。

|リモートコマンド|Brazeメソッド|
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
Braze SDKはTealium SDKと一緒にインストールされているため、対応するタグ構成でネイティブのBraze機能をトリガーできます。
</blockquote>


### SDKのセットアップ

#### 初期化

Braze APIキーとカスタムエンドポイントが必要で、タグ構成で構成する必要があります。

| リモートコマンド | Brazeメソッド (iOS) | Brazeメソッド (Android) |
|---|---|---|
| `initialize` | `Braze(configuration:)` | `configure()` |

以下のマッピングは起動オプションを構成するために使用されます。

| パラメータ | タイプ | 説明 |
|---|---|---|
| `api_key` (必須) |  `String` | APIキーを構成します |
| `custom_endpoint` (必須) |  `String` | カスタムAPIエンドポイントを構成します。この形式で送信されます `sdk.api.braze.eu` |
| `device_options` |  `[String]` | Braze SDKによって収集されるデバイスフィールドのホワイトリスト（デフォルトでは、すべてのフィールドが収集されます）。 |
| `enable_automatic_geofences` | `Bool` | ジオフェンスの自動収集を有効にします（`true` または `false`）。 |
| `enable_automatic_location` | `Bool` | 位置情報の収集を有効にします（`true` または `false`）。 |
| `enable_geofences` | `Bool` | ジオフェンスの収集を有効にします（`true` または `false`）。 |
| `flush_interval` |  `Double` | データフラッシュ間隔を構成します（秒単位）。値はNSTimeIntervalsに変換され、`1.0`より大きくなければなりません。 |
| `is_sdk_authentication_enabled` | `Bool` | SDK認証を有効にします、デフォルトは`false`です。 |
| `push_story_identifier` |  `String` | このキーは、Push Story Notification Content拡張のアプリグループ名を表す文字列値に構成されます。 |
| `request_processing_policy` |  `String` | SDKのリクエスト処理の可能な値（`manual` または `automatic`）。デフォルトは `automatic`です。 |
| `session_timeout` |  `Int` (秒) | セッションタイムアウトは秒単位です（デフォルトは `30` 秒）。 |
| `trigger_interval_seconds` | `Int` (秒) | アプリ内メッセージトリガー間の最小間隔をオーバーライドします（デフォルトは `30` 秒）。 |
| `use_uuid_as_device_id` | `Bool` | (iOS) デバイスIDとしてランダムに生成されたUUIDを使用するかどうかを決定します（デフォルトは `true`）。 |
| `forward_universal_links` | `Bool` | SDKが自動的にユニバーサルリンクを認識し、システムメソッドに転送するかどうかを指定します（デフォルトは `false`）。 |

Android  

- [Braze開発者ガイド: 初期SDKセットアップ](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/initial_sdk_setup/android_sdk_integration/)

iOS  

- [Braze開発者ガイド: 初期SDKセットアップ](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/initial_sdk_setup/#customizing-braze-on-startup)   
- [Braze開発者ガイド: ネットワークトラフィック制御の詳細](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/advanced_use_cases/fine_network_traffic_control/)  
- [Braze開発者ガイド: 位置情報とジオフェンス](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/advanced_use_cases/locations_and_geofences/)  
- [Braze開発者ガイド: Push Storyの構成](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/push_story/)  
- [Braze開発者ガイド: セッションの追跡](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/tracking_sessions/)


#### SDK認証署名の構成

| リモートコマンド | Brazeメソッド (iOS) | Brazeメソッド (Android)
|---|---|---|
| `setsdkauthsignature`| `set(sdkAuthenticationSignature:)` | `setSdkAuthenticationSignature` |

| パラメータ | タイプ |
|---|---|
| `sdk_authentication_signature` | `String` |

#### フラッシュ

| リモートコマンド | Brazeメソッド |
|---|---|
| `flush`| `requestImmediateDataFlush` |


- Braze開発者ガイド: アナリティクスの無効化  
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/advanced_use_cases/fine_network_traffic_control/)
### ユーザートラッキング

#### ユーザーIDの割り当て

| リモートコマンド | Brazeメソッド |
|---|---|
| `useridentifier`  | `changeUser` |

| パラメータ | タイプ |
|---|---|
| `user_id` (必須) | `String` |
| `sdk_authentication_signature` | `String` |


- Braze開発者ガイド: アナリティクス ユーザーID  
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/setting_user_ids/)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/setting_user_ids/#assigning-a-user-id)

#### ユーザーのエイリアス作成

| リモートコマンド | Brazeメソッド |
|---|---|
| `useralias` | `user.add(alias:)` |

| パラメータ | タイプ |
|----|---|
| `user_alias` (必須) | `String` |
| `alias_label` (必須) | `String` |

- Braze開発者ガイド: アナリティクス ユーザーエイリアス     
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/setting_user_ids/#aliasing-users)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/setting_user_ids/#aliasing-users)

### ユーザー属性

#### 標準属性

| イベント | Brazeメソッド |
|---|---|
| userattribute  | `Braze.User`オブジェクトのフィールドを構成 |

|  パラメータ | タイプ |
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

- Braze開発者ガイド: アナリティクス ユーザー属性
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/setting_custom_attributes/#assigning-standard-user-attributes)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/setting_custom_attributes/#assigning-standard-user-attributes)
- [Braze開発者ガイド: ユーザーデータAPI](https://www.braze.com/docs/api/endpoints/user_data/?redirected=true#user-attributes-object-specification)

#### カスタム属性の構成

| リモートコマンド | Brazeメソッド |
|---|---|
| `setcustomattribute` | `user.setCustomAttribute` |


| パラメータ | タイプ |
|---|---|
| `set_custom_attribute.PROPERTY` | `[String: Any]` / `JSONObject` |

- Braze開発者ガイド: アナリティクス カスタム属性  
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/setting_custom_attributes/#assigning-custom-user-attributes)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/setting_custom_attributes/#assigning-custom-user-attributes)
#### カスタム属性の解除

| リモートコマンド | Braze メソッド |
|---|---|
| `setcustomattribute` | `user.unsetCustomAttribute` |

| パラメータ | タイプ |
|---|---|
| `set_custom_attribute.PROPERTY` | `String` |

- Braze 開発者ガイド: アナリティクス カスタム属性  
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/setting_custom_attributes/#unsetting-a-custom-attribute)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/setting_custom_attributes/#assigning-custom-user-attributes)

#### カスタム属性のインクリメント

| リモートコマンド | Braze メソッド |
|---|---|
| `incrementcustomattribute` | `user.incrementCustomUserAttribute`|

| パラメータ | タイプ |
|---|---|
| `increment_custom_attribute.PROPERTY` | `String` |

- Braze 開発者ガイド: アナリティクス 属性のインクリメント
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/setting_custom_attributes/#incrementingdecrementing-custom-attributes)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/setting_custom_attributes/#assigning-custom-user-attributes)

#### カスタム配列属性の構成

| リモートコマンド | Braze メソッド |
|---|---|
| `setcustomarrayattribute` | `user.setCustomAttributeArray` |

| パラメータ | タイプ |
|---|---|
| `set_custom_array_attribute.PROPERTY` | `[String: [Any]]` / `JSONObject` |

- Braze 開発者ガイド: アナリティクス 配列属性  
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/setting_custom_attributes/#custom-attribute-with-an-array-value)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/setting_custom_attributes/#assigning-custom-user-attributes)

#### カスタム配列属性の追加

| リモートコマンド | Braze メソッド |
|---|---|
| `appendcustomarrayattribute` | `user.addToCustomAttributeArray` |

| パラメータ | タイプ |
|---|---|
| `append_custom_array_attribute.PROPERTY` | `[String: String]` / `JSONObject` |

- Braze 開発者ガイド: アナリティクス 配列属性  
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/setting_custom_attributes/#custom-attribute-with-an-array-value)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/setting_custom_attributes/#assigning-custom-user-attributes)

#### カスタム配列属性の削除

| リモートコマンド | Braze メソッド |
|---|---|
| `removecustomarrayattribute`| `user.removeFromCustomAttributeArray`|

| パラメータ | タイプ |
|---|---|
| `remove_custom_array_attribute.PROPERTY` | `[String: String]` / `JSONObject` |

- Braze 開発者ガイド: アナリティクス 配列属性  
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/setting_custom_attributes/#custom-attribute-with-an-array-value)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/setting_custom_attributes/#assigning-custom-user-attributes)

### カスタムイベントトラッキング

#### カスタムイベント

| リモートコマンド | Braze メソッド |
| --- | --- |
| `logcustomevent`  | `logCustomEvent` |

| パラメータ | タイプ |
|--- | --- |
|  `event_name` (必須) | `String` |
|  `event_properties` | `[String: Any]` / `JSONObject` |

- Braze 開発者ガイド: アナリティクス カスタムイベント
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/tracking_custom_events/)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/tracking_custom_events/)

### 通知

#### Eメール通知

| リモートコマンド | Braze メソッド |
|---|---|
| `emailnotification` | `setEmailNotificationSubscriptionType` |

| パラメータ | タイプ | 例 |
|---|---|---|
| `email_notification` | `String`| [`"optedin"`, `"subscribed"`, `"unsubscribed"`]|

- Braze 開発者ガイド: アナリティクス Eメール登録   
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/setting_custom_attributes/#setting-email-subscriptions)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/setting_custom_attributes/#setting-up-user-subscriptions)

#### サブスクリプショングループへの追加

| リモートコマンド | Braze メソッド |
|---|---|
| `addtosubscriptiongroup` | `user.addToSubscriptionGroup(id:)` |

| パラメータ | タイプ |
|---|---|
| `subscription_group_id` (必須) | `String` |

- [Braze 開発者ガイド: サブスクリプショングループ](https://www.braze.com/docs/user_guide/message_building_by_channel/email/managing_user_subscriptions/#updating-email-subscription-states)

#### サブスクリプショングループからの削除

| リモートコマンド | Braze メソッド |
|---|---|
| `removefromsubscriptiongroup` | `user.removeFromSubscriptionGroup(id:)` |

| パラメータ | タイプ |
|---|---|
| `subscription_group_id` (必須) | `String` |

- [Braze 開発者ガイド: サブスクリプショングループ](https://www.braze.com/docs/user_guide/message_building_by_channel/email/managing_user_subscriptions/#updating-email-subscription-states)

#### プッシュ通知

| リモートコマンド | Braze メソッド |
|---|---|
| `pushnotification` | `setPushNotificationSubscriptionType` |

| パラメータ | タイプ | 例 |
|---|---|---|
| `push_notification` | `String`| [`"optedin"`, `"subscribed"`, `"unsubscribed"`]|

- Braze 開発者ガイド: アナリティクス プッシュ通知  
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/setting_custom_attributes/#setting-up-user-subscriptions)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/setting_custom_attributes/#setting-up-user-subscriptions)

### 購入トラッキング

#### 購入ログ

| リモートコマンド | Braze メソッド |
|--- | ---|
| `logpurchase` | `logPurchase`|

| パラメータ | タイプ |
|---|---|
| `product_id` (必須)| `[String]` / `String[]` |
| `product_currency` (必須) | `String` / `String` |
| `price` (必須) | `[Double]` / `Double[]`|
| `product_qty`  | `[Int]` / `Int[]` |
| `purchase_properties` | `[AnyHashable: Any]` / `JSONObject` |

- Braze 開発者ガイド: アナリティクス 購入イベント  
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/logging_purchases/)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/logging_purchases/)

### 位置情報トラッキング

#### ユーザーの最後の既知の位置の構成

| リモートコマンド | Braze メソッド |
|---|---|
| `setlastknownlocation` | `user.setLastKnownLocation` |

| パラメータ | タイプ |
|---|---|
| `latitude` (必須) | `Double` |
| `longitude` (必須) | `Double` |
| `horizontalAccuracy` (必須) | `Double` |
| `altitude`  | `Double` |
| `verticalAccuracy` | `Double` |

- [Braze 開発者ガイド: アナリティクス 位置情報トラッキング](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/location_tracking/#enabling-automatic-location-tracking)

### データプライバシー（同意オプション）

#### SDKの有効化

| リモートコマンド | Braze メソッド (iOS) | Braze メソッド (Android) |
|---|---|---|
| `enablesdk` | `enabled` | `enableSdk` |

- Braze 開発者ガイド: アナリティクス 無効化  
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/disabling_tracking/)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/disabling_tracking/)

#### SDKの無効化

| リモートコマンド | Braze メソッド (iOS) | Braze メソッド (Android) |
|---|---|---|
| `disablesdk` | `enabled` | `disableSdk` |

- Braze 開発者ガイド: アナリティクス 無効化  
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/disabling_tracking/)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/disabling_tracking/)
#### データの消去

| リモートコマンド | Braze メソッド |
|---|---|
|  `wipedata`| `wipeData` |


- Braze 開発者ガイド: アナリティクスの無効化  
  - [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/analytics/disabling_tracking/)
  - [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/analytics/disabling_tracking/)

#### 広告トラッキングの有効化構成

| リモートコマンド | Braze メソッド |
|---|---|
| `setadtrackingenabled` | `set(adTrackingEnabled:)` |

| パラメータ | タイプ |
|---|---|
| `ad_tracking_enabled` (必須)| `Bool` |

## Braze インスタンスへのアクセス (iOS)

リモートコマンドは、イベントや購入のログ記録など、Brazeが提供する機能の一部をアプリにマッピングする便利な方法を提供します。
しかし、コンテンツカード、機能フラグ、通知などのいくつかのBraze機能は、アプリにBrazeインスタンスを使用して統合する必要があります。

Brazeインスタンスに直接アクセスするには、`onReady` メソッドを使用します。`onReady` メソッドは、適切に構成された後に完了ブロックでBrazeインスタンスを返します。

```swift
brazeRemoteCommand.onReady { braze in
    // ここでBrazeインスタンスを使用
}
```

Brazeインスタンスへの参照を取得したら、Brazeのドキュメントに記載されているように使用してください。

### 自動プッシュ統合

最新のBrazeバージョンは、リモート通知の処理を自動化する方法をサポートしています。詳細については、[Braze 開発者ガイド: 自動プッシュ統合](https://www.braze.com/docs/developer_guide/platform_integration_guides/swift/push_notifications/integration/#automatic-push-integration)を参照してください。

この機能を使用するには、アプリデリゲートの `didFinishLaunchingWithOptions` メソッドでメインスレッド上で同期的にBrazeインスタンスを初期化する必要があります。これは、リモートコマンド構成を使用するのではなく、Brazeインスタンスを直接構成する必要があることを意味します。

Brazeインスタンスを直接構成するには、このコードを使用します：

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    let brazeConfig = Braze.Configuration(apiKey: "YOUR_API_KEY", endpoint: "YOUR_ENDPOINT")
    brazeConfig.push.automation = true
    // ...
    // 他のすべての構成をここに追加
    // ...
    let brazeInstanceWrapper = BrazeInstance()
    brazeInstanceWrapper.initializeBraze(brazeConfig: brazeConfig)
    let brazeCommand = BrazeRemoteCommand(brazeInstance: brazeInstanceWrapper)
    let tealiumConfig = TealiumConfig(...)
    tealiumConfig.remoteCommands = [brazeCommand]
    // ... 
    // tealiumの初期化を完了
    return true
}
```

### マニュアルプッシュ統合

マニュアルプッシュ統合を実装するには、リモートコマンド構成を維持し、Brazeインスタンスに直接アクセスしてプッシュ統合を有効にします。

詳細については、[Braze 開発者ガイド: マニュアルプッシュ統合](https://www.braze.com/docs/developer_guide/platform_integration_guides/swift/push_notifications/integration/#manual-push-integration)を参照してください。