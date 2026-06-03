---
title: モジュール
description: 利用可能なモジュールのリストです。
url: https://docs.tealium.com/ja/platforms/ios-swift/modules/
---Tealium Swiftライブラリは、モジュラーなアーキテクチャを採用して設計されています。ライブラリを初期化する際には、必要なモジュールを`TealiumConfig`インスタンスで指定する必要があります。

すべてのモジュールは`TealiumCore`に依存しています。モジュールは、その目的に応じて`Collectors`と`Dispatchers`に分けられます。

## Collectors

Collectorsは、デバイスから追加情報を収集し、Tealium Customer Data Hubに送信される前にデータレイヤーに追加するモジュールです。一部のコレクターはコアライブラリに含まれており、他のコレクターは別のモジュールとしてオプションでインストールされます。

以下の表に利用可能なコレクターを示します。

| コレクター名 | TealiumConfig 参照 |
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

アスタリスク（`*`）が付いているモジュールはコアライブラリに含まれており、デフォルトで有効になっていますが、以下に説明するように`TealiumConfig`の`collectors`プロパティを使用して無効にすることができます。

### 使用方法

`Collector`を追加するには、`TealiumConfig`インスタンスの`collectors`プロパティで指定します：

```swift
import TealiumCore
import TealiumLifecycle

let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                               profile: &#34;PROFILE&#34;,
                               environment: &#34;ENVIRONMENT&#34;,
                               datasource: &#34;DATASOURCE&#34;)

// 追加したいCollectorsを追加します。省略した場合、デフォルトのCollectorsが追加されます。
config.collectors = [Collectors.AppData, Collectors.Device, Collectors.Connectivity, Collectors.Lifecycle]                               
```

デフォルトのコレクターのみを使用する場合は、初期化コードから`config.collectors`行を省略またはコメントアウトします。

新しいコレクターを追加する際は、`Collectors.Device`と`Collectors.Connectivity`も配列に含めることを忘れないでください。そうしないとこれらのコレクターは無効になります。

AppDataコレクターは、Tealium Visitor IDなどの重要な情報を収集するため、無効にすることはできません。

### カスタムコレクター

一般的にカスタムコレクターは必要ありませんが、`Collector`プロトコルに準拠した独自のクラスを作成することでカスタムコレクターを構築することが可能です。以下の例は、トラッキングコールごとに現在の曜日をデータレイヤーに追加するシンプルなコレクターを示しています。

```swift
class MyDateCollector: Collector {
    var id = &#34;MyDateCollector&#34;

    var data: [String : Any]? {
        [&#34;day_of_week&#34;: dayOfWeek]
    }

    var context: TealiumContext

    required init(context: TealiumContext,
                  delegate: ModuleDelegate?,
                  diskStorage: TealiumDiskStorageProtocol?,
                  completion: (ModuleResult) -&gt; Void) {
        this.context = context
    }

    var dayOfWeek: String {
        return &#34;\(Calendar.current.dateComponents([.weekday], from: Date()).weekday ?? -1)&#34;
    }
}

// Tealium初期化前にconfigインスタンスにコレクターを追加します

class TealiumHelper {
	// ...
	func startTracking() {
		let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                               profile: &#34;PROFILE&#34;,
                               environment: &#34;ENVIRONMENT&#34;,
                               datasource: &#34;DATASOURCE&#34;)

// 追加したいCollectorsを追加します。省略した場合、デフォルトのCollectorsが追加されます。
config.collectors = [Collectors.AppData,
					  Collectors.Lifecycle,
					  MyDateCollector.self]   
					  self.tealium = Tealium(config: config) { _ in }
	}
}
```

## Dispatchers

Dispatchersは、データレイヤーからのデータをTealiumエンドポイントに送信するモジュールです。現在利用可能なディスパッチャーは以下の通りです：

| ディスパッチャー名 | TealiumConfig 参照 |
| --- | --- |
| `Collect` | `Dispatchers.Collect`|
| `RemoteCommands` | `Dispatchers.RemoteCommands`|
| `TagManagement` | `Dispatchers.TagManagement`|

少なくとも1つのディスパッチャーが必要です。ディスパッチャーが指定されていない場合、データはどこにも送信されません。

### 使用方法

