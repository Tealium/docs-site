---
title: インストール
description: Tealium SDK for iOS (Swift) のインストール方法を学ぶ。
url: https://docs.tealium.com/ja/platforms/ios-swift/install/
---
現在のTealium for Swift SDKのバージョンは2.xです。以前のバージョンについては、[Swift 1.x](/ja/platforms/ios-swift-v1)または[Objective-C](/ja/platforms/ios-objective-c/)を参照してください。Swiftコードは既存のObjective-Cファイルと同じプロジェクト内で共存し、Objective-C APIへの完全なアクセスが可能で、採用が容易になります。

## 要件

* Xcode 7.0&#43;
* iOS 9.0&#43;, macOS 10.11&#43;, watchOS 3.0&#43;, tvOS 9.2&#43;
* [Tealium iQモバイルプロファイル]()
* [Tealiumカスタマーデータハブアカウント]()

## サンプルアプリ

iOS (Swift) の[サンプルアプリ](https://github.com/Tealium/tealium-swift/tree/master/samples)を探索して、Tealiumライブラリ、トラッキング方法、およびベストプラクティスの実装に慣れることができます。

Tealiumの実装をアプリの他の部分から抽象化するために、ヘルパークラスの使用をお勧めします。これにより、初期化とトラッキング呼び出しを行うための単一の入口点が提供されます。また、ヘルパーファイルのコードを更新することで、すべての`View`やSwiftファイルでコードを更新する必要がなくなります。

私たちの[サンプルヘルパークラス](https://github.com/Tealium/tealium-swift/tree/master/samples/TealiumSwiftExample)を探索してください。

## インストール

Tealium iOSライブラリはモジュールに分かれています。リソースフットプリントを小さく保つために、必要なモジュールのみをインストールすることをお勧めします。iOS用の利用可能なモジュールについて[詳しくはこちら](/ja/platforms/ios-swift/modules/)。

Tealium for iOSライブラリは、Swift Package Manager、CocoaPods、またはCarthageでインストールします。

### Swift Package Manager (推奨)

Swift Package Managerは、Tealium Swiftライブラリをインストールするための推奨される最も簡単な方法です：

1. Xcodeプロジェクトで、**File &gt; Add Package Dependencies**を選択します。
1. リポジトリURLを入力します：`https://github.com/tealium/tealium-swift`
1. バージョンルールを構成します。通常は`Up to next major`が推奨されます。現在のTealium Swiftライブラリバージョンがリストに表示されない場合は、Swiftパッケージキャッシュをリセットしてください。
1. インストールするモジュールを選択し、モジュールをインストールするアプリターゲットを選択します。

プロジェクトに複数のアプリターゲットがあり、複数のアプリターゲットにTealium Swiftライブラリが必要な場合は、**Frameworks and Libraries**セクションで手動で追加する必要があります。

追加のアプリターゲットにTealium Swiftライブラリをインストールするには：

1. **Project Navigator**でXcodeプロジェクトを選択します。
1. Xcodeプロジェクトで、**TARGETS**セクションのアプリターゲットを選択します。
1. **Frameworks and Libraries**に移動し、アプリターゲットに追加するTealium Swiftライブラリを選択します。

Swift Package Managerは、パッケージ内のターゲットを特定のプラットフォームに制限することはできません。たとえば、iOSのみに対応する[`TagManagement`](/ja/platforms/ios-swift/module-list/tag-management/)などのモジュールは、非iOSターゲットにもSPM経由でXCodeに利用可能になりますが、これらのモジュールをそれらのターゲットに追加すると、利用できないシステムライブラリのためにコンパイラがエラーを投げます。この制限は、iOS専用モジュールはiOSアプリにのみ追加されるべきであるため、ユーザーに影響を与えるべきではありません。

### CocoaPods

CocoaPodsでTealium for iOSライブラリをインストールするには（推奨）：

1. PodfileにTealium Swift pod `&#34;tealium-swift&#34;`を追加します。各モジュールにはサブスペックがあり、それぞれが&#34;Core&#34;モジュールに依存しています。サブスペックを指定しない場合、デフォルトですべてのモジュールがインストールされます。
      ```ruby
      # Uncomment the next line to define a global platform for your project
      platform :ios, &#39;11.0&#39;

      target &#39;CPodTest&#39; do
            # Comment the next line if you don&#39;t want to use dynamic frameworks
            use_frameworks!

            # Pods for CPodTest

            # new entry for Tealium pod
            pod &#39;tealium-swift&#39; # all modules
            # pod &#39;tealium-swift/TagManagement&#39; # to install individual modules only, use subspecs
      end
      ```

2. 必要なモジュールを追加したら、次のコマンドを実行します：
      ```ruby
      pod install
      ```
コマンドが正しいPodsを見つけられない場合は、`pod repo update`コマンドを実行してください。

3. `.xcworkspace`ファイルを使用してXcodeプロジェクトを開きます（`.xcodeproj`ファイルは使用しないでください）。

4. Tealiumをインスタンス化する予定のファイルで、任意の数のモジュールをインポートするには、次のインポートステートメントを追加します：
      ```swift
      import TealiumSwift
      ```

#### 推奨されるPodfile

Podfileに追加する推奨モジュールのリストは次のとおりです：

Podfileから特定のモジュールを無効にするには、`#`を使用してPodfile内の行をコメントアウトするか、行を削除します。

```ruby
# ...
# *** 推奨最小限:
# すべてのポッドはCoreに依存します。すべてのプラットフォームをサポートします。
pod &#34;tealium-swift/Core&#34;
pod &#34;tealium-swift/Lifecycle&#34;
pod &#34;tealium-swift/Collect&#34; # サーバーサイド製品用。たとえば：EventStream - 通常はこれまたはTealiumTagManagementですが、両方はあまりありません
# または
pod &#34;tealium-swift/TagManagement&#34; # Tealium iQ用
pod &#34;tealium-swift/RemoteCommands&#34;

# *** オプションのモジュール: これらのモジュールが必要ない場合があります。必要に応じて有効にしてください。   *** #

# アプリに訪問のオーディエンスと属性情報を提供します
# pod &#34;tealium-swift/VisitorService&#34;

# iOSのみ。アプリの帰属データと広告IDを収集します。
# pod &#34;tealium-swift/Attribution&#34;

# iOSとtvOSのみ。一般的には推奨されません。モジュールドキュメントの別のメモを参照してください。
# pod &#34;tealium-swift/Autotracking&#34;

# モジュールドキュメントの別のメモを参照してください。
# pod &#34;tealium-swift/Location&#34;

# iOSのみ。詳細なクラッシュ情報を報告します。
# 別のTealiumCrashReporter依存関係をインストールします（PLCrashReporterに基づいています）。
# pod &#34;TealiumCrashModule&#34;
# ...
```

### Carthage

CarthageでiOS (Swift) のTealiumをインストールするには：

1. Cartfileに次の内容を追加します：
      ```bash
      github &#34;tealium/tealium-swift&#34;
      ```

2. iOS、macOS、tvOS、watchOS用のフレームワークを生成するには、次のコマンドを実行します：
      ```bash
      carthage update
      ```

3. 特定のプラットフォーム、たとえばiOSのみをビルドし、初回ビルド後の後続のビルドを高速化するには、Carthageの`--platform`引数を使用します：
      ```bash
      carthage update --platform ios --cache-builds
      ```

4. 必要なフレームワークをXcodeプロジェクトの**General &gt; Embedded Binaries**セクションにドラッグします。
Tealiumフレームワークがプロジェクト構成のEmbedded Binariesセクションに追加されていることを確認してください。そうでない場合、アプリは起動時にクラッシュします。

5. アプリを提出する際に問題が発生しないように、[Carthage Getting Started](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos)ドキュメントに記載されている関連するビルドフェーズスクリプトを追加する手順に従ってください。
#### モジュールのインポート

Tealium Swift SDKは、複数のモジュール/フレームワークに分割されています。バイナリサイズを減らし、アプリのパフォーマンスを向上させるために、必要なモジュールのみをインポートしてください。

**モジュールインポートステートメント**

*  **TealiumCore** - Tealium、TealiumConfig、TealiumInstanceManagerに必要
*  **TealiumTagManagement** - Tealium iQへのトラックコールをディスパッチするために必要
*  **TealiumCollect**  - TealiumのCustomer Data Hubへのトラックコールをディスパッチするために必要
*  **TealiumRemoteCommands** - リモートコマンドAPIとのやり取りが必要な場合に必要
*  **TealiumLifecycle** - ライフサイクルイベントと関連データを収集する必要がある場合に必要

```swift
import TealiumCore
import TealiumTagManagement
import TealiumCollect
import TealiumRemoteCommands
import TealiumLifecycle
```

Carthageの制限のため、SDK全体をインポートする利便性と、完全にモジュール化されたインストールの柔軟性とパフォーマンス向上を選択する必要がありました。これによるデメリットは、使用したい各モジュールを個別に追加する必要があることです。

- Carthageは_すべて_のモジュールをビルドし、結果の `.framework` ファイルをCarthageビルドディレクトリに出力します。
- 不要なモジュールを削除し、必要なモジュールをXcodeにドラッグします。

詳細については、推奨されるモジュールリストに関する[モジュール](/ja/platforms/ios-swift/modules/)を参照してください。

## 初期化

Tealiumを初期化するには、[`TealiumConfig`](/ja/platforms/ios-swift/api/tealium-config/) インスタンスを [`Tealium()`](/ja/platforms/ios-swift/api/tealium/#tealium) コンストラクタに渡します。

Tealium iOSライブラリの単一のエントリポイントを提供し、将来のアップグレードを簡素化するトラッキングヘルパークラスを使用して、[`Tealium`](/ja/platforms/ios-swift/api/tealium/#class-tealium) インスタンスを管理します。

```swift
class TealiumHelper {
    static let shared = TealiumHelper()
    let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                               profile: &#34;PROFILE&#34;,
                               environment: &#34;ENVIRONMENT&#34;,
                               datasource: &#34;DATASOURCE&#34;)
    var tealium: Tealium?

    private init() {

        // 必要な構成オプションを追加
        config.batchingEnabled = true
        config.logLevel = .debug

        // 追加したいコレクター
        config.collectors = [Collectors.Lifecycle,
                             Collectors.Location,
                             Collectors.VisitorService]

        // 追加したいディスパッチャー
        config.dispatchers = [Dispatchers.TagManagement,
                              Dispatchers.RemoteCommands]

        tealium = Tealium(config: config)

        // オプションの初期化後の処理
        tealium?.dataLayer.add(key: &#34;mykey&#34;, value: &#34;myvalue&#34;, expiry: .forever)

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

次の項目を置き換えてください:
* `ACCOUNT`: ライブラリを初期化するために使用するTealiumアカウント名（小文字）
* `PROFILE`: ライブラリを初期化するために使用するTealiumプロファイル名（小文字）
* `ENVIRONMENT`: Tealiumを初期化する環境
* `DATASOURCE`: 使用するTealiumデータソース

モバイルパブリッシュ構成はデフォルトで有効になっており、使用しない場合は無効にする必要があります。iQタグ管理でモバイルパブリッシュ構成を構成するか、`config.shouldUseRemotePublishSettings = false`を使用して無効にします。

## ログレベル

ログレベルを構成するには、`TealiumConfig`インスタンスの[`logLevel`](/ja/platforms/ios-swift/api/tealium-config/#loglevel)プロパティを構成します:
```swift
config.logLevel = .debug // または .info, .error, .fault, .silent
```

デバッグ目的では、`.debug`が推奨されます。

デフォルトのログタイプは[`OSLog`](https://developer.apple.com/documentation/os/oslog)ですが、`TealiumConfig`オブジェクトの`logType`プロパティを更新することで`.print`に変更することができます:

```swift
config.logType = .print
```

また、`TealiumLogger`を使用する代わりに、`Logger`クラスを`TealiumLoggerProtocol`に準拠させ、そのクラスのインスタンスを`TealiumConfig`オブジェクトの`logger`プロパティに構成することで、独自のロガーを追加することも可能です。以下はその例です:

```swift
class CustomLogger: TealiumLoggerProtocol {
	// ... TealiumLoggerProtocolに準拠
	// さらに独自のメソッド
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

## AppDelegate Proxy

デフォルトでは、Tealium Swiftライブラリには、ディープリンクを自動的にトラッキングし、[モバイルトレースツール](/ja/platforms/getting-started-mobile/trace/#mobile-trace-tool)を使用してTealiumトレースセッションを開始するためのアプリのAppDelegateのプロキシが含まれています。この機能を使用したくない場合は、`TealiumConfig`インスタンスの`appDelegateProxyEnabled`プロパティを`false`に構成します。

```swift
config.appDelegateProxyEnabled = false
```

## イベントバッチ処理

イベントバッチ処理は、`TealiumConfig`インスタンスでローカルに構成するか、[モバイルパブリッシュ構成]()を使用して構成します。ローカル構成はリモート構成を上書きします。

この例では、イベントバッチ処理を有効にし、バッチサイズとキューサイズを構成します。

```swift
class TealiumHelper {
	var tealium: Tealium?
	// ...

	private init() {
		config.batchingEnabled = true            // バッチ処理を有効にする
		config.batchSize = 10                    // バッチのサイズ
		config.dispatchAfter = 25                // 25イベントごとにフラッシュ
		config.dispatchQueueLimit = 100          // 最大100イベントをキューに入れる
		config.dispatchExpiration = 5            // イベントの有効期限は5日
		// ...
	}
}
```

イベントバッチ処理をカスタマイズするための以下のオプションが利用可能です。

| プロパティ                                                                            | 説明                                                                                                                             |
|:------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------|
| [`batchingEnabled`](/ja/platforms/ios-swift/api/tealium-config/#batchingenabled)       | イベントバッチ処理を有効または無効にします（デフォルト：`false`）。                                                                                  |
| [`batchSize`](/ja/platforms/ios-swift/api/tealium-config/#batchsize)                   | 単一のバッチリクエストに組み合わせるイベントの数を構成します（最大：10）。                                                             |
| [`dispatchAfter`](/ja/platforms/ios-swift/api/tealium-config/#dispatchafter)           | キューがフラッシュされるイベントの数を構成します。                                                                             |
| [`dispatchExpiration`](/ja/platforms/ios-swift/api/tealium-config/#dispatchexpiration) | バッチの有効期限を日数で構成します。デバイスが長期間オフラインの場合、この期間を超える古いイベントは削除されます。                 |
| [`dispatchQueueLimit`](/ja/platforms/ios-swift/api/tealium-config/#dispatchqueuelimit) | キューに入れることができるイベントの最大数を構成します。この数に達し、キューがフラッシュされていない場合、最も古いイベントが削除されます。 |

#### タグ管理

タグ管理とイベントバッチ処理が有効になっている場合、トラッキングコールは個々のJavaScriptコールとして隠されたWebViewにディスパッチされます。

構成されたタグは個別にトリガーされ、デバイスからの複数のリクエストが発生します。これにより、リアルタイムイベントを送信するよりもデバイスの起動頻度が低くなり、デバイスのパフォーマンスが向上します。
#### Tealium Collect

このエンドポイントは現在、Tealium SDKによって生成された専用バッチ形式のバッチデータのみを受け付けています。
