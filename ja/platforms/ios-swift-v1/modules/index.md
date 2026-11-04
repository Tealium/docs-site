---
title: モジュール
description: 利用可能なモジュールの一覧です。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/modules/
---
<blockquote>
これは、Tealium for iOS（Swift）の旧バージョン（1.x）です。最新バージョンについては、[Tealium for iOS（Swift）2.x](https://docs.tealium.com/ja/platforms/ios-swift/)を参照してください。
</blockquote>


Tealium Swiftライブラリは、モジュール式アーキテクチャを中心に設計されています。モジュールが存在する場合は自動的にインスタンス化され、`TealiumConfig`インスタンスから構成を取得します。

すべてのモジュールは`TealiumCore`に依存しています。つまり、いずれかのオプションモジュールをインストールすると、`TealiumCore`もインストールされます。

## モジュール一覧

以下のモジュールは、優先順位（自動インスタンス化が行われる内部順序）に従って一覧表示されています。

| モジュール名 | モジュールID | 説明 | 対応プラットフォーム |
| --- | --- | --- | --- |
| [AppData](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/appdata/)|`appdata` | トラッキングデータに`app_uuid`を追加します | iOS、macOS、tvOS、watchOS |
| [Attribution](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/attribution/)|`attribution` | トラッキングデータにIDFAを追加します | iOS |
| [AutoTracking](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/autotracking/)|`autotracking` | `viewDidAppear`イベントを含む、ほとんどのUIに対するディスパッチを準備して送信します | iOS、tvOS |
| [Collect](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/collect/)|`collect` | トラッキング呼び出しをパッケージ化し、Tealium Collectまたはその他のカスタムURLエンドポイントに送信します | iOS、macOS、tvOS、watchOS |
| [ConsentManager](https://docs.tealium.com/ja/platforms/ios-swift/consent-management)|`consentmanager` | GDPRおよびプライバシー要件への準拠を支援します | iOS、macOS、tvOS、watchOS |
| [Connectivity](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/connectivity/)|connectivity | 接続が失われた場合、トラッキングメッセージに遅延送信用のフラグを構成できるようにします | iOS、macOS、tvOS、watchOS |
| [CrashReporter](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/crash-reporter/)|`crashreporter` | アプリのクラッシュを自動的にトラッキングします。モジュールを有効にして関連フレームワークをインストールすると、アプリでクラッシュが発生した場合にクラッシュイベントがトリガーされます。 | iOS |
| [DataSource](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/datasource/) | `datasource` | データソースID用の追加の構成初期化オプションを提供します。Swift 1.8.0以降ではCoreに含まれています。 | iOS、macOS、tvOS、watchOS |
| [DefaultStorage](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/defaults-storage/) | `defaultstorage` | 任意のモジュールに汎用的な永続化機能を追加します（UserDefaultsを使用）。Swift 1.8.0以降ではCoreに含まれています。 | iOS、tvOS、watchOS、macOS |
| [Delegate](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/delegate/)|`delegate` | トラッキングディスパッチを監視または抑制するためのマルチキャストデリゲートを追加します | iOS、macOS、tvOS、watchOS |
| [DeviceData](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/device-data/)|`devicedata` | すべてのトラッキングデータに追加のデバイス情報を加えます | iOS、macOS、tvOS、watchOS |
| [DispatchQueue](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/dispatch-queue/)|`dispatchqueue` | キューに登録されたディスパッチ用の永続保存を追加し、有効な場合はイベントバッチ処理を管理します | iOS、macOS、tvOS、watchOS |
| [FileStorage](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/file-storage/)|`filestorage` | 任意のモジュールに汎用的な永続化機能を追加します。Defaults Storageモジュールの代替となり、`NSKeyedArchiver`を使用します。Swift 1.8.0以降ではCoreに含まれています。 | iOS、macOS、watchOS、tvOS |
| [Lifecycle](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/lifecycle/)|`lifecycle` | 起動、ウェイク、スリープ、クラッシュの各インスタンスを自動または手動でトラッキングします | iOS、tvOS、watchOS |
| [Location](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/location/)| `location` | イベントにデバイスの位置情報を提供し、関心地点の周囲にジオフェンスを追加できるようにします | iOS、Mac Catalyst、macOS、tvOS、watchOS |
| [Logger](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/logger/)|`logger` | デバッグログを出力します | iOS、macOS、tvOS、watchOs |
| [PersistentData](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/persistent-data/)|`persistentdata` | すべてのトラッキングデータに永続データを追加できるようにします | iOS、macOS、tvOS、watchOS |
| [RemoteCommands](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/remote-commands/)|`remotecommands` | `URLScheme`、`UIWebView`、または`TagManagement`を通じて、構成可能なリモートコードブロックを実行できるようにします | iOS |
| [TagManagement](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/tag-management/)|`tagmanagement` | ライブラリでTIQ/`utag.js`を実行できる、`UIWebview`ベースのディスパッチサービスです | iOS |
| [Visitor Service](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/visitor-service/)|`visitorservice` | Visitor Serviceから更新された訪問プロファイルを取得します | iOS、macOS、tvOS、watchOS |
| [Volatile Data](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/volatile-data/)|`volatiledata` | すべてのトラッキングデータにセッション永続データを追加できるようにします（アプリの終了時またはクローズ時に消去されます） | iOS、macOS、tvOS、watchOS |

## 推奨モジュール

以下のセクションでは、推奨モジュールを示します。

### 基本実装

基本実装で推奨されるモジュールの一覧です。

* Core
* Attribution
* AppData
* Connectivity
* Delegate
* DeviceData
* DispatchQueue
* Lifecycle
* Logger
* PersistentData
* VolatileData

### タグ管理

タグ管理を導入する場合は、基本モジュールに加えて以下のモジュールが必要です。

* Consent Manager
* RemoteCommands
* TagManagement

### イベントストリーミングおよび顧客データプラットフォーム（CDP）

イベントストリーミングおよび顧客データプラットフォーム（CDP）を導入する場合は、基本モジュールに加えて以下のモジュールが必要です。

* Collect
* Consent Manager

## モジュールのインストール

CocoaPodsまたはCarthageを使用してモジュールをインストールします。

### CocoaPods

特定のモジュールを含める方法または除外する方法については、[CocoaPodsを使用したインストール](https://docs.tealium.com/ja/platforms/ios-swift/install/#cocoapods)を参照してください。

### Carthage

Carthageを使用してインストールする場合は、必要なモジュールを明示的にインポートする必要があります。必要に応じてすべてのモジュールをインポートし、前述のモジュール一覧を使用することもできますが、必要なモジュールのみをインポートすることでアプリを軽量化できます。特定のモジュールを含める方法または除外する方法については、[Carthageを使用したインストール](https://docs.tealium.com/ja/platforms/ios-swift/install/#carthage)を参照してください。

## モジュールの無効化

Tealium Swift SDKバージョン1.6.5より前では、CocoaPodsまたはCarthageを使用している場合、不要なモジュールを無効にする唯一の方法は、[TealiumConfig](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/)オブジェクトを使用して、有効または無効にするモジュールの配列（ホワイトリストまたはブラックリスト）を構成することでした。この場合も、すべてのコードは最終的なアプリバンドルにコンパイルされますが、無効にしたモジュールは非アクティブになります。

この方法は引き続きサポートされていますが、アプリバンドルにコンパイルするコード量を減らすことによるパフォーマンス向上を活用するため、以下のいずれかの方法に移行することをお勧めします。`TealiumConfig`オブジェクトではモジュール一覧を有効のまま安全に維持し、それと同時に不要なモジュールを削除できます。有効にしようとしたモジュールのコードがアプリバンドル内に存在しない場合でも、望ましくない結果は発生せず、単に何も効果がありません。

以下の例では、自動トラッキングモジュールをブラックリストに登録しています。

```swift
let modulesList = TealiumModulesList(isWhitelist: false, moduleNames: ["autotracking"])
config.setModulesList(modulesList)
```