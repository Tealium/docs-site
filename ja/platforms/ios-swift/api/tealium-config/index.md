---
title: TealiumConfig
description: メインのTealiumクラスの構成オプションを構成するためのクラスです。有効になっている場合、個々のモジュールはTealiumConfigクラスのために独自の拡張を提供します。
url: https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/
---## クラス: `TealiumConfig`

以下は、iOS (Swift) の `TealiumConfig` クラスで一般的に使用されるメソッドとプロパティの概要です。

| メソッド/プロパティ | 説明 |
| ----- | ------ |
| [`addRemoteCommand()`](#addremotecommand) | 後で実行するためのリモートコマンドを追加します |
| [`adobeVisitorAuthState`](#adobevisitorauthstate) | 訪問の現在の認証状態を構成します。 |
| [`adobeVisitorCustomVisitorId`](#adobevisitorcustomvisitorid) | 初期化時に既知の場合、Adobe ECIDに既知の訪問IDを構成します。将来ECIDが変更された場合は、`linkECIDToKnownIdentifier`を呼び出して訪問IDを更新してください。 |
| [`adobeVisitorDataProviderId`](#adobevisitordataproviderid) | Adobeから提供されるデータプロバイダーIDを構成します。これは、ECIDを既知のIDにリンクする際に必要です。 |
| [`adobeVisitorExistingEcid`](#adobevisitorexistingecid) | 以前のインストールからの既存のECIDを構成し、新しいECIDを要求する代わりに使用します。 |
| [`adobeVisitorOrgId`](#adobevisitororgid) | `@`部分を含むAdobe Org IDを含む文字列。 |
| [`adobeVisitorRetries`](#adobevisitorretries) | ECIDなしでトラッキングコールが送信される前に、無効な訪問IDのリトライが許可される回数。 |
| [`appDelegateProxyEnabled`](#appDelegateProxyEnabled) | Tealium AppDelegateプロキシを有効にする（デフォルト）または無効にする |
| [`autoTrackingBlocklistFilename`](#autotrackingblocklistfilename) | ローカルブロックリストファイルの名前を構成します。 |
| [`autoTrackingBlocklistURL`](#autotrackingblocklisturl) | リモートブロックリストファイルのURLを構成します。 |
| [`autoTrackingCollectorDelegate`](#autotrackingcollectordelegate) | 自動的に追跡されるビューのために実行されるグローバルデリゲートを構成します。 |
| [`batchingBypassKeys`](#batchingbypasskeys) | バッチ処理がバイパスされる（個別のイベントとして送信される）イベント名のリストを構成します。 |
| [`batchingEnabled`](#batchingenabled) | イベントのバッチ処理を有効または無効にします（デフォルトは無効）。 |
| [`batchSize`](#batchsize) | 単一のバッチリクエストに組み合わせるイベントの量を構成します（最大：10）。 |
| [`batteryReportingEnabled`](#batteryreportingenabled) | DeviceDataモジュールでのバッテリーレポートを有効または無効にします。 |
| [`connectivityRefreshEnabled`](#connectivityrefreshenabled) | 有効にすると（デフォルト）、接続性モジュールは指定された間隔で接続をチェックします。 |
| [`connectivityRefreshInterval`](#connectivityrefreshinterval) | デフォルトの接続性リフレッシュ間隔を秒単位で構成します。 |
| [`consentExpiry`](#consentexpiry) | ユーザーの同意選択の有効期限を構成します。 |
| [`consentLoggingEnabled`](#consentloggingenabled) | 同意ログ機能を有効または無効にします。 |
| [`consentPolicy`](#consentpolicy) | [同意ポリシー](https://docs.tealium.com/ja/platforms/ios-swift/consent-management/#set-policy)を構成します（デフォルトはGDPR）。 |
| [`deepLinkTrackingEnabled`](#deeplinktrackingenabled) | ディープリンクの自動追跡を有効または無効にします。 |
| [`desiredAccuracy`](#desiredaccuracy) | アプリが受け取りたい位置データの精度。 |
| [`diskStorageDirectory`](#diskstoragedirectory) | ディスク保存に使用するディレクトリを構成します。デフォルトは `.caches`。 |
| [`dispatchAfter`](#dispatchafter) | キューがフラッシュされるイベントの数を構成します。 |
| [`dispatchExpiration`](#dispatchexpiration) | バッチの有効期限を日数で構成します。デバイスが長期間オフラインの場合、古いイベントは削除されます。 |
| [`dispatchQueueLimit`](#dispatchqueuelimit) | キューされたイベントの最大数を構成します。この数に達し、キューがフラッシュされていない場合、最も古いイベントが削除されます。 |
| [`dispatchListeners`](#dispatchlisteners) | トラッキングコールのディスパッチ直前にリスニングするカスタム `DispatchListener` を追加するオプションを提供します。 |
| [`dispatchValidators`](#dispatchvalidators) | イベントをディスパッチ、キュー、またはドロップするかどうかを制御するカスタム `DispatchValidator` を追加するオプションを提供します。 |
| [`enableBackgroundLocation`](#enablebackgroundlocation) | アプリがバックグラウンドで実行されている間に位置情報の更新を有効にします。 |
| [`existingVisitorId`](#existingvisitorid) | アプリ拡張で第一者IDとして使用される既存の訪問IDを構成します。 |
| [`geofenceFileName`](#geofencefilename) | ローカルのジオフェンスJSONファイルアセットの名前を構成します。_ファイル拡張子は含めないでください。_ |
| [`geofenceTrackingEnabled`](#geofencetrackingenabled) | ジオフェンス追跡を無効または有効にします。 |
| [`geofenceUrl`](#geofenceurl) | ホストされているJSONファイルのURLを構成します。 |
| [`hostedDataLayerExpiry`](#hosteddatalayerexpiry) | ホストされたデータレイヤーデータの有効期限を構成します。 |
| [`hostedDataLayerKeys`](#hosteddatalayerkeys) | ホストされたデータレイヤーモジュールがデータレイヤーIDを検索する際に使用するイベントマッピングを構成します。 |
| [`isCollectEnabled`](#iscollectenabled) | Collectディスパッチャーを無効にするオプションを提供します。 |
| [`lifecycleAutoTrackingEnabled`](#lifecycleautotrackingenabled) | ライフサイクルの自動追跡を有効または無効にします。デフォルトは `true`です。`false`に構成した場合、ライフサイクルの起動/スリープ/ウェイクイベントが必要な場合は、`LifecycleModule`の公開メソッドを使用して手動で呼び出す必要があります。 |
| [`logger`](#logger) | 現在の `TealiumLogger` を置き換える、`TealiumLoggerProtocol` に準拠したカスタムロガーを構成します。 |
| [`logLevel`](#loglevel) | ログレベルプロパティを構成し、どれだけの情報がログに記録されるかを制御します。 |
| [`logType`](#logtype) | 新しいログタイプを構成します。 |
| [`memoryReportingEnabled`](#memoryreportingenabled) | DeviceDataモジュールでのメモリレポートを有効または無効にします。 |
| [`minimumFreeDiskSpace`](#minimumfreediskspace) | ディスク保存が有効になるための最小限の空きディスクスペースをメガバイト単位で構成します。 |
| [`minutesBetweenRefresh`](#minutesbetweenrefresh) | 公開構成を取得する頻度を決定します。 |
| [`onConsentExpiration`](#onconsentexpiration) | 同意選択が期限切れになった際に実行するコールバック。 |
| [`overrideCollectProfile`](#overrideCollectProfile) | データを異なるTealiumプロファイルに送信するためにTealium Collectプロファイルを上書きします。 |
| [`overrideCollectURL`](#overrideCollectURL) | データを異なるエンドポイントに送信するためにTealium Collect URLを上書きします。 |
| [`overrideCollectBatchURL`](#overrideCollectBatchURL) | データを異なるエンドポイントに送信するためにTealium Collect Batch URLを上書きします。 |
| [`overrideCollectDomain`](#overrideCollectDomain) | データを異なるエンドポイントに送信するためにTealium Collectドメイン名を上書きします。 |
| [`overrideConsentCategoriesKey`](#overrideconsentcategorieskey) | 同意カテゴリイベント属性の名前を上書きします。サーバーサイドの同意のカスタム実施をサポートするために使用します（デフォルト：`consent_categories`）。 |
| [`publishSettingsProfile`](#publishsettingsprofile) | 公開構成プロファイルを上書きします。 |
| [`publishSettingsURL`](#publishsettingsurl) | 公開構成URLを上書きします。 |
| [`remoteAPIEnabled`](#remoteapienabled) | `remote_api`イベントを有効または無効にします。DispatchQueueモジュールが使用されている場合、RemoteCommandsモジュールに必要です。 |
| [`remoteCommands`](#remotecommands) | 登録されているすべてのリモートコマンドの配列を返します。 |
| [`remoteHTTPCommandDisabled`](#remotehttpcommanddisabled) | `true`の場合、組み込みのリモートHTTPコマンドを無効にします。 |
| [`rootView`](#rootview) | `WKWebView`を取り付けるための現在の`UIView`を構成します。 |
| [`screenReportingEnabled`](#screenreportingenabled) | DeviceDataモジュールでのスクリーンレポートを有効または無効にします。
| [`searchAdsEnabled`](#searchadsenabled) | Apple Search Ads APIをAttributionモジュールで有効または無効にします |
| [`sendCrashDataOnCrashDetected`](#sendcrashdataoncrashdetected) | クラッシュが検出されたときにクラッシュイベントを送信し、そのイベントにのみクラッシュデータを追加します |
| [`sendDeepLinkEvent`](#senddeeplinkevent) | ディープリンクが受信されるたびに関連データを含む`deep_link`イベントを送信します |
| [`sessionCountingEnabled`](#sessioncountingenabled) | Tealium iQアカウントのセッションカウントを無効にします。TealiumのJavaScriptファイルを自己ホスティングしている場合はこれを使用してください |
| [`shouldAddCookieObserver`](#shouldaddcookieobserver) | `WKWebView`クッキーオブザーバーを追加するかどうかを決定します |
| [`shouldUseRemotePublishSettings`](#shoulduseremotepublishsettings) | モバイルパブリッシュ構成を構成します（デフォルト：有効）|
| [`skAdAttributionEnabled`](#skadattributionenabled) | [SKAdNetwork](https://developer.apple.com/documentation/storekit/skadnetwork)フレームワークの使用を有効にします |
| [`skAdConversionKeys`](#skadconversionkeys) | [`SKAdNetwork.updateConversionValue()`](https://developer.apple.com/documentation/storekit/skadnetwork/3566697-updateconversionvalue)メソッドを呼び出すイベントと値を定義します |
| [`tagManagementOverrideURL`](#tagmanagementoverrideurl) | タグ管理モジュールで使用されるデフォルトURLを上書きします |
| [`TealiumConfig()`](#tealiumconfig) | `TealiumConfig`オブジェクトのコンストラクタ |
| [`timedEventTriggers`](#timedeventtriggers) | タイムドイベントを自動的に追跡するための`TimedEventTrigger`オブジェクトのリスト |
| [`updateDistance`](#updatedistance)  | 位置情報の更新を受け取る距離間隔（メートル）を構成します |
| [`useHighAccuracy`](#usehighaccuracy) | 位置精度を低精度（デフォルト）または高精度に構成します |
| [`visitorIdentityKey`](#visitoridentitykey) | 顧客識別子を表すデータレイヤーキーを指定する構成キーです。[訪問の切り替え](https://docs.tealium.com/ja/platforms/getting-started-mobile/identity-resolution/#visitor-switching)を有効にするために使用できます |
| [`webviewProcessPool`](#webviewprocesspool) | アプリにTealiumタグ管理ウェブビュー以外のウェブビューが含まれている場合、クッキー同期の問題を防ぎます |
| [`webviewConfig`](#webviewconfig) | カスタム`WKWebviewConfiguration`オブジェクトを許可し、Tealiumタグ管理ウェブビューで使用されます |

### `addRemoteCommand()`

後で実行するためのリモートコマンドを追加します。

```swift
addRemoteCommand(command)
```

| パラメータ | タイプ            | 説明                                      |
|:----------|:----------------|:-------------------------------------------------|
| `command` | `RemoteCommand` | 追加される`TealiumRemoteCommand`のインスタンス |

Tealiumの初期化の前に配置された次の例は、リモートコマンドを追加する方法を示しています：

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

初期化時に既知のAdobe ECIDがある場合、そのECIDを既知の訪問IDに構成します。将来ECIDが変更された場合は、[`linkECIDToKnownIdentifier`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium/#linkecidtoknownidentifier)を呼び出して訪問IDを更新します。

```swift
config.adobeVisitorCustomVisitorId = "20381482060927465156359999806251989655"
```

### `adobeVisitorDataProviderId`

Adobeによって提供されるデータプロバイダーIDを構成します。これは、ECIDを既知のIDにリンクする際に必要です。

```swift
config.adobeVisitorDataProviderId = "01"
```

### `adobeVisitorExistingEcid`

以前のインストールからの既存のECIDを構成し、新しいECIDを要求する代わりに使用します。例えば、Adobe SDKなどです。

例：

```swift
config.adobeVisitorExistingEcid = "20381482060927465156359999806251989655"
```

### `adobeVisitorOrgId`

Adobe Org IDを含む文字列で、`@`部分を含みます。Org IDが提供されていない場合、モジュールは初期化されず、訪問IDは取得されません。Adobe ECIDなしで通常どおりトラッキングコールが続行されます。

```swift
config.adobeVisitorOrgId = STRING_VALUE
```

例：

```swift
config.adobeVisitorOrgId = "1A2A111A111150AA0A110A12@AdobeOrg"
```

### `adobeVisitorRetries`

無効な訪問IDのリトライが許可される回数を構成します。リクエストが失敗すると、ECIDなしでトラッキングコールが送信されます。

例：

```swift
config.adobeVisitorRetries = 5
```

### `appDelegateProxyEnabled`

AppDelegateプロキシを有効にして、自動的にディープリンクトラッキングを開始し、ディープリンクからTealiumトレースセッションを開始します。このプロパティはデフォルトで有効になっており、`true`に構成されています。無効にするには、プロパティを`false`に構成します。

```swift
config.appDelegateProxyEnabled = false
```

### `autoTrackingBlocklistFilename`

[AutoTrackingモジュール](https://docs.tealium.com/ja/platforms/ios-swift/module-list/autotracking/#block-list)で使用します。

自動トラッキングから除外するビューのリストを含むブロックリストファイルの名前を構成します。ファイルはAndroidの`assets`ディレクトリにある必要があります。

```swift
config.autoTrackingBlocklistFilename = "autotracking-blocklist.json"
```

### `autoTrackingBlocklistURL`

[AutoTrackingモジュール](https://docs.tealium.com/ja/platforms/ios-swift/module-list/autotracking/#block-list)で使用します。

自動トラッキングから除外するビューのリストを含むJSON形式のブロックリストファイルへのURLを構成します。

```swift
config.autoTrackingBlocklistUrl = "https://example.com/autotracking-blocklist.json"
```

### `autoTrackingCollectorDelegate`

[AutoTrackingモジュール](https://docs.tealium.com/ja/platforms/ios-swift/module-list/autotracking/)で使用します。

`TealiumConfig`オブジェクトに構成されたグローバルデリゲートで、[AutoTrackingモジュール](https://docs.tealium.com/ja/platforms/ios-swift/module-list/autotracking/)によって追跡されたビューに含まれるデータをカスタマイズするためにこのデリゲートを編集します。

```swift
config.autoTrackingCollectorDelegate = myCollectorDelegate
```

### `batchingBypassKeys`

バッチ処理をバイパスする（個々のイベントとして送信される）イベント名のリストを構成します。

```swift
config.batchingBypassKeys = ["home_screen"]
```

### `batchingEnabled`

イベントバッチ処理を有効または無効にします。デフォルトでは無効です。

```swift
config.batchingEnabled = true
```

### `batchSize`

単一のバッチリクエストに組み合わせるイベントの数を構成します。最大は10です。

```swift
config.batchSize = 8
```

### `Collectors`

コレクターは、デバイスから追加情報を収集し、データレイヤーに追加してからTealium Customer Data Hubに送信するモジュールです。いくつかのコレクターはコアライブラリに含まれており、他のコレクターは別のモジュールとしてオプションでインストールされます。

以下の表は、利用可能なコレクターをリストしています。デフォルトのコレクターはコレクター名の隣に`*`が付けられています。

| コレクター名  | TealiumConfig参照   |
|:----------------|:--------------------------|
| `AdobeVisitor`  | `Collectors.AdobeVisitor` |
| `AppData`*      | `Collectors.AppData`      |
| `Connectivity`* | `Collectors.Connectivity` |
| `Device`        | `Collectors.Device`       |
| `Lifecycle`     | `Collectors.Lifecycle`    |

これらのモジュールは、[`TealiumConfig`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/)の`collectors`プロパティを使用して有効または無効にされます。

次の例は、使用しているコレクターの既存のリストに追加します：

```swift
config.collectors = [Collectors.AdobeVisitor]
```

### `connectivityRefreshEnabled`

有効にすると（デフォルト）、接続性モジュールは指定された間隔（`setConnectivityRefreshInterval`を介して制御）で接続をチェックします。接続が再開されると、キューに入れられたディスパッチが送信されます。

```swift
config.connectivityRefreshEnabled = true
```

### `connectivityRefreshInterval`

秒単位でデフォルトの接続性リフレッシュ間隔を構成します。TealiumConfigインスタンスで構成されていない場合、デフォルトは30秒です。

```swift
config.connectivityRefreshInterval = 30
```
### `consentExpiry`

ユーザーの同意選択の有効期限を構成します。Tealiumを初期化する際にこのプロパティを構成します。同意選択のデフォルトの有効期限は以下の通りです：

- CCPA: 395日
- GDPR: 365日

以下は、同意の有効期限を90日に構成する例です。

```swift
config.consentExpiry = (90, .days)
```

### `consentLoggingEnabled`

[同意ログ記録](https://docs.tealium.com/consent-change-event-specifications/)機能を有効にし、すべての同意ステータス変更を監査目的でTealium Customer Data Hubに送信します。

```swift
config.consentLoggingEnabled = true
```

### `consentPolicy`

[同意ポリシー](https://docs.tealium.com/ja/platforms/ios-swift/consent-management/#set-policy)を構成します。このプロパティが構成されている場合のみ、同意マネージャーが有効になります。

```swift
config.consentPolicy = .ccpa
```

### `deepLinkTrackingEnabled`

標準的なディープリンク（Facebookや他のソースからのアプリへのリンクなど）およびQRトレースの自動追跡を有効または無効にします。デフォルトでは有効になっています。

```swift
config.deepLinkTrackingEnabled = true
```

### `desiredAccuracy`

アプリが受け取りたい位置情報の精度。

```swift
config.desiredAccuracy = .best
```

利用可能な`desiredAccuracy`オプションは以下の通りです：

| `desiredAccuracy` オプション | 説明                                                                                                  |
|:-------------------------|:-----------------------------------------------------------------------------------------------------|
| `.bestForNavigation`     | ナビゲーションアプリで常に正確な位置情報が必要な場合に使用する精度レベル |
| `.best`                  | 非常に高い精度が必要だが、ナビゲーションアプリほどの精度は必要ない場合                    |
| `.nearestTenMeters`      | 最寄りの10メートルまでの精度                                                                            |
| `.nearestHundredMeters`  | 最寄りの100メートルまでの精度                                                                           |
| `.reduced`               | 1-20キロメートル以内の精度                                                                              |
| `.withinOneKilometer`    | 最寄りの1キロメートルまでの精度                                                                          |
| `.withinThreeKilometers` | 最寄りの3キロメートルまでの精度                                                                         |

Appleの[位置精度定数](https://developer.apple.com/documentation/corelocation/cllocationaccuracy)についてもっと学ぶ。

### `diskStorageDirectory`

ディスク保存用のディレクトリを構成します。デフォルトは`.caches`です。

```swift
config.diskStorageDirectory = .documents
```

### `dispatchListeners`

追跡コールがディスパッチされる直前にリスニングするカスタム`DispatchListener`を追加するオプションを提供します。

```swift
config.dispatchListeners = [self]
```

### `dispatchValidators`

イベントをディスパッチするか、キューに入れるか、ドロップするかを制御するカスタム`DispatchValidator`を追加するオプションを提供します。

```swift
config.dispatchValidators = [self]
```

### `dispatchAfter`

自動的にキューをフラッシュするイベントの数を構成します。

```swift
config.dispatchAfter = 20
```

### `dispatchExpiration`

ディスパッチの有効期限を日数で構成します。デバイスが長期間オフラインの場合、古いイベントは削除されます。

```swift
config.dispatchExpiration = 5
```

### `dispatchQueueLimit`

イベントキューに格納するイベントの最大数を構成します。この数に達し、キューがフラッシュされていない場合、最も古いイベントが削除されます。

```swift
config.dispatchQueueLimit = 50
```

### `enableBackgroundLocation`

アプリがバックグラウンドで実行されている間に位置情報の更新を有効にします。

```swift
config.enableBackgroundLocation = true
```
### `batteryReportingEnabled`

デバイスデータモジュールでのバッテリー報告を有効または無効にします（デフォルト：有効）。

```swift
config.batteryReportingEnabled = true
```

### `screenReportingEnabled`

デバイスデータモジュールでのスクリーン報告を有効または無効にします（デフォルト：有効）。

```swift
config.screenReportingEnabled = true
```

### `minimumFreeDiskSpace`

ディスク保存を有効にするための最小限の空きディスクスペースをメガバイト単位で構成します。

```swift
config.minimumFreeDiskSpace = 25
```

### `minutesBetweenRefresh`

公開構成をフェッチする頻度を決定します。

```swift
config.minutesBetweenRefresh = 15
```

### `onConsentExpiration`

同意選択が期限切れになった際に実行するコールバック。

```swift
config.onConsentExpiration = {
	// 同意モーダルを表示
}
```

### `overrideCollectProfile`

データを異なるTealiumプロファイルに送信するためにTealium Collectプロファイルを上書きします。

```swift
config.overrideCollectProfile = "main"
```

### `overrideCollectURL`

データを異なるエンドポイントに送信するためにTealium Collect URLを上書きします。イベントバッチ機能を使用する場合は、[overrideCollectBatchURL](#overrideCollectBatchURL)プロパティも上書きしてください。

```swift
config.overrideCollectURL = url
```

| プロパティ値 | タイプ     | 説明               |
|:---------------|:---------|:--------------------|
| `url`          | `String` | 上書きするURL |

デフォルトのURLは以下の通りです：
```bash
https://collect.tealiumiq.com/event/
```

このプロパティは、カスタムホスト名を構成するか、特定の地域のホスト名を構成するために使用されます。以下の例では、EU Central地域内に留まるようにTealium Collectの基本URLを構成しています：

```swift
let url = "https://collect-eu-central-1.tealiumiq.com/event/"
config.overrideCollectURL = url
```

### `overrideCollectBatchURL`

データを異なるエンドポイントに送信するためにTealium CollectバッチURLを上書きします。

```swift
config.overrideCollectBatchURL = url
```

| プロパティ値 | タイプ     | 説明               |
|:---------------|:---------|:--------------------|
| `url`          | `String` | 上書きするURL |

イベントバッチングが有効な場合のデフォルトURLは以下の通りです：
```bash
https://collect.tealiumiq.com/bulk-event/
```

この方法は通常、カスタムホスト名を構成するか、特定の地域のホスト名を構成するために使用されます。以下の例では、EU Central地域内に留まるようにTealium Collectの基本URLを構成しています：

```swift
let url = "https://collect-eu-central-1.tealiumiq.com/bulk-event/"
config.overrideCollectBatchURL = url
```

### `overrideCollectDomain`

デフォルトのCollectドメインを上書きします。プロトコルを除外したホスト名（例：`my-company.com`）を値として構成します。このプロパティはバッチおよび単一イベントのディスパッチの両方に使用します。`overrideCollectURL`または`overrideCollectBatchURL`が入力されている場合、このプロパティが優先されます。

```swift
config.overrideCollectDomain = "my-company.com"
```

### `overrideConsentCategoriesKey`

同意イベントで送信される同意カテゴリ属性の名前を上書きします。サーバーサイドの同意をカスタムで強制するために使用します。デフォルト値は`consent_categories`です。

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

上書き後の同意イベント：
```
{
    "tealium_event"              : "grant_partial_consent",
    "policy"                     : "gdpr",
    "consent_categories_granted" : ["Affiliates", "Social"]
}
```

[サーバーサイドの同意の自動強制を無効にする方法](https://docs.tealium.com/server-side-consent-management/)について詳しく学びましょう。
### `TealiumConfig()`

`TealiumConfig` オブジェクトのコンストラクタ。このオブジェクトは、特定のアカウント用にライブラリを初期化するために必要です。

```swift
TealiumConfig(account:String, profile:String, environment:String, dataSource:String)
```

| パラメータ     | 型       | 説明                                       | 例                   |
|:--------------|:---------|:------------------------------------------|:---------------------|
| `account`     | `String` | Tealiumのアカウント名                      | `companyXYZ`         |
| `profile`     | `String` | Tealiumのプロファイル名                    | `main`               |
| `environment` | `String` | Tealiumの環境名                            | [`dev`, `qa`, `prod`]|
| `datasource`  | `String` | (オプション) CDHからのTealiumデータソースキー | `abc123`             |


### `timedEventTriggers`

タイムドイベントを自動的に追跡するための `TimedEventTrigger` オブジェクトのリスト。

```swift
config.timedEventTriggers = [TimedEventTrigger(start: "START_EVENT",
                                               stop: "STOP_EVENT",
                                               name: "TIMED_EVENT_NAME")]
```
以下は `TimedEventTrigger` のパラメータです：

| パラメータ | 型        | 説明                                                                 |
|:----------|:----------|:--------------------------------------------------------------------|
| `start`   | `String`  | タイムドイベントを開始する `TealiumEvent` の名前                     |
| `stop`    | `String`  | タイムドイベントを停止する `TealiumEvent` の名前                     |
| `name`    | `String?` | (オプション) タイムドイベントの名前 (デフォルト: `"START_EVENT::STOP_EVENT"`) |


### `updateDistance`

位置情報の更新を受け取る距離間隔（メートル）を構成します。


<blockquote>
このメソッドは `useHighAccuracy` が `true` に構成されている場合のみ使用してください。
</blockquote>



```swift
config.updateDistance = <Double>
```

| 型       | 説明                                       | 例      |
|:---------|:------------------------------------------|:--------|
| `Double` | 位置情報の更新を受け取る距離間隔（メートル） | `150.0` |

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

デフォルトでは無効に構成されており、位置情報の精度は低精度に構成されます。位置情報が有効なデバイスが500メートル以上移動すると、これは重要な位置情報の変更と見なされ、位置情報の更新が行われます。この構成では、位置情報の更新には通常5分以上かかります。

[Appleの重要な変更位置情報サービス](https://developer.apple.com/documentation/corelocation/getting_the_user_s_location/using_the_significant-change_location_service)についてもっと学ぶ。

有効にすると、データの精度を可能な限り高く構成します。最初のイベントはできるだけ早く配信され、その後、位置を特定し、データが利用可能になると追加のイベントが必要に応じて配信されます。

[Appleの位置情報の精度](https://developer.apple.com/documentation/corelocation/cllocationmanager/1423836-desiredaccuracy?language=swift)についてもっと学ぶ。

高精度を使用すると、位置情報の更新が頻繁に行われるため、低精度よりもデバイスのバッテリー消費が増加します。

```swift
config.useHighAccuracy = <Bool>
```

| 型        | 説明                         | 例      |
|:----------|:----------------------------|:--------|
| `Boolean` | 位置情報の精度を構成します   | `true`  |

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

データレイヤーで指定された `visitorIdentityKey` を使用して訪問の切り替えを有効にします。

例：

```swift
  func start() {
      let customerIdentifierKey = "customer_id"
      let config = TealiumConfig(account: "ACCOUNT",
                                 profile: "NAME",
                                 environment: "ENVIRONMENT",
                                 datasource: "DATASOURCE")
      config.visitorIdentityKey = customerIdentifierKey
      // データレイヤーに特定の顧客識別子を格納するために同じ customerIdentifierKey を使用します
  }
```

### `webviewProcessPool`

Tealium Tag Managementのウェブビュー以外にアプリに他のウェブビューが含まれている場合、クッキーの同期問題を防ぎます。アプリでウェブビューを使用する場合は、`WKProcessPool` のシングルトンインスタンスを作成して保持し、Tealiumをインスタンス化する前に構成します。

例：

```swift
let processPool = MyApp.wkProcessPool
config.webviewProcessPool = processPool
```

### `webviewConfig`

カスタム `WKWebviewConfiguration` オブジェクトを渡すことができ、Tealium Tag Managementのウェブビューで使用されます。このオプションを `webviewProcessPool` オプションの代わりに使用する場合は、カスタマイズ可能な `WKWebviewConfiguration` の `processPool` プロパティを介してシングルトン `WKProcessPool` を構成します。


<blockquote>
将来のAPI変更が行われた場合に必要になる可能性があるため、このオプションの使用を推奨します。
</blockquote>


例：

```swift
let processPool = MyApp.wkProcessPool
let configuration = WKWebViewConfiguration()
configuration.processPool = processPool
config.webviewConfig = configuration
```
