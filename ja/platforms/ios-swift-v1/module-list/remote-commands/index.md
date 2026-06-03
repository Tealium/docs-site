---
title: RemoteCommandsモジュール
description: Tealium iQタグ管理のイベントからネイティブコードブロックをトリガーすることを可能にし、拡張機能とロードルールによって制御されます。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/remote-commands/
---
[詳細はこちら](/ja/platforms/remote-commands/)をご覧ください。

## 要件

* Tealium iQタグ管理モジュール。コンパイル時の依存関係ではありませんが、リモートコマンドはこのモジュールからトリガーされます。

## 対応プラットフォーム

* iOS

## インストール

CocoaPodsまたはCarthageでRemoteCommandsモジュールをインストールします。

### CocoaPods

CocoaPodsでRemoteCommandsモジュールをインストールするには、Podfileに以下のpodを追加します：
```ruby
pod &#39;tealium-swift/TealiumRemoteCommands&#39;
```

フレームワークは自動的にインスタンス化されます。`TealiumCore` podに依存しています。[CocoaPodsを使用したiOSのインストールについての詳細はこちら](/ja/platforms/ios-swift-v1/install/#cocoapods)。

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

フレームワークは自動的にインスタンス化されます。`TealiumCore`に依存しています。追加のインポート文は必要ありません。[Carthageを使用したiOSのインストールについての詳細はこちら](/ja/platforms/ios-swift-v1/install/#carthage)。

## 例

Tealium IQでリモートコマンドタグが構成され、アプリにモジュールがインストールされたら、以下の例に示すように初期化に次の行を追加します：

```swift
class TealiumHelper {
	var tealium: Tealium?
	// ...
	private func initTealium() {
		let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
 	       		                 profile: &#34;PROFILE&#34;,
        	   	                 environment: &#34;ENVIRONMENT&#34;,
           		                 datasource: &#34;DATASOURCE&#34;)
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
| `commandId`   | リモートコマンドのための必須の文字列識別子 | `&#34;logger&#34; `       |
| `description` | リモートコマンドのオプションの文字列説明 | `&#34;Log Response object to console&#34;` |
| `queue`       | コードブロックをトリガーするキュー          | `DispatchQueue.main` |
| `completion`  | トリガーするコードブロック                      |                   |

以下は使用例です：

```swift
let customCommand = TealiumRemoteCommand(commandId: &#34;logger&#34;,
                                        description: &#34;Log Response object to console&#34;,
                                        queue: DispatchQueue.main)
                                        { (response) in
                                            // 実行するコード
                                            print(&#34;Custom command response: (response)&#34;)
                                        })
```

### `add()`

1.6.5以降、`TealiumConfig`の[`addRemoteCommand()`](/ja/platforms/ios-swift-v1/api/tealium-config/#addremotecommand)メソッドを使用してリモートコマンドを追加することをお勧めします

指定されたリモートコマンドをTealiumに登録して、後でトリガーできるようにします。Tealiumは新しいリモートコマンドを追加する前に初期化されている必要があります。

```swift
add(remoteCommand: TealiumRemoteCommand)
```

以下は使用例です：

```swift
var tealium: Tealium?
let customCommand = TealiumRemoteCommand(commandId: &#34;logger&#34;,
    description: nil,
    queue: DispatchQueue.main)
    { response in
        // 実行するコード
        print(&#34;Custom command response: (response)&#34;)
    })
if let remoteCommands = self.tealium?.remoteCommands() {
        remoteCommands.add(customCommand)
} else {
print(&#34;Remote commands not available&#34;)
}
```

### `remove()`
以前に登録されたリモートコマンドを削除して、再度トリガーされないようにします。

```swift
remove(commandWithId: String)
```

```swift
// &#34;tealium&#34;が以前にインスタンス化されたと仮定
tealium?.remoteCommands()?.remove(commandWithId: &#34;logger&#34;)
```

### `disableRemoteCommands()`

リモートコマンドモジュールを無効にします。

```swift
disableRemoteCommands()
```

以下は使用例です：

```swift
// &#34;tealium&#34;が以前にインスタンス化されたと仮定
tealium?.remoteCommands()?.disableRemoteCommands()
```

### `enableRemoteCommands()`

リモートコマンドモジュールを有効にします（以前に無効にされていた場合のみ必要です。デフォルトは有効です）。

```TealiumSwift
enabledRemoteCommands()
```

以下は使用例です：

```swift
// &#34;tealium&#34;が以前にインスタンス化されたと仮定
tealium?.remoteCommands()?.enableRemoteCommands()
```

### `disableRemoteHTTPCommand()`
組み込みのリモートHTTPコマンドを無効にしますが、他のコマンドのためにリモートコマンドモジュールは有効のままです。

```swift
disableRemoteHTTPCommand()
```

以下は使用例です：

```swift
// &#34;tealium&#34;が以前にインスタンス化されたと仮定
tealium?.remoteCommands()?.disableRemoteHTTPCommand()
```

### `enableRemoteHTTPCommand()`
組み込みのリモートHTTPコマンドを有効にします（以前に無効にされていた場合のみ必要です。デフォルトは有効です）。

```swift
enableRemoteHTTPCommand()`
```

以下は使用例です：

```swift
// &#34;tealium&#34;が以前にインスタンス化されたと仮定
tealium?.remoteCommands()?.enableRemoteHTTPCommand()
```


## リモートHTTPコマンド

これは、ネイティブコードからHTTPリクエストをトリガーし、レスポンスをTealium iQウェブビューに戻す、識別子`_http`の予約された内部コマンドです。このコマンドを使用する場合、特定のマッピング名を使用する必要があります：

| マッピング名 | 説明 |
| --- | --- |
| `url` | (必須) トリガーしたいリクエストのURL。 |
|`method`| (必須) 呼び出したいHTTPメソッド。現在サポートされているのはPUT、GET、POSTのみです。|
|`headers` |(オプション) リクエストと一緒に渡すヘッダーキーバリューペアを含むJavaScriptオブジェクト（JSON）。例えば、`{&#34;Content-Type&#34;: &#34;application/json&#34;}`。|
|`callback_function`| (オプション) コマンドが完了したときに呼び出されるJavaScript関数。コールバック関数には2つのパラメータが渡されます：`code`は404や200などのHTTPレスポンスコードで、`body`はリクエストからのレスポンスボディです。|

こちらがサンプルのコールバック関数です：

```swift
var my_callback = function(code, body) {
   // レスポンスボディがJSONオブジェクトであったと仮定すると、これはウェブビューのコンソールにmy_response_variableという変数をログに記録します
	console.log(body.my_response_variable);
}
```