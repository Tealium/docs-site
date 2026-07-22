---
title: リモートコマンド：Usabilla
description: AndroidおよびSwift/iOSのUsabillaに対するTealiumリモートコマンド統合。
url: https://docs.tealium.com/ja/platforms/remote-commands/integrations/usabilla/
---
## 要件

* UsabillaのアプリIDとフォームID
* 以下のいずれかのモバイルライブラリ：
  * [Tealium for Android-Kotlin](https://docs.tealium.com/ja/platforms/android-kotlin/) (1.0.0+)
  * [Tealium for Android-Java](https://docs.tealium.com/ja/platforms/android-java/) (Usabilla 1.0.0+の場合は5.9.0+、それ以前のバージョンの場合は<5.9.0)
  * [Tealium for iOS-Swift](https://docs.tealium.com/ja/platforms/ios-swift/)
* 以下のいずれかのリモートコマンド統合：
  * [Usabilla Remote Command JSON File](https://docs.tealium.com/ja/platforms/remote-commands/integrations/usabilla/#json-template) (Android-Kotlin 1.0.0+またはiOS-Swift 2.1.0+が必要)
  * Tealium Tag ManagementのUsabilla Remote Commandタグ

## 動作原理

Usabilla統合は3つのアイテムを使用します：

1. UsabillaネイティブSDK
2. Usabillaメソッドをラップするリモートコマンドモジュール
3. イベントトラッキングをネイティブのUsabillaコールに変換するJSON構成ファイルまたはRemote Commandタグ

アプリにUsabillaリモートコマンドモジュールを追加すると、必要なUsabillaライブラリが自動的にインストールされビルドされます。依存関係マネージャーのインストールを使用している場合、Usabilla SDKを別途インストールする必要はありません。

リモートコマンドオプションには2つあります：JSON構成ファイル、またはTag Managementを使用してマッピングを構成します。ベンダー統合には、アプリ内またはリモートでホストされるJSON構成ファイルが推奨されます。Tag Managementを使用する場合は、ベンダー統合のためのRemote Commandタグを追加します。[ベンダー統合についての詳細](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/#vendor-integrations)を学びましょう。

## インストール

### 依存関係マネージャ




1. Xcodeプロジェクトで、**File > Add Packages... > Add Package Dependency**を選択します。
2. リポジトリURLを入力します：`https://github.com/tealium/tealium-ios-usabilla-remote-command`。
3. バージョンルールを構成します。通常は`Up to next major`が推奨されます。現在の`TealiumUsabilla`バージョンがリストに表示されない場合は、Swiftパッケージキャッシュをリセットしてください。
4. インストールする`TealiumUsabilla`モジュールを選択し、そのモジュールをインストールするアプリターゲットを選択します。

プロジェクトに複数のアプリターゲットがあり、`TealiumUsabilla`モジュールを複数のアプリターゲットに追加する必要がある場合は、**Frameworks, Libraries, and Embedded Content**セクションで手動で追加する必要があります。

`TealiumUsabilla`を追加のアプリターゲットにインストールするには：

1. **Project Navigator**でXcodeプロジェクトを選択します。
2. Xcodeプロジェクトで、**TARGETS**セクションの下にあるアプリターゲットを選択します。
3. **General > Frameworks, Libraries & Embedded Content**に移動し、`TealiumUsabilla`モジュールをアプリターゲットに追加します。

Tealium Swiftライブラリから追加のモジュールを追加するには、[Swift Package Manager](https://docs.tealium.com/ja/platforms/ios-swift/install/#swift-package-manager-recommended)の指示に従ってください。




1. Podfileから`tealium-swift`と`pod "Usabilla"`を削除します。`tealium-swift`の依存関係はすでに`TealiumUsabilla`フレームワークに含まれています。

2. Podfileに次の依存関係を追加します：
      ```ruby
      pod "TealiumUsabilla"
      ```  
      `TealiumUsabilla`ポッドには次の`TealiumSwift`依存関係が含まれています：
      ```bash
      'tealium-swift/Core'
      'tealium-swift/TealiumDelegate'
      'tealium-swift/RemoteCommands'
      'tealium-swift/TagManagement'
      ```

3. `TealiumHelper`ファイルおよび`Tealium`クラスまたはUsabillaリモートコマンドにアクセスする他のファイルで`TealiumSwift`および`TealiumUsabilla`モジュールをインポートします。





1. Cartfileから`tealium-swift`を削除します。`tealium-swift`の依存関係はすでに`TealiumUsabilla`フレームワークに含まれています。

2. Cartfileに存在する場合は次の行を削除します：
      ```bash
      github "usabilla/usabilla-u4a-ios-swift-sdk"
      ```

3. Cartfileに次の依存関係を追加します：
      ```bash
      github "tealium/tealium-ios-usabilla-remote-command"
      ```


<blockquote>
Tealium for Swift SDK (バージョン1.6.5+)は、インストール時に`TealiumDelegate`モジュールが含まれている必要があります。
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

2. アプリプロジェクトの`build.gradle`ファイルに次の依存関係を追加して、Tealium-Usabillaリモートコマンドをインポートします：
      ```groovy
      dependencies {
            implementation 'com.tealium.remotecommands:usabilla:1.0.0'
      }
      ```



### 手動インストール




Usabillaリモートコマンドの手動インストールには、[Tealium for Swift](https://docs.tealium.com/ja/platforms/ios-swift/)ライブラリがインストールされている必要があります。iOSプロジェクトのUsabillaリモートコマンドをインストールするには：

1. まだ行っていない場合は、[Usabilla SDK](https://github.com/usabilla/usabilla-u4a-ios-swift-sdk)をインストールします。

2. [Tealium iOS Usabillaリモートコマンド](https://github.com/tealium/tealium-ios-usabilla-remote-command)リポジトリをクローンし、`Sources`フォルダ内のファイルをプロジェクトにドラッグします。

3. [`remoteAPIEnabled`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#remoteapienabled)構成フラグを`true`に構成します。




Usabillaリモートコマンドの手動インストールには、[Tealium for Android (Kotlin)](https://docs.tealium.com/ja/platforms/android-kotlin/install/)または[Tealium for Android (Java)](https://docs.tealium.com/ja/platforms/android-java/install/)がインストールされている必要があります。

AndroidプロジェクトのBranchリモートコマンドをインストールするには：

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

2. `<PROJECT_ROOT>/<MODULE>/libs`に`tealium-usabilla.aar`を追加します。

3. `build.gradle`ファイルにTealiumライブラリの依存関係を追加します：

      ```groovy
      dependencies {
            implementation(name:'tealium-usabilla', ext:'aar')
      }
      ```



## 初期化

すべてのTealiumライブラリにおいて、初期化時にUsabillaリモートコマンドを登録する必要があります。




TealiumのiOS（Swift）ライブラリ用にJSON構成ファイルまたはリモートコマンドタグでリモートコマンドを初期化します：
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
    let usabilla = UsabillaRemoteCommand() 

    // ローカルJSON
    //let usabilla = UsabillaRemoteCommand(type: .local(file: "usabilla"))

    // リモートJSON
    //let usabilla = UsabillaRemoteCommand(type: .remote(url: "https://some.domain.com/usabilla.json"))
    remoteCommands.add(usabilla)
}

```



TealiumのAndroid（Kotlin）ライブラリ用にJSON構成ファイルまたはリモートコマンドタグでリモートコマンドを初期化します：
```kotlin
val config = TealiumConfig(application,
        "ACCOUNT",
        "PROFILE",
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands, Dispatchers.TagManagement));
val usabilla = UsabillaRemoteCommand(TEALIUM_MAIN, config);

var tealium = Tealium.create(TEALIUM_MAIN, config) {

    // Webviewタグ
    remoteCommands?.add(usabilla);

    // ローカルJSON
    //remoteCommands?.add(usabilla, filename = "usabilla.json");

    // リモートJSON
    //remoteCommands?.add(usabilla, remoteUrl = "https://some.domain.com/usabilla.json");
}
```

Usabilla SDKのための追加（オプショナル）[初期化パラメータ](https://github.com/usabilla/usabilla-u4a-android-sdk#initialization)が利用可能です：

- `usabillaHttpClient = null`  
`HttpClient`オブジェクトをオーバーライドし、SDKによって実行されるすべての接続を処理するカスタムクライアントを注入する可能性を提供します。[カスタムHTTPクライアント](https://github.com/usabilla/usabilla-u4a-android-sdk#custom-http-client)についてもっと学びましょう。
- `usabillaReadyCallback = null`  
`UsabillaReadyCallback`オブジェクトをオーバーライドし、初期化プロセスが終了したときに通信するコールバックです。
- `autoFragmentManager = false`  
[パッシブフィードバック](https://github.com/usabilla/usabilla-u4a-android-sdk#passive-feedback)を無効にします（デフォルトでは有効）。パッシブフィードバックは、Androidの`FragmentManager`を最新の状態に保ち、`android.app.Application.ActivityLifecycleCallbacks`を使用して監視する必要があります。
- `autoFeedbackHandler = false`  
パッシブおよび[キャンペーン](https://github.com/usabilla/usabilla-u4a-android-sdk#campaigns)フィードバックフォームのイベントトラッキングの処理を無効にし、送信または却下されたフォームを自動的に削除する機能を無効にします（デフォルトでは有効）。二つの`android.content.BroadcastReceiver`が登録され、パッシブおよびキャンペーン[フィードバックフォームのクロージャ](https://github.com/usabilla/usabilla-u4a-android-sdk#feedback-submission-callback)を処理するUsabillaイベントをリッスンします。

オプショナルパラメータの使用例を以下に示します：
```kotlin
val usabilla = UsabillaRemoteCommand(TEALIUM_MAIN, config,
        usabillaHttpClient = null,
        usabillaReadyCallback = null,
        autoFragmentManager = false,
        autoFeedbackHandler = false);
```




AndroidのJSONリモートコマンドファイル機能はKotlin SDKでのみ利用可能です。TealiumのAndroid（Java）ライブラリ用にリモートコマンドタグを初期化します：
```java
Tealium.Config config = Tealium.Config.create(application, "ACCOUNT", "PROFILE", "ENVIRONMENT");
Tealium teal = Tealium.createInstance(TEALIUM_MAIN, config);

RemoteCommand usabilla = new UsabillaRemoteCommand(TEALIUM_MAIN, config);
teal.addRemoteCommand(usabilla);
```

Usabilla SDKのための追加（オプショナル）[初期化パラメータ](https://github.com/usabilla/usabilla-u4a-android-sdk#initialization)が利用可能です：

- `usabillaHttpClient = null`  
`HttpClient`オブジェクトをオーバーライドし、SDKによって実行されるすべての接続を処理するカスタムクライアントを注入する可能性を提供します。[カスタムHTTPクライアント](https://github.com/usabilla/usabilla-u4a-android-sdk#custom-http-client)についてもっと学びましょう。
- `usabillaReadyCallback = null`  
`UsabillaReadyCallback`オブジェクトをオーバーライドし、初期化プロセスが終了したときに通信するコールバックです。
- `autoFragmentManager = false`  
[パッシブフィードバック](https://github.com/usabilla/usabilla-u4a-android-sdk#passive-feedback)を無効にします（デフォルトでは有効）。パッシブフィードバックは、Androidの`FragmentManager`を最新の状態に保ち、`android.app.Application.ActivityLifecycleCallbacks`を使用して監視する必要があります。
- `autoFeedbackHandler = false`  
パッシブおよび[キャンペーン](https://github.com/usabilla/usabilla-u4a-android-sdk#campaigns)フィードバックフォームのイベントトラッキングの処理を無効にし、送信または却下されたフォームを自動的に削除する機能を無効にします（デフォルトでは有効）。二つの`android.content.BroadcastReceiver`が登録され、パッシブおよびキャンペーン[フィードバックフォームのクロージャ](https://github.com/usabilla/usabilla-u4a-android-sdk#feedback-submission-callback)を処理するUsabillaイベントをリッスンします。

オプショナルパラメータの使用例を以下に示します：
```java
RemoteCommand usabilla = new UsabillaRemoteCommand(TEALIUM_MAIN, config,
        usabillaHttpClient = null,
        usabillaReadyCallback = null,
        autoFragmentManager = false,
        autoFeedbackHandler = false);
```




## JSONテンプレート

[JSON構成ファイル](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/#json-configuration-file)を使用してリモートコマンドを構成する場合は、以下のテンプレートを参照してください。このテンプレートには、標準的なeコマースインストールで使用される一般的なマッピングが含まれています。必要に応じてマッピングを編集してください。

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

## トラック

成功および失敗したフォームのロード、およびパッシブおよびキャンペーンフィードバックフォームの両方について、イベントは自動的にトラッキングされます。

## サポートされているメソッド

Usabillaの各メソッドまたはプロパティにコマンドをマッピングします。Usabillaのメソッドまたはプロパティをトリガーするには、指定された形式で対応するコマンドを渡します。

| リモートコマンド       | Usabillaメソッド/プロパティ |
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
Usabilla SDKはTealium SDKと統合されているため、対応するタグ構成を与えることで、任意のネイティブUsabilla機能をトリガーすることができます。
</blockquote>


### SDKセットアップ


#### 初期化

Usabilla SDKは起動時に自動的に初期化されます。Usabilla APIキーはタグ構成で構成されます。

| リモートコマンド | Usabilla メソッド |
|---|---|
| `initialize`  | `initialize()` |

Usabilla 開発者ガイド: SDKの初期構成

- [iOS](https://github.com/usabilla/usabilla-u4a-ios-swift-sdk#initialization)
- [Android](https://github.com/usabilla/usabilla-u4a-android-sdk#initialization)

#### デバッグ

| リモートコマンド | Usabilla プロパティ |
|---|---|
| `debugenabled`  | `debugEnabled` |

|  パラメータ | タイプ |
|---|---|
|  `debugEnabled` (必須) | Bool |

Usabilla 開発者ガイド: SDKの初期構成

- [iOS](https://github.com/usabilla/usabilla-u4a-ios-swift-sdk#debugmode)  
- [Android](https://github.com/usabilla/usabilla-u4a-android-sdk#debug-mode)

#### キャンペーンの切り替え

| リモートコマンド | Usabilla プロパティ |
| :--- | :---|
| `displaycampaigns`  | `canDisplayCampaigns` |

|  パラメータ | タイプ |
|---|---|
|  `canDisplayCampaigns` (必須) | Bool |

Usabilla 開発者ガイド: キャンペーンの切り替え

- [iOS](https://github.com/usabilla/usabilla-u4a-ios-swift-sdk#campaign-toggling)


<blockquote>
Androidではキャンペーンの切り替えは利用できません
</blockquote>


### ターゲティングオプション

#### イベント送信

|  リモートコマンド | Usabilla メソッド |
|---|---|
| `sendevent`  | `sendEvent()` |

|  パラメータ | タイプ |
|---|---|
|  `event` (必須) | String |

Usabilla 開発者ガイド: ターゲティングオプション

- [iOS](https://github.com/usabilla/usabilla-u4a-ios-swift-sdk#targeting-options)
- [Android](https://github.com/usabilla/usabilla-u4a-android-sdk#targeting-options)

### カスタム変数の構成

|  リモートコマンド | Usabilla プロパティ |
|---|---|
| `setcustomvariable`  | `customVariables` |

|  パラメータ | タイプ |
|----|---|
| `custom.###` (必須) | String |

Usabilla 開発者ガイド: カスタム変数の構成

- [iOS](https://github.com/usabilla/usabilla-u4a-ios-swift-sdk#custom-variables)
- [Android](https://github.com/usabilla/usabilla-u4a-android-sdk#custom-variables)

### フォーム

#### フィードバックフォームの読み込み

|  リモートコマンド | Usabilla メソッド |
|---|---|
| `loadfeedbackform`  | `loadFeedbackForm` |

|  パラメータ | タイプ | 例 |
|----|---|---|
| `formId` (必須) | String |  |
| `fragmentId` (Androidのみ) | Integer | `R.id.activity_main` |

Usabilla 開発者ガイド: フィードバックフォームの読み込み

- [iOS](https://github.com/usabilla/usabilla-u4a-ios-swift-sdk#loading-a-form)
- [Android](https://github.com/usabilla/usabilla-u4a-android-sdk#loading-a-form)

#### フィードバックフォームの事前読み込み

|  リモートコマンド | Usabilla メソッド |
|---|---|
| `preloadfeedbackforms`  | `preloadFeedbackForms` |

|  パラメータ | タイプ |
|----|---|
| `formIds` (必須) | [String] |

Usabilla 開発者ガイド: フィードバックフォームの事前読み込み

- [iOS](https://github.com/usabilla/usabilla-u4a-ios-swift-sdk#preloading-a-form)
- [Android](https://github.com/usabilla/usabilla-u4a-android-sdk#preloading-a-form)

#### キャッシュされたフォームの削除

|  リモートコマンド | Usabilla メソッド |
|---|---|
| `removecachedforms`  | `removeCachedForms` |

Usabilla 開発者ガイド: キャッシュされたフォームの削除

- [iOS](https://github.com/usabilla/usabilla-u4a-ios-swift-sdk#preloading-a-form)
- [Android](https://github.com/usabilla/usabilla-u4a-android-sdk#reset-passive-forms)

#### 自動的に閉じる

| リモートコマンド | Usabilla プロパティ |
|---|---|
| `dismissautomatically`  | `dismissAutomatically` |

|  パラメータ | タイプ |
|---|---|
|  `dismissAutomatically` (必須) | Bool |

Usabilla 開発者ガイド: 手動で閉じる処理

- [iOS](https://github.com/usabilla/usabilla-u4a-ios-swift-sdk#handle-manual-dismiss)
- [Android](https://github.com/usabilla/usabilla-u4a-android-sdk#dismissing-forms)

#### リセット

| リモートコマンド | Usabilla プロパティ |
|---|---|
| `resetcampaigndata`  | `resetCampaignData` |

Usabilla 開発者ガイド: すべてのキャンペーンのリセット

- [iOS](https://github.com/usabilla/usabilla-u4a-ios-swift-sdk#resetting-all-campaigns)
- [Android](https://github.com/usabilla/usabilla-u4a-android-sdk#reset-campaigns-data)