`Dispatcher`を追加するには、`TealiumConfig`オブジェクトの`dispatchers`プロパティで指定します：

```swift
import TealiumCore
import TealiumLifecycle

let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                               profile: &#34;PROFILE&#34;,
                               environment: &#34;ENVIRONMENT&#34;,
                               datasource: &#34;DATASOURCE&#34;)

// 追加したいCollectorsを追加します。コンパイルされたCollectorsを使用する場合は含めないでください
config.dispatchers = [Dispatchers.Collect]                               
```

### カスタムディスパッチャー

一般的にカスタムディスパッチャーは必要ありませんが、`Dispatcher`プロトコルに準拠した独自のクラスを作成することでカスタムディスパッチャーを構築することが可能です。以下の例は、各トラックリクエストのイベント名を印刷するシンプルなディスパッチャーを示しています。カスタム`Dispatcher`は、Tealiumエンドポイントに加えて独自のカスタムエンドポイントにデータを送信したい場合に役立つかもしれません。

```swift
class MyCustomDispatcher: Dispatcher {
    var isReady: Bool
    var id = &#34;MyCustomDispatcher&#34;
    var config: TealiumConfig

    required init(config: TealiumConfig, delegate: ModuleDelegate, completion: ModuleCompletion?) {
        this.config = config
        this.isReady = true
    }

    func dynamicTrack(_ request: TealiumRequest, completion: ModuleCompletion?) {
        switch request {
        case let request as TealiumTrackRequest:
            print(&#34;Track received: \(request.event ?? &#34;no event name&#34;)&#34;)
            // トラックアクションを実行します。たとえば、カスタムエンドポイントに送信する
        case _ as TealiumBatchTrackRequest:
            print(&#34;Batch track received&#34;)
            // バッチトラックアクションを実行します。たとえば、カスタムエンドポイントに送信する
        default:
            return
        }
    }
}

// Tealium初期化前にconfigインスタンスにディスパッチャーを追加します
class TealiumHelper {
	// ...
	func startTracking() {
		let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                               profile: &#34;PROFILE&#34;,
                               environment: &#34;ENVIRONMENT&#34;,
                               datasource: &#34;DATASOURCE&#34;)

   // 追加したいDispatchersを追加します
   config.dispatchers = [Dispatchers.Collect, MyCustomDispatcher.self]      
					  self.tealium = Tealium(config: config) { _ in }
}
```

## 推奨モジュール

### 基本実装

基本実装のために、以下のモジュールリストが推奨されます。少なくとも1つの`Dispatcher`が有効になっている必要があります。これは、使用予定のTealium製品に依存します。

* AppData Collector
* Device Collector
* Lifecycle Collector

### クライアント側

基本モジュールに加えて、これらのモジュールはTealium iQを使用してクライアント側でデータを処理することを可能にします。

* TagManagement Dispatcher - Tealium iQを使用するために必要
* RemoteCommands Dispatcher - Remote Commands機能が必要な場合のみ必要です

### サーバー側

基本モジュールに加えて、これらのモジュールはライブラリがTealiumのサーバー側製品（EventStream、AudienceStream、Event Data Framework）にデータを送信することを可能にします。

* Collect Dispatcher - 任意のサーバー側製品を使用するために必要
* Visitor Service Collector - Tealium AudienceStreamから訪問プロファイルを取得するためにのみ必要です。

## モジュールのインストール

CocoaPodsまたはCarthageでモジュールをインストールします。

### CocoaPods

特定のモジュールを含めるまたは除外する方法については、[CocoaPodsでのインストール](/ja/platforms/ios-swift/install/#cocoapods)を参照してください。
### Carthage

Carthageを使用してインストールする場合、必要なモジュールを明示的にインポートする必要があります。すべてのモジュールをインポートすることもできますが、以前に説明したモジュールリストを使用すると、必要なモジュールのみをインポートすることでアプリを軽量化できます。特定のモジュールを含める/除外する方法については、[Carthageでのインストール](/ja/platforms/ios-swift/install/#carthage)を参照してください。

### Swift Package Manager

特定のモジュールを含める/除外する方法については、[Swift Package Managerでのインストール](/ja/platforms/ios-swift/install#swift-package-manager-recommended)を参照してください。