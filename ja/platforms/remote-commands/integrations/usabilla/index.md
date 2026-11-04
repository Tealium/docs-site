---
title: リモートコマンド：Usabilla
description: AndroidおよびSwift/iOS向けのTealiumリモートコマンドによるUsabilla連携。
url: https://docs.tealium.com/ja/platforms/remote-commands/integrations/usabilla/
---
## 要件

* UsabillaアプリIDとフォームID
* 次のいずれかのモバイルライブラリ：
  * [Tealium for Android-Kotlin](https://docs.tealium.com/ja/platforms/android-kotlin/)（1.0.0以降）
  * [Tealium for Android-Java](https://docs.tealium.com/ja/platforms/android-java/)（Usabilla 1.0.0以降の場合は5.9.0以降、以前のバージョンの場合は5.9.0未満）
  * [Tealium for iOS-Swift](https://docs.tealium.com/ja/platforms/ios-swift/)
* 次のいずれかのリモートコマンド連携：
  * [UsabillaリモートコマンドJSONファイル](https://docs.tealium.com/ja/platforms/remote-commands/integrations/usabilla/#json-template)（Android-Kotlin 1.0.0以降またはiOS-Swift 2.1.0以降が必要）
  * タグ管理のUsabillaリモートコマンドタグ

## 仕組み

Usabilla連携では、次の3つの要素を使用します。

1. UsabillaネイティブSDK
2. Usabillaのメソッドをラップするリモートコマンドモジュール
3. イベントトラッキングをUsabillaのネイティブ呼び出しに変換するJSON構成ファイルまたはリモートコマンドタグ

Usabillaリモートコマンドモジュールをアプリに追加すると、必要なUsabillaライブラリが自動的にインストールおよびビルドされます。依存関係マネージャーを使用してインストールする場合、Usabilla SDKを別途インストールする必要はありません。

リモートコマンドには、JSON構成ファイルを使用する方法と、タグ管理を使用してマッピングを構成する方法の2つがあります。ベンダー連携には、リモートでホストするかアプリ内にローカルで配置したJSON構成ファイルを使用することをお勧めします。タグ管理を使用する場合は、ベンダー連携用のリモートコマンドタグを追加します。[ベンダー連携](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/#vendor-integrations)の詳細をご覧ください。

## インストール

### 依存関係マネージャー




1. Xcodeプロジェクトで、**File > Add Packages... > Add Package Dependency**を選択します。
2. リポジトリURLとして`https://github.com/tealium/tealium-ios-usabilla-remote-command`を入力します。
3. バージョンルールを構成します。通常は`Up to next major`をお勧めします。現在の`TealiumUsabilla`バージョンがリストに表示されない場合は、Swiftパッケージのキャッシュをリセットしてください。
4. インストールする`TealiumUsabilla`モジュールを選択し、そのモジュールをインストールするアプリターゲットを選択します。

プロジェクトに複数のアプリターゲットがあり、複数のターゲットで`TealiumUsabilla`モジュールが必要な場合は、**Frameworks, Libraries, and Embedded Content**セクションで手動で追加する必要があります。

追加のアプリターゲットに`TealiumUsabilla`をインストールするには、次の手順を実行します。

1. **Project Navigator**でXcodeプロジェクトを選択します。
2. Xcodeプロジェクトの**TARGETS**セクションでアプリターゲットを選択します。
3. **General > Frameworks, Libraries & Embedded Content**に移動し、`TealiumUsabilla`モジュールを選択してアプリターゲットに追加します。

Tealium Swiftライブラリから追加のモジュールを追加するには、[Swift Package Manager](https://docs.tealium.com/ja/platforms/ios-swift/install/#swift-package-manager-recommended)の手順に従ってください。




1. Podfileに`tealium-swift`および`pod "Usabilla"`がすでに存在する場合は、それらを削除します。`tealium-swift`の依存関係は、すでに`TealiumUsabilla`フレームワークに含まれています。

2. 次の依存関係をPodfileに追加します。  
      ```ruby
      pod "TealiumUsabilla"
      ```  
      `TealiumUsabilla` Podには、次の`TealiumSwift`依存関係が含まれています。  
      ```bash
      'tealium-swift/Core'
      'tealium-swift/TealiumDelegate'
      'tealium-swift/RemoteCommands'
      'tealium-swift/TagManagement'
      ```

3. `TealiumHelper`ファイル、および`Tealium`クラスまたはUsabillaリモートコマンドにアクセスするその他のファイルに、`TealiumSwift`モジュールと`TealiumUsabilla`モジュールをインポートします。





1. Cartfileから`tealium-swift`を削除します。`tealium-swift`の依存関係は、すでに`TealiumUsabilla`フレームワークに含まれています。

2. Cartfileに次の行が存在する場合は削除します。  
      ```bash
      github "usabilla/usabilla-u4a-ios-swift-sdk"
      ```

3. 次の依存関係をCartfileに追加します。  
      ```bash
      github "tealium/tealium-ios-usabilla-remote-command"
      ```


<blockquote>
Tealium for Swift SDK（バージョン1.6.5以降）では、インストールに`TealiumDelegate`モジュールを含める必要があります。
</blockquote>






1. [Tealium for Android（Kotlin）](https://docs.tealium.com/ja/platforms/android-kotlin/install/)または[Tealium for Android（Java）](https://docs.tealium.com/ja/platforms/android-java/install/)をインストールし、まだ追加していない場合は、プロジェクトの最上位の`build.gradle`ファイルにTealium Maven URLを追加します。

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

2. アプリプロジェクトの`build.gradle`ファイルに次の依存関係を追加して、Tealium-Usabillaリモートコマンドをインポートします。  
      ```groovy
      dependencies {
            implementation 'com.tealium.remotecommands:usabilla:1.0.0'
      }
      ```



### 手動インストール




Usabillaリモートコマンドを手動でインストールするには、[Tealium for Swift](https://docs.tealium.com/ja/platforms/ios-swift/)ライブラリがインストールされている必要があります。iOSプロジェクトにUsabillaリモートコマンドをインストールするには、次の手順を実行します。

1. まだインストールしていない場合は、[Usabilla SDK](https://github.com/usabilla/usabilla-u4a-ios-swift-sdk)をインストールします。

2. [Tealium iOS Usabillaリモートコマンド](https://github.com/tealium/tealium-ios-usabilla-remote-command)リポジトリをクローンし、`Sources`フォルダー内のファイルをプロジェクトにドラッグします。

3. [`remoteAPIEnabled`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#remoteapienabled)構成フラグを`true.`に構成します。




Usabillaリモートコマンドを手動でインストールするには、[Tealium for Android（Kotlin）](https://docs.tealium.com/ja/platforms/android-kotlin/install/)または[Tealium for Android（Java）](https://docs.tealium.com/ja/platforms/android-java/install/)がインストールされている必要があります。

AndroidプロジェクトにBranchリモートコマンドをインストールするには、次の手順を実行します。

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

2. `tealium-usabilla.aar`を`<PROJECT_ROOT>/<MODULE>/libs`に追加します。

3. Tealiumライブラリの依存関係を`build.gradle`ファイルに追加します。

      ```groovy
      dependencies {
            implementation(name:'tealium-usabilla', ext:'aar')
      }
      ```



## 初期化

すべての Tealium ライブラリで、初期化時に Usabilla リモートコマンドを登録する必要があります。




JSON 構成ファイルまたは Remote Command タグを使用して、Tealium の iOS（Swift）ライブラリ用リモートコマンドを初期化します。    
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
    let usabilla = UsabillaRemoteCommand() 

    // Local JSON
    //let usabilla = UsabillaRemoteCommand(type: .local(file: "usabilla"))

    // Remote JSON
    //let usabilla = UsabillaRemoteCommand(type: .remote(url: "https://some.domain.com/usabilla.json"))
    remoteCommands.add(usabilla)
}

```



JSON 構成ファイルまたは Remote Command タグを使用して、Tealium の Android（Kotlin）ライブラリ用リモートコマンドを初期化します。
```kotlin
val config = TealiumConfig(application,
        "ACCOUNT",
        "PROFILE",
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands, Dispatchers.TagManagement));
val usabilla = UsabillaRemoteCommand(TEALIUM_MAIN, config);

var tealium = Tealium.create(TEALIUM_MAIN, config) {

    // Webview Tag
    remoteCommands?.add(usabilla);

    // Local JSON
    //remoteCommands?.add(usabilla, filename = "usabilla.json");

    // Remote JSON
    //remoteCommands?.add(usabilla, remoteUrl = "https://some.domain.com/usabilla.json");
}
```

Usabilla SDK では、追加の（オプションの）[初期化パラメータ](https://github.com/usabilla/usabilla-u4a-android-sdk#initialization)を使用できます。

- `usabillaHttpClient = null`  
`HttpClient` オブジェクトをオーバーライドし、SDK が行うすべての接続を処理するカスタムクライアントを挿入できるようにします。詳しくは、[カスタム HTTP クライアント](https://github.com/usabilla/usabilla-u4a-android-sdk#custom-http-client)を参照してください。
- `usabillaReadyCallback = null`  
初期化プロセスの終了を通知するために使用されるコールバックである `UsabillaReadyCallback` オブジェクトをオーバーライドします。
- `autoFragmentManager = false`  
デフォルトで有効になっている[パッシブフィードバック](https://github.com/usabilla/usabilla-u4a-android-sdk#passive-feedback)を無効にします。パッシブフィードバックでは、Android の `FragmentManager` を最新の状態に維持し、`android.app.Application.ActivityLifecycleCallbacks` を使用して監視する必要があります。
- `autoFeedbackHandler = false`  
パッシブおよび[キャンペーン](https://github.com/usabilla/usabilla-u4a-android-sdk#campaigns)のフィードバックフォームに関するイベントトラッキングの処理と、送信または閉じられたフォームの自動削除を無効にします（デフォルトでは有効）。パッシブとキャンペーンの両方の[フィードバックフォームの終了](https://github.com/usabilla/usabilla-u4a-android-sdk#feedback-submission-callback)を処理する Usabilla イベントをリッスンするために、2 つの `android.content.BroadcastReceiver` が登録されます。

次の例は、オプションパラメータの使用方法を示しています。  
```kotlin
val usabilla = UsabillaRemoteCommand(TEALIUM_MAIN, config,
        usabillaHttpClient = null,
        usabillaReadyCallback = null,
        autoFragmentManager = false,
        autoFeedbackHandler = false);
```




Android の JSON Remote Command ファイル機能は、Kotlin SDK でのみ使用できます。Tealium の Android（Java）ライブラリ用 Remote Command タグを初期化します。     
```java
Tealium.Config config = Tealium.Config.create(application, "ACCOUNT", "PROFILE", "ENVIRONMENT");
Tealium teal = Tealium.createInstance(TEALIUM_MAIN, config);

RemoteCommand usabilla = new UsabillaRemoteCommand(TEALIUM_MAIN, config);
teal.addRemoteCommand(usabilla);
```

Usabilla SDK では、追加の（オプションの）[初期化パラメータ](https://github.com/usabilla/usabilla-u4a-android-sdk#initialization)を使用できます。

- `usabillaHttpClient = null`  
`HttpClient` オブジェクトをオーバーライドし、SDK が行うすべての接続を処理するカスタムクライアントを挿入できるようにします。詳しくは、[カスタム HTTP クライアント](https://github.com/usabilla/usabilla-u4a-android-sdk#custom-http-client)を参照してください。
- `usabillaReadyCallback = null`  
初期化プロセスの終了を通知するために使用されるコールバックである `UsabillaReadyCallback` オブジェクトをオーバーライドします。
- `autoFragmentManager = false`  
デフォルトで有効になっている[パッシブフィードバック](https://github.com/usabilla/usabilla-u4a-android-sdk#passive-feedback)を無効にします。パッシブフィードバックでは、Android の `FragmentManager` を最新の状態に維持し、`android.app.Application.ActivityLifecycleCallbacks` を使用して監視する必要があります。
- `autoFeedbackHandler = false`  
パッシブおよび[キャンペーン](https://github.com/usabilla/usabilla-u4a-android-sdk#campaigns)のフィードバックフォームに関するイベントトラッキングの処理と、送信または閉じられたフォームの自動削除を無効にします（デフォルトでは有効）。パッシブとキャンペーンの両方の[フィードバックフォームの終了](https://github.com/usabilla/usabilla-u4a-android-sdk#feedback-submission-callback)を処理する Usabilla イベントをリッスンするために、2 つの `android.content.BroadcastReceiver` が登録されます。

次の例は、オプションパラメータの使用方法を示しています。  
```java
RemoteCommand usabilla = new UsabillaRemoteCommand(TEALIUM_MAIN, config,
        usabillaHttpClient = null,
        usabillaReadyCallback = null,
        autoFragmentManager = false,
        autoFeedbackHandler = false);
```




## JSON テンプレート

[JSON 構成ファイル](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/#json-configuration-file)を使用してリモートコマンドを構成する場合は、次のテンプレートを参照して作業を開始してください。このテンプレートには、標準的な e コマース実装で使用される一般的なマッピングが含まれています。必要に応じてマッピングを編集してください。

```json
{
  "config": {
    "appId": "YOUR_APP_ID",
    "debugEnabled": true
  },
  "mappings": {
      "event_name": "event",
      "display_campaigns": "canDisplayCampaigns",
      "dismiss_automatically": "dismissAutomatically",
      "form_id": "formId",
      "form_ids": "formIds",
      "customer_first_name": "custom.customer_first_name"
},
  "commands": {
    "launch": "initialize",
    "display_campaigns": "candisplaycampaigns",
    "dismiss": "dismissautomatically",
    "button_click": "sendevent",
    "load_form": "loadfeedbackform",
    "set_variables": "setcustomvariable",
    "reset": "resetcampaigndata"
  }
}
```

## トラッキング

フォームの読み込みが成功した場合と失敗した場合、およびパッシブフィードバックフォームとキャンペーンフィードバックフォームの両方について、イベントが自動的にトラッキングされます。

## サポートされているメソッド

各 Usabilla メソッドまたはプロパティにコマンドをマッピングします。Usabilla のメソッドまたはプロパティをトリガーするには、対応するコマンドを指定された形式で渡します。

| リモートコマンド       | Usabilla のメソッド／プロパティ |
| :-- | :-- |
| `initialize`           | `initialize()`           |
| `sendevent`            | `sendEvent()`            |
| `debugenabled`         | `debugEnabled`           |
| `displaycampaigns`     | `canDisplayCampaigns`    |
| `loadfeedbackform`     | `loadFeedbackForm()`     |
| `preloadfeedbackforms` | `preloadFeedbackForms()` |
| `removecachedforms`    | `removeCachedForms()`    |
| `dismissautomatically` | `dismissAutomatically`   |
| `setcustomvariable`    | `customVariables`        |
| `resetcampaigndata`    | `resetCampaignData()`    |


<blockquote>
Since the Usabilla SDK is integrated with the Tealium SDK, you may trigger any native Usabilla functionality given the corresponding tag configuration.
</blockquote>


### SDK のセットアップ
#### 初期化

Usabilla SDK は起動時に自動的に初期化されます。Usabilla API キーはタグ構成で指定します。

| リモートコマンド | Usabilla メソッド |
|---|---|
| `initialize`  | `initialize()` |

Usabilla 開発者ガイド：SDK の初期セットアップ

- [iOS](https://github.com/usabilla/usabilla-u4a-ios-swift-sdk#initialization)
- [Android](https://github.com/usabilla/usabilla-u4a-android-sdk#initialization)

#### デバッグ

| リモートコマンド | Usabilla プロパティ |
|---|---|
| `debugenabled`  | `debugEnabled` |

| パラメーター | 型 |
|---|---|
| `debugEnabled`（必須） | Bool |

Usabilla 開発者ガイド：SDK の初期セットアップ

- [iOS](https://github.com/usabilla/usabilla-u4a-ios-swift-sdk#debugmode)  
- [Android](https://github.com/usabilla/usabilla-u4a-android-sdk#debug-mode)

#### キャンペーンの切り替え

| リモートコマンド | Usabilla プロパティ |
| :--- | :---|
| `displaycampaigns`  | `canDisplayCampaigns` |

| パラメーター | 型 |
|---|---|
| `canDisplayCampaigns`（必須） | Bool |

Usabilla 開発者ガイド：キャンペーンの切り替え

- [iOS](https://github.com/usabilla/usabilla-u4a-ios-swift-sdk#campaign-toggling)


<blockquote>
Campaign toggling is not available for Android
</blockquote>


### ターゲティングオプション

#### イベントの送信

| リモートコマンド | Usabilla メソッド |
|---|---|
| `sendevent`  | `sendEvent()` |

| パラメーター | 型 |
|---|---|
| `event`（必須） | String |

Usabilla 開発者ガイド：ターゲティングオプション

- [iOS](https://github.com/usabilla/usabilla-u4a-ios-swift-sdk#targeting-options)
- [Android](https://github.com/usabilla/usabilla-u4a-android-sdk#targeting-options)

### カスタム変数の構成

| リモートコマンド | Usabilla プロパティ |
|---|---|
| `setcustomvariable`  | `customVariables` |

| パラメーター | 型 |
|----|---|
| `custom.###`（必須） | String |

Usabilla 開発者ガイド：カスタム変数の構成

- [iOS](https://github.com/usabilla/usabilla-u4a-ios-swift-sdk#custom-variables)
- [Android](https://github.com/usabilla/usabilla-u4a-android-sdk#custom-variables)

### フォーム

#### フィードバックフォームの読み込み

| リモートコマンド | Usabilla メソッド |
|---|---|
| `loadfeedbackform`  | `loadFeedbackForm` |

| パラメーター | 型 | 例 |
|----|---|---|
| `formId`（必須） | String |  |
| `fragmentId`（Android のみ） | Integer | `R.id.activity_main` |

Usabilla 開発者ガイド：フィードバックフォームの読み込み

- [iOS](https://github.com/usabilla/usabilla-u4a-ios-swift-sdk#loading-a-form)
- [Android](https://github.com/usabilla/usabilla-u4a-android-sdk#loading-a-form)

#### フィードバックフォームの事前読み込み

| リモートコマンド | Usabilla メソッド |
|---|---|
| `preloadfeedbackforms`  | `preloadFeedbackForms` |

| パラメーター | 型 |
|----|---|
| `formIds`（必須） | [String] |

Usabilla 開発者ガイド：フィードバックフォームの事前読み込み

- [iOS](https://github.com/usabilla/usabilla-u4a-ios-swift-sdk#preloading-a-form)
- [Android](https://github.com/usabilla/usabilla-u4a-android-sdk#preloading-a-form)

#### キャッシュされたフォームの削除

| リモートコマンド | Usabilla メソッド |
|---|---|
| `removecachedforms`  | `removeCachedForms` |

Usabilla 開発者ガイド：キャッシュされたフォームの削除

- [iOS](https://github.com/usabilla/usabilla-u4a-ios-swift-sdk#preloading-a-form)
- [Android](https://github.com/usabilla/usabilla-u4a-android-sdk#reset-passive-forms)

#### 自動的に閉じる

| リモートコマンド | Usabilla プロパティ |
|---|---|
| `dismissautomatically`  | `dismissAutomatically` |

| パラメーター | 型 |
|---|---|
| `dismissAutomatically`（必須） | Bool |

Usabilla 開発者ガイド：手動で閉じる

- [iOS](https://github.com/usabilla/usabilla-u4a-ios-swift-sdk#handle-manual-dismiss)
- [Android](https://github.com/usabilla/usabilla-u4a-android-sdk#dismissing-forms)

#### リセット

| リモートコマンド | Usabilla プロパティ |
|---|---|
| `resetcampaigndata`  | `resetCampaignData` |

Usabilla 開発者ガイド：すべてのキャンペーンのリセット

- [iOS](https://github.com/usabilla/usabilla-u4a-ios-swift-sdk#resetting-all-campaigns)
- [Android](https://github.com/usabilla/usabilla-u4a-android-sdk#reset-campaigns-data)