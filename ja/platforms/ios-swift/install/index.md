---
title: インストール
description: iOS（Swift）向けTealium SDKのインストール方法について説明します。
url: https://docs.tealium.com/ja/platforms/ios-swift/install/
---

<blockquote>
現在のTealium for Swift SDKのバージョンは2.xです。以前のバージョンについては、[Swift 1.x](https://docs.tealium.com/ja/platforms/ios-swift-v1)または[Objective-C](https://docs.tealium.com/ja/platforms/ios-objective-c/)を参照してください。Swiftコードは、同じプロジェクト内で既存のObjective-Cファイルと共存し、Objective-C APIへ完全にアクセスできるため、簡単に導入できます。
</blockquote>


## 要件

* Xcode 7.0以降
* iOS 9.0以降、macOS 10.11以降、watchOS 3.0以降、またはtvOS 9.2以降
* [タグ管理モバイルプロファイル](https://docs.tealium.com/create-mobile-profile/)
* [Tealium Customer Data Hubアカウント](https://docs.tealium.com/introduction-to-customer-data-hub/)

## サンプルアプリ

iOS（Swift）の[サンプルアプリ](https://github.com/Tealium/tealium-swift/tree/master/samples)を参照し、Tealiumライブラリ、トラッキングメソッド、およびベストプラクティスに基づく実装について理解を深めてください。

Tealiumの実装をアプリの他の部分から抽象化するため、ヘルパークラスの使用を推奨します。これにより、初期化とトラッキング呼び出しを行うためのエントリポイントを1つにまとめることができます。また、すべての`View`やSwiftファイルを変更するのではなく、ヘルパーファイル内のコードだけを更新できるようになります。

[サンプルヘルパークラス](https://github.com/Tealium/tealium-swift/tree/master/samples/TealiumSwiftExample)を参照してください。

## インストール

Tealium iOSライブラリはモジュールに分割されています。リソース使用量を抑えるため、必要なモジュールのみをインストールすることを推奨します。iOSで利用可能なモジュールについては、[詳細情報](https://docs.tealium.com/ja/platforms/ios-swift/modules/)を参照してください。

Swift Package Manager、CocoaPods、またはCarthageを使用してTealium for iOSライブラリをインストールします。

### Swift Package Manager（推奨）

Swift Package Managerは、Tealium Swiftライブラリをインストールするための最も簡単な推奨方法です。

1. Xcodeプロジェクトで、**File > Add Package Dependencies**を選択します。
1. リポジトリURLとして`https://github.com/tealium/tealium-swift`を入力します。
1. バージョンルールを構成します。通常は`Up to next major`を推奨します。現在のTealium Swiftライブラリのバージョンがリストに表示されない場合は、Swiftパッケージのキャッシュをリセットしてください。
1. インストールするモジュールを選択し、そのモジュールをインストールするアプリターゲットを選択します。

プロジェクトに複数のアプリターゲットがあり、追加のアプリターゲットでもTealium Swiftライブラリが必要な場合は、**Frameworks and Libraries**セクションで手動で追加する必要があります。

追加のアプリターゲットにTealium Swiftライブラリをインストールするには、次の手順を実行します。

1. **Project Navigator**でXcodeプロジェクトを選択します。
1. Xcodeプロジェクトの**TARGETS**セクションでアプリターゲットを選択します。
1. **Frameworks and Libraries**に移動し、Tealium Swiftライブラリを選択してアプリターゲットに追加します。


<blockquote>
Swift Package Managerでは、パッケージ内のターゲットを特定のプラットフォームに限定できません。たとえば、iOSのみをサポートする[`TagManagement`](https://docs.tealium.com/ja/platforms/ios-swift/module-list/tag-management/)などのモジュールも、iOS以外のターゲットで利用可能になります。これらのモジュールは、Xcode上のSPMを通じて技術的にはiOS以外のターゲットでも利用可能ですが、そのようなターゲットに追加すると、利用できないシステムライブラリが原因でコンパイラエラーが発生します。iOS専用モジュールはiOSアプリにのみ追加する必要があるため、この制限がユーザーに影響することはありません。
</blockquote>


### CocoaPods

CocoaPodsを使用してTealium for iOSライブラリをインストールするには、次の手順を実行します（推奨）。

1. Tealium SwiftのPod `"tealium-swift"`をPodfileに追加します。各モジュールに対応するsubspecがあり、それぞれが「Core」モジュールに依存しています。subspecを指定しない場合、デフォルトですべてのモジュールがインストールされます。
      ```ruby
      # Uncomment the next line to define a global platform for your project
      platform :ios, '11.0'

      target 'CPodTest' do
            # Comment the next line if you don't want to use dynamic frameworks
            use_frameworks!

            # Pods for CPodTest

            # new entry for Tealium pod
            pod 'tealium-swift' # all modules
            # pod 'tealium-swift/TagManagement' # to install individual modules only, use subspecs
      end
      ```

2. 必要なモジュールを追加したら、次のコマンドを実行します。
      ```ruby
      pod install
      ```

<blockquote>
コマンドで正しいPodが見つからない場合は、`pod repo update`コマンドを実行してください。
</blockquote>


3. `.xcworkspace`ファイルを使用してXcodeプロジェクトを開きます（`.xcodeproj`ファイルは使用しないでください）。

4. 任意の数のモジュールをインポートするには、Tealiumをインスタンス化するファイルに次のimport文を追加します。
      ```swift
      import TealiumSwift
      ```

#### 推奨Podfile

Podfileに追加することを推奨するモジュールの一覧を次に示します。


<blockquote>
Podfile内の特定のモジュールを無効にするには、`#`を使用して該当行をコメントアウトするか、その行を削除します。
</blockquote>


```ruby
# ...
# *** Recommended minimum:
# All pods depend on Core. Supports all platforms.
pod "tealium-swift/Core"
pod "tealium-swift/Lifecycle"
pod "tealium-swift/Collect" # for Server-side products. For example: Event Streaming - usually this or TealiumTagManagement, but not often both
# OR
pod "tealium-swift/TagManagement" # for Tag Management
pod "tealium-swift/RemoteCommands"

# *** Optional modules: You may not need these modules. Enable as required.   *** #

# Provides Visitor Audience and Attiribute information back to the app
# pod "tealium-swift/VisitorService"

# iOS Only. Gathers app attribution data and advertising IDs.
# pod "tealium-swift/Attribution"

# iOS and tvOS only. Generally not recommended. See separate notes in module documentation.
# pod "tealium-swift/Autotracking"

# See separate notes in module documentation.
# pod "tealium-swift/Location"

# iOS only. Reports detailed crash information.
# Installs separate TealiumCrashReporter dependency (based on PLCrashReporter).
# pod "TealiumCrashModule"
# ...
```

### Carthage

Carthageを使用してTealium for iOS（Swift）をインストールするには、次の手順を実行します。

1. Cartfileに次の内容を追加します。
      ```bash
      github "tealium/tealium-swift"
      ```

2. iOS、macOS、tvOS、およびwatchOS用のフレームワークを生成するには、次のコマンドを実行します。
      ```bash
      carthage update
      ```

3. iOSなどの特定のプラットフォームのみを対象にビルドし、初回ビルド後のビルドを高速化するには、Carthageの`--platform`引数を使用します。
      ```bash
      carthage update --platform ios --cache-builds
      ```

4. 必要なフレームワークを、Xcodeプロジェクトの**General > Embedded Binaries**セクションにドラッグします。

<blockquote>
Tealiumフレームワークがプロジェクト構成のEmbedded Binariesセクションに追加されていることを確認してください。追加されていない場合、アプリが起動時にクラッシュします。
</blockquote>


5. アプリの提出時に問題が発生しないよう、[Carthage Getting Started](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos)ドキュメントの手順に従って、該当するビルドフェーズスクリプトを追加します。
#### モジュールのインポート

Tealium Swift SDK は、個別のモジュール／フレームワークに分割されています。バイナリサイズを削減し、アプリのパフォーマンスを向上させるため、必要なモジュールのフレームワークのみをインポートしてください。

**モジュールのインポート文**

* **TealiumCore** - Tealium、TealiumConfig、TealiumInstanceManager に必要
* **TealiumTagManagement** - トラッキング呼び出しを Tag Management に送信するために必要
* **TealiumCollect** - トラッキング呼び出しを Tealium の Customer Data Hub に送信するために必要
* **TealiumRemoteCommands** - Remote Commands API と連携する場合に必要
* **TealiumLifecycle** - ライフサイクルイベントと関連データを収集する場合に必要

```swift
import TealiumCore
import TealiumTagManagement
import TealiumCollect
import TealiumRemoteCommands
import TealiumLifecycle
```

Carthage の制約により、SDK 全体をインポートする利便性と、完全なモジュール式インストールによる柔軟性およびパフォーマンス向上のどちらかを選択する必要がありました。そのため、使用する各モジュールを個別に追加する必要があります。

- Carthage はすべてのモジュールをビルドし、生成された `.framework` ファイルを Carthage のビルドディレクトリに出力します。
- 不要なモジュールを削除し、必要なモジュールを Xcode にドラッグします。

推奨されるモジュールの一覧について詳しくは、[モジュール](https://docs.tealium.com/ja/platforms/ios-swift/modules/)を参照してください。

## 初期化

Tealium を初期化するには、[`TealiumConfig`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/) インスタンスを [`Tealium()`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium/#tealium) コンストラクターに渡します。


<blockquote>
Tealium iOS ライブラリへの単一のエントリーポイントを提供し、今後のアップグレードを簡素化するトラッキングヘルパークラスを使用して、[`Tealium`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium/#class-tealium) インスタンスを管理してください。
</blockquote>


```swift
class TealiumHelper {
    static let shared = TealiumHelper()
    let config = TealiumConfig(account: "ACCOUNT",
                               profile: "PROFILE",
                               environment: "ENVIRONMENT",
                               datasource: "DATASOURCE")
    var tealium: Tealium?

    private init() {

        // add necessary config options
        config.batchingEnabled = true
        config.logLevel = .debug

        // add the Collectors you want
        config.collectors = [Collectors.Lifecycle,
                             Collectors.Location,
                             Collectors.VisitorService]

        // add the Dispatchers you want
        config.dispatchers = [Dispatchers.TagManagement,
                              Dispatchers.RemoteCommands]

        tealium = Tealium(config: config)

        // optional post init processing
        tealium?.dataLayer.add(key: "mykey", value: "myvalue", expiry: .forever)

    }

    public func start() {
        _ = TealiumHelper.shared
    }

    class func trackView(title: String, data: [String: Any]?) {
      let tealView = TealiumView(title, dataLayer: data)
      TealiumHelper.shared.tealium?.track(tealView)
    }

    class func trackEvent(title: String, data: [String: Any]?) {
      let tealEvent = TealiumEvent(title, dataLayer: data)
      TealiumHelper.shared.tealium?.track(tealEvent)
    }
}
```

以下を置き換えます。

* `ACCOUNT`：ライブラリの初期化に使用する Tealium アカウント名（小文字）。
* `PROFILE`：ライブラリの初期化に使用する Tealium プロファイル名（小文字）。
* `ENVIRONMENT`：Tealium を初期化する環境。
* `DATASOURCE`：使用する Tealium データソース。


<blockquote>
Mobile Publish Settings はデフォルトで有効になっているため、使用しない場合は無効にする必要があります。Tag Management で Mobile Publish Settings を構成するか、`config.shouldUseRemotePublishSettings = false` を使用して無効にしてください。
</blockquote>


## ログレベル

ログレベルを構成するには、`TealiumConfig` インスタンスの [`logLevel`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#loglevel) プロパティを構成します。

```swift
config.logLevel = .debug // or .info, .error, .fault, .silent
```

デバッグ用途では、`.debug` を推奨します。

デフォルトで使用されるログタイプは [`OSLog`](https://developer.apple.com/documentation/os/oslog) ですが、`TealiumConfig` オブジェクトの `logType` プロパティを更新することで、`.print` を使用するように変更できます。

```swift
config.logType = .print
```

`TealiumLogger` を使用する代わりに、独自のロガーを追加することもできます。そのためには、`Logger` クラスを `TealiumLoggerProtocol` に準拠させ、そのクラスのインスタンスを `TealiumConfig` オブジェクトの `logger` プロパティに構成します。以下に例を示します。

```swift
class CustomLogger: TealiumLoggerProtocol {
	// ... conforming to the TealiumLoggerProtocol
	// plus your own custom methods
}

class TealiumHelper {
	let customLogger = CustomLogger()
	var tealium: Tealium?
	// ...

	private init() {
		config.logger = customLogger
		// ...
	}
}

```

## AppDelegate プロキシ

デフォルトでは、Tealium Swift ライブラリにアプリの AppDelegate 用プロキシが含まれています。このプロキシは、ディープリンクを自動的にトラッキングし、[Mobile Trace Tool](https://docs.tealium.com/ja/platforms/getting-started-mobile/trace/#mobile-trace-tool) を使用して Tealium トレースセッションを開始します。この機能を使用しない場合は、`TealiumConfig` インスタンスの `appDelegateProxyEnabled` プロパティを `false` に構成します。

```swift
config.appDelegateProxyEnabled = false
```

## イベントのバッチ処理

イベントのバッチ処理は、`TealiumConfig` インスタンス上でローカルに構成するか、[Mobile Publish Settings](https://docs.tealium.com/create-mobile-profile/) を使用して構成できます。ローカル構成はリモート構成より優先されます。

次の例では、イベントのバッチ処理を有効にし、バッチサイズとキューサイズを構成します。

```swift
class TealiumHelper {
	var tealium: Tealium?
	// ...

	private init() {
		config.batchingEnabled = true            // enable batching
		config.batchSize = 10                    // size of batch
		config.dispatchAfter = 25                // flush after every 25 events
		config.dispatchQueueLimit = 100          // 100 max queued events
		config.dispatchExpiration = 5            // events expire/delete after 5 days
		// ...
	}
}
```

イベントのバッチ処理をカスタマイズするために、以下のオプションを使用できます。

| プロパティ | 説明 |
|:------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------|
| [`batchingEnabled`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#batchingenabled) | イベントのバッチ処理を有効または無効にします（デフォルト：`false`）。 |
| [`batchSize`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#batchsize) | 1 回のバッチリクエストにまとめるイベント数を構成します（最大：10）。 |
| [`dispatchAfter`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#dispatchafter) | キューをフラッシュするまでのイベント数を構成します。 |
| [`dispatchExpiration`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#dispatchexpiration) | バッチの有効期限を日数で構成します。デバイスが長期間オフラインになっている場合、この日数より古いイベントは削除されます。 |
| [`dispatchQueueLimit`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#dispatchqueuelimit) | キューに保持できるイベントの最大数を構成します。この数に達してもキューがフラッシュされていない場合、最も古いイベントが削除されます。 |

#### Tag Management

Tag Management とイベントのバッチ処理が有効になっている場合、トラッキング呼び出しは、非表示の WebView に個別の JavaScript 呼び出しとして送信されます。

構成済みのタグは個別にトリガーされるため、イベントごとに複数のリクエストがデバイスから送信されます。リアルタイムイベントを送信する場合よりもデバイスが起動する頻度が低くなるため、デバイスのパフォーマンスが向上します。
#### Tealium Collect

このエンドポイントは現在、Tealium SDK によって生成された独自のバッチ形式のバッチデータのみを受け付けます。