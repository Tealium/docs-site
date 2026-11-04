---
title: TealiumConfig
description: メインの Tealium クラスの構成オプションを指定するためのクラス。有効化されている各モジュールは、TealiumConfig クラス向けに独自の拡張機能を提供します。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-config/
---
## クラス：`TealiumConfig`

以下に、iOS（Swift）の `TealiumConfig` クラスでよく使用されるメソッドとプロパティの概要を示します。

| メソッド／プロパティ | 説明 |
| ----- | ------ |
| `addDelegate()` | TealiumDelegate プロトコルに準拠する新しいデリゲートを追加します |
| `addRemoteCommand()` | 後で実行するリモートコマンドを追加します |
| `batchingBypassKeys` | バッチ処理をバイパスする（個別のイベントとして送信する）イベント名のリストを構成します |
| `batchingEnabled` | イベントのバッチ処理を有効または無効（デフォルト）にします |
| `batchSize` | 1回のバッチリクエストにまとめるイベント数を構成します（最大：10） |
| `collectOverrideProfile` | Tealium Collect プロファイルをオーバーライドし、別の Tealium プロファイルにデータを送信します |
| `collectOverrideURL` | Tealium Collect URL をオーバーライドし、別のエンドポイントにデータを送信します |
| `connectivityRefreshEnabled` | 有効（デフォルト）の場合、接続モジュールは指定された間隔で接続を確認します |
| `connectivityRefreshInterval` | デフォルトの接続更新間隔を秒単位で構成します |
| `consentLoggingEnabled` | 同意ログ機能を有効または無効にします |
| `delegates` | 有効なデリゲートの配列を返します |
| `dispatchAfter` | キューをフラッシュするイベント数を構成します |
| `dispatchExpiration` | バッチの有効期限を日数で構成します。デバイスが長期間オフラインの場合、古いイベントは削除されます |
| `dispatchQueueLimit` | キューに格納できるイベントの最大数を構成します。この数に達してもキューがフラッシュされていない場合、最も古いイベントが削除されます。 |
| `enableRemoteHTTPCommand()` | 組み込みのリモート HTTP コマンドを有効にします |
| `existingVisitorId` | アプリ拡張機能でファーストパーティ ID として使用する既存の訪問 ID を構成します |
| `geofenceFileName` | ローカルのジオフェンス JSON ファイルアセットの名前を構成します。_ファイル拡張子は含めないでください。_ |
| `geofenceUrl` | ホストされている JSON ファイルの URL を構成します |
| `initialUserConsentCategories` | ライブラリの初回起動時に、ユーザーの初期同意カテゴリを構成します |
| `initialUserConsentStatus` | ユーザーの初期同意ステータスを構成します |
| `logLevel` | 新しいログレベルを構成します |
| `memoryReportingEnabled` | DeviceData モジュールのメモリレポートを有効または無効にします |
| `modulesList` | 有効または無効にするモジュールのリスト |
| `overrideConsentPolicy` | デフォルトの同意 `policy` パラメータをオーバーライドします |
| `remoteAPIEnabled` | `remote_api` イベントを有効（`true`）または無効（`false`）にします。DispatchQueue モジュールを使用している場合、RemoteCommands モジュールに必要です。 |
| `remoteCommand` | 登録されているすべてのリモートコマンドの配列を返します |
| `remoteHTTPCommandDisabled` | `true` の場合、組み込みのリモート HTTP コマンドを無効にします |
| `rootView` | `WKWebView` のアタッチ先となる現在の `UIView` を構成します |
| `searchAdsEnabled` | Attribution モジュールの Apple Search Ads API を有効または無効にします |
| `shouldAddCookieObserver` | Tealium が `WKWebView` Cookie Observer を追加するかどうかを指定します |
| `shouldUseRemotePublishSettings` | Mobile Publish Settings を構成します（デフォルト：有効） |
| `tagManagementOverrideURL` | Tag Management モジュールが使用するデフォルト URL をオーバーライドします |
| `TealiumConfig()` | `TealiumConfig` オブジェクトのコンストラクター |
| `updateDistance` | 位置情報の更新を受信する距離間隔（メートル）を構成します |
| `useHighAccuracy` | 位置情報の精度を低精度（デフォルト）または高精度に構成します |

