---
title: ヘルパークラスをレガシーSDKからTealium Prismへ移行する
description: iOSまたはAndroidアプリのTealiumHelperクラスを変更し、Tealium for SwiftまたはTealium for Android（Kotlin）の代わりにTealium Prismを経由してイベントを送信します。
url: https://docs.tealium.com/ja/platforms/prism-mobile/migrate-helper-class/
---

<blockquote>
このガイドでは、レガシーTealium SDKからTealium Prismへ移行するiOS（Swift）およびAndroid（Kotlin）アプリについて説明します。
</blockquote>


## 対象読者

Tealium for Swift 2.xまたはTealium for Android（Kotlin）1.xを使用しており、SDKをラップする`TealiumHelper`クラスがアプリにある場合を対象としています。このページでは、各レガシー呼び出しに代わるPrismの呼び出しを示します。SDK間での保存データの移行については説明しません。

## 始める前に

### 要件

* PrismにはiOS 13またはAndroid API 23が必要です。
* PrismのネイティブSDKはSwiftとKotlinのみをサポートします。JavaアプリではKotlin APIを呼び出します。Objective-Cはサポートされていません。

### 保存データ

保存データは移行されません。アップグレード後、ユーザーには新しい訪問IDが割り当てられ、永続データレイヤーは空になり、ライフサイクルカウンターはリセットされます。同じアカウントとプロファイルを使用してください。データ移行機能は今後のリリースで提供される予定です。

### ディスパッチャーとモジュール

Prismには、Tag Management（WebView）ディスパッチャー、リモートコマンド、組み込みの同意マネージャー、時間計測イベント、および以下のモジュールは含まれていません。
  * Ad Identifier
  * Attribution
  * AutoTracking
  * Crash Reporter
  * Hosted Data Layer
  * In-App Purchase
  * Install Referrer
  * Location
  * Media
  * Visitor Service

### 依存関係

Prismをインポートする前に、依存関係を更新します。

* **iOS**  
`tealium-swift`を`tealium-prism`（CocoaPods）、または`TealiumPrismCore`と`TealiumPrismLifecycle`（Swift Package Manager）に置き換えます。
* **Android**  
`com.tealium:kotlin-core`を、`com.tealium.prism:prism-bom` BOMおよび`prism-core`、`prism-lifecycle`に置き換えます。

## 初期化

レガシーSDKにはコレクターとディスパッチャーという2つのリストがあります。Prismには1つのモジュールリストに加えて、ローカル構成ファイル、リモート構成URL、およびプログラムによる構成ブロックがあります。



```swift
// Legacy
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
// Legacy
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



Prismでは、インスタンスは`ACCOUNT-PROFILE`をキーとして管理されます。`Tealium["main"]`は、Androidでは非同期の`Tealium.get("ACCOUNT-PROFILE") { }`に、iOSでは`TealiumInstanceManager.get(_:completion:)`に置き換わります。ほとんどのヘルパーは独自の参照を保持します。

## イベントまたはビューのトラッキング

Prismには`track`メソッドが1つあります。ビューまたはイベントのタイプはパラメーターとして指定し、データには`DataObject`を使用します。



```swift
// Legacy
tealium.track(TealiumEvent("purchase", dataLayer: ["order_id": "123"]))
tealium.track(TealiumView("home"))

// Prism
tealium.track("purchase", data: ["order_id": "123"])
tealium.track("home", type: .view)
```


```kotlin
// Legacy
tealium.track(TealiumEvent("purchase", mapOf("order_id" to "123")))
tealium.track(TealiumView("home"))

// Prism
tealium.track("purchase", DataObject.create { put("order_id", "123") })
tealium.track("home", DispatchType.View, DataObject.EMPTY_OBJECT)
```



## データレイヤー

`add`は`put`に、`delete`は`remove`に置き換わり、読み取りは非同期になります。有効期限の名前は変更されていませんが、Swiftの`.afterCustom`は廃止されました。代わりに`.after(Date)`を使用してください。



```swift
// Legacy
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
// Legacy
tealium.dataLayer.putString("user_tier", "gold", Expiry.FOREVER)
tealium.dataLayer.remove("user_tier")
val tier = tealium.dataLayer.getString("user_tier")

