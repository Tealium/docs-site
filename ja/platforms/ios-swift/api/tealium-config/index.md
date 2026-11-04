---
title: TealiumConfig
description: メインの Tealium クラスの構成オプションを構成するためのクラスです。有効になっている各モジュールは、TealiumConfig クラス用の独自の拡張機能を提供します。
url: https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/
---## クラス：`TealiumConfig`

以下は、iOS（Swift）の `TealiumConfig` クラスで一般的に使用されるメソッドとプロパティの概要です。

| メソッド／プロパティ | 説明 |
| ----- | ------ |
| [`addRemoteCommand()`](#addremotecommand) | 後で実行するリモートコマンドを追加します |
| [`adobeVisitorAuthState`](#adobevisitorauthstate) | 訪問の現在の認証状態を構成します。 |
| [`adobeVisitorCustomVisitorId`](#adobevisitorcustomvisitorid) | 初期化時に既知である場合、既知の訪問 ID を Adobe ECID に構成します。今後 ECID が変更された場合は、`linkECIDToKnownIdentifier` を呼び出して訪問 ID を更新します。 |
| [`adobeVisitorDataProviderId`](#adobevisitordataproviderid) | ECID を既知の ID にリンクする際に必要となる、Adobe から提供されたデータプロバイダー ID を構成します。 |
| [`adobeVisitorExistingEcid`](#adobevisitorexistingecid) | 新しい ECID を要求する代わりに使用する、Adobe SDK などの以前のインストールから取得した既存の ECID を構成します。 |
| [`adobeVisitorOrgId`](#adobevisitororgid) | `@` 部分を含む Adobe 組織 ID の文字列です。 |
| [`adobeVisitorRetries`](#adobevisitorretries) | リクエストが失敗するまでに許容される、無効な訪問 ID に対する再試行回数です。リクエストが失敗した場合でも、ECID なしでトラッキング呼び出しが送信されます。 |
| [`appDelegateProxyEnabled`](#appDelegateProxyEnabled) | Tealium AppDelegate プロキシを有効（デフォルト）または無効にします |
| [`autoTrackingBlocklistFilename`](#autotrackingblocklistfilename) | ローカルブロックリストファイルの名前を構成します。 |
| [`autoTrackingBlocklistURL`](#autotrackingblocklisturl) | リモートブロックリストファイルの URL を構成します。 |
| [`autoTrackingCollectorDelegate`](#autotrackingcollectordelegate) | 自動的にトラッキングされるビューに対して実行されるグローバルデリゲートを構成します。 |
| [`batchingBypassKeys`](#batchingbypasskeys) | バッチ処理をバイパスする（個別のイベントとして送信する）イベント名のリストを構成します |
| [`batchingEnabled`](#batchingenabled) | イベントのバッチ処理を有効または無効（デフォルト）にします |
| [`batchSize`](#batchsize) | 1 回のバッチリクエストにまとめるイベント数を構成します（最大：10） |
| [`batteryReportingEnabled`](#batteryreportingenabled) | DeviceData モジュールでのバッテリー情報のレポートを有効または無効にします |
| [`connectivityRefreshEnabled`](#connectivityrefreshenabled) | 有効（デフォルト）の場合、Connectivity モジュールは指定された間隔で接続を確認します |
| [`connectivityRefreshInterval`](#connectivityrefreshinterval) | デフォルトの接続状態更新間隔を秒単位で構成します |
| [`consentExpiry`](#consentexpiry) | ユーザーによる同意選択の有効期限を構成します |
| [`consentLoggingEnabled`](#consentloggingenabled) | 同意ログ機能を有効または無効にします |
| [`consentPolicy`](#consentpolicy) | [同意ポリシー](https://docs.tealium.com/ja/platforms/ios-swift/consent-management/#set-policy)を構成します（デフォルトは GDPR） |
| [`deepLinkTrackingEnabled`](#deeplinktrackingenabled) | ディープリンクの自動トラッキングを有効または無効にします |
| [`desiredAccuracy`](#desiredaccuracy) | アプリが受信する位置情報データの精度です |
| [`diskStorageDirectory`](#diskstoragedirectory) | ディスク保存に使用するディレクトリを構成します。デフォルトは `.caches` です。 |
| [`dispatchAfter`](#dispatchafter) | キューをフラッシュするまでのイベント数を構成します |
| [`dispatchExpiration`](#dispatchexpiration) | バッチの有効期限を日数で構成します。デバイスが長期間オフラインの場合、古いイベントは削除されます |
| [`dispatchQueueLimit`](#dispatchqueuelimit) | キューに保持できるイベントの最大数を構成します。この数に達してもキューがフラッシュされていない場合、最も古いイベントが削除されます。 |
| [`dispatchListeners`](#dispatchlisteners) | ディスパッチ直前のトラッキング呼び出しを監視するために、カスタム `DispatchListener` を追加するオプションを提供します |
| [`dispatchValidators`](#dispatchvalidators) | イベントをディスパッチ、キューイング、または破棄するかどうかを制御するために、カスタム `DispatchValidator` を追加するオプションを提供します |
| [`enableBackgroundLocation`](#enablebackgroundlocation) | アプリがバックグラウンドで実行されている間も位置情報の更新を有効にします |
| [`existingVisitorId`](#existingvisitorid) | アプリ拡張機能でファーストパーティ ID として使用する既存の訪問 ID を構成します |
| [`geofenceFileName`](#geofencefilename) | ローカルのジオフェンス JSON ファイルアセットの名前を構成します。_ファイル拡張子は含めないでください。_ |
| [`geofenceTrackingEnabled`](#geofencetrackingenabled) | ジオフェンストラッキングを無効または有効にします |
| [`geofenceUrl`](#geofenceurl) | ホストされている JSON ファイルの URL を構成します |
| [`hostedDataLayerExpiry`](#hosteddatalayerexpiry) | ホスト型データレイヤーのデータに有効期限を構成します |
| [`hostedDataLayerKeys`](#hosteddatalayerkeys) | ホスト型データレイヤーモジュールがデータレイヤー ID を検索するときに使用するイベントマッピングを構成します |
| [`isCollectEnabled`](#iscollectenabled) | Collect ディスパッチャーを無効にするオプションを提供します |
| [`lifecycleAutoTrackingEnabled`](#lifecycleautotrackingenabled) | ライフサイクルの自動トラッキングを有効または無効にします。デフォルトは `true` です。`false` に構成し、ライフサイクルの起動／スリープ／ウェイクイベントが必要な場合は、`LifecycleModule` のパブリックメソッドを使用して手動で呼び出す必要があります |
| [`logger`](#logger) | 現在の `TealiumLogger` を置き換える、`TealiumLoggerProtocol` に準拠したカスタムロガーを構成します |
| [`logLevel`](#loglevel) | ログに記録される情報量を制御するログレベルプロパティを構成します |
| [`logType`](#logtype) | 新しいログタイプを構成します |
| [`memoryReportingEnabled`](#memoryreportingenabled) | DeviceData モジュールでのメモリ情報のレポートを有効または無効にします |
| [`minimumFreeDiskSpace`](#minimumfreediskspace) | ディスク保存を有効にするために必要な最小空きディスク容量をメガバイト単位で構成します |
| [`minutesBetweenRefresh`](#minutesbetweenrefresh) | パブリッシュ構成を取得する頻度を決定します |
| [`onConsentExpiration`](#onconsentexpiration) | 同意選択の有効期限が切れたときに実行するコールバックです |
| [`overrideCollectProfile`](#overrideCollectProfile) | データを別の Tealium プロファイルに送信するため、Tealium Collect プロファイルをオーバーライドします |
| [`overrideCollectURL`](#overrideCollectURL) | データを別のエンドポイントに送信するため、Tealium Collect URL をオーバーライドします |
| [`overrideCollectBatchURL`](#overrideCollectBatchURL) | データを別のエンドポイントに送信するため、Tealium Collect Batch URL をオーバーライドします |
| [`overrideCollectDomain`](#overrideCollectDomain) | データを別のエンドポイントに送信するため、Tealium Collect ドメイン名をオーバーライドします |
| [`overrideConsentCategoriesKey`](#overrideconsentcategorieskey) | 同意カテゴリのイベント属性名をオーバーライドします。サーバー側で同意をカスタム適用する場合に使用します（デフォルト：`consent_categories`） |
| [`publishSettingsProfile`](#publishsettingsprofile) | パブリッシュ構成プロファイルをオーバーライドします |
| [`publishSettingsURL`](#publishsettingsurl) | パブリッシュ構成 URL をオーバーライドします |
| [`remoteAPIEnabled`](#remoteapienabled) | `remote_api` イベントを有効または無効にします。DispatchQueue モジュールを使用している場合、RemoteCommands モジュールに必要です。 |
| [`remoteCommands`](#remotecommands) | 登録されているすべてのリモートコマンドの配列を返します |
| [`remoteHTTPCommandDisabled`](#remotehttpcommanddisabled) | `true` の場合、組み込みのリモート HTTP コマンドを無効にします |
| [`rootView`](#rootview) | `WKWebView` の接続先となる現在の `UIView` を構成します |
| [`screenReportingEnabled`](#screenreportingenabled) | DeviceData モジュールでの画面情報のレポートを有効または無効にします |
| [`searchAdsEnabled`](#searchadsenabled) | AttributionモジュールのApple Search Ads APIを有効または無効にします |
| [`sendCrashDataOnCrashDetected`](#sendcrashdataoncrashdetected) | クラッシュが検出されたときにクラッシュイベントを送信し、そのイベントにのみクラッシュデータを追加します |
| [`sendDeepLinkEvent`](#senddeeplinkevent) | ディープリンクを受信するたびに、関連データを含む`deep_link`イベントを送信します |
| [`sessionCountingEnabled`](#sessioncountingenabled) | タグ管理アカウントのセッションカウントを無効にします。Tealium JavaScriptファイルをセルフホスティングする場合に使用します |
| [`shouldAddCookieObserver`](#shouldaddcookieobserver) | `WKWebView` Cookieオブザーバーを追加するかどうかを決定します |
| [`shouldUseRemotePublishSettings`](#shoulduseremotepublishsettings) | モバイルパブリッシュ構成を構成します（デフォルト：有効）|
| [`skAdAttributionEnabled`](#skadattributionenabled) | [SKAdNetwork](https://developer.apple.com/documentation/storekit/skadnetwork)フレームワークの使用を有効にします |
| [`skAdConversionKeys`](#skadconversionkeys) | [`SKAdNetwork.updateConversionValue()`](https://developer.apple.com/documentation/storekit/skadnetwork/3566697-updateconversionvalue)メソッドを呼び出すイベントと値を定義します |
| [`tagManagementOverrideURL`](#tagmanagementoverrideurl) | タグ管理モジュールで使用されるデフォルトURLを上書きします |
| [`TealiumConfig()`](#tealiumconfig) | `TealiumConfig`オブジェクトのコンストラクター |
| [`timedEventTriggers`](#timedeventtriggers) | 時間指定イベントを自動的にトラッキングするための`TimedEventTrigger`オブジェクトのリスト |
| [`updateDistance`](#updatedistance)  | 位置情報の更新を受信する距離間隔（メートル）を構成します |
| [`useHighAccuracy`](#usehighaccuracy) | 位置情報の精度を低精度（デフォルト）または高精度に構成します |
| [`visitorIdentityKey`](#visitoridentitykey) | 顧客識別子を表すデータレイヤーキーを指定する構成キーです。[訪問の切り替え](https://docs.tealium.com/ja/platforms/getting-started-mobile/identity-resolution/#visitor-switching)を有効にするために使用できます。 |
| [`webviewProcessPool`](#webviewprocesspool) | アプリにTealiumタグ管理WebView以外のWebViewが含まれている場合に、Cookieの同期に関する問題を防ぎます |
| [`webviewConfig`](#webviewconfig) | Tealiumタグ管理WebViewで使用するカスタム`WKWebviewConfiguration`オブジェクトを渡せるようにします |

### `addRemoteCommand()`

後で実行するリモートコマンドを追加します。

```swift
addRemoteCommand(command)
```

| パラメータ | 型              | 説明                                             |
|:-----------|:----------------|:-------------------------------------------------|
| `command`  | `RemoteCommand` | 追加する`TealiumRemoteCommand`のインスタンス |

次の例は、Tealiumの初期化前にリモートコマンドを追加する方法を示しています。

```swift
#if os(iOS)
let remoteCommand = RemoteCommand(commandId: "test",
        description: "test") { response in
			print("Remote Command 'test' executed")
}
config.addRemoteCommand(remoteCommand)
#endif
```

### `adobeVisitorAuthState`

訪問の現在の認証状態を構成します。

例：

```swift
config.adobeVisitorAuthState = .authenticated
config.adobeVisitorAuthState = .loggedOut
config.adobeVisitorAuthState = .unknown
```

### `adobeVisitorCustomVisitorId`

初期化時に既知である場合、既知の訪問IDをAdobe ECIDに構成します。今後ECIDが変更された場合は、[`linkECIDToKnownIdentifier`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium/#linkecidtoknownidentifier)を呼び出して訪問IDを更新します。

```swift
config.adobeVisitorCustomVisitorId = "20381482060927465156359999806251989655"
```

### `adobeVisitorDataProviderId`

ECIDを既知のIDにリンクするときに必要となる、Adobeから提供されたデータプロバイダーIDを構成します。

```swift
config.adobeVisitorDataProviderId = "01"
```

### `adobeVisitorExistingEcid`

新しいECIDを要求する代わりに、Adobe SDKなどの以前のインストールで使用されていた既存のECIDを構成します。

例：

```swift
config.adobeVisitorExistingEcid = "20381482060927465156359999806251989655"
```

### `adobeVisitorOrgId`

`@`部分を含むAdobe Org IDの文字列です。Org IDが指定されていない場合、モジュールは初期化されず、訪問IDは取得されません。トラッキング呼び出しはAdobe ECIDなしで通常どおり続行されます。

```swift
config.adobeVisitorOrgId = STRING_VALUE
```

例：

```swift
config.adobeVisitorOrgId = "1A2A111A111150AA0A110A12@AdobeOrg"
```

### `adobeVisitorRetries`

リクエストが失敗するまでに許容される、無効な訪問IDに対する再試行回数です。リクエストが失敗した場合でも、トラッキング呼び出しはECIDなしで送信されます。

例：

```swift
config.adobeVisitorRetries = 5
```

### `appDelegateProxyEnabled`

AppDelegateプロキシを有効にし、ディープリンクを自動的にトラッキングして、ディープリンクからTealiumトレースセッションを開始できるようにします。このプロパティはデフォルトで有効化され、`true`に構成されています。無効にするには、プロパティを`false`に構成します。

```swift
config.appDelegateProxyEnabled = false
```

### `autoTrackingBlocklistFilename`

[AutoTrackingモジュール](https://docs.tealium.com/ja/platforms/ios-swift/module-list/autotracking/#block-list)で使用します。

自動トラッキングから除外するビューのリストを含むブロックリストファイルの名前を構成します。このファイルはAndroidの`assets`ディレクトリに配置する必要があります。

```swift
config.autoTrackingBlocklistFilename = "autotracking-blocklist.json"
```

### `autoTrackingBlocklistURL`

[AutoTrackingモジュール](https://docs.tealium.com/ja/platforms/ios-swift/module-list/autotracking/#block-list)で使用します。

自動トラッキングから除外するビューのリストを含む、JSON形式のブロックリストファイルのURLを構成します。

```swift
config.autoTrackingBlocklistUrl = "https://example.com/autotracking-blocklist.json"
```

### `autoTrackingCollectorDelegate`

[AutoTrackingモジュール](https://docs.tealium.com/ja/platforms/ios-swift/module-list/autotracking/)で使用します。

`TealiumConfig`オブジェクトに構成され、[AutoTrackingモジュール](https://docs.tealium.com/ja/platforms/ios-swift/module-list/autotracking/)によってトラッキングされるビューに対して実行されるグローバルデリゲートです。このデリゲートを編集すると、特定のビューに含めるデータをカスタマイズできます。

```swift
config.autoTrackingCollectorDelegate = myCollectorDelegate
```

### `batchingBypassKeys`

バッチ処理を迂回し、個別のイベントとして送信するイベント名のリストを構成します。

```swift
config.batchingBypassKeys = ["home_screen"]
```

### `batchingEnabled`

イベントのバッチ処理を有効または無効にします。デフォルトでは無効です。

```swift
config.batchingEnabled = true
```

### `batchSize`

1回のバッチリクエストにまとめるイベント数を構成します。最大値は10です。

```swift
config.batchSize = 8
```

### `Collectors`

コレクターは、デバイスから補足情報を収集し、その情報がTealium Customer Data Hubに送信される前にデータレイヤーへ追加するモジュールです。一部のコレクターはコアライブラリに含まれていますが、その他はオプションであり、個別のモジュールとしてインストールします。

次の表に、利用可能なコレクターを示します。デフォルトのコレクターには、コレクター名の横に`*`が付いています。

| コレクター名    | TealiumConfigリファレンス |
|:----------------|:--------------------------|
| `AdobeVisitor`  | `Collectors.AdobeVisitor` |
| `AppData`*      | `Collectors.AppData`      |
| `Connectivity`* | `Collectors.Connectivity` |
| `Device`        | `Collectors.Device`       |
| `Lifecycle`     | `Collectors.Lifecycle`    |

これらのモジュールは、[`TealiumConfig`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/)の`collectors`プロパティを使用して有効または無効にします。

次の例では、使用中の既存のコレクターリストにコレクターを追加します。

```swift
config.collectors = [Collectors.AdobeVisitor]
```

### `connectivityRefreshEnabled`

有効な場合（デフォルト）、Connectivityモジュールは指定された間隔（`setConnectivityRefreshInterval`で制御）で接続を確認します。接続が回復すると、キューに入れられたディスパッチが直ちに送信されます。

```swift
config.connectivityRefreshEnabled = true
```

### `connectivityRefreshInterval`

デフォルトの接続更新間隔を秒単位で構成します。TealiumConfigインスタンスで構成されていない場合、デフォルトは30秒です。

```swift
config.connectivityRefreshInterval = 30
```
### `consentExpiry`

ユーザーの同意に関する選択の有効期限を構成します。Tealium の初期化時にこのプロパティを構成します。同意に関する選択のデフォルトの有効期限は次のとおりです。

- CCPA：395 日
- GDPR：365 日  

次の例では、同意の有効期限を 90 日に構成します。

```swift
config.consentExpiry = (90, .days)
```

### `consentLoggingEnabled`

[同意ログ](https://docs.tealium.com/consent-change-event-specifications/)機能を有効にします。この機能は、監査のために同意ステータスのすべての変更を Tealium Customer Data Hub に送信します。

```swift
config.consentLoggingEnabled = true
```

### `consentPolicy`

[同意ポリシー](https://docs.tealium.com/ja/platforms/ios-swift/consent-management/#set-policy)を構成します。同意マネージャーは、このプロパティが構成されている場合にのみ有効になります。

```swift
config.consentPolicy = .ccpa
```

### `deepLinkTrackingEnabled`

Facebook やその他のソースからアプリへのリンクなど、標準的なディープリンクおよび QR トレースの自動トラッキングを有効または無効にします。デフォルトでは有効です。

```swift
config.deepLinkTrackingEnabled = true
```

### `desiredAccuracy`

アプリが受信する位置データの精度です。

```swift
config.desiredAccuracy = .best
```

使用可能な `desiredAccuracy` オプションは次のとおりです。

| `desiredAccuracy` オプション | 説明 |
|:-------------------------|:-------------------------------------------------------------------------------------------------------------|
| `.bestForNavigation`     | 常に正確な位置情報を必要とするナビゲーションアプリでの使用を想定した精度レベル |
| `.best`                  | 非常に高い精度。ただし、ナビゲーションアプリで必要とされる精度レベルまでは不要 |
| `.nearestTenMeters`      | 10 メートル単位の精度 |
| `.nearestHundredMeters`  | 100 メートル単位の精度 |
| `.reduced`               | 1～20 キロメートル以内の精度 |
| `.withinOneKilometer`    | 1 キロメートル単位の精度 |
| `.withinThreeKilometers` | 3 キロメートル単位の精度 |

Apple の[目的の精度に関する定数](https://developer.apple.com/documentation/corelocation/cllocationaccuracy)の詳細をご覧ください。

### `diskStorageDirectory`

ディスク保存に使用するディレクトリを構成します。デフォルトは `.caches` です。

```swift
config.diskStorageDirectory = .documents
```

### `dispatchListeners`

ディスパッチ直前のトラッキング呼び出しをリッスンするために、カスタム `DispatchListener` を追加するオプションを提供します。

```swift
config.dispatchListeners = [self]
```

### `dispatchValidators`

イベントをディスパッチするか、キューに追加するか、破棄するかを制御するために、カスタム `DispatchValidator` を追加するオプションを提供します。

```swift
config.dispatchValidators = [self]
```

### `dispatchAfter`

キューを自動的にフラッシュするまでのイベント数です。

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

### `enableBackgroundLocation`

アプリがバックグラウンドで実行されている間の位置情報更新を有効にします。

```swift
config.enableBackgroundLocation = true
```

### `existingVisitorId`

既存の訪問 ID を構成します。この ID はアプリ拡張機能でファーストパーティ ID として使用されます。|

```swift
config.existingVisitorId = id
```

### `geofenceFileName`

ローカルのジオフェンスファイルアセットの名前を構成します。ファイル拡張子は含めないでください。

```swift
config.geofenceFileName = <String>
```

| 型       | 説明                | 例               |
|:---------|:-------------------|:-----------------|
| `String` | JSON ファイル名 | `geofences` |

### `geofenceTrackingEnabled`

ジオフェンストラッキングを無効または有効にします。

```swift
config.geofenceTrackingEnabled = false
```

| 型       | 説明                | 例               |
|:---------|:-------------------|:-----------------|
| `Bool` | ジオフェンシングを有効にするかどうかを示すブール値 | `false` |

### `geofenceUrl`

ホストされているジオフェンスファイルの URL を構成します。

```swift
config.geofenceUrl = <String (url)>
```

| 型       | 説明                        | 例                                       |
|:---------|:----------------------------|:-----------------------------------------|
| `String` | ジオフェンスファイルの URL | `https://example.com/.../geofences.json` |

### `hostedDataLayerExpiry`

ホスト型データレイヤーのデータに有効期限を構成します。このプロパティが構成されていない場合、ホスト型データレイヤーの項目はデフォルトで 7 日間保持され、この期間が終了すると再度ダウンロードされます。

```swift
config.hostedDataLayerExpiry = (1, unit: .minutes)
```


<blockquote>
有効期限を短くするとネットワークリクエストが増加するため、モバイルデバイスのバッテリー持続時間が短くなります。
</blockquote>


### `hostedDataLayerKeys`

ホスト型データレイヤーモジュールがデータレイヤー ID を取得するときに使用する、ホスト型データレイヤーキー（ルックアップ変数）を構成します。

```swift
config.hostedDataLayerKeys = ["product_view" : "product_id"]
```

### `isCollectEnabled`

Collect ディスパッチャーを無効にするオプションを提供します。主にリモートパブリッシュ構成での使用を目的としています。

```swift
config.isCollectEnabled = false
```

### `lifecycleAutoTrackingEnabled`

ライフサイクルの自動トラッキングを有効または無効にします。デフォルトは `true` です。`false` に構成した場合にライフサイクルの起動、スリープ、ウェイクイベントが必要であれば、`LifecycleModule` のパブリックメソッドを使用して手動で呼び出す必要があります。

```swift
config.lifecycleTrackingEnabled = false
```

### `logger`

現在の `TealiumLogger` を置き換える、`TealiumLoggerProtocol` に準拠したカスタムロガーを構成します。

次の例は、カスタムロガーを config オブジェクトに構成する方法を示しています。

```swift
class CustomLogger: TealiumLoggerProtocol {
	// ... conforming to the TealiumLoggerProtocol
	// plus your own custom methods
}

class TealiumHelper {
	let config = TealiumConfig(...)
	var tealium: Tealium?
	let customLogger = CustomLogger()

	// ...

	private init() {
		config.logger = customLogger
		// ...
		tealium = Tealium(config: config)
	}
}
```

### `logLevel`

ログに記録する情報量を制御するログレベルプロパティを、次のいずれかの値に構成します。

| ログレベル | ログアクティビティの説明 |
|:----------|:-----------------------------------------------------------------------------------------------|
| `.debug`  | アプリケーションのデバッグに使用されるデバッグレベルのイベント（開発環境に推奨） |
| `.info`   | アプリケーションの進行状況を示す情報イベント |
| `.error`  | 重大なエラーや障害などのエラーイベント |
| `.fault`  | システムレベルまたはマルチプロセスのエラーなどの障害または重大なイベント |
| `.silent` | ログを記録しない |

```swift
config.logLevel = .debug
```


<blockquote>
開発ログは Xcode コンソールまたは Mac のコンソールアプリで確認できます。本番ログは、iOS デバイスを接続してコンソールアプリで確認できます。
</blockquote>


### `logType`

新しいロガータイプを構成します。デフォルトは `.os` または [`OSLog`](https://developer.apple.com/documentation/os/oslog) です。

次の例は、ログタイプを `print` に構成する方法を示しています。

```swift
config.logType = .print
```

### `memoryReportingEnabled`

DeviceData モジュールでのメモリレポートを有効または無効にします（デフォルト：無効）。

```swift
config.memoryReportingEnabled = true
```
### `batteryReportingEnabled`

DeviceData モジュールでバッテリーレポートを有効または無効にします（デフォルト：有効）。

```swift
config.batteryReportingEnabled = true
```


### `screenReportingEnabled`

DeviceData モジュールで画面レポートを有効または無効にします（デフォルト：有効）。

```swift
config.screenReportingEnabled = true
```

### `minimumFreeDiskSpace`

ディスク保存を有効にするために必要な最小空きディスク容量をメガバイト単位で構成します。

```swift
config.minimumFreeDiskSpace = 25
```

### `minutesBetweenRefresh`

パブリッシュ構成を取得する頻度を指定します。

```swift
config.minutesBetweenRefresh = 15
```

### `onConsentExpiration`

同意の選択内容が期限切れになったときに実行するコールバックです。

```swift
config.onConsentExpiration = {
	// display consent modal
}
```

### `overrideCollectProfile`

Tealium Collect プロファイルを上書きし、別の Tealium プロファイルにデータを送信します。

```swift
config.overrideCollectProfile = "main"
```

### `overrideCollectURL`

Tealium Collect URL を上書きし、別のエンドポイントにデータを送信します。イベントバッチ機能を使用する場合は、[overrideCollectBatchURL](#overrideCollectBatchURL) プロパティも上書きしてください。

```swift
config.overrideCollectURL = url
```

| プロパティ値 | 型       | 説明                 |
|:-------------|:---------|:---------------------|
| `url`        | `String` | 上書きに使用する URL |

デフォルトの URL：  
```bash
https://collect.tealiumiq.com/event/
```

このプロパティは、カスタムホスト名または特定のリージョンのホスト名を構成するために使用します。次の例では、Tealium Collect のベース URL を EU Central リージョン内に維持するよう構成します。

```swift
let url = "https://collect-eu-central-1.tealiumiq.com/event/"
config.overrideCollectURL = url
```

### `overrideCollectBatchURL`

Tealium Collect のバッチ URL を上書きし、別のエンドポイントにデータを送信します。

```swift
config.overrideCollectBatchURL = url
```

| プロパティ値 | 型       | 説明                 |
|:-------------|:---------|:---------------------|
| `url`        | `String` | 上書きに使用する URL |

イベントバッチ使用時のデフォルト URL：  
```bash
https://collect.tealiumiq.com/bulk-event/
```

このメソッドは通常、カスタムホスト名または特定のリージョンのホスト名を構成するために使用します。次の例では、Tealium Collect のベース URL を EU Central リージョン内に維持するよう構成します。

```swift
let url = "https://collect-eu-central-1.tealiumiq.com/bulk-event/"
config.overrideCollectBatchURL = url
```

### `overrideCollectDomain`

デフォルトの Collect ドメインを上書きします。値には、`my-company.com` のようにプロトコルを除いたホスト名を構成します。このプロパティは、バッチイベントと単一イベントの両方のディスパッチに使用します。`overrideCollectURL` または `overrideCollectBatchURL` が構成されている場合、このプロパティが優先されます。

```swift
config.overrideCollectDomain = "my-company.com"
```

### `overrideConsentCategoriesKey`

同意イベントで送信される同意カテゴリ属性の名前を上書きします。サーバーサイド同意のカスタム適用をサポートする場合に使用します。デフォルト値は `consent_categories` です。

```swift
config.overrideConsentCategoriesKey = "consent_categories_granted"
```

デフォルトの同意イベント：
```
{
    "tealium_event"      : "grant_partial_consent",
    "policy"             : "gdpr",
    "consent_categories" : ["Affiliates", "Social"]
}
```

上書きした同意イベント：
```
{
    "tealium_event"              : "grant_partial_consent",
    "policy"                     : "gdpr",
    "consent_categories_granted" : ["Affiliates", "Social"]
}
```

詳しくは、[サーバーサイド同意の自動適用を無効にする方法](https://docs.tealium.com/server-side-consent-management/)を参照してください。


### `publishSettingsProfile`

パブリッシュ構成のプロファイルを上書きします。

```swift
config.publishSettingsProfile = "main"
```

### `publishSettingsURL`

パブリッシュ構成の URL を上書きします。

```swift
config.publishSettingsURL = "https://www.example.com/custom/publish/settings.html"
```

### `remoteAPIEnabled`

`remote_api` イベントを有効または無効にします。DispatchQueue モジュールを使用している場合、RemoteCommands モジュールに必要です。デフォルトは `false` です。

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
組み込みのリモート HTTP コマンドを無効にします（[Swift モジュール：RemoteCommands](https://docs.tealium.com/ja/platforms/ios-swift/module-list/remote-commands/)を参照）。

```swift
config.remoteHTTPCommandDisabled = true
```

### `rootView`

`WKWebView` のアタッチ先となる現在の `UIView` を構成します。プッシュ通知を使用する場合など、ビュー階層が複雑で自動検出に失敗する可能性がある場合にのみ必要です。

```swift
let view = self.view
config.rootView = view
```

### `searchAdsEnabled`
Attribution モジュールで Apple Search Ads API を有効または無効にします（デフォルト：無効）。

```swift
config.searchAdsEnabled = true
```

### `sendCrashDataOnCrashDetected`
クラッシュが検出されたときにクラッシュイベントを送信し、そのイベントにのみクラッシュデータを追加します（デフォルト：`false`）。

```swift
config.sendCrashDataOnCrashDetected = true
```

### `sendDeepLinkEvent`
ディープリンクを受信するたびに、関連データを含む `deep_link` イベントを送信します（デフォルト：`false`）。

```swift
config.sendDeepLinkEvent = true
```

### `sessionCountingEnabled`
Tag Management アカウントのセッションカウントを無効にします。Tealium JavaScript ファイルをセルフホストしている場合に使用してください（デフォルト：`true`）。

```swift
config.sessionCountingEnabled = false
```

### `shouldAddCookieObserver`

`true`（デフォルト）に構成すると、すべての Cookie を正常に移行するために `WKWebView` Cookie オブザーバーを追加するかどうかを決定します。`false` に構成した場合、複数の Cookie オブザーバーが存在すると、そのうちの1つだけが呼び出されるため、一部の Cookie が移行されない可能性があります。


```swift
config.shouldAddCookieObserver = false
```


<blockquote>
[`shouldAddCookieObserver`](#shouldaddcookieobserver) プロパティを使用すると、Cookie の同期中に独自の Cookie オブザーバーを使用できます。この場合、Cookie の構成後にメインスレッドで Cookie を取得する Cookie オブザーバーが必要です。この問題は `WKWebView` のバグが原因であり、独自のオブザーバーが呼び出されなくなります。
</blockquote>
  

### `shouldUseRemotePublishSettings`

[Mobile Publish Settings](https://docs.tealium.com/create-mobile-profile/)（バージョン1.9.0以降）を有効（デフォルト）または無効に構成します。

```swift
config.shouldUseRemotePublishSettings = false
```


<blockquote>
Mobile Publish Settings はデフォルトで有効になっているため、使用しない場合は無効にする必要があります。Tag Management で Mobile Publish Settings を構成するか、Swift のインストール時に `config.shouldUseRemotePublishSettings = false` を使用してこの機能を無効にしてください。これを行わないと、初期化に失敗し、トラッキングできなくなります。
</blockquote>


### `skAdAttributionEnabled`
Attribution モジュールで Apple SKAdNetwork API を有効または無効にします（デフォルト：無効）。                         

```swift
config.skAdAttributionEnabled = true
```

### `skAdConversionKeys`
`SKAdNetwork.updateConversionValue()` メソッドを呼び出すイベントと、コンバージョン値として使用するキーを定義する辞書です。                         

```swift
config.skAdConversionKeys = ["purchase": "number_of_coins"]
```

この場合、以下のイベントは `SKAdNetwork.updateConversionValue(40)` に相当します。

```swift
tealium?.track("purchase", dataLayer: ["number_of_coins": 40])
```

### `tagManagementOverrideURL`

Tag Management モジュールで使用されるデフォルト URL を上書きします。Tealium JavaScript ファイルをセルフホストしている場合に必要です。

次の例は、Tag Management モジュールで使用されるデフォルト URL を上書きする方法を示しています。

```swift
let url = "https://tags.mycdn.com/utag/myaccount/myprofile/myenv/mobile.html"
config.tagManagementOverrideURL =  url
```
### `TealiumConfig()`

`TealiumConfig` オブジェクトのコンストラクター。このオブジェクトは、特定のアカウント用にライブラリを初期化するために必要です。

```swift
TealiumConfig(account:String, profile:String, environment:String, dataSource:String)
```

| パラメーター | 型       | 説明                                       | 例                    |
|:--------------|:---------|:-------------------------------------------|:----------------------|
| `account`     | `String` | Tealium アカウント名                       | `companyXYZ`          |
| `profile`     | `String` | Tealium プロファイル名                     | `main`                |
| `environment` | `String` | Tealium 環境名                             | [`dev`, `qa`, `prod`] |
| `datasource`  | `String` | （任意）CDH の Tealium データソースキー    | `abc123`              |


### `timedEventTriggers`

時間指定イベントを自動的にトラッキングするための `TimedEventTrigger` オブジェクトのリスト。

```swift
config.timedEventTriggers = [TimedEventTrigger(start: "START_EVENT",
                                               stop: "STOP_EVENT",
                                               name: "TIMED_EVENT_NAME")]
```

`TimedEventTrigger` のパラメーターは次のとおりです。  

| パラメーター | 型        | 説明                                                                       |
|:-------------|:----------|:---------------------------------------------------------------------------|
| `start`      | `String`  | 時間指定イベントを開始する `TealiumEvent` の名前                           |
| `stop`       | `String`  | 時間指定イベントを停止する `TealiumEvent` の名前                           |
| `name`       | `String?` | （任意）時間指定イベントの名前（デフォルト：`"START_EVENT::STOP_EVENT"`）   |


### `updateDistance`

位置情報の更新を受信する距離間隔（メートル）を構成します。


<blockquote>
このメソッドは、`useHighAccuracy` が `true` に構成されている場合にのみ使用してください。
</blockquote>



```swift
config.updateDistance = <Double>
```

| 型       | 説明                                                   | 例      |
|:---------|:-------------------------------------------------------|:--------|
| `Double` | 位置情報の更新を受信する距離間隔（メートル）           | `150.0` |

使用例：

```swift
func start() {
      let config = TealiumConfig(account: "ACCOUNT",
                                 profile: "NAME",
                                 environment: "ENVIRONMENT",
                                 datasource: "DATASOURCE")
      // Tealium Location module config methods
      config.useHighAccuracy = true
      config.updateDistance = 150.0
  }
```

### `useHighAccuracy`

位置情報の精度を低精度（デフォルト）または高精度に構成します。

このプロパティはデフォルトで無効になっており、位置情報の精度は低精度に構成されます。位置情報が有効なデバイスが 500 メートル以上移動すると、位置情報の大幅な変化とみなされ、位置情報が更新されます。この構成では、通常、位置情報の更新に 5 分以上かかります。

詳しくは、[Apple の大幅変更位置情報サービス](https://developer.apple.com/documentation/corelocation/getting_the_user_s_location/using_the_significant-change_location_service)を参照してください。

有効にすると、このプロパティは位置データの精度を可能な限り高く構成します。最初のイベントは可能な限り迅速に配信され、その後も位置情報の特定を継続し、データが利用可能になった時点で必要に応じて追加のイベントを配信します。

詳しくは、[Apple の位置データの精度](https://developer.apple.com/documentation/corelocation/cllocationmanager/1423836-desiredaccuracy?language=swift)を参照してください。

高精度を使用すると位置情報の更新頻度が高くなるため、低精度を使用する場合よりもデバイスのバッテリー消費量が増加します。   

```swift
config.useHighAccuracy = <Bool>
```

| 型        | 説明                         | 例     |
|:----------|:-----------------------------|:-------|
| `Boolean` | 位置データの精度を構成します | `true` |


使用例：

```swift
func start() {
      let config = TealiumConfig(account: "ACCOUNT",
                                 profile: "NAME",
                                 environment: "ENVIRONMENT",
                                 datasource: "DATASOURCE")
      // Tealium Location module config methods
      config.useHighAccuracy = true
      config.updateDistance = 150.0
  }
```

### `visitorIdentityKey`

データレイヤー内で指定された `visitorIdentityKey` に基づく訪問の切り替えを有効にするために使用します。

例：   

```swift
  func start() {
      let customerIdentifierKey = "customer_id"
      let config = TealiumConfig(account: "ACCOUNT",
                                 profile: "NAME",
                                 environment: "ENVIRONMENT",
                                 datasource: "DATASOURCE")
      config.visitorIdentityKey = customerIdentifierKey
      // use the same customerIdentifierKey for storing a specific customer identifier in the data layer
  }
```

### `webviewProcessPool`

アプリに Tealium Tag Management の WebView 以外の WebView が含まれている場合に、Cookie の同期に関する問題を防ぎます。アプリで WebView を使用する場合は、シングルトンの `WKProcessPool` インスタンスを作成して保持し、Tealium をインスタンス化する前に構成してください。

例：   

```swift
let processPool = MyApp.wkProcessPool
config.webviewProcessPool = processPool
```

### `webviewConfig`

Tealium Tag Management の WebView で使用されるカスタム `WKWebviewConfiguration` オブジェクトを渡せるようにします。`webviewProcessPool` オプションの代わりにこのオプションを使用する場合は、カスタマイズ可能な `WKWebviewConfiguration` の `processPool` プロパティを通じて、シングルトンの `WKProcessPool` を構成してください。


<blockquote>
今後 `WKWebView` の API が変更された場合に必要となる可能性があるため、このオプションを使用することを推奨します。
</blockquote>


例：   

```swift
let processPool = MyApp.wkProcessPool
let configuration = WKWebViewConfiguration()
configuration.processPool = processPool
config.webviewConfig = configuration
```