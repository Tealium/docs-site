---
title: リモートコマンド：FullStory
description: AndroidおよびSwift/iOS向けのFullStory用Tealiumリモートコマンド統合。
url: https://docs.tealium.com/ja/platforms/remote-commands/integrations/fullstory/
---
## 要件

* 以下のいずれかのモバイルライブラリ：
    * [Tealium for Android-Kotlin](https://docs.tealium.com/ja/platforms/android-kotlin/)（1.0.0以降）
    * [Tealium for Android-Java](https://docs.tealium.com/ja/platforms/android-java/)（FullStory 1.0.0以降の場合は5.9.0以降、以前のバージョンの場合は5.9.0未満）
    * [Tealium for iOS-Swift](https://docs.tealium.com/ja/platforms/ios-swift/)（2.18.0以降）
* 以下のいずれかのリモートコマンド統合：
    * [FullStoryリモートコマンドJSONファイル](https://docs.tealium.com/ja/platforms/remote-commands/integrations/fullstory/#json-template)（Android-Kotlin 1.0.0以降またはiOS-Swift 2.18.0以降が必要）
    * タグ管理の[FullStoryリモートコマンドタグ](https://docs.tealium.com/fullstory-tag/)

## 仕組み

FullStory統合では、次の3つのコンポーネントを使用します。

1. FullStoryネイティブSDK。
1. FullStoryのメソッドをラップするリモートコマンドモジュール。
1. イベントトラッキングをネイティブのFullStory呼び出しに変換する、JSON構成ファイルまたはリモートコマンドタグ。

FullStoryリモートコマンドモジュールをアプリに追加すると、必要なFullStoryライブラリが自動的にインストールおよびビルドされます。依存関係マネージャーを使用してインストールする場合、FullStory SDKを個別にインストールする必要はありません。


<blockquote>
依存関係マネージャーとしてCocoaPodsまたはCarthageを使用している場合は、FullStoryコマンドラインツールを手動でダウンロードし、[ビルドスクリプト](#ios-build-script)として追加する必要があります。
</blockquote>


リモートコマンドには、次の2つのオプションがあります。

* リモートでホストするか、アプリ内にローカルで配置したJSON構成ファイルを使用する（推奨）。
* タグ管理を使用してマッピングを構成し、ベンダー統合用のリモートコマンドタグを追加する。

詳細については、[ベンダー統合](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/#vendor-integrations)を参照してください。

## インストール

### 依存関係マネージャー

次のいずれかの依存関係マネージャーを使用してモジュールをインストールすることをお勧めします。




1. Xcodeプロジェクトで、**File > Add Packages... > Add Package Dependency**を選択します。
1. 次のリポジトリURLを入力します：`https://github.com/tealium/tealium-ios-fullstory-remote-command`。
1. バージョンルールを構成します。`Up to next major`構成をお勧めします。現在の`TealiumFullstory`バージョンが一覧に表示されない場合は、Swiftパッケージのキャッシュをリセットしてください。
1. インストールする`TealiumFullstory`モジュールを選択し、そのモジュールをインストールするアプリターゲットを選択します。

プロジェクトに複数のアプリターゲットがあり、複数のターゲットで`TealiumFullstory`モジュールが必要な場合は、**Frameworks, Libraries, and Embedded Content**セクションで手動で追加する必要があります。

追加のアプリターゲットに`TealiumFullstory`をインストールするには、次の手順を実行します。

1. **Project Navigator**でXcodeプロジェクトを選択します。
1. Xcodeプロジェクトの**TARGETS**セクションでアプリターゲットを選択します。
1. **General > Frameworks, Libraries & Embedded Content**に移動し、`TealiumFullstory`モジュールを選択してアプリターゲットに追加します。

Tealium Swiftライブラリから追加のモジュールを追加するには、[Swift Package Manager](https://docs.tealium.com/ja/platforms/ios-swift/install/#swift-package-manager-recommended)の手順に従ってください。



CocoaPodsを使用してiOS用FullStoryリモートコマンドをインストールするには、次の手順を実行します。

1. Podfileに`tealium-swift`がすでに存在する場合は削除します。`tealium-swift`への依存関係は、すでに`TealiumFullstory`フレームワークに含まれています。
2. 次の依存関係をPodfileに追加します。  
    ```ruby
    pod "TealiumFullstory"
    ```
    `TealiumFullstory` Podには、次の`TealiumSwift`依存関係が含まれています。  
    ```bash
    'tealium-swift/Core'
    'tealium-swift/RemoteCommands'
    'tealium-swift/TagManagement'
    ```
3. `TealiumSwift`および`TealiumFullstory`モジュールを`TealiumHelper`ファイルと、`Tealium`クラスまたはFullStoryリモートコマンドにアクセスするその他のファイルにインポートします。





Carthageを使用してiOS用FullStoryリモートコマンドをインストールするには、次の手順を実行します。

1. Cartfileから`tealium-swift`を削除します。`tealium-swift`への依存関係は、すでに`TealiumFullstory`フレームワークに含まれています。
1. 次の依存関係をCartfileに追加します。
    ```bash
    github "tealium/tealium-ios-fullstory-remote-command"
    ```




Mavenを使用してAndroid用FullStoryリモートコマンドをインストールするには、次の手順を実行します。

1. まだ実行していない場合は、[Tealium for Android（Kotlin）](https://docs.tealium.com/ja/platforms/android-kotlin/install/)または[Tealium for Android（Java）](https://docs.tealium.com/ja/platforms/android-java/install/)をインストールし、Tealium Maven URLをプロジェクトの最上位`build.gradle`ファイルに追加します。
    ```groovy
    allprojects {
        repositories {
            mavenCentral()
            maven {
                url "https://maven.tealiumiq.com/android/releases/"
            }
            maven {
                url "https://maven.fullstory.com"
            }
        }
    }
    ```
2. アプリプロジェクトの`build.gradle`ファイルに次の依存関係を追加し、FullStory SDKとTealium-FullStoryリモートコマンドの両方をインポートします。
    ```groovy
    dependencies {
        implementation 'com.tealium.remotecommands:fullstory:1.1.0'
    }
    ```
3. FullStory Gradleプラグインをアプリ／モジュールの`build.gradle`に追加します。`<PLUGIN PROPERTIES>`を[利用可能なプロパティ](https://help.fullstory.com/hc/en-us/articles/360040596093-Getting-Started-with-Android-Data-Capture#01F5E7XFMG19SNYS77NYETKDMQ)に置き換えます。
    ```groovy
    fullstory {
        <PLUGIN PROPERTIES>
    }
    ```



### 手動インストール（iOS）

FullStoryリモートコマンドを手動でインストールするには、[Tealium for Swift](https://docs.tealium.com/ja/platforms/ios-swift/)ライブラリがインストールされている必要があります。iOSプロジェクトにFullStoryリモートコマンドをインストールするには、次の手順を実行します。

1. まだインストールしていない場合は、[FullStory SDK](https://help.fullstory.com/hc/en-us/articles/360042772333-Getting-Started-with-iOS-Data-Capture)をインストールします。
1. [Tealium iOS FullStoryリモートコマンド](https://github.com/tealium/tealium-ios-fullstory-remote-command)リポジトリをクローンし、`Sources`フォルダー内のファイルをプロジェクトにドラッグします。
1. `Dispatchers.RemoteCommands`をディスパッチャーとして追加します。
1. [`remoteAPIEnabled`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#remoteapienabled)構成フラグを`true`に構成します。

## 初期化

すべてのTealiumライブラリで、初期化時にFullStoryリモートコマンドを登録します。

### Android（Kotlin）

JSON構成ファイルまたはリモートコマンドタグを使用して、TealiumのAndroid（Kotlin）ライブラリのリモートコマンドを初期化します。




次のコードは、ローカルファイルオプションを使用するJSONリモートコマンド機能向けに設計されています。
```kotlin
val config = TealiumConfig(application,
    "ACCOUNT",
    "PROFILE",
    Environment.DEV,
    dispatchers = mutableSetOf(Dispatchers.RemoteCommands));

var tealium = Tealium.create(TEALIUM_MAIN, config) {
    // Initialize FullStory Remote Command
    val fullstoryCommand = FullStoryRemoteCommand()
    // register the command
    remoteCommands?.add(fullstoryCommand, filename = "tealium-fullstory.json")
}
```


次のコードは、リモートコマンドタグ機能向けに設計されています。
```kotlin
val config = TealiumConfig(application,
    "ACCOUNT",
    "PROFILE",
    Environment.DEV,
    dispatchers = mutableSetOf(Dispatchers.RemoteCommands));

var tealium = Tealium.create(TEALIUM_MAIN, config) {
    // Initialize FullStory Remote Command
    val fullstoryCommand = FullStoryRemoteCommand()
    // register the command
    remoteCommands?.add(fullstoryCommand)
}
```


### Android（Java）




Android 向け JSON リモートコマンドファイル機能は、Kotlin SDK でのみ利用できます。



次のコードは、リモートコマンドタグ機能で使用するためのものです。
```java
Tealium.Config config = Tealium.Config.create(application, "ACCOUNT", "PROFILE", "ENVIRONMENT");
Tealium teal = Tealium.createInstance(TEALIUM_MAIN, config);

FullStoryRemoteCommand fullstory = new FullStoryRemoteCommand();

// register the command
teal.addRemoteCommand(fullstory);
```



### iOS（Swift）

Tealium の iOS（Swift）ライブラリでは、JSON 構成ファイルまたはリモートコマンドタグを使用してリモートコマンドを初期化します。




次のコードは、ローカルファイルオプションを使用する JSON リモートコマンド機能で使用するためのものです。
```swift
var tealium : Tealium?
let config = TealiumConfig(account: "ACCOUNT",
    profile: "PROFILE",
    environment: "ENVIRONMENT",
    dataSource: "DATASOURCE",
    options: nil)
config.dispatchers = [Dispatchers.TagManagement, 
Dispatchers.RemoteCommands]
config.remoteAPIEnabled = true // Required to use Remote Commands

tealium = Tealium(config: config) { _ in
    guard let remoteCommands = self.tealium?.remoteCommands else {
        return
    }
    let fullstory = FullstoryRemoteCommand(type: .local(file: "fullstory"))
    remoteCommands.add(fullstory)
}
```



次のコードは、リモートコマンドタグ機能で使用するためのものです。
```swift
var tealium : Tealium?
let config = TealiumConfig(account: "ACCOUNT",
    profile: "PROFILE",
    environment: "ENVIRONMENT",
    dataSource: "DATASOURCE",
    options: nil)
config.dispatchers = [Dispatchers.TagManagement, 
Dispatchers.RemoteCommands]
config.remoteAPIEnabled = true // Required to use Remote Commands

tealium = Tealium(config: config) { _ in
    guard let remoteCommands = self.tealium?.remoteCommands else {
        return
    }
    let fullstory = FullstoryRemoteCommand()
    remoteCommands.add(fullstory)
}

```




## JSON テンプレート

[JSON 構成ファイル](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/#json-configuration-file)を使用してリモートコマンドを構成する場合は、次のテンプレートを参照して開始してください。このテンプレートには、標準的な E コマース実装で使用される一般的なマッピングが含まれています。必要に応じてマッピングを編集してください。

```json
{
  "config": {},
  "mappings": {
    "tealium_event": "event_name",
    "uid": "uid_str",
    "email": "user_variables.email_str",
    "phone": "user_variables.phone_str",
    "cart_id": "event.cart_id_str",
    "product_id": "event.product_id_str",
    "price": "event.price_real",
    "name": "event.name_str",
    "category": "event.categoryProperties"
  },
  "commands": {
    "launch": "logevent",
    "identify_user": "identify",
    "tealiumSampleEvent": "logevent",
    "tealiumSampleEventWithData": "logevent"
  }
}
```

## サポートされるメソッド

各 FullStory メソッドにコマンドをマッピングします。FullStory メソッドをトリガーするには、対応するコマンドを指定された形式で渡します。

| リモートコマンド | FullStory メソッド |
| -----------------| -------------------- |
| `logevent` | `FS.event()` |
| `identify` | `FS.identify()` |
| `setuservariables` | `FS.setUserVars()` |
| `shutdown` | `FS.shutdown()` |
| `restart` | `FS.restart()` |
| `consent` | `FS.consent()` |
| `anonymize` | `FS.anonymize()` |
| `resetidletimer` | `FS.resetIdleTimer()` |
| `log` | `FS.log()` |


<blockquote>
FullStory SDK は Tealium SDK とともにインストールされるため、Tealium FullStory リモートコマンドタグで提供されていない機能であっても、SDK を直接呼び出すことで、FullStory の任意のネイティブ機能をトリガーできます。
</blockquote>


### SDK のセットアップ

#### 初期化

FullStory SDK は起動時に自動的に初期化されます。

FullStory 開発者ガイド：SDK の初期セットアップ

* [モバイルのスタートガイド](https://developer.fullstory.com/mobile/getting-started/) 

### イベントの記録

| リモートコマンド | FullStory メソッド |
| ---------------- | ---------------- |
| `logevent` | `FS.event()` |

| パラメータ | 型 |
| --------- | ---- |
| `event_name`（必須） | 文字列 |
| `event` | マップ |

FullStory 開発者ガイド：イベントの記録

* [Android](https://developer.fullstory.com/mobile/android/capture-events/analytics-events/)
* [iOS](https://developer.fullstory.com/mobile/ios/capture-events/analytics-events/)

### 識別

| リモートコマンド | FullStory メソッド |
| -------------- | ---------------- |
| `identify` | `FS.identify()` |

| パラメータ | 型 |
| --------- | ---- |
| `uid`（必須） | 文字列 |
| `user_variables` | マップ |

FullStory 開発者ガイド：識別

* [Android](https://developer.fullstory.com/mobile/android/identification/identify-users/)
* [iOS](https://developer.fullstory.com/mobile/ios/identification/identify-users/)

### ユーザー変数の構成

| リモートコマンド | FullStory メソッド |
| -------------- | ---------------- |
| `setuservariables` | `FS.setUserVars()` |

| パラメータ | 型 |
| --------- | ---- |
| `user_variables`（必須） | マップ |


<blockquote>
`user_variables` パラメータはキーと値のペアで構成されるオブジェクトを受け取ります。キーは `strings` であり、値にはデータ型を表すサフィックス（例：`_str`、`_int`、`_bool`）がエンリッチメントされます。詳細については、[カスタム API プロパティの構成](https://developer.fullstory.com/mobile/user-identification/set-user-properties/)を参照してください。
</blockquote>


FullStory 開発者ガイド：ユーザー変数の構成

* [Android](https://developer.fullstory.com/mobile/android/identification/set-user-properties/)
* [iOS](https://developer.fullstory.com/mobile/ios/identification/set-user-properties/)

### シャットダウン

| リモートコマンド | FullStory メソッド |
| -------------- | ---------------- |
| `shutdown` | `FS.shutdown()` |

FullStory の記録を停止します。シャットダウン後に記録を再開するには、`restart` を使用します。

FullStory 開発者ガイド：シャットダウン

* [Android](https://developer.fullstory.com/mobile/android/fullcapture/capture-data/)
* [iOS](https://developer.fullstory.com/mobile/ios/fullcapture/capture-data/)

### 再起動

| リモートコマンド | FullStory メソッド |
| -------------- | ---------------- |
| `restart` | `FS.restart()` |

`shutdown` によって停止された FullStory の記録を再開します。

FullStory 開発者ガイド：再起動

* [Android](https://developer.fullstory.com/mobile/android/fullcapture/capture-data/)
* [iOS](https://developer.fullstory.com/mobile/ios/fullcapture/capture-data/)

### 同意

| リモートコマンド | FullStory メソッド |
| -------------- | ---------------- |
| `consent` | `FS.consent()` |

| パラメータ | 型 |
| --------- | ---- |
| `consent_granted`（必須） | ブール値 |

FullStory のセッション記録に対するユーザーの同意を許可または取り消します。

FullStory 開発者ガイド：同意

* [Android](https://developer.fullstory.com/mobile/android/fullcapture/user-consent/)
* [iOS](https://developer.fullstory.com/mobile/ios/fullcapture/user-consent/)

### 匿名化

| リモートコマンド | FullStory メソッド |
| -------------- | ---------------- |
| `anonymize` | `FS.anonymize()` |

現在のユーザーセッションを匿名化し、以前に構成されたユーザー識別情報をすべて削除します。

FullStory 開発者ガイド：匿名化

* [Android](https://developer.fullstory.com/mobile/android/identification/anonymize-users/)
* [iOS](https://developer.fullstory.com/mobile/ios/identification/anonymize-users/)

### アイドルタイマーのリセット

| リモートコマンド | FullStory メソッド |
| -------------- | ---------------- |
| `resetidletimer` | `FS.resetIdleTimer()` |

FullStory のアイドルタイムアウトタイマーをリセットし、現在のセッションを延長します。

FullStory 開発者ガイド：アイドルタイマーのリセット

* [Android](https://developer.fullstory.com/mobile/android/fullcapture/reset-idle-timer/)
* [iOS](https://developer.fullstory.com/mobile/ios/fullcapture/reset-idle-timer/)
### ログ

| リモートコマンド | FullStory メソッド |
| -------------- | ---------------- |
| `log` | `FS.log()` |

| パラメーター | 型 |
| --------- | ---- |
| `log_level`（必須） | 文字列 |
| `log_message`（必須） | 文字列 |

指定されたレベルでメッセージをログに記録します。使用できる `log_level` の値はプラットフォームによって異なります。

| プラットフォーム | 使用できる値 |
| -------- | --------------- |
| Android | `log`、`error`、`warn`/`warning`、`info`、`debug` |
| iOS | `assert`、`error`、`warning`、`info`、`debug` |

FullStory 開発者ガイド：ログ

* [Android](https://developer.fullstory.com/mobile/android/fullcapture/logging/)
* [iOS](https://developer.fullstory.com/mobile/ios/fullcapture/logging/)