// Prism
tealium.dataLayer.put("user_tier", "gold", Expiry.FOREVER)
tealium.dataLayer.remove("user_tier")
tealium.dataLayer.getString("user_tier").subscribe { result -> /* TealiumResult<String?> */ }
```



1つのトランザクションで複数の値を書き込むには、両方のプラットフォームで`dataLayer.transactionally { }`を使用します。

## 同意

現在、Prismでは同意管理を利用できません。Prismにはレガシーの同意マネージャーに相当する機能がなく、同意に基づいてイベントを保留またはブロックすることもありません。代わりに、ユーザーの同意に関する選択内容をデータレイヤーに渡し、[同意オーケストレーション](https://docs.tealium.com/about-consent-orchestration/)を使用してサーバー側で適用してください。詳細については、[同意](https://docs.tealium.com/platforms/prism-mobile/consent-management/)を参照してください。



```swift
// Legacy
config.consentPolicy = .gdpr
tealium.consentManager?.userConsentStatus = .consented
tealium.consentManager?.userConsentCategories = [.analytics]

// Prism
tealium.dataLayer.put(key: "consent_categories", converting: ["analytics"], expiry: .forever)
```


```kotlin
// Legacy
config.consentManagerPolicy = ConsentPolicy.GDPR
tealium.consentManager.userConsentStatus = ConsentStatus.CONSENTED

// Prism
tealium.dataLayer.put("consent_categories", DataList.create { add("analytics") }, Expiry.FOREVER)
```


## ビジター ID

ビジター ID のメソッドは `tealium.visitorId` に移動し、読み取りは非同期になります。ID キーは構成からビジター ID マネージャーモジュールの構成に移動します。



```swift
// Legacy
let id = tealium.visitorId
tealium.resetVisitorId()
tealium.clearStoredVisitorIds()
config.visitorIdentityKey = "customer_id"

// Prism
tealium.visitorId.current().subscribe { result in
    // Result<String, ModuleError<Error>>
}
tealium.visitorId.regenerate()          // returns the new ID in a result
tealium.visitorId.eraseLocalHistory()
// identity switching: Modules.visitorId(forcingSettings: { $0.setVisitorIdentityKey("customer_id") })
```


```kotlin
// Legacy
val id = tealium.visitorId
tealium.resetVisitorId()
tealium.clearStoredVisitorIds()
config.visitorIdentityKey = "customer_id"

// Prism
tealium.visitorId.current().subscribe { result -> /* TealiumResult<String> */ }
tealium.visitorId.regenerate()          // SingleResult<String>
tealium.visitorId.eraseLocalHistory()
// identity switching: Modules.visitorId { it.setVisitorIdentityKey("customer_id") }
```



現在のビジター ID を読み取るには、`visitorId.current()` を呼び出します。この ID は、すべてのイベントで `tealium_visitor_id` としても送信されます。

## リモートコマンドからディスパッチャーへの変更

Prism では、各ベンダーは Collect と同じ役割とライフサイクルを持つディスパッチャーモジュールです。ネイティブで動作し、ディスク上のキューに保存され、バリアによって制御され、構成ファイルから構成されます。公開済みのディスパッチャーが存在する場合（現時点では iOS 用 Firebase）はそれを使用し、存在しない場合は独自に作成してください。



```swift
// Legacy
let firebase = RemoteCommand(commandId: "firebase", description: "Firebase", type: .webview) { response in
    // call the Firebase SDK with response.payload
}
config.addRemoteCommand(firebase)

// Prism: implement Dispatcher, register its ModuleFactory in `modules`
final class MyDispatcher: Dispatcher {
    let id = "my_vendor"
    let version = "1.0.0"
    func dispatch(_ data: [Dispatch], completion: @escaping ([Dispatch]) -> Void) -> any Disposable {
        // send each dispatch payload to the vendor SDK; complete with the dispatches that succeeded
        return Disposables.disposed()
    }
    func updateConfiguration(_ configuration: DataObject) -> Self? { self }
    func shutdown() {}
}
```


```kotlin
// Legacy
tealium.remoteCommands?.add(FirebaseRemoteCommand(application))

// Prism: extend CommandDispatcher with named commands, register its ModuleFactory in `modules`
val commands = listOf(Command.synchronous("log_event") { payload -> /* vendor SDK call */ })
```



<!-- TODO 確認事項：iOS モジュール（別リポジトリ tealium-prism-ios-firebase-dispatcher）の Firebase ディスパッチャーファクトリー名。また、Kotlin の CommandDispatcher の完全なコンストラクター（id、version、commands、logger、logCategory、scheduler）と ModuleFactory のボイラープレートも確認すること。マージ後に Modules ページへのリンクを追加すること。 -->

## ロギング



```swift
// Legacy
config.logLevel = .info            // info, debug, error, fault, silent