### `addDelegate()`

TealiumDelegate プロトコルに準拠する新しいデリゲートを追加します。

```swift
addDelegate(delegate)
```

| パラメータ | 型 | 説明 |
|-------------|---------|---------------------------------------------------|
| `delegate` | `TealiumDelegate` | TealiumDelegate プロトコルに準拠するクラス |

次の例では、現在のモジュールが `TealiumDelegate` プロトコルを実装していることを前提としています。

```swift
config.addDelegate(self)
```

### `addRemoteCommand()`

後で実行するリモートコマンドを追加します。

```swift
addRemoteCommand(command)
```

| パラメータ | 型 | 説明 |
|-------------|---------|---------------------------------------------------|
| `command` | `TealiumRemoteCommand` | 追加する TealiumRemoteCommand のインスタンス |

次の例は Tealium の初期化前に配置し、リモートコマンドを追加する方法を示しています。

```swift
#if os(iOS)
let remoteCommand = TealiumRemoteCommand(commandId: "test",
        description: "test") { response in
			print("Remote Command 'test' executed")
}
config.addRemoteCommand(remoteCommand)
#endif
```

### `batchingBypassKeys`

バッチ処理をバイパスする（個別のイベントとして送信する）イベント名のリストを構成します。

```swift
config.batchingBypassKeys = ["home_screen"]
```

### `batchingEnabled`

イベントのバッチ処理を有効（`true`）または無効（`false`）にします。デフォルトでは無効です。

```swift
config.batchingEnabled = true
```

### `batchSize`

1回のバッチリクエストにまとめるイベント数を構成します。最大値は10です。

```swift
config.batchSize = 8
```

### `collectOverrideProfile`

Tealium Collect プロファイルをオーバーライドし、別の Tealium プロファイルにデータを送信します。

```swift
config.collectOverrideProfile = "main"
```

### `collectOverrideURL`

Tealium Collect URL をオーバーライドし、別のエンドポイントにデータを送信します。

```swift
config.collectOverrideURL = url
```

| プロパティ値 | 型 | 説明 |
| --- | --- | --- |
| `url` | `String` | オーバーライドする URL |

デフォルトの URL：  
```bash
https://collect.tealiumiq.com/event/
```

イベントのバッチ処理を使用する場合のデフォルト URL：  
```bash
https://collect.tealiumiq.com/bulk-event/
```

通常、このメソッドはカスタムホスト名または特定のリージョンのホスト名を構成するために使用します。次の例では、データを EU Central リージョン内に保持するように Tealium Collect のベース URL を構成します。

```swift
let url = "https://collect-eu-central-1.tealiumiq.com/event/"
config.collectOverrideURL = url
```

### `connectivityRefreshEnabled`

有効（デフォルト）の場合、接続モジュールは指定された間隔（`setConnectivityRefreshInterval` で制御）で接続を確認します。接続が再開されると、キューに格納されたディスパッチが直ちに送信されます。

```swift
config.connectivityRefreshEnabled = true
```

### `connectivityRefreshInterval`

デフォルトの接続更新間隔を秒単位で構成します。TealiumConfig インスタンスで構成されていない場合、デフォルトは30秒です。

```swift
config.connectivityRefreshInterval = 30
```

### `consentLoggingEnabled`

