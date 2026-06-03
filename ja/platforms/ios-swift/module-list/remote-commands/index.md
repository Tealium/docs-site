---
title: RemoteCommandsモジュール
description: Tealium iQタグ管理のイベントからネイティブコードブロックをトリガーすることを可能にし、拡張機能とロードルールによって制御されます。
url: https://docs.tealium.com/ja/platforms/ios-swift/module-list/remote-commands/
---
[リモートコマンド](/ja/platforms/remote-commands/)についてもっと学びましょう。

## 要件

* `webview`リモートコマンドを使用する場合、[TagManagementモジュール](/ja/platforms/ios-swift/module-list/tag-management/)が必要です。

コンパイル時の依存関係ではありませんが、リモートコマンドはモジュールからトリガーされます。

## 対応プラットフォーム

* iOS
* macOS（JSONのみ）
* tvOS（JSONのみ）
* watchOS（JSONのみ）

## インストール

Swift Package Manager、CocoaPods、またはCarthageでRemoteCommandsモジュールをインストールします。

### Swift Package Manager（推奨）

バージョン1.9.0以降でサポートされているSwift Package Manager（SMP）は、Tealium Swiftライブラリをインストールするための推奨される最も簡単な方法です：

1. Xcodeプロジェクトで**File &gt; Add Package Dependencies**を選択します。
2. リポジトリURLを入力します：`https://github.com/tealium/tealium-swift`
3. バージョンルールを構成します。通常、`&#34;Up to next major&#34;`が推奨されます。現在のTealium Swiftライブラリバージョンがリストに表示されない場合は、Swiftパッケージキャッシュをリセットしてください。
4. インストールするモジュールのリストからRemoteCommandsモジュールを選択し、Xcodeプロジェクトのアプリターゲットの**Frameworks and Libraries**に追加します。

