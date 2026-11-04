---
title: RemoteCommandsモジュール
description: 拡張機能と読み込みルールによって制御される、タグ管理のイベントからのネイティブコードブロックの実行を可能にします。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/remote-commands/
---
リモートコマンドについて[詳しくはこちら](https://docs.tealium.com/ja/platforms/remote-commands/)をご覧ください。

## 要件

* Tag Managementモジュール。コンパイル時の依存関係ではありませんが、リモートコマンドはこのモジュールからトリガーされます。

## サポートされるプラットフォーム

* iOS

## インストール

CocoaPodsまたはCarthageを使用してRemoteCommandsモジュールをインストールします。

### CocoaPods

CocoaPodsを使用してRemoteCommandsモジュールをインストールするには、次のpodをPodfileに追加します。  
```ruby
pod 'tealium-swift/TealiumRemoteCommands'
```

フレームワークは自動的にインスタンス化されます。このフレームワークは`TealiumCore` podに依存しています。iOSでのCocoaPodsのインストールについては、[詳しくはこちら](https://docs.tealium.com/ja/platforms/ios-swift-v1/install/#cocoapods)をご覧ください。

### Carthage

Carthageを使用してRemoteCommandsモジュールをインストールするには、次の手順に従います。

1. Xcodeで、アプリターゲットの「General」構成ページに移動します。

2. **Embedded Binaries**セクションに次のフレームワークを追加します。  
      ```ruby
      TealiumRemoteCommands.framework
      ```
3. RemoteCommands APIを操作する必要がある場合は、次の必須import文をプロジェクトに追加します。  
      ```swift
      import TealiumRemoteCommands
      ```

フレームワークは自動的にインスタンス化されます。このフレームワークは`TealiumCore`に依存しています。追加のimport文は必要ありません。iOSでのCarthageのインストールについては、[詳しくはこちら](https://docs.tealium.com/ja/platforms/ios-swift-v1/install/#carthage)をご覧ください。

## 例

Tag ManagementでRemote Commandタグを構成し、アプリにモジュールをインストールしたら、次の例に示すように初期化処理へ以下の行を追加します。

```swift
class TealiumHelper {
	var tealium: Tealium?
	// ...
	private func initTealium() {
		let config = TealiumConfig(account: "ACCOUNT",
 	       		                 profile: "PROFILE",
        	   	                 environment: "ENVIRONMENT",
           		                 datasource: "DATASOURCE")
    	guard let remoteCommands = self?.tealium?.remoteCommands() else {
          return
        }
        let brazeCommand = BrazeCommand(brazeTracker: BrazeTracker())
        let brazeRemoteCommand = brazeCommand.remoteCommand()
        remoteCommands.add(brazeRemoteCommand)

		// ...
	}
}
```

## データレイヤー

このモジュールによって追加される変数はありません。

## APIリファレンス

### `init()`

`add`コマンドに渡す準備ができた、新しいリモートコマンドオブジェクトを作成します。

| パラメータ | 説明 | 例 |
|-------------|---------------------------------------------------|--------------------|
| `commandId` | リモートコマンドの必須の文字列識別子 | `"logger" ` |
| `description` | リモートコマンドの任意の文字列による説明 | `"Log Response object to console"` |
| `queue` | コードブロックをトリガーするキュー | `DispatchQueue.main` |
| `completion` | トリガーするコードブロック | |

使用例は次のとおりです。

```swift
let customCommand = TealiumRemoteCommand(commandId: "logger",
                                        description: "Log Response object to console",
                                        queue: DispatchQueue.main)
                                        { (response) in
                                            // code to execute
                                            print("Custom command response: (response)")
                                        })
```

### `add()`


<blockquote>
バージョン1.6.5以降では、`TealiumConfig`の[`addRemoteCommand()`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-config/#addremotecommand)メソッドを使用してリモートコマンドを追加することを推奨します。
</blockquote>


指定したリモートコマンドを、後でトリガーできるようTealiumに登録します。新しいリモートコマンドを追加する前に、Tealiumを初期化しておく必要があります。

```swift
add(remoteCommand: TealiumRemoteCommand)
```

使用例は次のとおりです。

```swift
var tealium: Tealium?
let customCommand = TealiumRemoteCommand(commandId: "logger",
    description: nil,
    queue: DispatchQueue.main)
    { response in
        // code to execute
        print("Custom command response: (response)")
    })
if let remoteCommands = self.tealium?.remoteCommands() {
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
// assumes "tealium" previously instantiated
tealium?.remoteCommands()?.remove(commandWithId: "logger")
```

### `disableRemoteCommands()`

リモートコマンドモジュールを無効にします。

```swift
disableRemoteCommands()
```

使用例は次のとおりです。

```swift
// assumes "tealium" previously instantiated
tealium?.remoteCommands()?.disableRemoteCommands()
```

### `enableRemoteCommands()`

リモートコマンドモジュールを有効にします（以前に無効化した場合にのみ必要です。デフォルトでは有効です）。

```TealiumSwift
enabledRemoteCommands()
```

使用例は次のとおりです。

```swift
// assumes "tealium" previously instantiated
tealium?.remoteCommands()?.enableRemoteCommands()
```

### `disableRemoteHTTPCommand()`

組み込みのリモートHTTPコマンドを無効にしますが、他のコマンドに対してリモートコマンドモジュールは有効なままにします。

```swift
disableRemoteHTTPCommand()
```

使用例は次のとおりです。

```swift
// assumes "tealium" previously instantiated
tealium?.remoteCommands()?.disableRemoteHTTPCommand()
```

### `enableRemoteHTTPCommand()`

組み込みのリモートHTTPコマンドを有効にします（以前に無効化した場合にのみ必要です。デフォルトでは有効です）。

```swift
enableRemoteHTTPCommand()`
```

使用例は次のとおりです。

```swift
// assumes "tealium" previously instantiated
tealium?.remoteCommands()?.enableRemoteHTTPCommand()
```

## リモートHTTPコマンド

これは、識別子`_http`を持つ予約済みの内部コマンドです。ネイティブコードからHTTPリクエストをトリガーし、そのレスポンスをTag ManagementのWebビューに返します。Webブラウザーで発生する可能性があるCORS制限を回避するために使用される場合があります。このコマンドを使用するには、次の特定のマッピング名を使用する必要があります。

| マッピング名 | 説明 |
| --- | --- |
| `url` | （必須）トリガーするリクエストのURL。 |
| `method` | （必須）呼び出すHTTPメソッド。現在サポートされているメソッドはPUT、GET、POSTのみです。v |
| `headers` | （任意）リクエストとともに渡すヘッダーのキーと値のペアを含むJavaScriptオブジェクト（JSON）。例：`{"Content-Type": "application/json"}`。 |
| `callback_function` | （任意）コマンドの完了時に呼び出されるJavaScript関数。コールバック関数には2つのパラメータが渡されます。`code`は404や200などのHTTPレスポンスコードで、`body`はリクエストのレスポンス本文です。 |

コールバック関数の例を次に示します。

```swift
var my_callback = function(code, body) {
   // assuming the response body was a JSON object, this logs a variable called my_response_variable to the console in the web view
	console.log(body.my_response_variable);
}
```