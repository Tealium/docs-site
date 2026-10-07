---
title: レガシーSDKからTealium Prismへのヘルパークラスの移行
description: iOSまたはAndroidアプリのTealiumHelperクラスをTealium for SwiftまたはTealium for Android（Kotlin）からTealium Prismを介してイベントをルーティングするように変更します。
url: https://docs.tealium.com/ja/administration/early-access/tealium-prism/migrate-helper-class/
---
## 対象者

Tealium for Swift 2.xまたはTealium for Android（Kotlin）1.xを使用しているアプリがあり、SDKをラップする`TealiumHelper`クラスがある方。このページでは、各レガシーコールを置き換えるPrismコールを示します。SDK間で保存されたデータを移動する方法については説明しません。

## 開始する前に

### 要件

* PrismはiOS 13またはAndroid API 23を必要とします。
* PrismはSwiftおよびKotlinのみ対応しています。JavaアプリはKotlin APIを呼び出します。Objective-Cはサポートされていません。

### 保存されたデータ

保存されたデータは移動しません。アップグレード後、ユーザーは新しい訪問ID、空の永続データレイヤー、リセットされたライフサイクルカウンターを取得します。同じアカウントとプロファイルを保持します。データ移行は後のリリースで計画されています。

### ディスパッチャーとモジュール

Prismにはタグ管理（Webビュー）ディスパッチャー、リモートコマンド、組み込みの同意管理者、タイムドイベント、以下のモジュールが含まれていません：
  * 広告識別子
  * アトリビューション
  * 自動追跡
  * クラッシュレポーター
  * ホストされたデータレイヤー
  * アプリ内購入
  * インストールリファラー
  * 位置情報
  * メディア
  * 訪問サービス

### 依存関係

Prismをインポートする前に依存関係を更新してください：

* **iOS**  
`TealiumSwift`を`TealiumPrism`（CocoaPods）または`TealiumPrismCore`および`TealiumPrismLifecycle`（Swift Package Manager）に置き換えます。
* **Android**  
`com.tealium:kotlin-core`を`com.tealium.prism:prism-bom` BOMおよび`prism-core`、`prism-lifecycle`に置き換えます。

## 初期化

レガシーにはコレクターとディスパッチャーの2つのリストがあります。Prismにはモジュールの1つのリスト、ローカル構成ファイル、リモート構成URL、およびプログラム構成のブロックがあります。



```swift
// レガシー
let config = TealiumConfig(account: "ACCOUNT", profile: "PROFILE",
                           environment: "prod", dataSource: "DATASOURCE")
config.collectors = [Collectors.AppData, Collectors.Lifecycle]
config.dispatchers = [Dispatchers.Collect, Dispatchers.TagManagement]
tealium = Tealium(config: config) { _ in }

// Prism
let config = TealiumConfig(
    account: "ACCOUNT", profile: "PROFILE", environment: "prod",
    dataSource: "DATASOURCE",
    modules: [Modules.appData(), Modules.lifecycle(), Modules.collect()],
    settingsFile: "TealiumSettings",
    settingsUrl: "https://tags.tiqcdn.com/utag/ACCOUNT/PROFILE/prod/mobile_settings.json",
    forcingSettings: { $0.setMinLogLevel(.info) })
tealium = Tealium.create(config: config) { result in
    // Result<Tealium, Error>
}
```


```kotlin
// レガシー
val config = TealiumConfig(application, "ACCOUNT", "PROFILE", Environment.PROD,
    dataSourceId = "DATASOURCE",
    collectors = mutableSetOf(Collectors.App, Collectors.Device),
    dispatchers = mutableSetOf(Dispatchers.Collect, Dispatchers.TagManagement),
    modules = mutableSetOf(Modules.Lifecycle))
Tealium.create("main", config) { }

// Prism
val config = TealiumConfig.Builder(application, "ACCOUNT", "PROFILE", Environment.PROD,
        listOf(Modules.appData(), Modules.deviceData(), Modules.lifecycle(), Modules.collect()))
    .setDataSource("DATASOURCE")
    .setSettingsFile("tealium-settings.json")
    .setSettingsUrl("https://tags.tiqcdn.com/utag/ACCOUNT/PROFILE/prod/mobile_settings.json")
    .configureCoreSettings { it.setLogLevel(LogLevel.INFO) }
    .build()
tealium = Tealium.create(config) { result -> /* TealiumResult<Tealium> */ }
```



