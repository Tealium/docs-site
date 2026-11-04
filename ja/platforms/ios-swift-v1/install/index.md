---
title: インストール
description: iOS（Swift）向けTealium SDKをインストールする方法。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/install/
---

<blockquote>
これは、Tealium for iOS（Swift）の旧バージョン（1.x）です。最新バージョンについては、[Tealium for iOS（Swift）2.x](https://docs.tealium.com/ja/platforms/ios-swift/)を参照してください。
</blockquote>


## 要件

* Xcode 7.0以降
* iOS 9.0以降、macOS 10.11以降、watchOS 3.0以降、またはtvOS 9.2以降
* [タグ管理モバイルプロファイル](https://docs.tealium.com/create-mobile-profile/)
* [Tealium Customer Data Hubアカウント](https://docs.tealium.com/introduction-to-customer-data-hub/)

## サンプルアプリ

Tealiumライブラリ、トラッキングメソッド、ベストプラクティスに沿った実装について理解を深めるには、Swiftの[サンプルアプリ](https://github.com/Tealium/tealium-swift/tree/master/samples)を参照してください。

Tealiumの実装をアプリの他の部分から分離するために、ヘルパークラスを使用することをお勧めします。これにより、初期化とトラッキング呼び出しを実行するためのエントリポイントを1つにまとめることができます。また、個々の`ViewController`やSwiftファイルを変更することなく、ヘルパーファイル内のコードだけを更新できます。

[サンプルヘルパークラス](https://github.com/Tealium/tealium-swift/tree/master/samples/TealiumSwiftExample)を参照してください。

## インストール

Tealium iOSライブラリは複数のモジュールに分かれています。リソース使用量を抑えるため、必要なモジュールのみをインストールすることをお勧めします。iOSで利用できるモジュールについて[詳しくはこちら](https://docs.tealium.com/ja/platforms/ios-swift-v1/modules/)を参照してください。

Swift Package Manager、CocoaPods、またはCarthageを使用して、Tealium for iOSライブラリをインストールします。



<blockquote>
同意管理が不要な場合は、同意管理モジュールを除外または無効化してください。[同意管理](https://docs.tealium.com/ja/platforms/ios-swift-v1/consent-management/)モジュールはデフォルトで有効になっており、初期状態ではトラッキング呼び出しの送信を防止します。トラッキング呼び出しを許可するには、同意ステータスを`.consented`に構成します。
</blockquote>
  

### Swift Package Manager（推奨）

バージョン1.9.0以降でサポートされているSwift Package Managerは、Tealium Swiftライブラリをインストールするための推奨される最も簡単な方法です。

1. Xcodeプロジェクトで、**File > Add Packages... > Add Package Dependency**を選択します。
2. リポジトリURLとして`https://github.com/tealium/tealium-swift`を入力します。
3. バージョンルールを構成します。通常は`Up to next major`をお勧めします。現在のTealium Swiftライブラリのバージョンが一覧に表示されない場合は、Swiftパッケージのキャッシュをリセットしてください。
4. インストールするモジュールを選択し、そのモジュールをインストールするアプリターゲットを選択します。

プロジェクトに複数のアプリターゲットがあり、追加のアプリターゲットでもTealium Swiftライブラリが必要な場合は、**Frameworks, Libraries, and Embedded Content**セクションで手動で追加する必要があります。

追加のアプリターゲットにTealium Swiftライブラリをインストールするには、次の手順を実行します。

1. **Project Navigator**でXcodeプロジェクトを選択します。
2. Xcodeプロジェクトの**TARGETS**セクションでアプリターゲットを選択します。
3. **General > Frameworks, Libraries & Embedded Content**に移動し、Tealium Swiftライブラリを選択してアプリターゲットに追加します。

Swift Package Managerには次の制限があります。

- 単一ターゲット内で複数言語のソースを使用できないため、[`CrashReporter`](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/crash-reporter/)および[`AutoTracking`](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/autotracking/)モジュールはSwift Package Managerではサポートされていません。Swift Package Managerを使用する前に、これらのモジュールが不要であることを確認してください。
- パッケージ内のターゲットを特定のプラットフォームに制限することはできません。そのため、iOSでのみサポートされる[`TagManagement`](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/tag-management/)などのモジュールも、iOS以外のターゲットで利用可能になります。これらのモジュールをiOS以外のターゲットに追加すると、利用できないシステムライブラリが原因でコンパイラエラーが発生します。

### CocoaPods

CocoaPodsを使用してTealium for iOSライブラリをインストールするには（推奨）、次の手順を実行します。

1. Tealium Swift Podの`"tealium-swift"`をPodfileに追加します。各モジュールに対応するサブスペックがあり、それぞれが「Core」モジュールに依存しています。サブスペックを指定しない場合は、デフォルトですべてのモジュールがインストールされます。  
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

2. 必要なモジュールを追加したら、次のコマンドを実行します。     
      ```ruby
      pod install
      ```  
      
<blockquote>
コマンドで正しいPodが見つからない場合は、`pod repo update`コマンドを実行してみてください。
</blockquote>


      3. `.xcworkspace`ファイルを使用してXcodeプロジェクトを開きます（`.xcodeproj`ファイルは使用しないでください）。

      4. 任意の数のモジュールをインポートするには、Tealiumをインスタンス化するファイルに次のimport文を追加します。   
      ```swift
      import TealiumSwift
      ```
#### 推奨 Podfile

以下は推奨される Podfile です。


<blockquote>
To disable specific modules from the Podfile, comment them out in the Podfile with `#`.
</blockquote>


```ruby
# Podfile
# replace CPodTest with your target
target 'CPodTest' do
    # Comment the next line if you're not using Swift and don't
    # want to use dynamic frameworks
    use_frameworks!

    # Pods for CPodTest
    # *** Recommended minimum:
    # Only disable if you're sure you don't need them.  ***

    # All pods depend on Core. Supports all platforms.
    pod "tealium-swift/Core"
    # All platforms. Provides important info about
    # the app bundle.
    pod "tealium-swift/TealiumAppData"
    # All platforms. Sends data to Tealium Customer Data Hub.
    pod "tealium-swift/TealiumCollect"
    # All platforms. Assists with GDPR/privacy compliance.
    pod "tealium-swift/TealiumConsentManager"
    # iOS, macOS, tvOS only. Detects connectivity state and queues track calls while offline.
    # Should be used in conjunction with TealiumDispatchQueue module.
    pod "tealium-swift/TealiumConnectivity"

    # DataSource is included in the Core for Swift 1.8.0+. Uncomment for prior versions.
    # All platforms. Adds "tealium_datasource" to each dispatch, and extends TealiumConfig class.
    # pod "tealium-swift/TealiumDataSource"

    # FileStorage is included in the Core for Swift 1.8.0+. Uncomment for prior versions.
    # All platforms. Stores persistent data to File Storage.
    # Bundles PersistentData module.
    # Should not be used if DefaultsStorage module is in use.
    # Pick the option that best suits you.
    # pod "tealium-swift/TealiumFileStorage"

    # All platforms. Enables the use of delegates
    # and completion handlers on the Tealium class.
    pod "tealium-swift/TealiumDelegate"
    # All platforms. Adds device information to each dispatch.
    pod "tealium-swift/TealiumDeviceData"
    # All platforms. Enables offline storage of queued events.
    # (required for Consent, Connectivity).
    pod "tealium-swift/TealiumDispatchQueue"
    # All platforms. Add app lifecycle information to each dispatch.
    pod "tealium-swift/TealiumLifecycle"
    # All platforms. Enables logging information to the LLDB console.
    pod "tealium-swift/TealiumLogger"
    # iOS only. Used with the TagManagement module to trigger Remote Commands
    pod "tealium-swift/TealiumRemoteCommands"
    # iOS only. Enables Tag Management.
    pod "tealium-swift/TealiumTagManagement"
    # All platforms. Adds important data to each dispatch, and enables temporary storage of data for the current session.
    pod "tealium-swift/TealiumVolatileData"

    # *** Optional modules: You may not need these modules. Enable as required.   *** #

    # iOS Only. Gathers app attribution data and advertising IDs.
    # pod "tealium-swift/TealiumAttribution"

    # iOS and tvOS only. Generally not recommended. See separate notes in module documentation.
    # pod "tealium-swift/TealiumAutotracking"

    # DefaultStorage is included in the Core for Swift 1.8.0+. Uncomment for prior versions.
    # All platforms. Stores persistent data to UserDefaults. Bundles PersistentData module. Should not be used if FileStorage module is in use.
    # pod "tealium-swift/TealiumDefaultsStorage"

    # iOS only. Reports detailed crash information. Installs separate TealiumCrashReporter dependency (based on PLCrashReporter).
    # pod "tealium-swift/Crash"
end
```

#### 完全な Podfile

完全な Podfile は、オプションとして指定されているすべてのモジュールを含む Tealium for iOS（Swift）全体をインポートします。

```ruby
# Uncomment the next line to define a global platform for your project
platform :ios, '9.0'

target 'CPodTest' do
    # Comment the next line if you're not using Swift and don't want to use dynamic frameworks
    use_frameworks!

    # Pods for CPodTest

    # new entry for Tealium pod
    pod 'tealium-swift'
end
```

特定のモジュールを無効にするには、`TealiumModulesList` 構造体と、[`TealiumConfig`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-config/) クラスでモジュールをブラックリストに登録するための関連メソッドを参照してください。

### Carthage

Carthage を使用して Tealium for iOS（Swift）をインストールするには、次の手順を実行します。

1. Cartfile に以下を追加します。    
      ```ruby
      github "tealium/tealium-swift"
      ```

2. iOS、macOS、tvOS、および watchOS 用のフレームワークを生成するには、次のコマンドを実行します。  
      ```ruby
      carthage update
      ```

3. iOS など、特定のプラットフォーム向けにのみビルドし、初回ビルド後の後続ビルドを高速化するには、Carthage の `--platform` 引数を使用します。  
      ```ruby
      carthage update --platform ios --cache-builds
      ```

4. 必要なフレームワークを、Xcode プロジェクトの **General > Embedded Binaries** セクションにドラッグします。  
      
<blockquote>
Verify that the Tealium frameworks have been added to the Embedded Binaries section in your project settings, otherwise your app crashes at launch.
</blockquote>
  

5. アプリの提出時に問題が発生しないよう、Carthage の[はじめに](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos)ドキュメントに記載されている手順に従い、該当するビルドフェーズスクリプトを追加します。

#### モジュールについて（1.6.5 以降）

バージョン 1.6.5 以降、Tealium Swift SDK は個別のモジュール／フレームワークに分割されています。これにより、使用するモジュールに対応する特定のフレームワークだけをインポートできるため、バイナリサイズが削減され、最終的にアプリのパフォーマンスが向上します。

**モジュールの import 文**  
```swift
import TealiumCore              // required for Tealium, TealiumConfig, TealiumInstanceManager
import TealiumVolatileData      // required if you want to store volatile data through the Volatile Data API
//import TealiumFileStorage     // Included in TealiumCore for Swift 1.8.0+. Import for prior versions.
//import TealiumDefaultsStorage // Included in TealiumCore for Swift 1.8.0+. Import for prior versions if you need to store persistent data
import TealiumRemoteCommands    // required if you need to interact with the Remote Commands API
import TealiumDelegate          // required if you need to set up a tracking delegate
//import TealiumDataSource      // Included in TealiumCore for Swift 1.8.0+. Import for prior versions to
                                //     allow datasource param to be set on the TealiumConfig class instance
import TealiumLifecycle         // only required if you need to manually call the Lifecycle API
```

Carthage の制約により、SDK 全体をインポートできる利便性と、完全にモジュール化されたインストールによる柔軟性およびパフォーマンス向上のどちらかを選択する必要がありました。この方法の欠点は、使用する各モジュールを個別に追加する必要があることです。

- Carthage は、_すべて_のモジュールをビルドし、生成された `.framework` ファイルを Carthage のビルドディレクトリに出力します。
- 不要なモジュールを削除し、必要なモジュールを Xcode にドラッグします。

推奨モジュールリストの詳細については、[モジュール](https://docs.tealium.com/ja/platforms/ios-swift-v1/modules/)を参照してください。
## 初期化

[`Tealium`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium/#class-tealium) クラスの初期化処理を一元管理することを推奨します。これにより、Tealium iOS ライブラリへの単一のエントリーポイントが提供され、将来のアップグレードが簡単になります。

Tealium を初期化するには、次の例のように、[`TealiumConfig`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-config/) インスタンスを [`Tealium()`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium/#tealium) コンストラクターに渡します。

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
		// add config options as required
		config.setLogLevel(.verbose)
		// initialize and keep a reference to Tealium
		tealium = Tealium(config: config) { moduleResponses in
		    // Completion block; perform post-init tasks here
		}
	}
}
```



<blockquote>
バージョン 1.9.0 以降では、Mobile Publish Settings がデフォルトで有効になっているため、使用しない場合は無効にする必要があります。タグ管理で Mobile Publish Settings を構成するか、`config.shouldUseRemotePublishSettings = false` を使用して無効にしてください。
</blockquote>


## ログレベル

ログレベルを構成するには、`TealiumConfig` インスタンスで [`setLogLevel()`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-config/#setloglevel) メソッドを、次のいずれかの値を指定して呼び出します。

* `none`
* `.errors`
* `.warnings`
* `.verbose`

デバッグ目的では、次の例のように `.verbose` を指定することを推奨します。

```swift
config.setLogLevel(.verbose)
```

## イベントのバッチ処理

バージョン 1.9.0 より前の Tealium Swift ライブラリでは、[Mobile Publish Settings](https://docs.tealium.com/create-mobile-profile/) が使用されていませんでした。そのため、SDK の初期化時にイベントのバッチ処理を有効にして構成する必要があります。バージョン 1.9.0 以降では Mobile Publish Settings がサポートされ、イベントのバッチ処理をリモートで構成できます。

次の例では、イベントのバッチ処理を有効にし、バッチサイズとキューサイズを構成します。

```swift
import TealiumDispatchQueue // required for event batching options
class TealiumHelper {
	var tealium: Tealium?
	// ...

	private func initTealium() {
		let config = TealiumConfig(account: "ACCOUNT",
 	       		                   profile: "PROFILE",
                               environment: "ENVIRONMENT",
                               datasource: "DATASOURCE")
		config.batchingEnabled = true            // enable batching
		config.batchSize = 10                    // size of batch
		config.dispatchAfter = 25                // flush after every 25 events
		config.dispatchQueueLimit = 100          // 100 max queued events
		config.dispatchExpiration = 5            // events expire/delete after 5 days
		// ...
	}
}
```

イベントのバッチ処理をカスタマイズするために、次のオプションを使用できます。

| プロパティ | 説明 |
| --- | --- |
| [`batchingEnabled`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-config/#batchingenabled) | イベントのバッチ処理を有効または無効にします（デフォルト：`false`）。 |
| [`batchSize`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-config/#batchsize) | 1 回のバッチリクエストにまとめるイベント数を構成します（最大：10）。 |
| [`dispatchAfter`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-config/#dispatchafter) | キューをフラッシュするまでのイベント数を構成します。 |
| [`dispatchExpiration`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-config/#dispatchexpiration) | バッチの有効期限を日数で構成します。デバイスが長期間オフラインになっている場合、この期間を超えたイベントは削除されます。 |
| [`dispatchQueueLimit`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-config/#dispatchqueuelimit) | キューに格納できるイベントの最大数を構成します。この数に達してもキューがフラッシュされていない場合、最も古いイベントが削除されます。 |

### タグ管理

タグ管理とイベントのバッチ処理を有効にすると、トラッキング呼び出しは、非表示の WebView に対する個別の JavaScript 呼び出しとして送信されます。

構成されたタグは個別にトリガーされるため、イベントごとに複数のリクエストがデバイスから送信されます。リアルタイムイベントを送信する場合よりもデバイスの起動頻度が低くなるため、デバイスのパフォーマンスが向上します。

### Tealium Collect

現在、このエンドポイントは、Tealium SDK によって独自のバッチ形式で生成されたバッチデータのみを受け付けます。