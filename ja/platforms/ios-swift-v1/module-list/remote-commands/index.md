---
title: RemoteCommandsモジュール
description: Tealium iQタグ管理のイベントからネイティブコードブロックをトリガーすることを可能にし、拡張機能とロードルールによって制御されます。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/remote-commands/
---
[詳細はこちら](https://docs.tealium.com/ja/platforms/remote-commands/)をご覧ください。

## 要件

* Tealium iQタグ管理モジュール。コンパイル時の依存関係ではありませんが、リモートコマンドはこのモジュールからトリガーされます。

## 対応プラットフォーム

* iOS

## インストール

CocoaPodsまたはCarthageでRemoteCommandsモジュールをインストールします。

### CocoaPods

CocoaPodsでRemoteCommandsモジュールをインストールするには、Podfileに以下のpodを追加します：
```ruby
pod 'tealium-swift/TealiumRemoteCommands'
```

フレームワークは自動的にインスタンス化されます。`TealiumCore` podに依存しています。[CocoaPodsを使用したiOSのインストールについての詳細はこちら](https://docs.tealium.com/ja/platforms/ios-swift-v1/install/#cocoapods)。

### Carthage

CarthageでRemoteCommandsモジュールをインストールするには、以下の手順に従ってください：

1. XcodeでアプリターゲットのGeneral構成ページに移動します。

2. **Embedded Binaries**セクションに以下のフレームワークを追加します：
      ```ruby
      TealiumRemoteCommands.framework
      ```
3. RemoteCommands APIと連携する必要がある場合は、プロジェクトに以下の必要なインポート文を追加します：
      ```swift
      import TealiumRemoteCommands
      ```

フレームワークは自動的にインスタンス化されます。`TealiumCore`に依存しています。追加のインポート文は必要ありません。[Carthageを使用したiOSのインストールについての詳細はこちら](https://docs.tealium.com/ja/platforms/ios-swift-v1/install/#carthage)。

## 例

Tealium IQでリモートコマンドタグが構成され、アプリにモジュールがインストールされたら、以下の例に示すように初期化に次の行を追加します：

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
新しいリモートコマンドオブジェクトを作成し、`add`コマンドに渡す準備をします。

| パラメータ   | 説明                                       | 例       |
|-------------|---------------------------------------------------|--------------------|
| `commandId`   | リモートコマンドのための必須の文字列識別子 | `"logger" `       |
| `description` | リモートコマンドのオプションの文字列説明 | `"Log Response object to console"` |
| `queue`       | コードブロックをトリガーするキュー          | `DispatchQueue.main` |
| `completion`  | トリガーするコードブロック                      |                   |

以下は使用例です：

```swift
let customCommand = TealiumRemoteCommand(commandId: "logger",
                                        description: "Log Response object to console",
                                        queue: DispatchQueue.main)
                                        { (response) in
                                            // 実行するコード
                                            print("Custom command response: (response)")
                                        })
```

### `add()`


<blockquote>
1.6.5以降、`TealiumConfig`の[`addRemoteCommand()`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-config/#addremotecommand)メソッドを使用してリモートコマンドを追加することをお勧めします
</blockquote>


指定されたリモートコマンドをTealiumに登録して、後でトリガーできるようにします。Tealiumは新しいリモートコマンドを追加する前に初期化されている必要があります。

```swift
add(remoteCommand: TealiumRemoteCommand)
```

以下は使用例です：

```swift
var tealium: Tealium?
let customCommand = TealiumRemoteCommand(commandId: "logger",
    description: nil,
    queue: DispatchQueue.main)
    { response in
        // 実行するコード
        print("Custom command response: (response)")
    })
if let remoteCommands = self.tealium?.remoteCommands() {
        remoteCommands.add(customCommand)
} else {
print("Remote commands not available")
}
```

### `remove()`
以前に登録されたリモートコマンドを削除して、再度トリガーされないようにします。

```swift
remove(commandWithId: String)
```

```swift
// "tealium"が以前にインスタンス化されたと仮定
tealium?.remoteCommands()?.remove(commandWithId: "logger")
```

### `disableRemoteCommands()`

リモートコマンドモジュールを無効にします。

```swift
disableRemoteCommands()
```

以下は使用例です：

```swift
// "tealium"が以前にインスタンス化されたと仮定
tealium?.remoteCommands()?.disableRemoteCommands()
```

### `enableRemoteCommands()`

リモートコマンドモジュールを有効にします（以前に無効にされていた場合のみ必要です。デフォルトは有効です）。

```TealiumSwift
enabledRemoteCommands()
```

以下は使用例です：

```swift
// "tealium"が以前にインスタンス化されたと仮定
tealium?.remoteCommands()?.enableRemoteCommands()
```

### `disableRemoteHTTPCommand()`
組み込みのリモートHTTPコマンドを無効にしますが、他のコマンドのためにリモートコマンドモジュールは有効のままです。

```swift
disableRemoteHTTPCommand()
```

以下は使用例です：

```swift
// "tealium"が以前にインスタンス化されたと仮定
tealium?.remoteCommands()?.disableRemoteHTTPCommand()
```

### `enableRemoteHTTPCommand()`
組み込みのリモートHTTPコマンドを有効にします（以前に無効にされていた場合のみ必要です。デフォルトは有効です）。

```swift
enableRemoteHTTPCommand()`
```

以下は使用例です：

```swift
// "tealium"が以前にインスタンス化されたと仮定
tealium?.remoteCommands()?.enableRemoteHTTPCommand()
```


## リモートHTTPコマンド

これは、ネイティブコードからHTTPリクエストをトリガーし、レスポンスをTealium iQウェブビューに戻す、識別子`_http`の予約された内部コマンドです。このコマンドを使用する場合、特定のマッピング名を使用する必要があります：

| マッピング名 | 説明 |
| --- | --- |
| `url` | (必須) トリガーしたいリクエストのURL。 |
|`method`| (必須) 呼び出したいHTTPメソッド。現在サポートされているのはPUT、GET、POSTのみです。|
|`headers` |(オプション) リクエストと一緒に渡すヘッダーキーバリューペアを含むJavaScriptオブジェクト（JSON）。例えば、`{"Content-Type": "application/json"}`。|
|`callback_function`| (オプション) コマンドが完了したときに呼び出されるJavaScript関数。コールバック関数には2つのパラメータが渡されます：`code`は404や200などのHTTPレスポンスコードで、`body`はリクエストからのレスポンスボディです。|

こちらがサンプルのコールバック関数です：

```swift
var my_callback = function(code, body) {
   // レスポンスボディがJSONオブジェクトであったと仮定すると、これはウェブビューのコンソールにmy_response_variableという変数をログに記録します
	console.log(body.my_response_variable);
}
```