Prismは`ACCOUNT-PROFILE`でインスタンスをキーします。`Tealium["main"]`はAndroidで非同期の`Tealium.get("ACCOUNT-PROFILE") { }`に、iOSでは`TealiumInstanceManager.get(_:completion:)`になります。ほとんどのヘルパーは自分の参照を保持します。

## イベントまたはビューをトラックする

Prismには1つの`track`メソッドがあります。ビューまたはイベントタイプはパラメータであり、データは`DataObject`です。



```swift
// レガシー
tealium.track(TealiumEvent("purchase", dataLayer: ["order_id": "123"]))
tealium.track(TealiumView("home"))

// Prism
tealium.track("purchase", data: ["order_id": "123"])
tealium.track("home", type: .view)
```
<!-- TODO verify: does DataObject conform to ExpressibleByDictionaryLiteral, or must the sample use a DataObject builder? Signature confirmed: track(_ name: String, type: DispatchType = .event, data: DataObject? = nil). -->


```kotlin
// レガシー
tealium.track(TealiumEvent("purchase", mapOf("order_id" to "123")))
tealium.track(TealiumView("home"))

// Prism
tealium.track("purchase", DataObject.create { put("order_id", "123") })
tealium.track("home", DispatchType.View, DataObject.EMPTY_OBJECT)
```



## データレイヤー

`add`は`put`に、`delete`は`remove`になり、読み取りは非同期です。有効期限の名前は変更されていませんが、Swiftの`.afterCustom`はなくなりました。代わりに`.after(Date)`を使用します。



```swift
// レガシー
tealium.dataLayer.add(key: "user_tier", value: "gold", expiry: .forever)
tealium.dataLayer.delete(for: "user_tier")
let tier = tealium.dataLayer.all["user_tier"]

// Prism
tealium.dataLayer.put(key: "user_tier", value: "gold", expiry: .forever)
tealium.dataLayer.remove(key: "user_tier")
tealium.dataLayer.get(key: "user_tier", as: String.self).subscribe { result in
    // Result<String?, ModuleError<Error>>
}
```


```kotlin
// レガシー
tealium.dataLayer.putString("user_tier", "gold", Expiry.FOREVER)
tealium.dataLayer.remove("user_tier")
val tier = tealium.dataLayer.getString("user_tier")

// Prism
tealium.dataLayer.put("user_tier", "gold", Expiry.FOREVER)
tealium.dataLayer.remove("user_tier")
tealium.dataLayer.getString("user_tier").subscribe { result -> /* TealiumResult<String?> */ }
```



1回のトランザクションで複数の値を書き込むには、両プラットフォームで`dataLayer.transactionally { }`を使用します。

## 同意

Prismには独自の同意ステータスやカテゴリーはありません。同意管理プラットフォーム（CMP）が真実の情報源です。ユーザーの決定を一連の目的として公開する小さなアダプタを実装し、各目的をそれが解放するディスパッチャーにマッピングします。



```swift
// レガシー
config.consentPolicy = .gdpr
tealium.consentManager?.userConsentStatus = .consented
tealium.consentManager?.userConsentCategories = [.analytics]

// Prism
final class MyCMPAdapter: CMPAdapter {
    let id = "my_cmp"
    let allPurposes: Set<String>? = ["analytics", "marketing"]
    let consentDecision: Observable<ConsentDecision?>   // emit on every user decision
    // TODO verify: how a customer constructs the Observable (Subject type name).
}
config.enableConsentIntegration(with: MyCMPAdapter(), forcingConfiguration: {
    $0.addPurpose("analytics", dispatcherIds: ["Collect"])
})
```


