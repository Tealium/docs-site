---
title: リモートコマンド：Contentsquare
description: AndroidおよびSwift/iOS向けのContentsquare用Tealiumリモートコマンド統合。
url: https://docs.tealium.com/ja/platforms/remote-commands/integrations/contentsquare/
---
## 要件

* 次のいずれかのモバイルライブラリ：
  * [Tealium for Android-Kotlin](https://docs.tealium.com/ja/platforms/android-kotlin/)（1.0.0以降）
  * [Tealium for Android-Java](https://docs.tealium.com/ja/platforms/android-java/)（Contentsquare 1.0.0以降の場合は5.9.0以降、以前のバージョンの場合は5.9.0未満）
  * [Tealium for iOS-Swift](https://docs.tealium.com/ja/platforms/ios-swift/)
* 次のいずれかのリモートコマンド統合：
  * [ContentsquareリモートコマンドJSONファイル](https://docs.tealium.com/ja/platforms/remote-commands/integrations/contentsquare/#json-template)（Android-Kotlin 1.0.0以降またはiOS-Swift 2.12.0以降が必要）
  * タグ管理のContentsquareリモートコマンドタグ

## 仕組み

Contentsquare統合では、次の3つの項目を使用します。

1. ContentsquareネイティブSDK
2. Contentsquareのメソッドをラップするリモートコマンドモジュール
3. イベントトラッキングをContentsquareのネイティブ呼び出しに変換するJSON構成ファイルまたはリモートコマンドタグ

Contentsquareリモートコマンドモジュールをアプリに追加すると、必要なContentsquareライブラリが自動的にインストールおよびビルドされます。依存関係マネージャーを使用してインストールする場合、Contentsquare SDKを個別にインストールする必要はありません。

リモートコマンドには、JSON構成ファイルを使用する方法と、タグ管理を使用してマッピングを構成する方法の2つがあります。ベンダー統合には、リモートまたはアプリ内のローカルに配置したJSON構成ファイルを使用することを推奨します。タグ管理を使用する場合は、ベンダー統合用のリモートコマンドタグを追加します。[ベンダー統合](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/#vendor-integrations)の詳細をご覧ください。

## インストール

### 依存関係マネージャー




1. Xcodeプロジェクトで、**File > Add Packages... > Add Package Dependency**を選択します。
2. リポジトリURLとして`https://github.com/tealium/tealium-ios-contentsquare-remote-command`を入力します。
3. バージョンルールを構成します。通常は`Up to next major`を推奨します。現在の`TealiumContentSquare`バージョンがリストに表示されない場合は、Swiftパッケージのキャッシュをリセットしてください。
4. インストールする`TealiumContentSquare`モジュールを選択し、そのモジュールをインストールするアプリターゲットを選択します。

プロジェクトに複数のアプリターゲットがあり、さらに多くのアプリターゲットで`TealiumContentSquare`モジュールが必要な場合は、**Frameworks, Libraries, and Embedded Content**セクションで手動で追加する必要があります。

追加のアプリターゲットに`TealiumContentSquare`をインストールするには、次の手順を実行します。

1. **Project Navigator**でXcodeプロジェクトを選択します。
2. Xcodeプロジェクトの**TARGETS**セクションでアプリターゲットを選択します。
3. **General > Frameworks, Libraries & Embedded Content**に移動し、`TealiumContentSquare`モジュールを選択してアプリターゲットに追加します。

Tealium Swiftライブラリから追加のモジュールを追加するには、[Swift Package Manager](https://docs.tealium.com/ja/platforms/ios-swift/install/#swift-package-manager-recommended)の手順に従ってください。




1. Podfileに`tealium-swift`および`pod "CS_iOS_SDK"`がすでに存在する場合は削除します。`tealium-swift`の依存関係は、すでに`TealiumContentsquare`フレームワークに含まれています。

2. Podfileに次の依存関係を追加します。
      ```ruby
      pod "TealiumContentsquare"
      ```
      `TealiumContentsquare` Podには、次の`TealiumSwift`依存関係が含まれています。  
      ```bash
      'tealium-swift/Core'
      'tealium-swift/RemoteCommands'
      ```

3. `TealiumHelper`ファイル、および`Tealium`クラスまたはContentsquareリモートコマンドにアクセスするその他のファイルで、`TealiumSwift`モジュールと`TealiumContentsquare`モジュールをインポートします。





1. Cartfileから`tealium-swift`を削除します。`tealium-swift`の依存関係は、すでに`TealiumContentsquare`フレームワークに含まれています。

2. Cartfileに次の行が存在する場合は削除します。  
      ```bash
      github "ContentSquare/CS_iOS_SDK"
      ```

3. Cartfileに次の依存関係を追加します。  
      ```bash
      github "tealium/tealium-ios-contentsquare-remote-command"
      ```


<blockquote>
Tealium for Swift SDK（バージョン1.6.5以降）では、インストールに`TealiumDelegate`モジュールを含める必要があります。
</blockquote>






1. まだ行っていない場合は、[Tealium for Android（Kotlin）](https://docs.tealium.com/ja/platforms/android-kotlin/install/)または[Tealium for Android（Java）](https://docs.tealium.com/ja/platforms/android-java/install/)をインストールし、プロジェクトの最上位`build.gradle`ファイルにTealium Maven URLを追加します。

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

2. アプリプロジェクトの`build.gradle`ファイルに次の依存関係を追加して、Contentsquare SDKとTealium-Contentsquareリモートコマンドの両方をインポートします。  
      ```groovy
      dependencies {
            implementation 'com.tealium.remotecommands:contentsquare:2.3.0'
      }
      ```



### 手動インストール




Contentsquareリモートコマンドを手動でインストールするには、[Tealium for Swift](https://docs.tealium.com/ja/platforms/ios-swift/)ライブラリがインストールされている必要があります。iOSプロジェクトにContentsquareリモートコマンドをインストールするには、次の手順を実行します。

1. まだインストールしていない場合は、[Contentsquare SDK](https://docs.contentsquare.com/ios/#how-to-include-it)をインストールします。

2. [Tealium iOS Contentsquareリモートコマンド](https://github.com/tealium/tealium-ios-contentsquare-remote-command)リポジトリをクローンし、`Sources`フォルダー内のファイルをプロジェクトにドラッグします。

3. [`remoteAPIEnabled`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#remoteapienabled)構成フラグを`true.`に構成します。




Contentsquareリモートコマンドを手動でインストールするには、[Tealium for Android（Kotlin）](https://docs.tealium.com/ja/platforms/android-kotlin/install/)または[Tealium for Android（Java）](https://docs.tealium.com/ja/platforms/android-java/install/)がインストールされている必要があります。

AndroidプロジェクトにContentsquareリモートコマンドをインストールするには、次の手順を実行します。

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

2. `tealium-contentsquare.aar`を`<PROJECT_ROOT>/<MODULE>/libs`に追加します。

3. `build.gradle`ファイルにTealiumライブラリの依存関係を追加します。

      ```groovy
      dependencies {
            implementation(name:'tealium-contentsquare', ext:'aar')
      }
      ```



## 初期化

すべての Tealium ライブラリで、初期化時に Contentsquare リモートコマンドを登録します。





JSON 構成ファイルまたは Remote Command タグを使用して、Tealium の iOS（Swift）ライブラリのリモートコマンドを初期化します。
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
    let contentsquare = ContentsquareRemoteCommand()   

    // Local JSON
    //let contentsquare = ContentsquareRemoteCommand(type: .local(file: "contentsquare")) 

    // Remote JSON
    //let contentsquare = ContentsquareRemoteCommand(type: .remote(url: "https://some.domain.com/contentsquare.json")) 

    remoteCommands.add(contentsquare)
}
```


JSON 構成ファイルまたは Remote Command タグを使用して、Tealium の Android（Kotlin）ライブラリのリモートコマンドを初期化します。
```kotlin
val config = TealiumConfig(application,
        "ACCOUNT",
        "PROFILE",
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands, Dispatchers.TagManagement));
var tealium = Tealium.create(TEALIUM_MAIN, config) {
    // Initialize with `Application` to take advantage of consent management and other
    // advanced features
    val contentsquare = ContentsquareRemoteCommand(this);

    // Or for simple tracking, you can initialize without `Application`
    val contentsquare = ContentsquareRemoteCommand();
    // register the command

    // Webview Tag
    remoteCommands?.add(contentsquare); 

    // Local JSON
    //remoteCommands?.add(contentsquare, filename = "contentsquare.json"); 

    // Remote JSON
    //remoteCommands?.add(contentsquare, remoteUrl = "https://some.domain.com/contentsquare.json"); 
```



Remote Command タグを使用して、Tealium の Android（Java）ライブラリのリモートコマンドを初期化します。  
```java
import com.tealium.remotecommands.contentsquare.ContentsquareRemoteCommand;

Tealium.Config config = Tealium.Config.create(application, "ACCOUNT", "PROFILE", "ENVIRONMENT");
Tealium teal = Tealium.createInstance(TEALIUM_MAIN, config);

// Initialize with `Application` to take advantage of consent management and other
// advanced features
ContentsquareRemoteCommand contentsquare = new ContentsquareRemoteCommand(this);

// Or for simple tracking, you can initialize without `Application`
ContentsquareRemoteCommand contentsquare = new ContentsquareRemoteCommand();

// register the command
teal.addRemoteCommand(contentsquare);
```



## JSON テンプレート

[JSON 構成ファイル](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/#json-configuration-file)を使用してリモートコマンドを構成する場合は、以下のテンプレートを使用して作業を開始してください。このテンプレートには、標準的な e コマース実装で使用される一般的なマッピングが含まれています。必要に応じてマッピングを編集してください。

```json
{
  "config": {},
  "mappings": {
    "screen": "screen_name",
    "dynamic_var": "dynamic_var",
    "user_id": "user_identifier",
    "custom_vars": "custom_vars",
    "price": "purchase.price",
    "currency": "purchase.currency",
    "transaction_id": "purchase.transaction_id"
  },
  "commands": {
    "screen_title": "sendscreenview",
    "dynamic_var": "senddynamicvar",
    "user_identifier": "senduseridentifier",
    "transaction": "sendtransaction",
    "stop_tracking": "stoptracking",
    "resume_tracking": "resumetracking",
    "forget_me": "forgetme",
    "opt_in": "optin",
    "opt_out": "optout"
  }
}
```

## サポートされるメソッド

各 Contentsquare メソッドにコマンドをマッピングします。Contentsquare メソッドをトリガーするには、対応するコマンドを指定された形式で渡します。

| リモートコマンド      | Contentsquare メソッド  |
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


<blockquote>
Contentsquare SDK は Tealium SDK とともにインストールされるため、対応するタグ構成に基づいて任意の Contentsquare ネイティブ機能をトリガーできます。
</blockquote>


### SDK のセットアップ

#### 初期化

Contentsquare SDK は起動時に自動的に初期化されます。

Contentsquare 開発者ガイド：SDK の初期セットアップ

- [Android](https://docs.contentsquare.com/android/#add-contentsquare-to-your-app)
- [iOS](https://docs.contentsquare.com/ios/#get-started)

### 画面のトラッキング

| リモートコマンド   | Contentsquare メソッド |
| ---------------- | -------------------- |
| `sendscreenview` | `send`               |

| パラメータ                | 型       |
| ------------------------ | -------- |
| `screen_name`（必須）     | `String` |
| `custom_vars`（任意）     | `Array`  |

**カスタム変数の形式：**
各カスタム変数オブジェクトには、以下を含める必要があります。

- `index`（必須）：`Int` - カスタム変数のインデックス
- `name`（必須）：`String` - カスタム変数名  
- `value`（必須）：`String` - カスタム変数の値

Contentsquare 開発者ガイド：アナリティクスユーザー ID  

- [Android](https://docs.contentsquare.com/android/#track-screens)
- [iOS](https://docs.contentsquare.com/ios/#track-screens)

### トランザクションのトラッキング

| リモートコマンド    | Contentsquare メソッド |
| ----------------- | -------------------- |
| `sendtransaction` | `send`               |

| パラメータ                   | 型                |
| --------------------------- | ----------------- |
| `price`（必須）              | `Double or Float` |
| `currency`（必須）           | `String`          |
| `transaction_id`（任意）     | `String`          |

Contentsquare 開発者ガイド：トランザクションのトラッキング  

- [Android](https://docs.contentsquare.com/android/#track-transactions)
- [iOS](https://docs.contentsquare.com/ios/#track-transactions)

### 動的変数のトラッキング

| リモートコマンド    | Contentsquare メソッド |
| ----------------- | -------------------- |
| `senddynamicvar`  | `send`               |

| パラメータ                   | 型                |
| --------------------------- | ----------------- |
| `dynamic_var`（必須）        | `Object`          |


<blockquote>
`dynamic_var` パラメータはキーと値のペアで構成される JSON オブジェクトを受け取ります。キーは `strings`、値は `UInt32` または `strings` です。例：`{"my_dynamic_string_var_name": "some string value"}`、`{"my_dynamic_int_var_name": 123}`、`{"my_dynamic_string_var_name": "some string value," "my_dynamic_int_var_name": 123}`。
</blockquote>


Contentsquare 開発者ガイド：動的変数のトラッキング

- [Android](https://docs.contentsquare.com/android/#track-dynamic-variables)
- [iOS](https://docs.contentsquare.com/ios/#track-dynamic-variables)

### ユーザー識別子のトラッキング

| リモートコマンド       | Contentsquare メソッド |
| -------------------- | -------------------- |
| `senduseridentifier` | `sendUserIdentifier` |

| パラメータ                        | 型       |
| -------------------------------- | -------- |
| `user_identifier`（必須）         | `String` |

Contentsquare 開発者ガイド：ユーザー識別子のトラッキング

- [Android](https://docs.contentsquare.com/en/android/session-replay/)
- [iOS](https://docs.contentsquare.com/en/ios/session-replay/)

### 同意オプション
#### トラッキングの停止／再開

| リモートコマンド | Contentsquareメソッド |
| ---------------- | -------------------- |
| `stoptracking`   | `stopTracking`       |
| `resumetracking` | `resumeTracking`     |

Contentsquare開発者ガイド：トラッキングの停止／再開

- [Android](https://docs.contentsquare.com/android/#stop-resume-tracking)
- [iOS](https://docs.contentsquare.com/ios/#stop-resume-tracking)

#### オプトイン

| リモートコマンド | Contentsquareメソッド |
| ---------------- | -------------------- |
| `optin`          | `optIn`              |

Contentsquare開発者ガイド：オプトイン

- [Android](https://docs.contentsquare.com/android/#opt-in)
- [iOS](https://docs.contentsquare.com/ios/#opt-in)

#### オプトアウト

| リモートコマンド | Contentsquareメソッド |
| ---------------- | -------------------- |
| `optout`         | `optOut`             |

Contentsquare開発者ガイド：オプトアウト

- [Android](https://docs.contentsquare.com/android/#opt-out)
- [iOS](https://docs.contentsquare.com/ios/#opt-out)

#### Forget Me

| リモートコマンド | Contentsquareメソッド |
| ---------------- | -------------------- |
| `forgetme`       | `forgetMe`           |

Contentsquare開発者ガイド：Forget Me

- [Android](https://docs.contentsquare.com/android/#forget-me)
- [iOS](https://docs.contentsquare.com/ios/#forget-me)