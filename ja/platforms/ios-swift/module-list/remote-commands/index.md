---
title: RemoteCommandsモジュール
description: 拡張機能と読み込みルールによって制御される、タグ管理のイベントからのネイティブコードブロックのトリガーを有効にします。
url: https://docs.tealium.com/ja/platforms/ios-swift/module-list/remote-commands/
---
[リモートコマンド](https://docs.tealium.com/ja/platforms/remote-commands/)の詳細をご覧ください。

## 要件

* `webview`リモートコマンドを使用する場合は、[TagManagementモジュール](https://docs.tealium.com/ja/platforms/ios-swift/module-list/tag-management/)が必要です。

コンパイル時の依存関係ではありませんが、リモートコマンドはこのモジュールからトリガーされます。

## サポート対象プラットフォーム

* iOS
* macOS（JSONのみ）
* tvOS（JSONのみ）
* watchOS（JSONのみ）

## インストール

Swift Package Manager、CocoaPods、またはCarthageを使用してRemoteCommandsモジュールをインストールします。

### Swift Package Manager（推奨）

バージョン1.9.0以降でサポートされているSwift Package Manager（SPM）は、Tealium Swiftライブラリをインストールするための推奨かつ最も簡単な方法です。

1. Xcodeプロジェクトで、**File > Add Package Dependencies**を選択します。
2. リポジトリURLとして`https://github.com/tealium/tealium-swift`を入力します。
3. バージョンルールを構成します。通常は`"Up to next major"`を推奨します。現在のTealium Swiftライブラリのバージョンがリストに表示されない場合は、Swiftパッケージのキャッシュをリセットしてください。
4. インストールするモジュールのリストからRemoteCommandsモジュールを選択し、Xcodeプロジェクトの各アプリターゲットにある**Frameworks and Libraries**に追加します。

[iOS向けSPMのインストール](https://docs.tealium.com/ja/platforms/ios-swift/install/#swift-package-manager-recommended)の詳細をご覧ください。

### CocoaPods

CocoaPodsを使用してRemoteCommandsモジュールをインストールするには、Podfileに次のPodを追加します。  
```perl
pod 'tealium-swift/RemoteCommands'
```

[iOS向けCocoaPodsのインストール](https://docs.tealium.com/ja/platforms/ios-swift/install/#cocoapods)の詳細をご覧ください。

### Carthage

Carthageを使用してRemoteCommandsモジュールをインストールするには、次の手順に従います。

1. XcodeでアプリターゲットのGeneral構成ページに移動します。

2. **Embedded Binaries**セクションに次のフレームワークを追加します。  
      ```perl
      TealiumRemoteCommands.framework
      ```
3. RemoteCommands APIを操作する必要がある場合は、次の必須のimport文をプロジェクトに追加します。  

      ```swift
      import TealiumRemoteCommands
      ```

[iOS向けCarthageのインストール](https://docs.tealium.com/ja/platforms/ios-swift/install/#carthage)の詳細をご覧ください。

## リモートコマンドのオプション

リモートコマンドには、次の2つの構成オプションがあります。

* **JSONファイル**  
ローカルで読み込むかリモートでホストされるJSONファイルで、ベンダー構成、データマッピング、イベントトリガーが含まれます。
* **リモートコマンドタグ**  
ベンダーのAPIに対する構成オプションを提供するタグ管理内のタグです（Tag Managementモジュールとともに使用します）。

[リモートコマンドのベンダー統合一覧](https://docs.tealium.com/ja/platforms/remote-commands/integrations/)を参照してください。

### 例

タグ管理でリモートコマンドタグを構成します。アプリ内またはリモートサーバー上のJSONファイルも使用できます。構成後、`TealiumConfig`で[`addRemoteCommand()`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#addremotecommand)を使用してリモートコマンドを登録します。`Tealium`を初期化する前に登録を完了してください。





```swift
var tealium: Tealium?

let config = TealiumConfig(account: "ACCOUNT",
                           profile: "PROFILE",
                           environment: "ENVIRONMENT",
                           dataSource: "DATASOURCE")

let remoteCommand = RemoteCommand(commandId: "display", description: "Display Prompt") { response in
    guard let payload = response.payload else {
        return
    }
    print("Use response payload: \(payload)")
}
config.addRemoteCommand(remoteCommand)

tealium = Tealium(config: config)
```




```swift
var tealium: Tealium?

let config = TealiumConfig(account: "ACCOUNT",
                           profile: "PROFILE",
                           environment: "ENVIRONMENT",
                           dataSource: "DATASOURCE")

let remoteCommand = RemoteCommand(commandId: "display", description: "Display Prompt", type: .local(file: "FILENAME")) { response in
    guard let payload = response.payload else {
        return
    }
    print("Use response payload: \(payload)")
}
config.addRemoteCommand(remoteCommand)

tealium = Tealium(config: config)
```





```swift
var tealium: Tealium?

let config = TealiumConfig(account: "ACCOUNT",
                           profile: "PROFILE",
                           environment: "ENVIRONMENT",
                           dataSource: "DATASOURCE")

let remoteCommand = RemoteCommand(commandId: "display", description: "Display Prompt", type: .remote(url: "https://tags.tiqcdn.com/dle/ACCOUNT/PROFILE/FILENAME.json")) { response in
    guard let payload = response.payload else {
        return
    }
    print("Use response payload: \(payload)")
}
config.addRemoteCommand(remoteCommand)

tealium = Tealium(config: config)
```





### 初期化後にリモートコマンドを追加する

`Tealium`の初期化後にリモートコマンドを追加するには、`tealium.remoteCommands`マネージャーを使用します。すべてのイベントを確実に受信できるよう、可能な場合は`TealiumConfig`にリモートコマンドを追加してください。デフォルトでは、`webview`コマンドは読み込み時に初期化されるため、後から`tealium.remoteCommands`を使用して追加すると、初期化を受信できない場合があります。

`Tealium`の初期化後にリモートコマンドを追加する必要がある場合は、次のパターンを使用します。

```swift
tealium = Tealium(config: config)

let remoteCommand = RemoteCommand(
    commandId: "display",
    description: "Display Prompt",
    type: .remote(url: "https://tags.tiqcdn.com/dle/ACCOUNT/PROFILE/FILENAME.json")) { response in
    guard let payload = response.payload else {
        return
    }
    print("Use response payload: \(payload)")
}
tealium?.remoteCommands.add(remoteCommand)
```

## データレイヤー

このモジュールによって追加される変数はありません。

## APIリファレンス

### `init()`
`add`コマンドに渡すことができる、新しいリモートコマンドオブジェクトを作成します。

| パラメータ | 説明 | 例 |
|-------------|---------------------------------------------------|--------------------|
| `commandId` | リモートコマンドに必須の文字列識別子 | `"logger" ` |
| `description` | リモートコマンドの任意の文字列説明 | `"Log Response object to console"` |
| `type` | リモートコマンドのタイプ（webview（デフォルト）、ローカルJSON、またはリモートJSON） | `.local(file: "logger")` |
| `completion` | トリガーするコードブロック | |

使用例を次に示します。

```swift
let customCommand = TealiumRemoteCommand(commandId: "logger",
                                        description: "Log Response object to console",
                                        type: .local(file: "logger"))
                                        { (response) in
                                            // code to execute
                                            print("Custom command response: \(response)")
                                        })
```
### `add()`


<blockquote>
1.6.5以降では、`TealiumConfig`の[`addRemoteCommand()`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#addremotecommand)メソッドを使用してリモートコマンドを追加することを推奨します。
</blockquote>


指定したリモートコマンドを、後でトリガーできるようTealiumに登録します。新しいリモートコマンドを追加する前に、Tealiumを初期化しておく必要があります。

```swift
add(_ remoteCommand: TealiumRemoteCommandProtocol)
```

以下に使用例を示します。

```swift
var tealium: Tealium?
let customCommand = RemoteCommand(commandId: "logger",
    description: nil)
    { response in
        // code to execute
        print("Custom command response: \(response)")
    }
if let remoteCommands = self.tealium?.remoteCommands {
        remoteCommands.add(customCommand)
} else {
		print("Remote commands not available")
}
```

### `remove()`

以前に登録したリモートコマンドを削除し、再度トリガーされないようにします。

```swift
remove(commandWithId: String)
```

```swift
remove(jsonCommand: String)
```

```swift
// assumes "tealium" previously instantiated
tealium?.remoteCommands?.remove(commandWithId: "logger")

tealium?.remoteCommands?.remove(jsonCommand: "logger")
```

### `remoteHTTPCommandDisabled`

`true`の場合、組み込みのリモートHTTPコマンドを無効にしますが、その他のコマンドで使用できるようリモートコマンドモジュールは有効なままになります。デフォルトは`false`です。つまり、[リモートHTTPコマンド](#remote-http-command)は有効です。

```swift
remoteHTTPCommandDisabled
```

以下に使用例を示します。

```swift
// assumes "config" previously instantiated (`TealiumConfig()`)
config.remoteHTTPCommandDisabled = false
```

## リモートHTTPコマンド

これは、識別子が`_http`である予約済みの内部コマンドです。ネイティブコードからHTTPリクエストをトリガーし、そのレスポンスをタグ管理Webビューに返します。Webブラウザーで発生する可能性のあるCORS制限を回避するために使用されることがあります。このコマンドを使用するには、次の特定のマッピング名を使用する必要があります。

| マッピング名 | 説明 |
| --- | --- |
| `url` | （必須）トリガーするリクエストのURL。 |
| `method` | （必須）呼び出すHTTPメソッド。現在サポートされているメソッドはPUT、GET、POSTのみです。 |
| `headers` | （任意）リクエストとともに渡すヘッダーのキーと値のペアを含むJavaScriptオブジェクト（JSON）。例：`{"Content-Type": "application/json"}`。 |
| `callback_function` | （任意）コマンドの完了時に呼び出されるJavaScript関数。コールバック関数には2つのパラメータが渡されます。`code`は404や200などのHTTPレスポンスコードで、`body`はリクエストのレスポンス本文です。 |

以下にコールバック関数の例を示します。

```swift
var my_callback = function(code, body) {
   // assuming the response body was a JSON object, this logs a variable called my_response_variable to the console in the web view
	console.log(body.my_response_variable);
}
```