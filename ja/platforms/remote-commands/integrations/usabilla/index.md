---
title: リモートコマンド：Usabilla
description: AndroidおよびSwift/iOSのUsabillaに対するTealiumリモートコマンド統合。
url: https://docs.tealium.com/ja/platforms/remote-commands/integrations/usabilla/
---
## 要件

* UsabillaのアプリIDとフォームID
* 以下のいずれかのモバイルライブラリ：
  * [Tealium for Android-Kotlin](/ja/platforms/android-kotlin/) (1.0.0&#43;)
  * [Tealium for Android-Java](/ja/platforms/android-java/) (Usabilla 1.0.0&#43;の場合は5.9.0&#43;、それ以前のバージョンの場合は&lt;5.9.0)
  * [Tealium for iOS-Swift](/ja/platforms/ios-swift/)
* 以下のいずれかのリモートコマンド統合：
  * [Usabilla Remote Command JSON File](/ja/platforms/remote-commands/integrations/usabilla/#json-template) (Android-Kotlin 1.0.0&#43;またはiOS-Swift 2.1.0&#43;が必要)
  * Tealium Tag ManagementのUsabilla Remote Commandタグ

## 動作原理

Usabilla統合は3つのアイテムを使用します：

1. UsabillaネイティブSDK
2. Usabillaメソッドをラップするリモートコマンドモジュール
3. イベントトラッキングをネイティブのUsabillaコールに変換するJSON構成ファイルまたはRemote Commandタグ

アプリにUsabillaリモートコマンドモジュールを追加すると、必要なUsabillaライブラリが自動的にインストールされビルドされます。依存関係マネージャーのインストールを使用している場合、Usabilla SDKを別途インストールする必要はありません。

リモートコマンドオプションには2つあります：JSON構成ファイル、またはTag Managementを使用してマッピングを構成します。ベンダー統合には、アプリ内またはリモートでホストされるJSON構成ファイルが推奨されます。Tag Managementを使用する場合は、ベンダー統合のためのRemote Commandタグを追加します。[ベンダー統合についての詳細](/ja/platforms/remote-commands/how-it-works/#vendor-integrations)を学びましょう。

## インストール

### 依存関係マネージャ




1. Xcodeプロジェクトで、**File &gt; Add Packages... &gt; Add Package Dependency**を選択します。
2. リポジトリURLを入力します：`https://github.com/tealium/tealium-ios-usabilla-remote-command`。
3. バージョンルールを構成します。通常は`Up to next major`が推奨されます。現在の`TealiumUsabilla`バージョンがリストに表示されない場合は、Swiftパッケージキャッシュをリセットしてください。
4. インストールする`TealiumUsabilla`モジュールを選択し、そのモジュールをインストールするアプリターゲットを選択します。

プロジェクトに複数のアプリターゲットがあり、`TealiumUsabilla`モジュールを複数のアプリターゲットに追加する必要がある場合は、**Frameworks, Libraries, and Embedded Content**セクションで手動で追加する必要があります。

`TealiumUsabilla`を追加のアプリターゲットにインストールするには：

1. **Project Navigator**でXcodeプロジェクトを選択します。
2. Xcodeプロジェクトで、**TARGETS**セクションの下にあるアプリターゲットを選択します。
3. **General &gt; Frameworks, Libraries &amp; Embedded Content**に移動し、`TealiumUsabilla`モジュールをアプリターゲットに追加します。

Tealium Swiftライブラリから追加のモジュールを追加するには、[Swift Package Manager](/ja/platforms/ios-swift/install/#swift-package-manager-recommended)の指示に従ってください。




1. Podfileから`tealium-swift`と`pod &#34;Usabilla&#34;`を削除します。`tealium-swift`の依存関係はすでに`TealiumUsabilla`フレームワークに含まれています。

2. Podfileに次の依存関係を追加します：
      ```ruby
      pod &#34;TealiumUsabilla&#34;
      ```  
      `TealiumUsabilla`ポッドには次の`TealiumSwift`依存関係が含まれています：
      ```bash
      &#39;tealium-swift/Core&#39;
      &#39;tealium-swift/TealiumDelegate&#39;
      &#39;tealium-swift/RemoteCommands&#39;
      &#39;tealium-swift/TagManagement&#39;
      ```

3. `TealiumHelper`ファイルおよび`Tealium`クラスまたはUsabillaリモートコマンドにアクセスする他のファイルで`TealiumSwift`および`TealiumUsabilla`モジュールをインポートします。





1. Cartfileから`tealium-swift`を削除します。`tealium-swift`の依存関係はすでに`TealiumUsabilla`フレームワークに含まれています。

2. Cartfileに存在する場合は次の行を削除します：
      ```bash
      github &#34;usabilla/usabilla-u4a-ios-swift-sdk&#34;
      ```

3. Cartfileに次の依存関係を追加します：
      ```bash
      github &#34;tealium/tealium-ios-usabilla-remote-command&#34;
      ```

Tealium for Swift SDK (バージョン1.6.5&#43;)は、インストール時に`TealiumDelegate`モジュールが含まれている必要があります。





1. まだ行っていない場合は、[Tealium for Android (Kotlin)](/ja/platforms/android-kotlin/install/)または[Tealium for Android (Java)](/ja/platforms/android-java/install/)をインストールし、プロジェクトのトップレベルの`build.gradle`ファイルにTealium Maven URLを追加します。

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

2. アプリプロジェクトの`build.gradle`ファイルに次の依存関係を追加して、Tealium-Usabillaリモートコマンドをインポートします：
      ```groovy
      dependencies {
            implementation &#39;com.tealium.remotecommands:usabilla:1.0.0&#39;
      }
      ```



### 手動インストール




Usabillaリモートコマンドの手動インストールには、[Tealium for Swift](/ja/platforms/ios-swift/)ライブラリがインストールされている必要があります。iOSプロジェクトのUsabillaリモートコマンドをインストールするには：

1. まだ行っていない場合は、[Usabilla SDK](https://github.com/usabilla/usabilla-u4a-ios-swift-sdk)をインストールします。

2. [Tealium iOS Usabillaリモートコマンド](https://github.com/tealium/tealium-ios-usabilla-remote-command)リポジトリをクローンし、`Sources`フォルダ内のファイルをプロジェクトにドラッグします。

3. [`remoteAPIEnabled`](/ja/platforms/ios-swift/api/tealium-config/#remoteapienabled)構成フラグを`true`に構成します。




Usabillaリモートコマンドの手動インストールには、[Tealium for Android (Kotlin)](/ja/platforms/android-kotlin/install/)または[Tealium for Android (Java)](/ja/platforms/android-java/install/)がインストールされている必要があります。

AndroidプロジェクトのBranchリモートコマンドをインストールするには：

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

2. `&lt;PROJECT_ROOT&gt;/&lt;MODULE&gt;/libs`に`tealium-usabilla.aar`を追加します。

3. `build.gradle`ファイルにTealiumライブラリの依存関係を追加します：

      ```groovy
      dependencies {
            implementation(name:&#39;tealium-usabilla&#39;, ext:&#39;aar&#39;)
      }
      ```



## 初期化

すべてのTealiumライブラリにおいて、初期化時にUsabillaリモートコマンドを登録する必要があります。




TealiumのiOS（Swift）ライブラリ用にJSON構成ファイルまたはリモートコマンドタグでリモートコマンドを初期化します：
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
    let usabilla = UsabillaRemoteCommand() 

    // ローカルJSON
    //let usabilla = UsabillaRemoteCommand(type: .local(file: &#34;usabilla&#34;))

    // リモートJSON
    //let usabilla = UsabillaRemoteCommand(type: .remote(url: &#34;https://some.domain.com/usabilla.json&#34;))
    remoteCommands.add(usabilla)
}

```



TealiumのAndroid（Kotlin）ライブラリ用にJSON構成ファイルまたはリモートコマンドタグでリモートコマンドを初期化します：
```kotlin
val config = TealiumConfig(application,
        &#34;ACCOUNT&#34;,
        &#34;PROFILE&#34;,
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands, Dispatchers.TagManagement));
val usabilla = UsabillaRemoteCommand(TEALIUM_MAIN, config);

var tealium = Tealium.create(TEALIUM_MAIN, config) {

    // Webviewタグ
    remoteCommands?.add(usabilla);

    // ローカルJSON
    //remoteCommands?.add(usabilla, filename = &#34;usabilla.json&#34;);

    // リモートJSON
    //remoteCommands?.add(usabilla, remoteUrl = &#34;https://some.domain.com/usabilla.json&#34;);
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
Tealium.Config config = Tealium.Config.create(application, &#34;ACCOUNT&#34;, &#34;PROFILE&#34;, &#34;ENVIRONMENT&#34;);
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

[JSON構成ファイル](/ja/platforms/remote-commands/how-it-works/#json-configuration-file)を使用してリモートコマンドを構成する場合は、以下のテンプレートを参照してください。このテンプレートには、標準的なeコマースインストールで使用される一般的なマッピングが含まれています。必要に応じてマッピングを編集してください。

```json
{
  &#34;config&#34;: {
    &#34;appId&#34;: &#34;YOUR_APP_ID&#34;,
    &#34;debugEnabled&#34;: true
  },
  &#34;mappings&#34;: {
      &#34;event_name&#34;: &#34;event&#34;,
      &#34;display_campaigns&#34;: &#34;canDisplayCampaigns&#34;,
      &#34;dismiss_automatically&#34;: &#34;dismissAutomatically&#34;,
      &#34;form_id&#34;: &#34;formId&#34;,
      &#34;form_ids&#34;: &#34;formIds&#34;,
      &#34;customer_first_name&#34;: &#34;custom.customer_first_name&#34;
},
  &#34;commands&#34;: {
    &#34;launch&#34;: &#34;initialize&#34;,
    &#34;display_campaigns&#34;: &#34;candisplaycampaigns&#34;,
    &#34;dismiss&#34;: &#34;dismissautomatically&#34;,
    &#34;button_click&#34;: &#34;sendevent&#34;,
    &#34;load_form&#34;: &#34;loadfeedbackform&#34;,
    &#34;set_variables&#34;: &#34;setcustomvariable&#34;,
    &#34;reset&#34;: &#34;resetcampaigndata&#34;
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

Usabilla SDKはTealium SDKと統合されているため、対応するタグ構成を与えることで、任意のネイティブUsabilla機能をトリガーすることができます。

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

Androidではキャンペーンの切り替えは利用できません

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