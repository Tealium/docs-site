---
title: モジュール
description: 利用可能なモジュールのリストです。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/modules/
---
<blockquote>
これはiOS（Swift）用Tealiumの以前のバージョン（1.x）です。最新バージョンについては、[Tealium for iOS (Swift) 2.x](https://docs.tealium.com/ja/platforms/ios-swift/)をご覧ください。
</blockquote>


Tealium Swiftライブラリは、モジュラーアーキテクチャを中心に設計されています。モジュールは存在する場合に自動的にインスタンス化され、`TealiumConfig`インスタンスから構成を取得します。

すべてのモジュールは`TealiumCore`に依存しています。これは、任意のオプションモジュールをインストールすると`TealiumCore`もインストールされることを意味します。

## モジュールリスト

以下に優先順位（自動インスタンス化が行われる内部順序）でモジュールをリストアップします。

| モジュール名 | モジュールID |説明 | 対応プラットフォーム |
| --- | --- | --- | --- |
| [AppData](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/appdata/)|`appdata` | トラックデータに`app_uuid`を追加 | iOS, macOS, tvOS, watchOS |
| [Attribution](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/attribution/)|`attribution` | トラックデータにIDFAを追加 | iOS |
| [AutoTracking](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/autotracking/)|`autotracking` | `viewDidAppear`イベントを含むほとんどのUIのディスパッチを準備・送信 | iOS, tvOS |
| [Collect](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/collect/)|`collect` | トラックコールをTealium Collectまたは他のカスタムURLエンドポイントにパッケージして配信 | iOS, macOS, tvOS, watchOS |
| [ConsentManager](https://docs.tealium.com/ja/platforms/ios-swift/consent-management)|`consentmanager` | GDPR/プライバシーのコンプライアンスを支援 | iOS, macOS, tvOS, watchOS |
| [Connectivity](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/connectivity/)|connectivity | 接続の喪失による遅延配信のためにトラックメッセージにフラグを追加 | iOS, macOS, tvOS, watchOS |
| [CrashReporter](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/crash-reporter/)|`crashreporter` | アプリのクラッシュを自動的にトラック。モジュールが有効になり、関連するフレームワークがインストールされると、アプリでクラッシュが発生した場合にクラッシュイベントがトリガーされます。 | iOS |
| [DataSource](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/datasource/) | `datasource` | データソースIDのための追加の構成初期化オプションを追加。Swift 1.8.0+でCoreに含まれています。 | iOS, macOS, tvOS, watchOS |
| [DefaultStorage](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/defaults-storage/) | `defaultstorage` | 任意のモジュールの一般的な永続性機能を追加（UserDefaultsによってバックアップされます）。Swift 1.8.0+でCoreに含まれています。 | iOS, tvOS, watchOS, macOS |
| [Delegate](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/delegate/)|`delegate` | トラックディスパッチの監視または抑制のためのマルチキャストデリゲートを追加 | iOS, macOS, tvOS, watchOS |
| [DeviceData](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/device-data/)|`devicedata` | すべてのトラックデータに追加のデバイス情報を追加 | iOS, macOS, tvOS, watchOS |
| [DispatchQueue](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/dispatch-queue/)|`dispatchqueue` | キューに入れられたディスパッチの永続的な保存を追加し、有効になっている場合はイベントバッチ処理を管理 | iOS, macOS, tvOS, watchOS |
| [FileStorage](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/file-storage/)|`filestorage` | 任意のモジュールの一般的な永続性機能を追加 - Defaults Storageモジュールを置き換えます（`NSKeyedArchiver`によってバックアップされます）。Swift 1.8.0+でCoreに含まれています。 | iOS, macOS, watchOS, tvOS |
| [Lifecycle](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/lifecycle/)|`lifecycle` | 起動、起床、睡眠、クラッシュインスタンスをトラック（自動または手動） | iOS, tvOS, watchOS |
| [Location](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/location/)| `location` | イベントのためのデバイスの位置情報を提供し、興味のあるポイント周辺にジオフェンスを追加する機能 | iOS, Mac Catalyst, macOS, tvOS, watchOS |
| [Logger](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/logger/)|`logger` | デバッグログ | iOS, macOS, tvOS, watchOs |
| [PersistentData](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/persistent-data/)|`persistentdata` | すべてのトラックデータに永続的なデータを追加する機能 | iOS, macOS, tvOS, watchOS |
| [RemoteCommands](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/remote-commands/)|`remotecommands` | `URLScheme`、`UIWebView`、または`TagManagement`を介して構成可能なリモートコードブロックの実行を許可 | iOS |
| [TagManagement](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/tag-management/)|`tagmanagement` | `UIWebview`ベースのディスパッチサービスで、ライブラリがTIQ/`utag.js`を実行することを許可 | iOS |
| [Visitor Service](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/visitor-service/)|`visitorservice` | 訪問サービスから更新された訪問プロファイルを取得 | iOS, macOS, tvOS, watchOS |
| [Volatile Data](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/volatile-data/)|`volatiledata` | すべてのトラックデータにセッション永続的なデータを追加する機能（アプリ終了/閉鎖時にクリア） | iOS, macOS, tvOS, watchOS |

## 推奨モジュール

以下のセクションでは、推奨モジュールをリストアップします。

### 基本実装
これは基本実装のための推奨モジュールリストです。

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
基本モジュールに加えて、タグ管理インストールに必要なモジュールです。

* Consent Manager
* RemoteCommands
* TagManagement

### Tealium EventStream/AudienceStream
基本モジュールに加えて、EventStream/ AudienceStreamインストールに必要なモジュールです。

* Collect
* Consent Manager

## モジュールのインストール

CocoaPodsまたはCarthageでモジュールをインストールします。

### CocoaPods

特定のモジュールを含める/除外する方法については、[CocoaPodsでのインストール](https://docs.tealium.com/ja/platforms/ios-swift/install/#cocoapods)を参照してください。

### Carthage

Carthageでインストールする場合、必要なモジュールを明示的にインポートする必要があります。必要に応じてすべてのモジュールをインポートすることもできますが、必要なモジュールのみをインポートするとアプリが軽くなります。特定のモジュールを含める/除外する方法については、[Carthageでのインストール](https://docs.tealium.com/ja/platforms/ios-swift/install/#carthage)を参照してください。


## モジュールの無効化

Tealium Swift SDKのバージョン1.6.5以前では、CocoaPodsまたはCarthageを使用している場合、不要なモジュールを無効にする唯一の方法は、[TealiumConfig](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/)オブジェクトを使用して、有効/無効モジュールの配列（ホワイトリスト/ブラックリスト）を構成することでした。このシナリオでは、すべてのコードが最終的なアプリバンドルにコンパイルされていましたが、無効にされたモジュールは非アクティブ化されていました。

この方法はまだサポートされていますが、アプリバンドルにコードをコンパイルする量を減らすことに関連するパフォーマンス向上を活用するために、以下の他の方法に移行することをお勧めします。`TealiumConfig`オブジェクトでモジュールリストを有効にしたまま、不要なモジュールを同時に削除します。モジュールを有効にしようとすると、アプリバンドルにコードが存在しない場合、望ましくない結果を引き起こすことはなく、単に効果がありません。

次の例では、自動追跡モジュールをブラックリストに登録します：

```swift
let modulesList = TealiumModulesList(isWhitelist: false, moduleNames: ["autotracking"])
config.setModulesList(modulesList)
```