```kotlin
// レガシー
config.consentManagerPolicy = ConsentPolicy.GDPR
tealium.consentManager.userConsentStatus = ConsentStatus.CONSENTED

// Prism
class MyCmpAdapter : CmpAdapter {
    override val id = "my_cmp"
    override allPurposes: Set<String>? = setOf("analytics", "marketing")
    override val consentDecision: Observable<ConsentDecision?> = TODO()
}
TealiumConfig.Builder(https://docs.tealium.com/* ... */)
    .enableConsentIntegration(MyCmpAdapter()) { it.addPurpose("analytics", listOf("Collect")) }
```



<!-- TODO verify: ConsentDecision.DecisionType case names. Also verify addPurpose parameter types on Kotlin ConsentConfigurationBuilder. Consent surface is the least stable API at 0.6.0 (MT-2080 replay fix open). -->
## 訪問ID



```swift
// レガシー
let id = tealium.visitorId
tealium.resetVisitorId()
config.visitorIdentityKey = "customer_id"

// プリズム
tealium.resetVisitorId()          // 新しいIDを結果として返す
tealium.clearStoredVisitorIds()
// アイデンティティの切り替え: forcingSettings: { $0.setVisitorIdentityKey("customer_id") }
```


```kotlin
// レガシー
val id = tealium.visitorId
tealium.resetVisitorId()
config.visitorIdentityKey = "customer_id"

// プリズム
tealium.resetVisitorId()          // SingleResult<String>
tealium.clearStoredVisitorIds()
// アイデンティティの切り替え: .configureCoreSettings { it.setVisitorIdentityKey("customer_id") }
```



Prism 0.6.0では、現在の訪問IDを読み取る方法はありません。IDはすべてのイベントで `tealium_visitor_id` として送信されます。

## リモートコマンドがディスパッチャーになる

Prismでは、各ベンダーはCollectと同じ役割とライフサイクルを持つディスパッチャーモジュールです：ネイティブ、ディスクにキュー、同意とバリアによって制御され、構成ファイルから構成されます。公開されているディスパッチャーを使用するか（今日のiOSではFirebase）、自分で書いてください。



```swift
// レガシー
let firebase = RemoteCommand(commandId: "firebase", description: "Firebase", type: .webview) { response in
    // Firebase SDKをレスポンスのペイロードで呼び出す
}
config.addRemoteCommand(firebase)

// プリズム: Dispatcherを実装し、そのModuleFactoryを `modules` に登録する
final class MyDispatcher: Dispatcher {
    let id = "my_vendor"
    let version = "1.0.0"
    func dispatch(_ data: [Dispatch], completion: @escaping ([Dispatch]) -> Void) -> any Disposable {
        // 各ディスパッチペイロードをベンダーSDKに送信し、成功したディスパッチで完了する
    }
    func updateConfiguration(_ configuration: DataObject) -> Self? { self }
    func shutdown() {}
}
```


```kotlin
// レガシー
tealium.remoteCommands?.add(FirebaseRemoteCommand(application))

// プリズム: CommandDispatcherを拡張して名前付きコマンドを登録し、そのModuleFactoryを `modules` に登録する
val commands = listOf(Command.synchronous("log_event") { payload -> /* ベンダーSDK呼び出し */ })
```



<!-- TODO 確認: iOSモジュール用Firebaseディスパッチャーファクトリーの名前（別のリポジトリ tealium-prism-ios-firebase-dispatcher）。また、Kotlinの完全なCommandDispatcherコンストラクター（id, version, commands, logger, logCategory, scheduler）とModuleFactoryのボイラープレートを確認する。マージされたらModulesページへのリンクを追加する。 -->

## ロギング



```swift
// レガシー
config.logLevel = .info            // info, debug, error, fault, silent

// プリズム
forcingSettings: { $0.setMinLogLevel(.debug) }   // trace, debug, info, warn, error, silent
config.loggerType = .custom(myLogHandler)        // オプション
```


