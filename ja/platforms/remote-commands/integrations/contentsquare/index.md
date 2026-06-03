---
title: リモートコマンド：Contentsquare
description: AndroidおよびSwift/iOS用ContentsquareのTealiumリモートコマンド統合。
url: https://docs.tealium.com/ja/platforms/remote-commands/integrations/contentsquare/
---
## 要件

* 以下のいずれかのモバイルライブラリ：
  * [Tealium for Android-Kotlin](/ja/platforms/android-kotlin/) (1.0.0&#43;)
  * [Tealium for Android-Java](/ja/platforms/android-java/) (Contentsquare 1.0.0&#43;の場合は5.9.0&#43;、それ以前のバージョンの場合は&lt;5.9.0)
  * [Tealium for iOS-Swift](/ja/platforms/ios-swift/)
* 以下のいずれかのリモートコマンド統合：
  * [Contentsquare Remote Command JSON File](/ja/platforms/remote-commands/integrations/contentsquare/#json-template) (Android-Kotlin 1.0.0&#43;またはiOS-Swift 2.12.0&#43;が必要)
  * Tealium iQ Tag ManagementのContentsquare Remote Commandタグ

## 動作原理

Contentsquare統合は3つのアイテムを使用します：

1. ContentsquareネイティブSDK
2. Contentsquareメソッドをラップするリモートコマンドモジュール
3. イベントトラッキングをネイティブのContentsquareコールに変換するJSON構成ファイルまたはRemote Commandタグ

アプリにContentsquareリモートコマンドモジュールを追加すると、必要なContentsquareライブラリが自動的にインストールされビルドされます。依存関係マネージャーのインストールを使用している場合、別途Contentsquare SDKをインストールする必要はありません。

リモートコマンドオプションには2つあります：JSON構成ファイル、またはiQ Tag Managementを使用してマッピングを構成します。JSON構成ファイルは、ベンダー統合のための推奨オプションで、アプリ内またはリモートでホストされます。iQ Tag Managementを使用する場合は、ベンダー統合のためのRemote Commandタグを追加します。[ベンダー統合についての詳細はこちら](/ja/platforms/remote-commands/how-it-works/#vendor-integrations)。

## インストール

### 依存関係マネージャ




1. Xcodeプロジェクトで、**File &gt; Add Packages... &gt; Add Package Dependency**を選択します。
2. リポジトリURLを入力します：`https://github.com/tealium/tealium-ios-contentsquare-remote-command`。
3. バージョンルールを構成します。通常は`Up to next major`が推奨されます。現在の`TealiumContentSquare`バージョンがリストに表示されない場合は、Swiftパッケージキャッシュをリセットしてください。
4. インストールする`TealiumContentSquare`モジュールを選択し、そのモジュールをインストールしたいアプリターゲットを選択します。

プロジェクトに複数のアプリターゲットがあり、`TealiumContentSquare`モジュールを複数のアプリターゲットに追加する必要がある場合は、**Frameworks, Libraries, and Embedded Content**セクションで手動で追加する必要があります。

追加のアプリターゲットに`TealiumContentSquare`をインストールするには：

1. **Project Navigator**でXcodeプロジェクトを選択します。
2. Xcodeプロジェクトで、**TARGETS**セクションの下にあるアプリターゲットを選択します。
3. **General &gt; Frameworks, Libraries &amp; Embedded Content**に移動し、`TealiumContentSquare`モジュールを選択してアプリターゲットに追加します。

Tealium Swiftライブラリから追加のモジュールを追加するには、[Swift Package Manager](/ja/platforms/ios-swift/install/#swift-package-manager-recommended)の指示に従ってください。




1. Podfileから`tealium-swift`と`pod &#34;CS_iOS_SDK&#34;`を削除します。`tealium-swift`の依存関係はすでに`TealiumContentsquare`フレームワークに含まれています。

2. Podfileに次の依存関係を追加します：
      ```ruby
      pod &#34;TealiumContentsquare&#34;
      ```
      `TealiumContentsquare`ポッドには次の`TealiumSwift`依存関係が含まれています：
      ```bash
      &#39;tealium-swift/Core&#39;
      &#39;tealium-swift/RemoteCommands&#39;
      ```

3. `TealiumHelper`ファイルおよび`Tealium`クラスまたはContentsquare Remote Commandにアクセスする他のファイルで`TealiumSwift`および`TealiumContentsquare`モジュールをインポートします。





1. Cartfileから`tealium-swift`を削除します。`tealium-swift`の依存関係はすでに`TealiumContentsquare`フレームワークに含まれています。

2. Cartfileに存在する場合は次の行を削除します：
      ```bash
      github &#34;ContentSquare/CS_iOS_SDK&#34;
      ```

3. Cartfileに次の依存関係を追加します：
      ```bash
      github &#34;tealium/tealium-ios-contentsquare-remote-command&#34;
      ```

Tealium for Swift SDK (バージョン1.6.5&#43;)は、インストール時に`TealiumDelegate`モジュールを含める必要があります。





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

2. アプリプロジェクトの`build.gradle`ファイルにContentquare SDKとTealium-Contentsquareリモートコマンドの依存関係を追加します：
      ```groovy
      dependencies {
            implementation &#39;com.tealium.remotecommands:contentsquare:2.3.0&#39;
      }
      ```


### 手動インストール




Contentsquareリモートコマンドの手動インストールには、[Tealium for Swift](/ja/platforms/ios-swift/)ライブラリがインストールされている必要があります。iOSプロジェクト用のContentsquareリモートコマンドをインストールするには：

1. まだ行っていない場合は、[Contentsquare SDK](https://docs.contentsquare.com/ios/#how-to-include-it)をインストールします。

2. [Tealium iOS Contentsquareリモートコマンド](https://github.com/tealium/tealium-ios-contentsquare-remote-command)リポジトリをクローンし、`Sources`フォルダ内のファイルをプロジェクトにドラッグします。

3. [`remoteAPIEnabled`](/ja/platforms/ios-swift/api/tealium-config/#remoteapienabled)構成フラグを`true`に構成します。




Contentsquareリモートコマンドの手動インストールには、[Tealium for Android (Kotlin)](/ja/platforms/android-kotlin/install/)または[Tealium for Android (Java)](/ja/platforms/android-java/install/)がインストールされている必要があります。

Androidプロジェクト用のContentsquareリモートコマンドをインストールするには：

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

2. `&lt;PROJECT_ROOT&gt;/&lt;MODULE&gt;/libs`に`tealium-contentsquare.aar`を追加します。

3. `build.gradle`ファイルにTealiumライブラリの依存関係を追加します：

      ```groovy
      dependencies {
            implementation(name:&#39;tealium-contentsquare&#39;, ext:&#39;aar&#39;)
      }
      ```



## 初期化

すべてのTealiumライブラリで、初期化時にContentsquareのリモートコマンドを登録します。





TealiumのiOS（Swift）ライブラリ用のJSON構成ファイルまたはリモートコマンドタグでリモートコマンドを初期化します：
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
    let contentsquare = ContentsquareRemoteCommand()   

    // ローカルJSON
    //let contentsquare = ContentsquareRemoteCommand(type: .local(file: &#34;contentsquare&#34;)) 

    // リモートJSON
    //let contentsquare = ContentsquareRemoteCommand(type: .remote(url: &#34;https://some.domain.com/contentsquare.json&#34;)) 

    remoteCommands.add(contentsquare)
}
```


TealiumのAndroid（Kotlin）ライブラリ用のJSON構成ファイルまたはリモートコマンドタグでリモートコマンドを初期化します：
```kotlin
val config = TealiumConfig(application,
        &#34;ACCOUNT&#34;,
        &#34;PROFILE&#34;,
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands, Dispatchers.TagManagement));
var tealium = Tealium.create(TEALIUM_MAIN, config) {
    // `Application`を使用して初期化することで、同意管理などの高度な機能を利用できます
    val contentsquare = ContentsquareRemoteCommand(this);

    // シンプルなトラッキングの場合、`Application`なしで初期化することもできます
    val contentsquare = ContentsquareRemoteCommand();
    // コマンドを登録

    // Webviewタグ
    remoteCommands?.add(contentsquare); 

    // ローカルJSON
    //remoteCommands?.add(contentsquare, filename = &#34;contentsquare.json&#34;); 

    // リモートJSON
    //remoteCommands?.add(contentsquare, remoteUrl = &#34;https://some.domain.com/contentsquare.json&#34;); 
```



TealiumのAndroid（Java）ライブラリ用のリモートコマンドタグでリモートコマンドを初期化します：  
```java
import com.tealium.remotecommands.contentsquare.ContentsquareRemoteCommand;

Tealium.Config config = Tealium.Config.create(application, &#34;ACCOUNT&#34;, &#34;PROFILE&#34;, &#34;ENVIRONMENT&#34;);
Tealium teal = Tealium.createInstance(TEALIUM_MAIN, config);

// `Application`を使用して初期化することで、同意管理などの高度な機能を利用できます
ContentsquareRemoteCommand contentsquare = new ContentsquareRemoteCommand(this);

// シンプルなトラッキングの場合、`Application`なしで初期化することもできます
ContentsquareRemoteCommand contentsquare = new ContentsquareRemoteCommand();

// コマンドを登録
teal.addRemoteCommand(contentsquare);
```



## JSONテンプレート

[JSON構成ファイル](/ja/platforms/remote-commands/how-it-works/#json-configuration-file)を使用してリモートコマンドを構成する場合は、以下のテンプレートを参照してください。このテンプレートには、標準的なeコマースインストールで使用される一般的なマッピングが含まれています。必要に応じてマッピングを編集してください。

```json
{
  &#34;config&#34;: {},
  &#34;mappings&#34;: {
    &#34;screen&#34;: &#34;screen_name&#34;,
    &#34;dynamic_var&#34;: &#34;dynamic_var&#34;,
    &#34;user_id&#34;: &#34;user_identifier&#34;,
    &#34;custom_vars&#34;: &#34;custom_vars&#34;,
    &#34;price&#34;: &#34;purchase.price&#34;,
    &#34;currency&#34;: &#34;purchase.currency&#34;,
    &#34;transaction_id&#34;: &#34;purchase.transaction_id&#34;
  },
  &#34;commands&#34;: {
    &#34;screen_title&#34;: &#34;sendscreenview&#34;,
    &#34;dynamic_var&#34;: &#34;senddynamicvar&#34;,
    &#34;user_identifier&#34;: &#34;senduseridentifier&#34;,
    &#34;transaction&#34;: &#34;sendtransaction&#34;,
    &#34;stop_tracking&#34;: &#34;stoptracking&#34;,
    &#34;resume_tracking&#34;: &#34;resumetracking&#34;,
    &#34;forget_me&#34;: &#34;forgetme&#34;,
    &#34;opt_in&#34;: &#34;optin&#34;,
    &#34;opt_out&#34;: &#34;optout&#34;
  }
}
```

## サポートされているメソッド

Contentsquareメソッドに対応するコマンドをマッピングします。Contentsquareメソッドをトリガーするには、指定された形式で対応するコマンドを渡します。

| リモートコマンド      | Contentsquareメソッド  |
| ------------------- | --------------------- |
| `sendscreenview`    | `send()`              |
| `sendtransaction`   | `send()`              |
| `senddynamicvar`    | `send()`              |
| `senduseridentifier`| `sendUserIdentifier()`|
| `stoptracking`      | `stopTracking()`      |
| `resumetracking`    | `resumeTracking()`    |
| `forgetme`          | `forgetMe()`          |
| `optin`             | `optIn()`             |
| `optout`            | `optOut()`            |

Contentsquare SDKはTealium SDKと並行してインストールされているため、対応するタグ構成を与えることで、任意のネイティブContentsquare機能をトリガーできます。

### SDKセットアップ

#### 初期化

Contentsquare SDKは起動時に自動的に初期化されます。

Contentsquare開発者ガイド：初期SDKセットアップ

- [Android](https://docs.contentsquare.com/android/#add-contentsquare-to-your-app)
- [iOS](https://docs.contentsquare.com/ios/#get-started)

### 画面のトラッキング

| リモートコマンド   | Contentsquareメソッド |
| ---------------- | -------------------- |
| `sendscreenview` | `send`               |

| パラメータ                | タイプ     |
| ------------------------ | -------- |
| `screen_name` (必須) | `String` |
| `custom_vars` (オプション) | `Array`  |

**カスタム変数の形式：**
各カスタム変数オブジェクトには以下が含まれる必要があります：
- `index` (必須): `Int` - カスタム変数のインデックス
- `name` (必須): `String` - カスタム変数の名前  
- `value` (必須): `String` - カスタム変数の値

Contentsquare開発者ガイド：アナリティクスユーザーID  

- [Android](https://docs.contentsquare.com/android/#track-screens)
- [iOS](https://docs.contentsquare.com/ios/#track-screens)

### トランザクションのトラッキング

| リモートコマンド    | Contentsquareメソッド |
| ----------------- | -------------------- |
| `sendtransaction` | `send`               |

| パラメータ                   | タイプ              |
| --------------------------- | ----------------- |
| `price` (必須)          | `Double or Float` |
| `currency` (必須)       | `String`          |
| `transaction_id` (オプション) | `String`          |

Contentsquare開発者ガイド：トランザクションのトラッキング  

- [Android](https://docs.contentsquare.com/android/#track-transactions)
- [iOS](https://docs.contentsquare.com/ios/#track-transactions)

### 動的変数のトラッキング

| リモートコマンド    | Contentsquareメソッド |
| ----------------- | -------------------- |
| `senddynamicvar`  | `send`               |

| パラメータ                   | タイプ              |
| --------------------------- | ----------------- |
| `dynamic_var` (必須)    | `Object`          |

 `dynamic_var`パラメータは、キーが`strings`で値が`UInt32`または`strings`のキーバリューペアのJSONオブジェクトを取ります。例：`{&#34;my_dynamic_string_var_name&#34;: &#34;some string value&#34;}`, `{&#34;my_dynamic_int_var_name&#34;: 123}`, `{&#34;my_dynamic_string_var_name&#34;: &#34;some string value,&#34; &#34;my_dynamic_int_var_name&#34;: 123}`.

Contentsquare開発者ガイド：動的変数のトラッキング

- [Android](https://docs.contentsquare.com/android/#track-dynamic-variables)
- [iOS](https://docs.contentsquare.com/ios/#track-dynamic-variables)

### ユーザー識別子のトラッキング

| リモートコマンド       | Contentsquareメソッド |
| -------------------- | -------------------- |
| `senduseridentifier` | `sendUserIdentifier` |

| パラメータ                        | タイプ     |
| -------------------------------- | -------- |
| `user_identifier` (必須)     | `String` |

Contentsquare開発者ガイド：ユーザー識別子のトラッキング

- [Android](https://docs.contentsquare.com/en/android/session-replay/)
- [iOS](https://docs.contentsquare.com/en/ios/session-replay/)

### 同意オプション

#### トラッキングの停止/再開

| リモートコマンド   | Contentsquare メソッド |
| ---------------- | -------------------- |
| `stoptracking`   | `stopTracking`       |
| `resumetracking` | `resumeTracking`     |

Contentsquare 開発者ガイド: トラッキングの停止/再開

- [Android](https://docs.contentsquare.com/android/#stop-resume-tracking)
- [iOS](https://docs.contentsquare.com/ios/#stop-resume-tracking)

#### オプトイン

| リモートコマンド | Contentsquare メソッド |
| -------------- | -------------------- |
| `optin`        | `optIn`              |

Contentsquare 開発者ガイド: オプトイン

- [Android](https://docs.contentsquare.com/android/#opt-in)
- [iOS](https://docs.contentsquare.com/ios/#opt-in)

#### オプトアウト

| リモートコマンド | Contentsquare メソッド |
| -------------- | -------------------- |
| `optout`       | `optOut`             |

Contentsquare 開発者ガイド: オプトアウト

- [Android](https://docs.contentsquare.com/android/#opt-out)
- [iOS](https://docs.contentsquare.com/ios/#opt-out)

#### 私を忘れてください

| リモートコマンド | Contentsquare メソッド |
| -------------- | -------------------- |
| `forgetme`     | `forgetMe`           |

Contentsquare 開発者ガイド: 私を忘れてください

- [Android](https://docs.contentsquare.com/android/#forget-me)
- [iOS](https://docs.contentsquare.com/ios/#forget-me)