---
title: リモートコマンド：FullStory
description: AndroidおよびSwift/iOS用FullStoryのTealiumリモートコマンド統合
url: https://docs.tealium.com/ja/platforms/remote-commands/integrations/fullstory/
---
## 必要条件

* 以下のいずれかのモバイルライブラリ：
    * [Tealium for Android-Kotlin](/ja/platforms/android-kotlin/) (1.0.0&#43;)
    * [Tealium for Android-Java](/ja/platforms/android-java/) (FullStory 1.0.0&#43;の場合は5.9.0&#43;、それ以前のバージョンの場合は&lt;5.9.0)
    * [Tealium for iOS-Swift](/ja/platforms/ios-swift/) (2.18.0&#43;)
* 以下のいずれかのリモートコマンド統合：
    * [FullStory Remote Command JSON File](/ja/platforms/remote-commands/integrations/fullstory/#json-template) (Android-Kotlin 1.0.0&#43;またはiOS-Swift 2.18.0&#43;が必要)
    * Tealium iQタグ管理内の[FullStory Remote Command tag]()

## 動作原理

FullStory統合は3つのコンポーネントを使用します：

1. FullStoryネイティブSDK。
1. FullStoryメソッドをラップするリモートコマンドモジュール。
1. イベントトラッキングをネイティブFullStoryコールに変換するJSON構成ファイルまたはRemote Commandタグ。

アプリにFullStoryリモートコマンドモジュールを追加すると、必要なFullStoryライブラリが自動的にインストールされビルドされます。依存関係マネージャーのインストールを使用している場合、FullStory SDKを別途インストールする必要はありません。

依存関係マネージャーとしてCocoaPodsまたはCarthageを使用している場合は、[ビルドスクリプト](#ios-build-script)として追加できるようにFullStoryコマンドラインツールを手動でダウンロードする必要があります。

リモートコマンドのオプションは2つあります：

* JSON構成ファイルを使用する（推奨）、リモートまたはアプリ内にローカルでホストされます。
* iQタグ管理を使用してマッピングを構成し、ベンダー統合のRemote Commandタグを追加します。

詳細については、[ベンダー統合](/ja/platforms/remote-commands/how-it-works/#vendor-integrations)を参照してください。

## インストール

### 依存関係マネージャー

モジュールのインストールには、以下の依存関係マネージャーのいずれかを使用することをお勧めします：




1. Xcodeプロジェクトで、**File &gt; Add Packages... &gt; Add Package Dependency**を選択します。
1. 次のリポジトリURLを入力します：`https://github.com/tealium/tealium-ios-fullstory-remote-command`。
1. バージョンルールを構成します。`Up to next major`構成を推奨します。現在の`TealiumFullstory`バージョンがリストに表示されない場合は、Swiftパッケージキャッシュをリセットしてください。
1. インストールする`TealiumFullstory`モジュールを選択し、モジュールをインストールするアプリターゲットを選択します。

プロジェクトに複数のアプリターゲットがあり、`TealiumFullstory`モジュールを複数のアプリターゲットに追加する必要がある場合は、**Frameworks, Libraries, and Embedded Content**セクションで手動で追加する必要があります。

追加のアプリターゲットに`TealiumFullstory`をインストールするには：

1. **Project Navigator**でXcodeプロジェクトを選択します。
1. Xcodeプロジェクトで、**TARGETS**セクションのアプリターゲットを選択します。
1. **General &gt; Frameworks, Libraries &amp; Embedded Content**に移動し、`TealiumFullstory`モジュールをアプリターゲットに追加します。

Tealium Swiftライブラリから追加のモジュールを追加するには、[Swift Package Manager](/ja/platforms/ios-swift/install/#swift-package-manager-recommended)の指示に従ってください。



iOS用のFullStoryリモートコマンドをCocoaPodsを使用してインストールするには：

1. Podfileにすでに存在する場合は`tealium-swift`を削除します。`tealium-swift`の依存関係は、すでに`TealiumFullstory`フレームワークに含まれています。
2. Podfileに次の依存関係を追加します：
    ```ruby
    pod &#34;TealiumFullstory&#34;
    ```
    `TealiumFullstory`ポッドには、次の`TealiumSwift`依存関係が含まれています：
    ```bash
    &#39;tealium-swift/Core&#39;
    &#39;tealium-swift/RemoteCommands&#39;
    &#39;tealium-swift/TagManagement&#39;
    ```
3. `TealiumHelper`ファイルおよび`Tealium`クラスまたはFullStory Remote Commandにアクセスする他のファイルに`TealiumSwift`および`TealiumFullstory`モジュールをインポートします。





iOS用のFullStoryリモートコマンドをCarthageを使用してインストールするには：

1. Cartfileから`tealium-swift`を削除します。`tealium-swift`の依存関係は、すでに`TealiumFullstory`フレームワークに含まれています。
1. Cartfileに次の依存関係を追加します：
    ```bash
    github &#34;tealium/tealium-ios-fullstory-remote-command&#34;
    ```




Android用のFullStoryリモートコマンドをMavenを使用してインストールするには：

1. まだ行っていない場合は、[Tealium for Android (Kotlin)](/ja/platforms/android-kotlin/install/)または[Tealium for Android (Java)](/ja/platforms/android-java/install/)をインストールし、プロジェクトのトップレベルの`build.gradle`ファイルにTealium Maven URLを追加します。
    ```groovy
    allprojects {
        repositories {
            mavenCentral()
            maven {
                url &#34;https://maven.tealiumiq.com/android/releases/&#34;
            }
            maven {
                url &#34;https://maven.fullstory.com&#34;
            }
        }
    }
    ```
2. アプリプロジェクトの`build.gradle`ファイルに次の依存関係を追加することで、FullStory SDKとTealium-FullStoryリモートコマンドの両方をインポートします：
    ```groovy
    dependencies {
        implementation &#39;com.tealium.remotecommands:fullstory:1.1.0&#39;
    }
    ```
3. App/Moduleの`build.gradle`にFullStory gradleプラグインを追加します。`&lt;PLUGIN PROPERTIES&gt;`を[利用可能なプロパティ](https://help.fullstory.com/hc/en-us/articles/360040596093-Getting-Started-with-Android-Data-Capture#01F5E7XFMG19SNYS77NYETKDMQ)で置き換えます：
    ```groovy
    fullstory {
        &lt;PLUGIN PROPERTIES&gt;
    }
    ```



### マニュアルインストール（iOS）

iOS用のFullStoryリモートコマンドのマニュアルインストールには、[Tealium for Swift](/ja/platforms/ios-swift/)ライブラリがインストールされている必要があります。iOSプロジェクト用のFullStoryリモートコマンドをインストールするには：

1. まだ行っていない場合は、[FullStory SDK](https://help.fullstory.com/hc/en-us/articles/360042772333-Getting-Started-with-iOS-Data-Capture)をインストールします。
1. [Tealium iOS FullStoryリモートコマンド](https://github.com/tealium/tealium-ios-fullstory-remote-command)リポジトリをクローンし、`Sources`フォルダ内のファイルをプロジェクトにドラッグします。
1. `Dispatchers.RemoteCommands`をディスパッチャーとして追加します。
1. [`remoteAPIEnabled`](/ja/platforms/ios-swift/api/tealium-config/#remoteapienabled)構成フラグを`true`に構成します。

## 初期化

すべてのTealiumライブラリについて、初期化時にFullStoryリモートコマンドを登録します。

### Android (Kotlin)

TealiumのAndroid (Kotlin)ライブラリ用に、JSON構成ファイルまたはRemote Commandタグを使用してリモートコマンドを初期化します。




次のコードは、ローカルファイルオプションを使用するJSON Remote Commands機能用に設計されています：
```kotlin
val config = TealiumConfig(application,
    &#34;ACCOUNT&#34;,
    &#34;PROFILE&#34;,
    Environment.DEV,
    dispatchers = mutableSetOf(Dispatchers.RemoteCommands));

var tealium = Tealium.create(TEALIUM_MAIN, config) {
    // FullStory Remote Commandを初期化
    val fullstoryCommand = FullStoryRemoteCommand()
    // コマンドを登録
    remoteCommands?.add(fullstoryCommand, filename = &#34;tealium-fullstory.json&#34;)
}
```


次のコードは、Remote Commandタグ機能を使用するために設計されています：
```kotlin
val config = TealiumConfig(application,
    &#34;ACCOUNT&#34;,
    &#34;PROFILE&#34;,
    Environment.DEV,
    dispatchers = mutableSetOf(Dispatchers.RemoteCommands));

var tealium = Tealium.create(TEALIUM_MAIN, config) {
    // FullStory Remote Commandを初期化
    val fullstoryCommand = FullStoryRemoteCommand()
    // コマンドを登録
    remoteCommands?.add(fullstoryCommand)
}
```


### Android (Java)




Android用のJSON Remote Commandファイル機能は、Kotlin SDKでのみ利用可能です。



以下のコードは、Remote Commandタグ機能で使用するために設計されています：
```java
Tealium.Config config = Tealium.Config.create(application, &#34;ACCOUNT&#34;, &#34;PROFILE&#34;, &#34;ENVIRONMENT&#34;);
Tealium teal = Tealium.createInstance(TEALIUM_MAIN, config);

FullStoryRemoteCommand fullstory = new FullStoryRemoteCommand();

// コマンドを登録
teal.addRemoteCommand(fullstory);
```



### iOS (Swift)

TealiumのiOS (Swift)ライブラリでJSON構成ファイルまたはRemote Commandタグを使用してリモートコマンドを初期化します。




以下のコードは、JSON Remote Commands機能で使用するために設計されており、ローカルファイルオプションを使用します：
```swift
var tealium : Tealium?
let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
    profile: &#34;PROFILE&#34;,
    environment: &#34;ENVIRONMENT&#34;,
    dataSource: &#34;DATASOURCE&#34;,
    options: nil)
config.dispatchers = [Dispatchers.TagManagement, 
Dispatchers.RemoteCommands]
config.remoteAPIEnabled = true // Remote Commandsを使用するために必要

tealium = Tealium(config: config) { _ in
    guard let remoteCommands = self.tealium?.remoteCommands else {
        return
    }
    let fullstory = FullstoryRemoteCommand(type: .local(file: &#34;fullstory&#34;))
    remoteCommands.add(fullstory)
}
```



以下のコードは、Remote Commandタグ機能で使用するために設計されています：
```swift
var tealium : Tealium?
let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
    profile: &#34;PROFILE&#34;,
    environment: &#34;ENVIRONMENT&#34;,
    dataSource: &#34;DATASOURCE&#34;,
    options: nil)
config.dispatchers = [Dispatchers.TagManagement, 
Dispatchers.RemoteCommands]
config.remoteAPIEnabled = true // Remote Commandsを使用するために必要

tealium = Tealium(config: config) { _ in
    guard let remoteCommands = self.tealium?.remoteCommands else {
        return
    }
    let fullstory = FullstoryRemoteCommand()
    remoteCommands.add(fullstory)
}

```




## JSONテンプレート

[JSON構成ファイル](/ja/platforms/remote-commands/how-it-works/#json-configuration-file)を使用してリモートコマンドを構成する場合は、以下のテンプレートを参照してください。このテンプレートには、標準的なeコマースインストールで使用される一般的なマッピングが含まれています。必要に応じてマッピングを編集してください。

```json
{
  &#34;config&#34;: {},
  &#34;mappings&#34;: {
    &#34;tealium_event&#34;: &#34;event_name&#34;,
    &#34;uid&#34;: &#34;uid_str&#34;,
    &#34;email&#34;: &#34;user_variables.email_str&#34;,
    &#34;phone&#34;: &#34;user_variables.phone_str&#34;,
    &#34;cart_id&#34;: &#34;event.cart_id_str&#34;,
    &#34;product_id&#34;: &#34;event.product_id_str&#34;,
    &#34;price&#34;: &#34;event.price_real&#34;,
    &#34;name&#34;: &#34;event.name_str&#34;,
    &#34;category&#34;: &#34;event.categoryProperties&#34;
  },
  &#34;commands&#34;: {
    &#34;launch&#34;: &#34;logevent&#34;,
    &#34;identify_user&#34;: &#34;identify&#34;,
    &#34;tealiumSampleEvent&#34;: &#34;logevent&#34;,
    &#34;tealiumSampleEventWithData&#34;: &#34;logevent&#34;
  }
}
```

## サポートされているメソッド

各FullStoryメソッドにコマンドをマッピングします。特定の形式で対応するコマンドを渡すことで、FullStoryメソッドをトリガーできます。

| Remote Command | FullStory Method |
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

FullStory SDKはTealium SDKと一緒にインストールされているため、Tealium FullStory Remote Commandタグによって提供されていない機能であっても、SDKを直接呼び出すことで任意のネイティブFullStory機能をトリガーできます。

### SDKセットアップ

#### 初期化

FullStory SDKは起動時に自動的に初期化されます。

FullStory開発者ガイド：初期SDKセットアップ

* [モバイルの開始](https://developer.fullstory.com/mobile/getting-started/) 

### ログイベント

| Remote Command | FullStory Method |
| ---------------- | ---------------- |
| `logevent` | `FS.event()` |

| パラメータ | タイプ |
| --------- | ---- |
| `event_name` (必須) | 文字列 |
| `event` | マップ |

FullStory開発者ガイド：ログイベント

* [Android](https://developer.fullstory.com/mobile/android/capture-events/analytics-events/)
* [iOS](https://developer.fullstory.com/mobile/ios/capture-events/analytics-events/)

### 識別

| Remote Command | FullStory Method |
| -------------- | ---------------- |
| `identify` | `FS.identify()` |

| パラメータ | タイプ |
| --------- | ---- |
| `uid` (必須) | 文字列 |
| `user_variables` | マップ |

FullStory開発者ガイド：識別

* [Android](https://developer.fullstory.com/mobile/android/identification/identify-users/)
* [iOS](https://developer.fullstory.com/mobile/ios/identification/identify-users/)

### ユーザー変数の構成

| Remote Command | FullStory Method |
| -------------- | ---------------- |
| `setuservariables` | `FS.setUserVars()` |

| パラメータ | タイプ |
| --------- | ---- |
| `user_variables` (必須) | マップ |

 `user_variables`パラメータは、キーが`strings`で値がデータタイプ（例：`_str`, `_int`, `_bool`）で接尾辞が付けられたキー値ペアのオブジェクトを取ります。詳細については、[カスタムAPIプロパティの構成](https://developer.fullstory.com/mobile/user-identification/set-user-properties/)を参照してください。

FullStory開発者ガイド：ユーザー変数の構成

* [Android](https://developer.fullstory.com/mobile/android/identification/set-user-properties/)
* [iOS](https://developer.fullstory.com/mobile/ios/identification/set-user-properties/)

### シャットダウン

| Remote Command | FullStory Method |
| -------------- | ---------------- |
| `shutdown` | `FS.shutdown()` |

FullStoryの記録を停止します。記録を再開するには`restart`を使用します。

FullStory開発者ガイド：シャットダウン

* [Android](https://developer.fullstory.com/mobile/android/fullcapture/capture-data/)
* [iOS](https://developer.fullstory.com/mobile/ios/fullcapture/capture-data/)

### リスタート

| Remote Command | FullStory Method |
| -------------- | ---------------- |
| `restart` | `FS.restart()` |

`shutdown`で停止した後、FullStoryの記録を再開します。

FullStory開発者ガイド：リスタート

* [Android](https://developer.fullstory.com/mobile/android/fullcapture/capture-data/)
* [iOS](https://developer.fullstory.com/mobile/ios/fullcapture/capture-data/)

### 同意

| Remote Command | FullStory Method |
| -------------- | ---------------- |
| `consent` | `FS.consent()` |

| パラメータ | タイプ |
| --------- | ---- |
| `consent_granted` (必須) | ブール値 |

FullStoryセッション記録のためのユーザー同意を付与または取り消します。

FullStory開発者ガイド：同意

* [Android](https://developer.fullstory.com/mobile/android/fullcapture/user-consent/)
* [iOS](https://developer.fullstory.com/mobile/ios/fullcapture/user-consent/)

### 匿名化

| Remote Command | FullStory Method |
| -------------- | ---------------- |
| `anonymize` | `FS.anonymize()` |

現在のユーザーセッションを匿名化し、以前に構成されたユーザー識別を削除します。

FullStory開発者ガイド：匿名化

* [Android](https://developer.fullstory.com/mobile/android/identification/anonymize-users/)
* [iOS](https://developer.fullstory.com/mobile/ios/identification/anonymize-users/)

### アイドルタイマーのリセット

| Remote Command | FullStory Method |
| -------------- | ---------------- |
| `resetidletimer` | `FS.resetIdleTimer()` |

FullStoryのアイドルタイムアウトタイマーをリセットし、現在のセッションを延長します。

FullStory開発者ガイド：アイドルタイマーのリセット

* [Android](https://developer.fullstory.com/mobile/android/fullcapture/reset-idle-timer/)
* [iOS](https://developer.fullstory.com/mobile/ios/fullcapture/reset-idle-timer/)
### ログ

| リモートコマンド | FullStory メソッド |
| -------------- | ---------------- |
| `log` | `FS.log()` |

| パラメータ | タイプ |
| --------- | ---- |
| `log_level` (必須) | 文字列 |
| `log_message` (必須) | 文字列 |

指定されたレベルでメッセージを記録します。プラットフォームによって受け入れられる `log_level` の値は異なります：

| プラットフォーム | 受け入れられる値 |
| -------- | --------------- |
| Android | `log`, `error`, `warn`/`warning`, `info`, `debug` |
| iOS | `assert`, `error`, `warning`, `info`, `debug` |

FullStory 開発者ガイド：ログ

* [Android](https://developer.fullstory.com/mobile/android/fullcapture/logging/)
* [iOS](https://developer.fullstory.com/mobile/ios/fullcapture/logging/)