```kotlin
// レガシー
config.logLevel = LogLevel.DEV     // DEV, QA, PROD, SILENT

// プリズム
.configureCoreSettings { it.setLogLevel(LogLevel.DEBUG) }  // TRACE, DEBUG, INFO, WARN, ERROR, SILENT
.setLogHandler(myLogHandler)                                // オプション
```



レベルは `mobile_settings.json` の `core` の下の `log_level` キーでリモートで構成することもでき、プログラム的な値が優先されます。

## 終了処理



```swift
// レガシー
tealium.disable()

// プリズム
tealium.shutdown()   // その後の呼び出しは TealiumError.instanceShutdown で失敗する
```


```kotlin
// レガシー
Tealium.destroy("main")

// プリズム
tealium.shutdown()   // または Tealium.shutdown("ACCOUNT-PROFILE")
```



`shutdown()` を呼び出す前に、保持しているすべてのサブスクリプションを破棄してください。

## 挙動の違い

| 領域 | レガシー | プリズム |
|---|---|---|
| キューイング | 1つのキュー。バッチ処理とオフラインは構成フラグごとに処理される。 | ディスパッチャーごとに1つのSQLiteキュー。すべてのイベントは送信前に書き込まれ、確認された送信後に削除される。バリア（接続性、バッチ処理）がキューを解放する。`flushEventQueue()` で強制的に実行する。 |
| 同意 | SDKがステータスとカテゴリを保存する。同意が得られるまでイベントはキューに入る。 | SDKは何も保存しない。CMPアダプターが目的を公開する。各目的は名前付きディスパッチャーを解放する。保持されたイベントはリストにあるディスパッチャーのために再発火する。 |
| 構成 | プログラム的な構成とTealium iQからの `mobile.json` | ローカルファイル < リモートURL（オフライン用にキャッシュ） < プログラム的。プログラム的な値はリモートで上書きされることはない。モジュールはそれに対する構成が存在するときのみ開始される。 |
| タグロジック | utag.js in a webview | デバイス上のトランスフォーマー：値を構成、小文字に変換、永続化、分離されたランタイムのJavaScript。ウェブビューなし。 |
| スレッディングと結果 | 混在。いくつかの同期読み取り。発射して忘れる。 | すべての公開呼び出しは任意のスレッドから安全で、1つのSDKキュー上で実行される。すべての書き込みまたは読み取りは `SingleResult` または `Single` を返す。エラーを確認するために購読するか、無視する。完了はSDKキューで実行され、あなたのものではない。 |
| 保存されたデータ | SDKのアップグレードをまたいで持続する | 0.6.0でレガシーから持ち越されない |

## チェックリスト

1. 配備ターゲットをiOS 13またはAPI 23に上げる。
1. 依存関係と `import` を交換する。
1. 2つのコレクターとディスパッチャーリストを1つの `modules` リストに置き換える。Tag ManagementとRemote Commandsを削除する。
1. `settingsFile` または `settingsUrl` を追加する。モジュールごとのオプションを構成ファイルまたは `forcingSettings` / `configureCoreSettings` に移動する。
1. `Tealium(config:)` または `Tealium.create(name, config)` を `Tealium.create(config)` に置き換える。
1. `TealiumEvent` / `TealiumView` を `track(name, type:, data:)` に置き換える。
1. `add` を `put` に、`delete` を `remove` に名前を変更する。
1. 読み取りを非同期にする。
1. 同意マネージャーをCMPアダプターと目的マッピングに置き換える。
1. 各リモートコマンドをディスパッチャーモジュールに置き換える。
1. ログレベルを構成に移動する。
1. `disable()` と `destroy()` を `shutdown()` に置き換える。
1. 新規インストールとレガシーアプリからのアップグレードでテストする。
1. アップグレード時に新しい訪問IDが発行されることを期待する。

## ヘルプの入手先

移行のタイムラインについての質問は、[サポートに連絡](https://docs.tealium.com/support/)してください。SDKの欠陥は [tealium-prism-swift](https://github.com/tealium/tealium-prism-swift/issues) と [tealium-prism-kotlin](https://github.com/tealium/tealium-prism-kotlin/issues) で報告してください。