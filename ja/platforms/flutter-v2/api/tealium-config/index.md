---
title: TealiumConfig
description: メインの Tealium クラスの構成オプションを構成するためのクラスです。有効になっている各モジュールは、`TealiumConfig` クラス用に独自の拡張機能を提供します。
url: https://docs.tealium.com/ja/platforms/flutter-v2/api/tealium-config/
---
<blockquote>
これは Tealium for Flutter の旧バージョン（2.x）です。最新バージョンについては、[Tealium for Flutter](https://docs.tealium.com/ja/platforms/flutter/)を参照してください。
</blockquote>


## `TealiumConfig`

以下に、`TealiumConfig` クラスのプロパティの概要を示します。

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `account` | `String` | （必須）Tealium アカウント名 | `companyXYZ`|
| `batchingEnabled` | `bool` | イベントのバッチ処理を有効または無効にします（デフォルト：無効） | `false` |
| `collectors` | `List<Collectors>` | （必須）Tealium ライブラリの初期化に使用する [`Collectors`](#collectors) のリストを構成します | `[Collectors.AppData]` |
| `consentExpiry`| [`ConsentExpiry`](#consentexpiry) | ユーザーの同意構成の有効期限を構成します（デフォルトはポリシーによって異なります） | `ConsentExpiry(90, TimeUnit.DAYS)` |
| `consentLoggingEnabled` | `bool` | 監査目的ですべての同意ステータスの変更を Tealium Customer Data Hub に送信する[同意ログ](https://docs.tealium.com/consent-change-event-specifications/)機能を有効にします（デフォルト：有効） | `true` |
| `consentPolicy`| [`ConsentPolicy`](#consentpolicy) | CCPA や GDPR などの同意ポリシーを構成します。同意マネージャーは、このプロパティが構成されている場合にのみ有効になります。 | `ConsentPolicy.GDPR` |
| `customVisitorId` | `String` | カスタム訪問 ID を構成します | `ALK2398LSDKJ3289SLKJ3298SLKJ3`|
| `dataSource` | `String` | CDH データソースキー |`abc123` |
| `deepLinkTrackingEnabled` | `bool` | Facebook などからアプリへのリンクを含む[標準ディープリンクの自動トラッキング](https://docs.tealium.com/ja/platforms/getting-started-mobile/deep-linking/#readout)と QR Trace を有効または無効にします（デフォルト：有効） | `false` |
| `dispatchers` | `List<Dispatchers>` | （必須）Tealium ライブラリの初期化に使用する [`Dispatchers`](#dispatchers) のリストを構成します | `[Dispatchers.Collect]` |
| `environment` | [`TealiumEnvironment`](#tealiumenvironment) | （必須）Tealium 環境名 | `TealiumEnvironment.dev` |
| `lifecycleAutotrackingEnabled` | `bool` | ライフサイクルの自動トラッキングを有効または無効にします（デフォルト：有効） | `false` |
| `loglevel`| [`LogLevel`](#loglevel) | ログに記録する情報量を制御するログレベルプロパティを構成します（デフォルト：サイレント） | `LogLevel.DEV` |
| `memoryReportingEnabled` | `bool` | DeviceData モジュールでのメモリレポートを有効または無効にします（デフォルト：無効） | `true` |
| `overrideCollectBatchURL` | `String` | Tealium Collect のバッチ URL を上書きし、別のエンドポイントにデータを送信します | `https://example.com/batch-event` |
| `overrideCollectDomain` | `String` | Tealium Collect ドメインを上書きします | `"custom-domain.example.com"` |
| `overrideCollectProfile` | `String` | トラッキングデータで送信される Tealium プロファイルを上書きします。 | `custom-profile` |
| `overrideCollectURL` | `String` | Tealium Collect URL を上書きし、別のエンドポイントにデータを送信します。イベントのバッチ処理機能を使用する場合は、`overrideCollectBatchURL` プロパティも上書きしてください。 | `https://example.com/event` |
| `overrideLibrarySettingsURL` | `String` | パブリッシュ構成の URL を上書きします。 | `https://example.com/mobile.html` |
| `overrideTagManagementURL` | `String` | Tag Management モジュールが使用するデフォルト URL を上書きします。Tealium JavaScript ファイルをセルフホスティングする場合に必要です | `https://example.com/mobile.html` |
| `profile` | `String` | （必須）Tealium プロファイル名 | `main` |
| `qrTraceEnabled` | `bool` | [QR Trace](https://docs.tealium.com/ja/platforms/getting-started-mobile/trace/#how-it-works) を有効または無効にします（デフォルト：有効） | `false` |
| `remoteCommands` | `List<RemoteCommand>` | 初期化時に追加するリモートコマンドのリスト | `[RemoteCommand("firebase", path: "firebase.json")]` |
| `sessionCountingEnabled` | `bool` | Tag Management アカウントのセッションカウントを有効または無効にします。Tealium JavaScript ファイルをセルフホスティングする場合に使用します（デフォルト：有効） | `false` |
| `useRemoteLibrarySettings`| `bool` | [モバイルパブリッシュ構成](https://docs.tealium.com/create-mobile-profile/)を有効または無効にします（デフォルト：有効）。Tag Management でモバイルパブリッシュ構成を構成するか、この機能を無効にしてください。 | `false` |
| [`visitorIdentityKey`](#visitoridentitykey) | `String` | 顧客識別子を表すデータレイヤーキーを指定します。このキーを使用して[訪問の切り替え](https://docs.tealium.com/ja/platforms/getting-started-mobile/identity-resolution/#visitor-switching)を有効にできます。 |
| `visitorServiceEnabled`| `bool` | [Data Layer Enrichment API](https://docs.tealium.com/data-layer-enrichment-api/) を使用した訪問プロファイルの自動取得を有効または無効にします（デフォルト：無効） | `true` |


### `Collectors`

コレクターは、デバイスから補足情報を収集し、Tealium Customer Data Hub に送信される前にデータレイヤーへ追加するモジュールです。一部のコレクターはコアライブラリに含まれていますが、その他のコレクターはオプションであり、個別のモジュールとしてインストールされます。

次の表に、利用可能なコレクターを示します。

| コレクター名 | TealiumConfig の参照 |
| --- | --- |
| `AppData`（デフォルト） | `Collectors.AppData`|
| `Connectivity`（デフォルト） | `Collectors.Connectivity`|
| `DeviceData` | `Collectors.DeviceData`|
| `Lifecycle` | `Collectors.Lifecycle`|

これらのモジュールは、[`TealiumConfig`](https://docs.tealium.com/ja/platforms/flutter-v2/api/tealium-config/) の `collectors` プロパティを使用して有効または無効にします。


### `ConsentExpiry`

ユーザーの同意構成の有効期限を定義します。

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `time` | `int` | 有効期限が切れるまでの時間 | `90` |
| `unit` | `TimeUnit` | 有効期限が切れるまでの時間単位 | `TimeUnit.DAYS` |

例：

```dart
ConsentExpiry(90, TimeUnit.DAYS)
```

以下の時間単位を使用できます。

| 時間単位 | 説明 |
| --- | --- |
| `TimeUnit.DAYS`| 日|
| `TimeUnit.HOURS`| 時間|
| `TimeUnit.MINUTES`| 分|
| `TimeUnit.MONTHS`| 月|


### `ConsentPolicy`

準拠する同意ポリシーを定義します。[`TealiumConfig`](https://docs.tealium.com/ja/platforms/flutter-v2/api/tealium-config/) オブジェクトに同意ポリシーが定義されていない場合、同意マネージャーは無効になります。

例：

```dart
ConsentPolicy.GDPR
```

| 同意ポリシー | 説明 |
| --- | --- |
| `ConsentPolicy.GDPR` | GDPR |
| `ConsentPolicy.CCPA` | CCPA |


### `Dispatchers`

ディスパッチャーは、データレイヤーから Tealium エンドポイントへデータを送信するモジュールです。現在、以下のディスパッチャーを使用できます。

| ディスパッチャー名 | TealiumConfig の参照 |
| --- | --- |
| `Collect` | `Dispatchers.Collect`|
| `RemoteCommands` | `Dispatchers.RemoteCommands`|
| `TagManagement` | `Dispatchers.TagManagement`|


<blockquote>
少なくとも 1 つのディスパッチャーが必要です。ディスパッチャーを指定しない場合、トラッキングは行われません。
</blockquote>



### `Expiry`

有効期限があるプロパティを構成する際の有効期限を定義します。

例：

```dart
Expiry.session
```

以下の有効期限オプションを使用できます。

| 値 | 説明 |
| :-- | :-- |
| `Expiry.session`（デフォルト）| 現在アクティブなセッションの存続期間 |
| `Expiry.forever` | アプリがインストールされている間は無期限 |
| `Expiry.untilRestart` | アプリが再起動するまで |

### `LogLevel`

ログに記録する情報量を制御する `loglevel` プロパティを構成します。

以下のログレベルを使用できます。

| 値 | 説明 |
| --- | --- |
| `LogLevel.DEV` | アプリケーションの進行状況を示す情報イベント |
| `LogLevel.QA` | アプリケーションのデバッグに使用するデバッグレベルのイベント |
| `LogLevel.PROD` | 重大なエラーや障害などのエラーイベント |
| `LogLevel.SILENT` | ログ記録なし（デフォルト） |

例：

```dart
LogLevel.DEV
```
### `TealiumEnvironment`

環境は、3つのデフォルト環境（Dev、QA、Prod）のいずれか、またはTealiumのパブリッシュ先として構成されたカスタム環境です。これらの環境から1つを選択します。

例：

```dart
TealiumEnvironment.dev
```

| 値 | 説明 |
| --- | --- |
| `TealiumEnvironment.dev` | 開発 |
| `TealiumEnvironment.qa` | QA/UAT |
| `TealiumEnvironment.prod` | 本番 |

### `visitorIdentityKey`

データレイヤー内の指定された `visitorIdentityKey` で訪問の切り替えを有効にするために使用します。