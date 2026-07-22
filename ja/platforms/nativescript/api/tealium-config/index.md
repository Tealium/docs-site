---
title: TealiumConfig
description: メインのTealiumクラスの構成オプションを構成するためのクラスです。個々のモジュールは、有効になっている場合にのみ、TealiumConfigクラスの拡張機能を提供します。
url: https://docs.tealium.com/ja/platforms/nativescript/api/tealium-config/
---
## `TealiumConfig`

以下は、`TealiumConfig`クラスのプロパティを要約したものです。

| パラメータ | タイプ | 説明 | 例 |
| --- | --- | --- | --- |
| `account` | `String` | (必須) Tealiumアカウント名 | `companyXYZ`|
| `collectors` | `Collectors[]` | (必須) Tealiumライブラリを初期化するための[`Collectors`](#collectors)のリストを構成します。 | `[Collectors.AppData]` |
| `consentExpiry`| [`ConsentExpiry`](#consentexpiry) | ユーザーの同意構成の有効期限を構成します。 (デフォルトはポリシーに依存します) | `new ConsentExpiry(90, TimeUnit.days)` |
| `consentLoggingEnabled`| `Boolean` | [同意ログ](https://docs.tealium.com/consent-change-event-specifications/)機能を有効にし、すべての同意ステータスの変更を監査目的でTealium Customer Data Hubに送信します。 (デフォルト: 有効) | `true` |
| `consentPolicy`| [`ConsentPolicy`](#consentpolicy) | CCPAやGDPRなどの同意ポリシーを構成します。このプロパティが構成されている場合にのみ、同意マネージャーが有効になります。 | `ConsentPolicy.gdpr` |
| `customVisitorId` | `String` | カスタムのビジターIDを構成します。 | `ALK2398LSDKJ3289SLKJ3298SLKJ3` |
| `dataSource` | `String` | CDHデータソースキー | `abc123` |
| `deepLinkTrackingEnabled` | `Boolean` | Facebookやその他のソースからアプリへのリンクなどの[標準的なディープリンクの自動トラッキング](https://docs.tealium.com/ja/platforms/getting-started-mobile/deep-linking/#readout)を有効または無効にします。また、QRトレースも有効または無効にします。 (デフォルト: 有効) | `false` |
| `dispatchers` | `Dispatchers[]` | (必須) Tealiumライブラリを初期化するための[`Dispatchers`](#dispatchers)のリストを構成します。| `[Dispatchers.Collect]` |
| `environment` | [`TealiumEnvironment`](#tealiumenvironment) | (必須) Tealium環境名 |  `TealiumEnvironment.dev` |
| `loglevel`| [`LogLevel`](#loglevel) | ログレベルプロパティを構成し、ログに記録される情報の量を制御します (デフォルト: silent) | `LogLevel.dev` |
| `lifecycleAutotrackingEnabled`| `Boolean` | ライフサイクルの自動トラッキングを有効または無効にします。 (デフォルト: 有効) | `false` |
| `memoryReportingEnabled` | `Boolean` | DeviceDataモジュールでのメモリレポートの有効または無効を構成します (デフォルト: 無効)。 | `true` |
| `overrideCollectURL`| `String` | Tealium Collect URLを別のエンドポイントに送信するためにオーバーライドします。イベントバッチング機能を使用している場合は、`overrideCollectBatchURL`プロパティもオーバーライドします。 | `https://custom-domain.com/event` |
| `overrideCollectBatchURL`| `String` | Tealium CollectバッチURLを別のエンドポイントに送信するためにオーバーライドします。 | `https://custom-domain.com/batch-event` |
| [`overrideCollectProfile`](#overridecollectprofile)| `String` | Tealium Collectプロファイルを別のTealiumプロファイルに送信するためにオーバーライドします。 | `custom-profile` |
| [`overrideCollectDomain`](#overridecollectdomain)| `String` | Tealium Collect URLのドメイン名を別のエンドポイントに送信するためにオーバーライドします。 | `custom-domain` |
| `overrideLibrarySettingsURL` | `String` | 公開構成URLをオーバーライドします。 | `https://custom-domain.com/mobile.html` |
| `overrideTagManagementURL` | `String` | タグ管理モジュールで使用されるデフォルトのURLをオーバーライドします。TealiumのJavaScriptファイルを自己ホストしている場合に必要です。 | `https://custom-domain.com/path/env/utag.js` |
| `profile` | `String` | (必須) Tealiumプロファイル名 | `main` |
| `qrTraceEnabled` | `Boolean` | [QRトレース](https://docs.tealium.com/ja/platforms/getting-started-mobile/trace/#mobile-trace-tool)を有効または無効にします。 (デフォルト: 有効) | `false` |
| [`sessionCountingEnabled`](#sessioncountingenabled) | `Boolean` | Tealium iQアカウントのセッションカウントを有効または無効にします。TealiumのJavaScriptファイルを自己ホストしている場合は、これを`false`に構成します。 (デフォルト: 有効) | `false` |
| `useRemoteLibrarySettings`| `Boolean` | [モバイル公開構成](https://docs.tealium.com/creating-a-mobile-profile/)を有効または無効にします (デフォルト: 有効)。iQタグ管理でモバイル公開構成を構成するか、機能を無効にします。 | `false` |
| `visitorServiceEnabled`| `Boolean` | [データレイヤー拡張API](https://docs.tealium.com/data-layer-enrichment-api/)を使用してビジタープロファイルの自動取得を有効または無効にします (デフォルト: 無効) | `true` |
| `visitorServiceRefreshInterval`| `String` | ビジタープロファイルのリフレッシュ間隔を分単位で構成します。整数のみがサポートされています。例えば、"2"は2分です。 | `"2"` |


### `Collectors`

Collectorsは、デバイスから補足情報を収集し、Tealium Customer Data Hubに送信する前にデータレイヤーに追加するモジュールです。一部のCollectorsはコアライブラリに含まれており、他のものはオプションとして別のモジュールとしてインストールされます。

以下の表は、利用可能なCollectorsをリストアップしています。デフォルトのCollectorsは、Collectorsの横に`*`が付いています。

| Collector名 | TealiumConfig参照 |
| --- | --- |
| `AppData`* | `Collectors.AppData`|
| `Connectivity`* | `Collectors.Connectivity`|
| `Device` | `Collectors.Device`|
| `Lifecycle` | `Collectors.Lifecycle`|

これらのモジュールは、[`TealiumConfig`](https://docs.tealium.com/ja/platforms/nativescript/api/tealium-config/)の`collectors`プロパティを使用して有効または無効にできます。


### `ConsentPolicy`

遵守する同意ポリシーを定義します。[`TealiumConfig`](https://docs.tealium.com/ja/platforms/nativescript/api/tealium-config/)オブジェクトに同意ポリシーが定義されていない場合、同意マネージャーは無効になります。

例:

`ConsentPolicy.gdpr`

以下の同意ポリシーが利用可能です:

| 値 | 説明 |
| --- | --- |
| `.gdpr` | GDPR |
| `.ccpa` | CCPA |


### `ConsentExpiry`

ユーザーの同意構成の有効期限を定義します。

| パラメータ | タイプ | 説明 | 例 |
| --- | --- | --- | --- |
| `time` | `Number` | 有効期限までの時間の量 | `90` |
| `unit` | `TimeUnit` | 有効期限までの時間の単位 | `TimeUnit.days` |

例:

`new ConsentExpiry(90, TimeUnit.days)`

#### TimeUnit

以下の時間単位が利用可能です:

| 値 | 説明 |
| --- | --- |
| `.minutes` | 分 |
| `.hours` | 時間 |
| `.days` | 日 |
| `.months` | 月 |


### `Dispatchers`

Dispatchersは、データレイヤーからTealiumエンドポイントにデータを送信するモジュールです。現在利用可能なDispatchersは以下の通りです:

| Dispatcher名 | TealiumConfig参照 |
| --- | --- |
| `Collect` | `Dispatchers.Collect`|
| `RemoteCommands` | `Dispatchers.RemoteCommands`|
| `TagManagement` | `Dispatchers.TagManagement`|


<blockquote>
少なくとも1つのdispatcherが必要です。dispatcherが指定されていない場合、トラッキングは行われません。
</blockquote>



### `LogLevel`

`logLevel`プロパティを構成し、ログに記録される情報の量を制御します。

以下のログレベルが利用可能です:

| 値 | 説明 |
| --- | --- |
| `LogLevel.dev` | アプリケーションの進行状況を示す情報イベント |
| `LogLevel.qa` | アプリケーションのデバッグに使用されるデバッグレベルのイベント |
| `LogLevel.prod` | クリティカルなエラーや障害などのエラーイベント |
| `LogLevel.silent` | ログなし (デフォルト) |

### `overrideCollectProfile`

Tealium Collectプロファイルを別のTealiumプロファイルに送信するためにオーバーライドします。

```swift
config.overrideCollectProfile = "main"
```

### `overrideCollectDomain`

Tealium Collect URLのドメイン名を別のエンドポイントに送信するためにオーバーライドします。

```swift
config.overrideCollectDomain = "my-company.com"
```

### `sessionCountingEnabled`
Tealium iQアカウントのセッションカウントを有効または無効にします。TealiumのJavaScriptファイルを自己ホストしている場合は、これを`false`に構成します (デフォルト: 有効)。                         

```swift
config.sessionCountingEnabled = false
```

### `TealiumEnvironment`

環境は、Tealiumが公開する3つのデフォルト環境（Dev、QA、Prod）またはカスタム環境のいずれかです。これらの環境のいずれかを選択します。

例:

`TealiumEnvironment.dev`

| 値 | 説明 |
| --- | --- |
| `.dev` | 開発 |
| `.qa` | QA/UAT |
| `.prod` | 本番 |


### `VisitorProfile`

ビジタープロファイルは、各属性のフレンドリーな名前を含むオブジェクトです。`currentVisit`プロパティがあり、ビジター/ビジット属性タイプを区別することができます。各属性の値は、サブスクリプトを使用してIDでアクセスします。属性が存在しない場合は、`null`が返されます。以下のリストを参照してください。

**属性タイプ**

| パラメータ | プロパティ | 値 |
| --- | --- | --- |
| `arraysOfBooleans` | id: String, value: Boolean[]   | `id: "5129", value: [true,false,true,true]` |
| `arraysOfNumbers`  | id: String, value: Number[]    | `id: "57", value: [4.82125, 16.8, 0.5714285714285714]` |
| `arraysOfStrings`  | id: String, value: String[]    | `id: "5213", value: ["green shirts", "green shirts", "blue shirts"]` |
| `audiences`        | id: String, value: String      | `id: "tealiummobile\_demo\_103", value: "iOS Users"` |
| `badges`           | id: String, value: Boolean     | `id: "2815", value: true` |
| `booleans`         | id: String, value: Boolean     | `id: "4868", value: true` |
| `currentVisit`     | 現在のビジットのビジタープロファイルのすべての属性。現在のビジットプロファイルにはAudiencesやBadgesは含まれません。 | `TealiumCurrentVisitProfile(dates: ["5376": 1567536668080, "10": 1567536668000], booleans: ["4530": true], numbers: ["32": 3.8])`  |
| `dates`            | id: String, value: Number      | `id: "22", value: 1567120112000` |
| `numbers`          | id: String, value: Number      | `id: "5728", value: 4.82125` |
| `setOfStrings`     | id: String, value: Set(String) | `id: "5211", value: ["green shirts", "red shirts", "blue shirts"]` |
| `strings`          | id: String, value: String      | `id: "5380", value: "green shirts"` |
| `tallies`          | id: String, value: Object      | `"57": [["category 1": 2.0], "category 2": 1.0]]` |
| `tallyValue`       | id: String, value: Number      | `["category 1": 2.0]` |


