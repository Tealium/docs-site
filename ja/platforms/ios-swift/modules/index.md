---
title: モジュール
description: 利用可能なモジュールの一覧。
url: https://docs.tealium.com/ja/platforms/ios-swift/modules/
---Tealium Swiftライブラリは、モジュール式アーキテクチャを中心に設計されています。必要なモジュールは、ライブラリを初期化する際に`TealiumConfig`インスタンスで指定する必要があります。

すべてのモジュールは`TealiumCore`に依存しています。モジュールは、その目的に応じて`Collectors`と`Dispatchers`に分けられます。

## コレクター

コレクターは、デバイスから補足情報を収集し、Tealium Customer Data Hubに送信される前にデータレイヤーへ追加するモジュールです。一部のコレクターはコアライブラリに含まれていますが、その他はオプションであり、個別のモジュールとしてインストールします。

次の表に、利用可能なコレクターを示します。

| コレクター名 | TealiumConfigの参照 |
| --- | --- |
| `AppData`* | `Collectors.AppData`|
| `Attribution` | `Collectors.Attribution`|
| `Connectivity`* | `Collectors.Connectivity`|
| `Device`* | `Collectors.Device`|
| `Crash` | `Collectors.Crash`|
| `AutoTracking` | `Collectors.AutoTracking `|
| `Lifecycle` | `Collectors.Lifecycle`|
| `Location` | `Collectors.Location`|
| `VisitorService` | `Collectors.VisitorService`|

アスタリスク（`*`）が付いたモジュールは、コアライブラリに含まれています。これらはデフォルトで有効ですが、以下で説明する`TealiumConfig`の`collectors`プロパティを使用して無効にできます。

### 使用方法

`Collector`を追加するには、`TealiumConfig`インスタンスの`collectors`プロパティで指定します。

```swift
import TealiumCore
import TealiumLifecycle

let config = TealiumConfig(account: "ACCOUNT",
                               profile: "PROFILE",
                               environment: "ENVIRONMENT",
                               datasource: "DATASOURCE")

// Adds the Collectors you want. If omitted, default Collectors are added.
config.collectors = [Collectors.AppData, Collectors.Device, Collectors.Connectivity, Collectors.Lifecycle]                               
```

デフォルトのコレクターのみを使用するには、初期化コードから`config.collectors`の行を省略するか、コメントアウトします。


<blockquote>
When adding new collectors, be sure to also include `Collectors.Device` and `Collectors.Connectivity` in the array, otherwise these collectors will be disabled.
</blockquote>


AppDataコレクターは、Tealium訪問IDなどの重要な情報を収集するため、無効にすることはできません。

### カスタムコレクター

通常、カスタムコレクターは必要ありませんが、`Collector`プロトコルに準拠する独自のクラスを作成することで、カスタムコレクターを構築できます。次の例では、現在の曜日を収集し、トラッキング呼び出しごとにデータレイヤーへ追加するシンプルなコレクターを示します。

```swift
class MyDateCollector: Collector {
    var id = "MyDateCollector"

    var data: [String : Any]? {
        ["day_of_week": dayOfWeek]
    }

    var context: TealiumContext

    required init(context: TealiumContext,
                  delegate: ModuleDelegate?,
                  diskStorage: TealiumDiskStorageProtocol?,
                  completion: (ModuleResult) -> Void) {
        self.context = context
    }

    var dayOfWeek: String {
        return "\(Calendar.current.dateComponents([.weekday], from: Date()).weekday ?? -1)"
    }
}

// Add collector to your config instance prior to Tealium initialization

class TealiumHelper {
	// ...
	func startTracking() {
		let config = TealiumConfig(account: "ACCOUNT",
                               profile: "PROFILE",
                               environment: "ENVIRONMENT",
                               datasource: "DATASOURCE")

// Add the Collectors you want. If omitted, default Collectors are added.
config.collectors = [Collectors.AppData,
					  Collectors.Lifecycle,
					  MyDateCollector.self]   
					  self.tealium = Tealium(config: config) { _ in }
	}
}
```

## ディスパッチャー

ディスパッチャーは、データレイヤーからデータを取得し、Tealiumエンドポイントへ送信するモジュールです。現在、次のディスパッチャーを利用できます。

| ディスパッチャー名 | TealiumConfigの参照 |
| --- | --- |
| `Collect` | `Dispatchers.Collect`|
| `RemoteCommands` | `Dispatchers.RemoteCommands`|
| `TagManagement` | `Dispatchers.TagManagement`|


