---
title: TealiumConfig
description: メインの Tealium クラスの構成オプションを構成するためのクラスです。有効になっている各モジュールは、TealiumConfig クラス用の独自の拡張機能を提供します。
url: https://docs.tealium.com/ja/platforms/nativescript/api/tealium-config/
---
## `TealiumConfig`

以下に、`TealiumConfig` クラスのプロパティの概要を示します。

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `account` | `String` | （必須）Tealium アカウント名 | `companyXYZ`|
| `collectors` | `Collectors[]` | （必須）Tealium ライブラリの初期化に使用する [`Collectors`](#collectors) のリストを構成します | `[Collectors.AppData]` |
| `consentExpiry`| [`ConsentExpiry`](#consentexpiry) | ユーザーの同意構成の有効期限を構成します。（デフォルトはポリシーによって異なります） | `new ConsentExpiry(90, TimeUnit.days)` |
| `consentLoggingEnabled`| `Boolean` | [同意ログ](https://docs.tealium.com/consent-change-event-specifications/)機能を有効にします。この機能は、監査のためにすべての同意ステータスの変更を Tealium Customer Data Hub に送信します。（デフォルト：有効） | `true` |
| `consentPolicy`| [`ConsentPolicy`](#consentpolicy) | CCPA や GDPR などの同意ポリシーを構成します。このプロパティが構成されている場合にのみ、同意マネージャーが有効になります。 | `ConsentPolicy.gdpr` |
| `customVisitorId` | `String` | カスタム訪問 ID を構成します | `ALK2398LSDKJ3289SLKJ3298SLKJ3` |
| `dataSource` | `String` | CDH データソースキー | `abc123` |
| `deepLinkTrackingEnabled` | `Boolean` | Facebook やその他のソースからアプリへのリンクなど、[標準ディープリンクの自動トラッキング](https://docs.tealium.com/ja/platforms/getting-started-mobile/deep-linking/#readout)と QR Trace を有効または無効にします。（デフォルト：有効） | `false` |
| `dispatchers` | `Dispatchers[]` | （必須）Tealium ライブラリの初期化に使用する [`Dispatchers`](#dispatchers) のリストを構成します | `[Dispatchers.Collect]` |
| `environment` | [`TealiumEnvironment`](#tealiumenvironment) | （必須）Tealium 環境名 | `TealiumEnvironment.dev` |
| `loglevel`| [`LogLevel`](#loglevel) | 記録する情報量を制御するログレベルプロパティを構成します（デフォルト：サイレント） | `LogLevel.dev` |
| `lifecycleAutotrackingEnabled`| `Boolean` | ライフサイクルの自動トラッキングを有効または無効にします。（デフォルト：有効） | `false` |
| `memoryReportingEnabled` | `Boolean` | DeviceData モジュールのメモリレポートを有効または無効にします（デフォルト：無効）。 | `true` |
| `overrideCollectURL`| `String` | Tealium Collect URL を上書きして、別のエンドポイントにデータを送信します。イベントバッチ処理機能を使用する場合は、`overrideCollectBatchURL` プロパティも上書きしてください。 | `https://custom-domain.com/event` |
| `overrideCollectBatchURL`| `String` | Tealium Collect のバッチ URL を上書きして、別のエンドポイントにデータを送信します。 | `https://custom-domain.com/batch-event` |
| [`overrideCollectProfile`](#overridecollectprofile)| `String` | Tealium Collect プロファイルを上書きして、別の Tealium プロファイルにデータを送信します。 | `custom-profile` |
| [`overrideCollectDomain`](#overridecollectdomain)| `String` | Tealium Collect URL のドメイン名を上書きして、別のエンドポイントにデータを送信します。 | `custom-domain` |
| `overrideLibrarySettingsURL` | `String` | パブリッシュ構成 URL を上書きします。 | `https://custom-domain.com/mobile.html` |
| `overrideTagManagementURL` | `String` | Tag Management モジュールが使用するデフォルト URL を上書きします。Tealium JavaScript ファイルをセルフホスティングする場合に必要です。 | `https://custom-domain.com/path/env/utag.js` |
| `profile` | `String` | （必須）Tealium プロファイル名 | `main` |
| `qrTraceEnabled` | `Boolean` | [QR Trace](https://docs.tealium.com/ja/platforms/getting-started-mobile/trace/#mobile-trace-tool) を有効または無効にします。（デフォルト：有効） | `false` |
| [`sessionCountingEnabled`](#sessioncountingenabled) | `Boolean` | Tag Management アカウントのセッションカウントを有効または無効にします。Tealium JavaScript ファイルをセルフホスティングする場合は、これを `false` に構成してください。（デフォルト：有効） | `false` |
| `useRemoteLibrarySettings`| `Boolean` | [Mobile Publish Settings](https://docs.tealium.com/create-mobile-profile/) を有効または無効にします（デフォルト：有効）。Tag Management で Mobile Publish Settings を構成するか、この機能を無効にしてください。 | `false` |
| `visitorServiceEnabled`| `Boolean` | [Data Layer Enrichment API](https://docs.tealium.com/data-layer-enrichment-api/) を使用した訪問プロファイルの自動取得を有効または無効にします（デフォルト：無効） | `true` |
| `visitorServiceRefreshInterval`| `String` | 訪問プロファイルを更新する間隔を分単位で構成します。整数のみがサポートされます。たとえば、`"2"` は 2 分を表します。 | `"2"` |


### `Collectors`

コレクターは、デバイスから補足情報を収集し、Tealium Customer Data Hub に送信される前にデータレイヤーへ追加するモジュールです。一部のコレクターはコアライブラリに含まれていますが、その他は任意であり、個別のモジュールとしてインストールされます。

次の表に、利用可能なコレクターを示します。デフォルトのコレクターには、コレクター名の横に `*` が付いています。

| コレクター名 | TealiumConfig の参照 |
| --- | --- |
| `AppData`* | `Collectors.AppData`|
| `Connectivity`* | `Collectors.Connectivity`|
| `Device` | `Collectors.Device`|
| `Lifecycle` | `Collectors.Lifecycle`|

これらのモジュールは、[`TealiumConfig`](https://docs.tealium.com/ja/platforms/nativescript/api/tealium-config/) の `collectors` プロパティを使用して有効または無効にします。


### `ConsentPolicy`

準拠する同意ポリシーを定義します。[`TealiumConfig`](https://docs.tealium.com/ja/platforms/nativescript/api/tealium-config/) オブジェクトで同意ポリシーが定義されていない場合、同意マネージャーは無効になります。

例：

`ConsentPolicy.gdpr`

次の同意ポリシーを使用できます。

| 値 | 説明 |
| --- | --- |
| `.gdpr` | GDPR |
| `.ccpa` | CCPA |


### `ConsentExpiry`

ユーザーの同意構成の有効期限を定義します。

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `time` | `Number` | 有効期限までの時間 | `90` |
| `unit` | `TimeUnit` | 有効期限までの時間の単位 | `TimeUnit.days` |

例：

`new ConsentExpiry(90, TimeUnit.days)`

#### TimeUnit

次の時間単位を使用できます。

| 値 | 説明 |
| --- | --- |
| `.minutes` | 分 |
| `.hours` | 時間 |
| `.days` | 日 |
| `.months` | 月 |


### `Dispatchers`

ディスパッチャーは、データレイヤーから Tealium エンドポイントにデータを送信するモジュールです。現在、次のディスパッチャーを使用できます。

| ディスパッチャー名 | TealiumConfig の参照 |
| --- | --- |
| `Collect` | `Dispatchers.Collect`|
| `RemoteCommands` | `Dispatchers.RemoteCommands`|
| `TagManagement` | `Dispatchers.TagManagement`|


<blockquote>
少なくとも 1 つのディスパッチャーが必要です。ディスパッチャーが指定されていない場合、トラッキングは行われません。
</blockquote>



### `LogLevel`

記録する情報量を制御する `logLevel` プロパティを構成します。

次のログレベルを使用できます。

| 値 | 説明 |
| --- | --- |
| `LogLevel.dev` | アプリケーションの進行状況を示す情報イベント |
| `LogLevel.qa` | アプリケーションのデバッグに使用するデバッグレベルのイベント |
| `LogLevel.prod` | 重大なエラーや障害などのエラーイベント |
| `LogLevel.silent` | ログを記録しません（デフォルト） |

### `overrideCollectProfile`

Tealium Collect プロファイルを上書きして、別の Tealium プロファイルにデータを送信します。

```swift
config.overrideCollectProfile = "main"
```

### `overrideCollectDomain`

Tealium Collect URL のドメイン名を上書きして、別のエンドポイントにデータを送信します。

```swift
config.overrideCollectDomain = "my-company.com"
```

### `sessionCountingEnabled`

Tag Management アカウントのセッションカウントを有効または無効にします。Tealium JavaScript ファイルをセルフホスティングする場合は、これを `false` に構成してください（デフォルト：有効）。

```swift
config.sessionCountingEnabled = false
```
### `TealiumEnvironment`

環境は、3つのデフォルト環境（開発、QA、本番）のいずれか、またはTealiumのパブリッシュ先として構成されたカスタム環境です。これらの環境から1つを選択します。

例：

`TealiumEnvironment.dev`

| 値 | 説明 |
| --- | --- |
| `.dev` | 開発 |
| `.qa` | QA/UAT |
| `.prod` | 本番 |


### `VisitorProfile`

訪問プロファイルは、各属性のわかりやすい名前を格納するオブジェクトです。訪問属性と訪問属性のタイプを区別するための`currentVisit`プロパティがあります。添字を使用し、IDで各属性値にアクセスします。属性が存在しない場合は、`null`が返されます。例については、以下のリストを参照してください。

**属性タイプ**

| パラメーター | プロパティ | 値 |
| --- | --- | --- |
| `arraysOfBooleans` | id: String, value: Boolean[]   | `id: "5129", value: [true,false,true,true]` |
| `arraysOfNumbers`  | id: String, value: Number[]    | `id: "57", value: [4.82125, 16.8, 0.5714285714285714]` |
| `arraysOfStrings`  | id: String, value: String[]    | `id: "5213", value: ["green shirts", "green shirts", "blue shirts"]` |
| `audiences`        | id: String, value: String      | `id: "tealiummobile\_demo\_103", value: "iOS Users"` |
| `badges`           | id: String, value: Boolean     | `id: "2815", value: true` |
| `booleans`         | id: String, value: Boolean     | `id: "4868", value: true` |
| `currentVisit`     | 現在の訪問のvisitorProfileに含まれるすべての属性。現在の訪問プロファイルには、オーディエンスまたはバッジは含まれません。 | `TealiumCurrentVisitProfile(dates: ["5376": 1567536668080, "10": 1567536668000], booleans: ["4530": true], numbers: ["32": 3.8])`  |
| `dates`            | id: String, value: Number      | `id: "22", value: 1567120112000` |
| `numbers`          | id: String, value: Number      | `id: "5728", value: 4.82125` |
| `setOfStrings`     | id: String, value: Set(String) | `id: "5211", value: ["green shirts", "red shirts", "blue shirts"]` |
| `strings`          | id: String, value: String      | `id: "5380", value: "green shirts"` |
| `tallies`          | id: String, value: Object      | `"57": [["category 1": 2.0], "category 2": 1.0]]` |
| `tallyValue`       | id: String, value: Number      | `["category 1": 2.0]` |