[同意ログ](https://docs.tealium.com/consent-change-event-specifications/)機能を有効にします。この機能は、監査のためにすべての同意ステータスの変更を Tealium Customer Data Hub に送信します。

```swift
config.consentLoggingEnabled = true
```

### `delegates`

有効なデリゲートの配列を返します。

次の例は、有効なデリゲートの配列を取得する方法を示しています。

```swift
let delegates = config.delegates
```

### `dispatchAfter`

キューを自動的にフラッシュするイベント数です。

```swift
config.dispatchAfter = 20
```

### `dispatchExpiration`

ディスパッチの有効期限を日数で構成します。デバイスが長期間オフラインの場合、古いイベントは削除されます。

```swift
config.dispatchExpiration = 5
```

### `dispatchQueueLimit`

イベントキューに保存するイベントの最大数を構成します。この数に達してもキューがフラッシュされていない場合、最も古いイベントが削除されます。

```swift
config.dispatchQueueLimit = 50
```

### `enableRemoteHTTPCommand()`

組み込みのリモート HTTP コマンドを有効にします（[Swift モジュール：RemoteCommands](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/remote-commands/)を参照）。

```swift
enableRemoteHTTPCommand()
```

### `existingVisitorId`

アプリ拡張機能でファーストパーティ ID として使用する既存の訪問 ID を構成します。

```swift
config.existingVisitorId = id
```
### `geofenceFileName`

ローカルのジオフェンスファイルアセットの名前を構成します。ファイル拡張子は含めないでください。

```swift
config.geofenceFileName = <String>
```

| 型 | 説明 | 例 |
| --- | --- | --- |
| `String` | JSONファイル名 | `"geofences"` |

### `geofenceUrl`

ホストされているジオフェンスファイルのURLを構成します。

```swift
config.geofenceUrl = <String (url)>
```

| 型 | 説明 | 例 |
 --- | --- | --- |
| `String` | ジオフェンスファイルのURL | `"https://example.com/.../geofences.json"` |

### `initialUserConsentCategories`

ライブラリが初めて起動するときのユーザーの初期同意カテゴリーを構成します。保存済みの構成がある場合は、構成オブジェクトで渡された構成よりも保存済みの構成が優先されます。同意ステータスを `.consented` に構成します。

```swift
config.initialUserConsentCategories = [.cdp, .analytics]
```

### `initialUserConsentStatus`

ユーザーの初期同意ステータスを構成します。この構成は、ライブラリが初めて起動するときにユーザーに適用されます。保存済みの構成がある場合は、構成オブジェクトで渡された構成よりも保存済みの構成が優先されます。

ステータスが `.consented` の場合、同意済みカテゴリーのリストに利用可能なすべての同意カテゴリーを含めるよう構成します。カテゴリーを個別に選択して構成することはできません。

同意が付与される前のイベントをキューに入れるデフォルトの動作を上書きし、同意前に追跡されたすべてのイベントを無視するには、このメソッドを使用します。構成オブジェクトに次の行を追加します。

```swift
config.initialUserConsentStatus = .notConsented
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `status` | `TealiumConsentStatus` | TealiumConsentStatus列挙型の値 | [`.unknown`, `.consented`, `.notConsented`] |

以下は、`TealiumConsentStatus`列挙型の各Tealium同意ステータスを定義しています。

**.unknown**  
`unknown`ステータスは、同意マネージャーのデフォルト構成です。この状態では、明示的な`consented`または`notConsented`ステータスが指定されるまで、同意マネージャーはイベントをローカルでキューに入れます。

**.consented**  
`consented`ステータスは、ユーザーがトラッキングに同意した場合に構成されます。この状態では、同意マネージャーはすべてのトラッキング呼び出しを通常どおり続行できます。

**.notConsented**  
`notConsented`ステータスは、ユーザーがトラッキングを拒否した場合に構成されます。この状態では、同意マネージャーはすべてのトラッキング呼び出しを破棄し、SDKによる以降の処理を停止します。

### `logLevel`

新しいログレベルを構成します（[Swiftモジュール：Logger](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/logger/)を参照）。

次の例は、ログレベルを`errors`に構成する方法を示しています。

```swift
let newLogLevel = TealiumLogLevel.errors
config.logLevel = newLogLevel
```

### `memoryReportingEnabled`

DeviceDataモジュールのメモリレポートを有効または無効にします（デフォルト：無効）。

```swift
config.memoryReportingEnabled = true
```

### `modulesList`

新しいモジュールリストを構成します（[モジュールリスト](https://docs.tealium.com/ja/platforms/ios-swift-v1/modules/)を参照）。

次の例は、autotrackingモジュールをブラックリストに登録する方法を示しています。

```swift
let modulesList = TealiumModulesList(isWhitelist: false, moduleNames: ["autotracking"])
config.modulesList = list
```

TealiumModulesListの`struct`には、次のパラメータがあります。

| パラメータ | 型 | 説明 | 例 |
|------------|---------|---------------------------------------------------| ------- |
| `isWhiteList` | `Bool` | モジュールリストがブラックリスト（`false`）かホワイトリスト（`true`）かを指定します | `moduleNames: ["autotracking"] ` |
| `modulesList` | `[String]` | 有効または無効にするモジュール名の配列 | [`"true"`, `"false"`] |

### `overrideConsentPolicy`

デフォルトの同意`policy`パラメータを上書きします（デフォルト：`"gdpr"`）。

```swift
let policy = "ccpa"
config.overrideConsentPolicy = policy
```

### `remoteAPIEnabled`

`remote_api`イベントを有効（`true`）または無効（`false`）にします。DispatchQueueモジュールを使用している場合、RemoteCommandsモジュールに必要です。デフォルトは`false`です。

```swift
config.remoteAPIEnabled = true
```

### `remoteCommands`

登録されているすべてのリモートコマンドの配列を返します。

次の例は、登録されているすべてのリモートコマンドの配列を取得する方法を示しています。

```swift
let remoteCommands = config.remoteCommands
```

### `remoteHTTPCommandDisabled`

組み込みのリモートHTTPコマンドを無効にします（[Swiftモジュール：RemoteCommands](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/remote-commands/)を参照）。

```swift
config.remoteHTTPCommandDisabled = true
```

### `rootView`

`WKWebView`をアタッチする現在の`UIView`を構成します。プッシュ通知を使用する場合など、複雑なビュー階層によって自動検出に失敗する可能性がある場合にのみ必要です。

```swift
let view = self.view
config.rootView = view
```

### `searchAdsEnabled`

DeviceDataモジュールのメモリレポートを有効または無効にします（デフォルト：無効）。

```swift
config.searchAdsEnabled = true
```

### `shouldAddCookieObserver`

`true`（デフォルト）に構成すると、このメソッドは、すべてのCookieを正常に移行するためにCookieオブザーバーを追加する必要があるかどうかを決定します。`false`に構成した場合、複数のCookieオブザーバーが存在すると、そのうち1つだけが呼び出されるため、一部のCookieが移行されない可能性があります。

```swift
config.shouldAddCookieObserver = false
```


<blockquote>
[`shouldAddCookieObserver`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-config/#shouldaddcookieobserver)プロパティを使用すると、Cookieの同期中に独自のCookieオブザーバーを使用できます。この場合、Cookieを構成した後、メインスレッドでCookieを取得するためのCookieオブザーバーが必要です。この問題は`WKWebView`のバグによって発生し、独自のオブザーバーが呼び出されなくなります。
</blockquote>
  

### `shouldUseRemotePublishSettings`

[モバイルパブリッシュ構成](https://docs.tealium.com/create-mobile-profile/)（バージョン1.9.0以降）を有効（デフォルト）または無効に構成します。

```Swift
config.shouldUseRemotePublishSettings = false
```


<blockquote>
バージョン1.9.0以降では、モバイルパブリッシュ構成がデフォルトで有効になっているため、使用しない場合は無効にする必要があります。タグ管理でモバイルパブリッシュ構成を構成するか、Swiftのインストール構成で`config.shouldUseRemotePublishSettings = false`を使用して無効にしてください。これを行わないと、初期化に失敗し、トラッキングできなくなります。
</blockquote>


### `tagManagementOverrideURL`

タグ管理モジュールが使用するデフォルトURLを上書きします。Tealium JavaScriptファイルをセルフホスティングする場合に必要です。

次の例は、タグ管理モジュールが使用するデフォルトURLを上書きする方法を示しています。

```swift
let url = "https://tags.mycdn.com/utag/myaccount/myprofile/myenv/mobile.html"
config.tagManagementOverrideURL =  url
```

### `TealiumConfig()`

`TealiumConfig`オブジェクトのコンストラクターです。このオブジェクトは、特定のアカウント用にライブラリを初期化するために必要です。

```swift
TealiumConfig(account:String, profile:String, environment:String, optionalData:Dictionary, dataSource:String)
```

| パラメータ | 型 | 説明 | 例 |
|---------------|-----------|--------------------------------------------------| ------- |
| `account` | `String` | Tealiumアカウント名 | `"companyXYZ"` |
| `profile` | `String` | Tealiumプロファイル名 | `"main"` |
| `environment` | `String` | Tealium環境名 | [`"dev"`, `"qa"`, `"prod"`] |
| `datasource` | `String` | （任意）CDHのTealiumデータソースキー | `"abc123"` |
### `updateDistance`

位置情報の更新を受信する距離間隔（メートル）を構成します。


<blockquote>
このメソッドは、`useHighAccuracy`が`true`に構成されている場合にのみ使用してください。
</blockquote>



```swift
config.updateDistance = <Double>
```

| 型 | 説明 | 例 |
| --- | --- | --- |
| `Double` | 位置情報の更新を受信する距離間隔（メートル） | `150.0` |

使用例：

```swift
func start() {
      let config = TealiumConfig(account: "ACCOUNT",
                                 profile: "NAME",
                                 environment: "ENVIRONMENT",
                                 datasource: "DATASOURCE",
                                 optionalData: nil)
      // Tealium Location module config methods
      config.useHighAccuracy = true
      config.updateDistance = 150.0
  }
```

### `useHighAccuracy`

位置情報の精度を低精度（デフォルト）または高精度に構成します。

このプロパティはデフォルトで無効（`false`）になっており、位置情報の精度は低精度に構成されます。位置情報が有効になっているデバイスが500メートル以上移動すると、位置情報の大幅な変化と見なされ、位置情報が更新されます。この構成では通常、位置情報の更新に5分以上かかります。

詳しくは、[Appleの大幅変更位置情報サービス](https://developer.apple.com/documentation/corelocation/getting_the_user_s_location/using_the_significant-change_location_service)を参照してください。

有効（`true`）にすると、位置データの精度が可能な限り高い精度に構成されます。最初のイベントは可能な限り迅速に配信され、その後も位置情報の特定を継続し、必要に応じてデータが利用可能になった時点で追加のイベントを配信します。

詳しくは、[Appleの位置データの精度](https://developer.apple.com/documentation/corelocation/cllocationmanager/1423836-desiredaccuracy?language=swift)を参照してください。

高精度を使用すると、位置情報の更新頻度が高くなるため、低精度の場合よりもデバイスのバッテリー消費量が増加します。

```swift
config.useHighAccuracy = <Bool>
```

| 型 | 説明 | 例 |
| --- | --- | --- |
| `Boolean` | 位置データの精度を構成します | `true` |


使用例：

```swift
func start() {
      let config = TealiumConfig(account: "ACCOUNT",
                                 profile: "NAME",
                                 environment: "ENVIRONMENT",
                                 datasource: "DATASOURCE",
                                 optionalData: nil)
      // Tealium Location module config methods
      config.useHighAccuracy = true
      config.updateDistance = 150.0
  }
```