<blockquote>
At least one dispatcher is required. If no dispatchers are specified, your data is not sent anywhere.
</blockquote>


### 使用方法

`Dispatcher`を追加するには、`TealiumConfig`オブジェクトの`dispatchers`プロパティで指定します。

```swift
import TealiumCore
import TealiumLifecycle

let config = TealiumConfig(account: "ACCOUNT",
                               profile: "PROFILE",
                               environment: "ENVIRONMENT",
                               datasource: "DATASOURCE")

// Add the Collectors. you want Do not include if you want to use compiled Collectors
config.dispatchers = [Dispatchers.Collect]                               
```

### カスタムディスパッチャー

通常、カスタムディスパッチャーは必要ありませんが、`Dispatcher`プロトコルに準拠する独自のクラスを作成することで、カスタム`Dispatcher`を構築できます。次の例では、トラッキングリクエストごとにイベント名を出力するシンプルなディスパッチャーを示します。Tealiumエンドポイントに加えて、独自のカスタムエンドポイントへデータを送信する場合は、カスタム`Dispatcher`が役立つことがあります。

```swift
class MyCustomDispatcher: Dispatcher {
    var isReady: Bool
    var id = "MyCustomDispatcher"
    var config: TealiumConfig

    required init(config: TealiumConfig, delegate: ModuleDelegate, completion: ModuleCompletion?) {
        self.config = config
        self.isReady = true
    }

    func dynamicTrack(_ request: TealiumRequest, completion: ModuleCompletion?) {
        switch request {
        case let request as TealiumTrackRequest:
            print("Track received: \(request.event ?? "no event name")")
            // perform track action. For example, send to custom endpoint
        case _ as TealiumBatchTrackRequest:
            print("Batch track received")
            // perform batch track action. For example, send to custom endpoint
        default:
            return
        }
    }
}

// Add dispatcher to your config instance prior to Tealium initialization
class TealiumHelper {
	// ...
	func startTracking() {
		let config = TealiumConfig(account: "ACCOUNT",
                               profile: "PROFILE",
                               environment: "ENVIRONMENT",
                               datasource: "DATASOURCE")

   // add the Dispatchers you want
   config.dispatchers = [Dispatchers.Collect, MyCustomDispatcher.self]      
					  self.tealium = Tealium(config: config) { _ in }
}
```

## 推奨モジュール

### 基本実装

基本実装では、次のモジュールを推奨します。使用予定のTealium製品に応じて、少なくとも1つの`Dispatcher`を有効にする必要があります。

* AppDataコレクター
* Deviceコレクター
* Lifecycleコレクター

### クライアントサイド

基本モジュールに加えて、次のモジュールを使用すると、TealiumライブラリがTag Managementを使用してクライアントサイドでデータを処理できるようになります。

* TagManagementディスパッチャー - Tag Managementを使用するために必要
* RemoteCommandsディスパッチャー - Remote Commands機能が必要な場合にのみ必要

### サーバーサイド

基本モジュールに加えて、次のモジュールを使用すると、ライブラリからTealiumのサーバーサイド製品（Event Streaming、Customer Data Platform（CDP）、Event Data Framework）へデータを送信できるようになります。

* Collectディスパッチャー - サーバーサイド製品を使用するために必要
* Visitor Serviceコレクター - Customer Data Platform（CDP）から訪問プロファイルを取得する場合にのみ必要

## モジュールのインストール

CocoaPodsまたはCarthageを使用してモジュールをインストールします。

### CocoaPods

特定のモジュールを含める方法と除外する方法については、[CocoaPodsを使用したインストール](https://docs.tealium.com/ja/platforms/ios-swift/install/#cocoapods)を参照してください。
### Carthage

Carthage でインストールする場合は、必要なモジュールを明示的にインポートする必要があります。必要に応じてすべてのモジュールをインポートし、前述のモジュールリストを使用することもできますが、必要なモジュールだけをインポートすることで、アプリを軽量化できます。特定のモジュールを含める、または除外する手順については、[Carthage でインストール](https://docs.tealium.com/ja/platforms/ios-swift/install/#carthage)を参照してください。

### Swift Package Manager

特定のモジュールを含める、または除外する手順については、[Swift Package Manager でインストール](https://docs.tealium.com/ja/platforms/ios-swift/install#swift-package-manager-recommended)を参照してください。