// Prism
forcingSettings: { $0.setMinLogLevel(.debug) }   // trace, debug, info, warn, error, silent
config.loggerType = .custom(myLogHandler)        // optional
```


```kotlin
// Legacy
config.logLevel = LogLevel.DEV     // DEV, QA, PROD, SILENT

// Prism
.configureCoreSettings { it.setLogLevel(LogLevel.DEBUG) }  // TRACE, DEBUG, INFO, WARN, ERROR, SILENT
.setLogHandler(myLogHandler)                                // optional
```



ログレベルは、`mobile_settings.json` の `core` にある `log_level` キーを使用してリモートから構成することもできます。プログラムで指定した値が優先されます。

## 終了処理



```swift
// Legacy
tealium.disable()

// Prism
tealium.shutdown()   // later calls fail with TealiumError.instanceShutdown
```


```kotlin
// Legacy
Tealium.destroy("main")

// Prism
tealium.shutdown()   // or Tealium.shutdown("ACCOUNT-PROFILE")
```



`shutdown()` を呼び出す前に、保持しているすべてのサブスクリプションを破棄してください。

## 動作の違い

| 項目 | Legacy | Prism |
|---|---|---|
| キュー処理 | キューは 1 つです。バッチ処理とオフライン処理は、構成フラグごとに処理されます。 | ディスパッチャーごとに 1 つの SQLite キューがあります。すべてのイベントは送信前に書き込まれ、送信が確認された後に削除されます。バリア（接続状態、バッチ処理）がキューを解放します。`flushEventQueue()` を使用すると強制的に解放できます。 |
| 同意 | SDK がステータスとカテゴリーを保存します。同意が得られるまで、イベントはキューに保持されます。 | 現在は利用できません。イベントは保持もブロックもされません。同意に関する選択内容をデータレイヤーで渡し、サーバー側で適用してください。 |
| 構成 | プログラムによる構成と Tag Management からの `mobile.json` | ローカルファイル < リモート URL（オフライン用にキャッシュ）< プログラムによる構成、の順で優先されます。プログラムで指定した値がリモートから上書きされることはありません。モジュールは、そのモジュール用の構成が存在する場合にのみ起動します。 |
| タグロジック | WebView 内の utag.js | デバイス上の Transformer：値の構成、小文字への変換、永続化、分離されたランタイム内での JavaScript 実行。WebView は使用しません。 |
| スレッド処理と結果 | 混在しています。一部は同期読み取りです。処理結果は通知されません。 | すべての公開呼び出しは任意のスレッドから安全に実行でき、単一の SDK キュー上で処理されます。すべての書き込みまたは読み取りは `SingleResult` または `Single` を返します。エラーを確認するにはサブスクライブし、不要であれば無視できます。完了処理は呼び出し元のキューではなく、SDK キュー上で実行されます。 |
| 保存済みデータ | SDK のアップグレード後も保持されます | 0.7.0 では Legacy から引き継がれません |

## チェックリスト

1. デプロイメントターゲットを iOS 13 または API 23 に引き上げます。
1. 依存関係と `import` を置き換えます。
1. コレクターとディスパッチャーの 2 つのリストを、1 つの `modules` リストに置き換えます。Tag Management と Remote Commands は削除します。
1. `settingsFile` または `settingsUrl` を追加します。モジュールごとのオプションを構成ファイルまたは `forcingSettings` / `configureCoreSettings` に移動します。
1. `Tealium(config:)` または `Tealium.create(name, config)` を `Tealium.create(config)` に置き換えます。
1. `TealiumEvent` / `TealiumView` を `track(name, type:, data:)` に置き換えます。
1. `add` を `put` に、`delete` を `remove` に名前変更します。
1. 読み取りを非同期にします。
1. 同意マネージャーを、データレイヤー内の同意データとサーバー側の適用処理に置き換えます。
1. 各リモートコマンドをディスパッチャーモジュールに置き換えます。
1. ログレベルを構成に移動します。
1. `disable()` と `destroy()` を `shutdown()` に置き換えます。
1. 新規インストール時と Legacy アプリからのアップグレード時の両方をテストします。
1. アップグレード時には新しいビジター ID が生成されることに注意してください。

## サポート情報

移行スケジュールに関する質問については、[サポートにお問い合わせください](https://docs.tealium.com/support/)。SDK の不具合は、[tealium-prism-swift](https://github.com/tealium/tealium-prism-swift/issues) および [tealium-prism-kotlin](https://github.com/tealium/tealium-prism-kotlin/issues) に報告してください。