[iOSのSPMインストール](/ja/platforms/ios-swift/install/#swift-package-manager-recommended)についてもっと学びましょう。

### CocoaPods

CocoaPodsでRemoteCommandsモジュールをインストールするには、Podfileに次のポッドを追加します：
```perl
pod &#39;tealium-swift/RemoteCommands&#39;
```

[iOSのCocoaPodsインストール](/ja/platforms/ios-swift/install/#cocoapods)についてもっと学びましょう。

### Carthage

CarthageでRemoteCommandsモジュールをインストールするには、次の手順に従います：

1. XcodeでアプリターゲットのGeneral構成ページに移動します。

2. **Embedded Binaries**セクションに次のフレームワークを追加します：
      ```perl
      TealiumRemoteCommands.framework
      ```
3. RemoteCommands APIと連携する必要がある場合は、プロジェクトに次の必要なインポートステートメントを追加します：

      ```swift
      import TealiumRemoteCommands
      ```

[iOSのCarthageインストール](/ja/platforms/ios-swift/install/#carthage)についてもっと学びましょう。

## リモートコマンドのオプション

リモートコマンドには2つの構成オプションがあります：

* **JSONファイル**  
ベンダー構成、データマッピング、イベントトリガーを含む、ローカルまたはリモートでホストされたJSONファイル。
* **リモートコマンドタグ**  
iQタグ管理内のタグで、ベンダーのAPIの構成オプションを提供します（Tag Managementモジュールと使用する場合）。

[リモートコマンドベンダー統合のリスト](/ja/platforms/remote-commands/integrations/)を参照してください。

### 例

Tealium iQタグ管理でリモートコマンドタグを構成します。アプリ内またはリモートサーバー上のJSONファイルを使用することもできます。構成後、`TealiumConfig`の[`addRemoteCommand()`](/ja/platforms/ios-swift/api/tealium-config/#addremotecommand)を使用してリモートコマンドを登録します。`Tealium`を初期化する前に登録を完了してください：





```swift
var tealium: Tealium?

let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                           profile: &#34;PROFILE&#34;,
                           environment: &#34;ENVIRONMENT&#34;,
                           dataSource: &#34;DATASOURCE&#34;)

let remoteCommand = RemoteCommand(commandId: &#34;display&#34;, description: &#34;Display Prompt&#34;) { response in
    guard let payload = response.payload else {
        return
    }
    print(&#34;Use response payload: \(payload)&#34;)
}
config.addRemoteCommand(remoteCommand)

tealium = Tealium(config: config)
```




```swift
var tealium: Tealium?

let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                           profile: &#34;PROFILE&#34;,
                           environment: &#34;ENVIRONMENT&#34;,
                           dataSource: &#34;DATASOURCE&#34;)

let remoteCommand = RemoteCommand(commandId: &#34;display&#34;, description: &#34;Display Prompt&#34;, type: .local(file: &#34;FILENAME&#34;)) { response in
    guard let payload = response.payload else {
        return
    }
    print(&#34;Use response payload: \(payload)&#34;)
}
config.addRemoteCommand(remoteCommand)

tealium = Tealium(config: config)
```





```swift
var tealium: Tealium?

let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                           profile: &#34;PROFILE&#34;,
                           environment: &#34;ENVIRONMENT&#34;,
                           dataSource: &#34;DATASOURCE&#34;)

let remoteCommand = RemoteCommand(commandId: &#34;display&#34;, description: &#34;Display Prompt&#34;, type: .remote(url: &#34;https://tags.tiqcdn.com/dle/ACCOUNT/PROFILE/FILENAME.json&#34;)) { response in
    guard let payload is response.payload else {
        return
    }
    print(&#34;Use response payload: \(payload)&#34;)
}
config.addRemoteCommand(remoteCommand)

tealium = Tealium(config: config)
```





### 初期化後にリモートコマンドを追加する

`Tealium`を初期化した後、`tealium.remoteCommands`マネージャーを使用してリモートコマンドを追加します。可能な限り、すべてのイベントを受信するために`TealiumConfig`でリモートコマンドを追加することをお勧めします。デフォルトでは、`webview`コマンドはロード時に初期化されるため、後から`tealium.remoteCommands`を介して追加すると、初期化を逃す可能性があります。

`Tealium`が初期化された後にリモートコマンドを追加する必要がある場合は、次のパターンを使用します：

```swift
tealium = Tealium(config: config)

let remoteCommand = RemoteCommand(
    commandId: &#34;display&#34;,
    description: &#34;Display Prompt&#34;,
    type: .remote(url: &#34;https://tags.tiqcdn.com/dle/ACCOUNT/PROFILE/FILENAME.json&#34;)) { response in
    guard let payload = response.payload else {
        return
    }
    print(&#34;Use response payload: \(payload)&#34;)
}
tealium?.remoteCommands.add(remoteCommand)
```

## データレイヤー

このモジュールによって追加される変数はありません。

## APIリファレンス

### `init()`
`add`コマンドに渡すための新しいリモートコマンドオブジェクトを作成します。

| パラメータ   | 説明                                       | 例       |
|-------------|---------------------------------------------------|--------------------|
| `commandId`   | リモートコマンドのための必須の文字列識別子 | `&#34;logger&#34; `       |
| `description` | リモートコマンドのオプションの文字列説明 | `&#34;Log Response object to console&#34;` |
| `type`       | リモートコマンドのタイプ（デフォルトはwebview、ローカルまたはリモートのJSON）     | `.local(file: &#34;logger&#34;)` |
| `completion`  | トリガーするコードブロック                      |                   |

以下は使用例です：

```swift
let customCommand = TealiumRemoteCommand(commandId: &#34;logger&#34;,
                                        description: &#34;Log Response object to console&#34;,
                                        type: .local(file: &#34;logger&#34;))
                                        { (response) in
                                            // 実行するコード
                                            print(&#34;Custom command response: \(response)&#34;)
                                        })
```
### `add()`

1.6.5以降、`TealiumConfig`の[`addRemoteCommand()`](/ja/platforms/ios-swift/api/tealium-config/#addremotecommand)メソッドを使用してリモートコマンドを追加することを推奨します。

Tealiumに特定のリモートコマンドを登録し、後でトリガーできるようにします。新しいリモートコマンドを追加する前にTealiumが初期化されている必要があります。

```swift
add(_ remoteCommand: TealiumRemoteCommandProtocol)
```

以下は使用例です：

```swift
var tealium: Tealium?
let customCommand = RemoteCommand(commandId: &#34;logger&#34;,
    description: nil)
    { response in
        // 実行するコード
        print(&#34;カスタムコマンドの応答: \(response)&#34;)
    }
if let remoteCommands = self.tealium?.remoteCommands {
        remoteCommands.add(customCommand)
} else {
		print(&#34;リモートコマンドは利用できません&#34;)
}
```

### `remove()`
以前に登録されたリモートコマンドを削除し、再度トリガーされるのを防ぎます。

```swift
remove(commandWithId: String)
```

```swift
remove(jsonCommand: String)
```

```swift
// &#34;tealium&#34;は以前にインスタンス化されていると仮定
tealium?.remoteCommands?.remove(commandWithId: &#34;logger&#34;)

tealium?.remoteCommands?.remove(jsonCommand: &#34;logger&#34;)
```

### `remoteHTTPCommandDisabled`
`true`の場合、組み込みのリモートHTTPコマンドを無効にしますが、他のコマンド用のリモートコマンドモジュールは有効のままです。デフォルトは`false` - [リモートHTTPコマンド](#remote-http-command)が有効です。

```swift
remoteHTTPCommandDisabled
```

以下は使用例です：

```swift
// &#34;config&#34;は以前にインスタンス化されていると仮定 (`TealiumConfig()`)
config.remoteHTTPCommandDisabled = false
```

## リモートHTTPコマンド

これは、ネイティブコードからHTTPリクエストをトリガーし、Tealium iQウェブビューにレスポンスを返す内部コマンドで、識別子は`_http`です。これは、ウェブブラウザで遭遇する可能性のあるCORS制限を回避するためにいくつかの場合に使用されます。このコマンドを使用するには、特定のマッピング名を使用する必要があります：

| マッピング名 | 説明 |
| --- | --- |
| `url` | (必須) トリガーしたいリクエストのURL。 |
|`method`| (必須) 呼び出すHTTPメソッド。現在サポートされているのはPUT、GET、POSTのみです。|
|`headers` |(オプション) リクエストと共に渡すヘッダーのキーと値のペアを含むJavaScriptオブジェクト（JSON）。例えば、`{&#34;Content-Type&#34;: &#34;application/json&#34;}`。|
|`callback_function`| (オプション) コマンドが完了したときに呼び出されるJavaScript関数。コールバック関数には2つのパラメータが渡されます：`code`はHTTPレスポンスコード（例：404または200）、`body`はリクエストからのレスポンスボディです。|

以下はコールバック関数の例です：

```swift
var my_callback = function(code, body) {
   // レスポンスボディがJSONオブジェクトであったと仮定すると、これはウェブビューのコンソールにmy_response_variableという変数をログに記録します
	console.log(body.my_response_variable);
}
```