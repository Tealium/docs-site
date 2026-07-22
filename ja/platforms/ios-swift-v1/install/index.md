---
title: インストール
description: iOS（Swift）用Tealium SDKのインストール方法。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/install/
---

<blockquote>
これはiOS（Swift）用Tealiumの以前のバージョン（1.x）です。最新バージョンについては、[iOS（Swift）用Tealium 2.x](https://docs.tealium.com/ja/platforms/ios-swift/)をご覧ください。
</blockquote>


## 必要条件

* Xcode 7.0+
* iOS 9.0+、macOS 10.11+、watchOS 3.0+、またはtvOS 9.2+
* [Tealium iQモバイルプロファイル](https://docs.tealium.com/creating-a-mobile-profile/)
* [Tealiumカスタマーデータハブアカウント](https://docs.tealium.com/introduction-to-customer-data-hub/)

## サンプルアプリ

Tealiumライブラリ、トラッキング方法、およびベストプラクティスの実装に慣れるために、Swiftの[サンプルアプリ](https://github.com/Tealium/tealium-swift/tree/master/samples)を探索してください。

Tealiumの実装をアプリの他の部分から抽象化するために、ヘルパークラスの使用をお勧めします。これにより、初期化およびトラッキングコールを行うための単一のエントリーポイントが提供されます。また、ヘルパーファイルのコードを更新することで、すべての`ViewController`やSwiftファイルでコードを更新する必要がなくなります。

私たちの[サンプルヘルパークラス](https://github.com/Tealium/tealium-swift/tree/master/samples/TealiumSwiftExample)を探索してください。

## インストール

Tealium iOSライブラリはモジュールに分かれています。リソースフットプリントを小さく保つために、必要なモジュールのみをインストールすることをお勧めします。iOS用に利用可能なモジュールについて[詳しくはこちら](https://docs.tealium.com/ja/platforms/ios-swift-v1/modules/)。

Swift Package Manager、CocoaPods、またはCarthageを使用してiOS用Tealiumライブラリをインストールします。



<blockquote>
同意管理が不要な場合は、同意管理モジュールを除外または無効にしてください。[同意管理](https://docs.tealium.com/ja/platforms/ios-swift-v1/consent-management/)モジュールはデフォルトで有効になっており、最初はトラッキングコールの送信を防ぎます。トラッキングコールを許可するには、同意ステータスを`.consented`に構成してください。
</blockquote>
  

### Swift Package Manager（推奨）

バージョン1.9.0+でサポートされているSwift Package Managerは、Tealium Swiftライブラリをインストールするための推奨される最も簡単な方法です：

1. Xcodeプロジェクトで、**File > Add Packages... > Add Package Dependency**を選択します。
2. リポジトリURLを入力します：`https://github.com/tealium/tealium-swift`
3. バージョンルールを構成します。通常、「Up to next major」が推奨されます。現在のTealium Swiftライブラリバージョンがリストに表示されない場合は、Swiftパッケージキャッシュをリセットしてください。
4. インストールするモジュールを選択し、モジュールをインストールするアプリターゲットを選択します。

プロジェクトに複数のアプリターゲットがあり、より多くのアプリターゲットにTealium Swiftライブラリが必要な場合は、**Frameworks, Libraries, and Embedded Content**セクションで手動で追加する必要があります。

追加のアプリターゲットにTealium Swiftライブラリをインストールするには：

1. **Project Navigator**でXcodeプロジェクトを選択します。
2. Xcodeプロジェクトで、**TARGETS**セクションのアプリターゲットを選択します。
3. **General > Frameworks, Libraries & Embedded Content**に移動し、アプリターゲットに追加するTealium Swiftライブラリを選択します。

Swift Package Managerには次の制限があります：

- 単一ターゲット内の混合言語ソースがサポートされていないため、[`CrashReporter`](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/crash-reporter/)および[`AutoTracking`](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/autotracking/)モジュールはSwift Package Managerを通じてサポートされていません。これらのモジュールが必要でないことを確認してからSwift Package Managerを使用してください。
- パッケージ内のターゲットを特定のプラットフォームに制限することはできません。iOSのみでサポートされている[`TagManagement`](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/tag-management/)などのモジュールも、非iOSターゲットで利用可能になります。これらのモジュールを非iOSターゲットに追加すると、利用できないシステムライブラリのためにコンパイラがエラーを投げます。

### CocoaPods

CocoaPods（推奨）を使用してiOS用Tealiumライブラリをインストールするには：

1. PodfileにTealium Swift pod `"tealium-swift"`を追加します。それぞれのモジュールにはサブスペックがあり、それぞれが"Core"モジュールに依存しています。サブスペックを指定しない場合、デフォルトですべてのモジュールがインストールされます。
      ```ruby
      # Uncomment the next line to define a global platform for your project
      platform :ios, '9.0'

      target 'CPodTest' do
            # Comment the next line if you don't want to use dynamic frameworks
            use_frameworks!

            # Pods for CPodTest

            # new entry for Tealium pod
            pod 'tealium-swift' # all modules
            # pod 'tealium-swift/TealiumTagManagement' # to install individual modules only, use subspecs
      end
      ```

2. 必要なモジュールを追加したら、次のコマンドを実行します：
      ```ruby
      pod install
      ```  
      
<blockquote>
コマンドが正しいPodsを見つけられない場合は、`pod repo update`コマンドを実行してください。
</blockquote>


      3. `.xcworkspace`ファイルを使用してXcodeプロジェクトを開きます（`.xcodeproj`ファイルは使用しないでください）。

      4. モジュールをいくつかインポートするには、Tealiumをインスタンス化する予定のファイルに次のインポートステートメントを追加します：
      ```swift
      import TealiumSwift
      ```
#### 推奨されるPodfile

以下は推奨されるPodfileです：


<blockquote>
Podfileから特定のモジュールを無効にするには、Podfile内で`#`を使ってコメントアウトしてください。
</blockquote>


```ruby
# Podfile
# ターゲットをCPodTestに置き換えてください
target 'CPodTest' do
    # Swiftを使用していない場合、または動的フレームワークを使用したくない場合は、次の行をコメントアウトしてください
    use_frameworks!

    # CPodTestのためのPods
    # *** 推奨最小限:
    # 必要ないと確信している場合のみ無効にしてください。  ***

    # すべてのプラットフォームでCoreに依存します。すべてのプラットフォームをサポートします。
    pod "tealium-swift/Core"
    # すべてのプラットフォーム。アプリバンドルに関する重要な情報を提供します。
    pod "tealium-swift/TealiumAppData"
    # すべてのプラットフォーム。データをTealium Customer Data Hubに送信します。
    pod "tealium-swift/TealiumCollect"
    # すべてのプラットフォーム。GDPR/プライバシーのコンプライアンスを支援します。
    pod "tealium-swift/TealiumConsentManager"
    # iOS、macOS、tvOSのみ。接続状態を検出し、オフライン中にトラックコールをキューに入れます。
    # TealiumDispatchQueueモジュールと併用する必要があります。
    pod "tealium-swift/TealiumConnectivity"

    # DataSourceはSwift 1.8.0+のCoreに含まれています。以前のバージョンではコメントを外してください。
    # すべてのプラットフォーム。各ディスパッチに"tealium_datasource"を追加し、TealiumConfigクラスを拡張します。
    # pod "tealium-swift/TealiumDataSource"

    # FileStorageはSwift 1.8.0+のCoreに含まれています。以前のバージョンではコメントを外してください。
    # すべてのプラットフォーム。永続的なデータをファイル保存に保存します。
    # PersistentDataモジュールをバンドルします。
    # DefaultsStorageモジュールが使用されている場合は使用しないでください。
    # 最適なオプションを選択してください。
    # pod "tealium-swift/TealiumFileStorage"

    # すべてのプラットフォーム。Tealiumクラスにデリゲートと完了ハンドラの使用を可能にします。
    pod "tealium-swift/TealiumDelegate"
    # すべてのプラットフォーム。各ディスパッチにデバイス情報を追加します。
    pod "tealium-swift/TealiumDeviceData"
    # すべてのプラットフォーム。キューに入れられたイベントのオフライン保存を有効にします。
    # (Consent、Connectivityが必要です)。
    pod "tealium-swift/TealiumDispatchQueue"
    # すべてのプラットフォーム。各ディスパッチにアプリのライフサイクル情報を追加します。
    pod "tealium-swift/TealiumLifecycle"
    # すべてのプラットフォーム。LLDBコンソールに情報をログします。
    pod "tealium-swift/TealiumLogger"
    # iOSのみ。TagManagementモジュールと連携してリモートコマンドをトリガーします。
    pod "tealium-swift/TealiumRemoteCommands"
    # iOSのみ。Tealium Tag Managementを有効にします。
    pod "tealium-swift/TealiumTagManagement"
    # すべてのプラットフォーム。各ディスパッチに重要なデータを追加し、現在のセッションのためにデータの一時的な保存を可能にします。
    pod "tealium-swift/TealiumVolatileData"

    # *** オプショナルモジュール: これらのモジュールが必要ない場合があります。必要に応じて有効にしてください。   *** #

    # iOSのみ。アプリのアトリビューションデータと広告IDを収集します。
    # pod "tealium-swift/TealiumAttribution"

    # iOSとtvOSのみ。一般的には推奨されません。モジュールドキュメント内の別のメモを参照してください。
    # pod "tealium-swift/TealiumAutotracking"

    # DefaultStorageはSwift 1.8.0+のCoreに含まれています。以前のバージョンではコメントを外してください。
    # すべてのプラットフォーム。永続的なデータをUserDefaultsに保存します。PersistentDataモジュールをバンドルします。FileStorageモジュールが使用されている場合は使用しないでください。
    # pod "tealium-swift/TealiumDefaultsStorage"

    # iOSのみ。詳細なクラッシュ情報を報告します。別のTealiumCrashReporter依存関係をインストールします（PLCrashReporterに基づいています）。
    # pod "tealium-swift/Crash"
end
```

#### 完全なPodfile

完全なPodfileは、オプショナルとして指定されたすべてのモジュールを含む、iOS（Swift）用Tealium全体をインポートします：

```ruby
# プロジェクトのグローバルプラットフォームを定義するために次の行のコメントを外してください
platform :ios, '9.0'

target 'CPodTest' do
    # Swiftを使用していない場合、または動的フレームワークを使用したくない場合は、次の行をコメントアウトしてください
    use_frameworks!

    # CPodTestのためのPods

    # Tealium podの新しいエントリ
    pod 'tealium-swift'
end
```
特定のモジュールを無効にするには、[`TealiumConfig`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-config/)クラスの`TealiumModulesList`構造体と関連するメソッドを参照してください。

### Carthage

Carthageを使用してiOS（Swift）用Tealiumをインストールするには：

1. Cartfileに次の内容を追加します：
      ```ruby
      github "tealium/tealium-swift"
      ```

2. iOS、macOS、tvOS、およびwatchOS用のフレームワークを生成するには、次のコマンドを実行します：
      ```ruby
      carthage update
      ```

3. 特定のプラットフォーム（例：iOS）のみをビルドし、初回ビルド後の後続のビルドを高速化するには、Carthageの`--platform`引数を使用します：
      ```ruby
      carthage update --platform ios --cache-builds
      ```

4. 必要なフレームワークをXcodeプロジェクトの**General > Embedded Binaries**セクションにドラッグします。
      
<blockquote>
Tealiumフレームワークがプロジェクト構成のEmbedded Binariesセクションに追加されていることを確認してください。そうでないと、アプリが起動時にクラッシュします。
</blockquote>
  

5. Carthage [Getting Started](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos)ドキュメントに記載されている指示に従って、関連するビルドフェーズスクリプトを追加します。これにより、アプリを提出する際に問題が発生しないようにします。


#### モジュールについて (1.6.5+)
バージョン1.6.5以降、Tealium Swift SDKは個別のモジュール/フレームワークに分割されました。これにより、必要なモジュールのみをインポートすることができ、バイナリサイズを削減し、最終的にアプリのパフォーマンスを向上させることができます。

**モジュールインポートステートメント**  
```swift
import TealiumCore              // Tealium, TealiumConfig, TealiumInstanceManagerに必要
import TealiumVolatileData      // Volatile Data APIを通じて揮発性データを保存する場合に必要
//import TealiumFileStorage     // Swift 1.8.0+のTealiumCoreに含まれています。以前のバージョンではインポートしてください。
//import TealiumDefaultsStorage // Swift 1.8.0+のTealiumCoreに含まれています。永続的なデータを保存する必要がある場合は、以前のバージョンでインポートしてください。
import TealiumRemoteCommands    // Remote Commands APIを使用する必要がある場合に必要
import TealiumDelegate          // トラッキングデリゲートを構成する必要がある場合に必要
//import TealiumDataSource      // Swift 1.8.0+のTealiumCoreに含まれています。以前のバージョンではTealiumConfigクラスインスタンスにデータソースパラメータを構成するためにインポートしてください。
import TealiumLifecycle         // Lifecycle APIを手動で呼び出す必要がある場合のみ必要
```

Carthageの制限のため、SDK全体をインポートする便利さと、完全にモジュラーなインストールの柔軟性とパフォーマンス向上を選択する必要がありました。このアプローチの欠点は、使用したい各モジュールを個別に追加する必要があることです。

- Carthageは_すべて_のモジュールをビルドし、結果の`.framework`ファイルをCarthageビルドディレクトリに出力します。
- 必要ないモジュールを削除し、必要なモジュールをXcodeにドラッグします。

[モジュール](https://docs.tealium.com/ja/platforms/ios-swift-v1/modules/)で推奨されるモジュールリストの詳細をご覧ください。
## 初期化

[`Tealium`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium/#class-tealium) クラスの初期化を管理することをお勧めします。これにより、Tealium iOS ライブラリのエントリーポイントが一つになり、将来のアップグレードが簡単になります。

Tealium を初期化するには、以下の例に示すように、[`TealiumConfig`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-config/) インスタンスを [`Tealium()`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium/#tealium) コンストラクタに渡します：

```swift
class TealiumHelper {

static let shared = TealiumHelper()
var tealium: Tealium?

	private init() {
		initTealium()
	}

	private func initTealium() {
		let config = TealiumConfig(account: "ACCOUNT",
   	       		                   profile: "PROFILE",
        	   	                   environment: "ENVIRONMENT",
           		                   datasource: "DATASOURCE")
		// 必要に応じて構成オプションを追加
		config.setLogLevel(.verbose)
		// Tealium の参照を初期化して保持
		tealium = Tealium(config: config) { moduleResponses in
		    // 初期化後のタスクをここで実行
		}
	}
}
```


<blockquote>
バージョン 1.9.0 以降では、モバイル公開構成がデフォルトで有効になっており、使用しない場合は無効にする必要があります。iQ タグ管理でモバイル公開構成を構成するか、`config.shouldUseRemotePublishSettings = false` を使用して無効にします。
</blockquote>


## ログレベル

ログレベルを構成するには、`TealiumConfig` インスタンスで [`setLogLevel()`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-config/#setloglevel) メソッドを呼び出し、以下の値のいずれかを使用します：

* `none`
* `.errors`
* `.warnings`
* `.verbose`

デバッグ目的で、以下の例に示すように `.verbose` を推奨します：

```swift
config.setLogLevel(.verbose)
```

## イベントバッチ処理

バージョン 1.9.0 以前では、Tealium Swift ライブラリは [モバイル公開構成](https://docs.tealium.com/creating-a-mobile-profile/) を使用していませんでした。したがって、SDK の初期化時にイベントバッチ処理を有効にして構成する必要があります。バージョン 1.9.0 以降では、モバイル公開構成のサポートが提供され、イベントバッチ処理をリモートで構成できます。

この例では、イベントバッチ処理を有効にし、バッチサイズとキューサイズを構成します。

```swift
import TealiumDispatchQueue // イベントバッチ処理オプションに必要
class TealiumHelper {
	var tealium: Tealium?
	// ...

	private func initTealium() {
		let config = TealiumConfig(account: "ACCOUNT",
 	       		                   profile: "PROFILE",
                               environment: "ENVIRONMENT",
                               datasource: "DATASOURCE")
		config.batchingEnabled = true            // バッチ処理を有効にする
		config.batchSize = 10                    // バッチのサイズ
		config.dispatchAfter = 25                // 25 イベントごとにフラッシュ
		config.dispatchQueueLimit = 100          // 最大キューイベント数 100
		config.dispatchExpiration = 5            // イベントの有効期限は 5 日間
		// ...
	}
}
```

イベントバッチ処理をカスタマイズするための以下のオプションが利用可能です。

| プロパティ | 説明 |
| --- | --- |
| [`batchingEnabled`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-config/#batchingenabled) | イベントバッチ処理を有効または無効にします（デフォルト：`false`）。 |
| [`batchSize`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-config/#batchsize) | 単一のバッチリクエストに組み合わせるイベントの数を構成します（最大：10）。 |
| [`dispatchAfter`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-config/#dispatchafter) | キューがフラッシュされるイベント数を構成します。 |
| [`dispatchExpiration`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-config/#dispatchexpiration) | バッチの有効期限を日数で構成します。デバイスが長期間オフラインの場合、この期間を超えたイベントは削除されます。 |
| [`dispatchQueueLimit`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-config/#dispatchqueuelimit) | キューイベントの最大数を構成します。この数に達し、キューがフラッシュされていない場合、最も古いイベントが削除されます。 |

### タグ管理

タグ管理とイベントバッチ処理が有効になっている場合、トラッキングコールは個々の JavaScript コールとして隠されたウェブビューにディスパッチされます。

構成されたタグは個別にトリガーされ、デバイスからの複数のリクエストが発生します。これにより、リアルタイムイベントを送信するよりもデバイスの起動が頻繁に行われないため、デバイスのパフォーマンスが向上します。

### Tealium Collect

このエンドポイントは現在、Tealium SDK によって生成されたバッチデータのみを受け入れます。