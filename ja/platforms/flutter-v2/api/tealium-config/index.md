---
title: TealiumConfig
description: Tealiumクラスの構成オプションを構成するためのクラス。個々のモジュールは、有効になっている場合、`TealiumConfig`クラスの拡張を提供します。
url: https://docs.tealium.com/ja/platforms/flutter-v2/api/tealium-config/
---これはFlutter用Tealiumの以前のバージョン（2.x）です。最新バージョンについては、[Flutter用Tealium](/ja/platforms/flutter/)を参照してください。

## `TealiumConfig`

以下は、`TealiumConfig`クラスのプロパティをまとめたものです。

| パラメータ | タイプ | 説明 | 例 |
| --- | --- | --- | --- |
| `account` | `String` | （必須）Tealiumアカウント名 | `companyXYZ`|
| `batchingEnabled` | `bool` | イベントバッチ処理を有効または無効にする（デフォルト：無効） | `false` |
| `collectors` | `List&lt;Collectors&gt;` | （必須）Tealiumライブラリを初期化するための[`Collectors`](#collectors)のリストを構成する | `[Collectors.AppData]` |
| `consentExpiry`| [`ConsentExpiry`](#consentexpiry) | ユーザーの同意構成の有効期限を構成する（デフォルトはポリシーに依存） | `ConsentExpiry(90, TimeUnit.DAYS)` |
| `consentLoggingEnabled` | `bool` | [同意ログ記録]()機能を有効にする。これにより、すべての同意状態の変更が監査目的でTealium Customer Data Hubに送信される（デフォルト：有効） | `true` |
| `consentPolicy`| [`ConsentPolicy`](#consentpolicy) | 同意ポリシー（CCPAまたはGDPRなど）を構成する。このプロパティが構成されている場合のみ、同意マネージャーが有効になる。 | `ConsentPolicy.GDPR` |
| `customVisitorId` | `String` | カスタム訪問IDを構成する | `ALK2398LSDKJ3289SLKJ3298SLKJ3`|
| `dataSource` | `String` | CDHデータソースキー |`abc123` |
| `deepLinkTrackingEnabled` | `bool` | [標準的なディープリンクの自動追跡](/ja/platforms/getting-started-mobile/deep-linking/#readout)を有効または無効にする。これには、FacebookなどのソースからのアプリへのリンクやQRトレースが含まれる（デフォルト：有効） | `false` |
| `dispatchers` | `List&lt;Dispatchers&gt;` | （必須）Tealiumライブラリを初期化するための[`Dispatchers`](#dispatchers)のリストを構成する| `[Dispatchers.Collect]` |
| `environment` | [`TealiumEnvironment`](#tealiumenvironment) | （必須）Tealium環境名 |  `TealiumEnvironment.dev` |
| `lifecycleAutotrackingEnabled` | `bool` | ライフサイクル自動追跡を有効または無効にする（デフォルト：有効） | `false` |
| `loglevel`| [`LogLevel`](#loglevel) | ログレベルプロパティを構成する。これにより、記録される情報の量が制御される（デフォルト：無音） | `LogLevel.DEV` |
| `memoryReportingEnabled` | `bool` | DeviceDataモジュールでのメモリレポートを有効または無効にする（デフォルト：無効） | `true` |
| `overrideCollectBatchURL` | `String` | Tealium CollectバッチURLを上書きして、データを別のエンドポイントに送信する | `https://example.com/batch-event` |
| `overrideCollectDomain` | `String` | Tealium Collectドメインを上書きする | `&#34;custom-domain.example.com&#34;` |
| `overrideCollectProfile` | `String` | トラッキングデータで送信されるTealiumプロファイルを上書きする。 | `custom-profile` |
| `overrideCollectURL` | `String` | Tealium Collect URLを上書きして、データを別のエンドポイントに送信する。イベントバッチ処理機能を使用する場合は、`overrideCollectBatchURL`プロパティも上書きする。 | `https://example.com/event` |
| `overrideLibrarySettingsURL` | `String` | 公開構成URLを上書きする。 | `https://example.com/mobile.html` |
| `overrideTagManagementURL` | `String` | タグ管理モジュールで使用されるデフォルトURLを上書きする。これは、Tealium JavaScriptファイルを自己ホスティングしている場合に必要です | `https://example.com/mobile.html` |
| `profile` | `String` | （必須）Tealiumプロファイル名 | `main` |
| `qrTraceEnabled` | `bool` | [QRトレース](/ja/platforms/getting-started-mobile/trace/#how-it-works)を有効または無効にする（デフォルト：有効） | `false` |
| `remoteCommands` | `List&lt;RemoteCommand&gt;` | 初期化中に追加するリモートコマンドのリスト | `[RemoteCommand(&#34;firebase&#34;, path: &#34;firebase.json&#34;)]` |
| `sessionCountingEnabled` | `bool` | Tealium iQアカウントのセッションカウントを有効または無効にする。Tealium JavaScriptファイルを自己ホスティングしている場合に使用する（デフォルト：有効） | `false` |
| `useRemoteLibrarySettings`| `bool` | [モバイル公開構成]()を有効または無効にする（デフォルト：有効）。iQタグ管理でモバイル公開構成を構成するか、この機能を無効にする。 | `false` |
| [`visitorIdentityKey`](#visitoridentitykey) | `String` | 顧客識別子を表すデータレイヤーキーを指定する。このキーを使用して[訪問の切り替え](/ja/platforms/getting-started-mobile/identity-resolution/#visitor-switching)を有効にすることができる。 |
| `visitorServiceEnabled`| `bool` | [Data Layer Enrichment API]()を使用して訪問プロファイルの自動取得を有効または無効にする（デフォルト：無効） | `true` |


### `Collectors`

Collectorsは、デバイスから追加情報を収集し、データレイヤーに追加してからTealium Customer Data Hubに送信するモジュールです。一部のコレクターはコアライブラリに含まれており、他のコレクターは別のモジュールとしてオプションでインストールされます。

利用可能なコレクターを以下の表に示します：

| コレクター名 | TealiumConfig参照 |
| --- | --- |
| `AppData`（デフォルト） | `Collectors.AppData`|
| `Connectivity`（デフォルト） | `Collectors.Connectivity`|
| `DeviceData` | `Collectors.DeviceData`|
| `Lifecycle` | `Collectors.Lifecycle`|

これらのモジュールは、[`TealiumConfig`](/ja/platforms/flutter-v2/api/tealium-config/)の`collectors`プロパティを使用して有効または無効にされます。


### `ConsentExpiry`

ユーザーの同意構成の有効期限を定義します。

| パラメータ | タイプ | 説明 | 例 |
| --- | --- | --- | --- |
| `time` | `int` | 有効期限までの時間 | `90` |
| `unit` | `TimeUnit` | 有効期限までの時間単位 | `TimeUnit.DAYS` |

例：

```dart
ConsentExpiry(90, TimeUnit.DAYS)
```

利用可能な時間単位：

| 時間単位 | 説明 |
| --- | --- |
| `TimeUnit.DAYS`| 日数|
| `TimeUnit.HOURS`| 時間|
| `TimeUnit.MINUTES`| 分|
| `TimeUnit.MONTHS`| 月数|


### `ConsentPolicy`

同意ポリシーを定義します。[`TealiumConfig`](/ja/platforms/flutter-v2/api/tealium-config/)オブジェクトに同意ポリシーが定義されていない場合、同意マネージャーは無効になります。

例：

```dart
ConsentPolicy.GDPR
```

| 同意ポリシー | 説明 |
| --- | --- |
| `ConsentPolicy.GDPR` | GDPR |
| `ConsentPolicy.CCPA` | CCPA |


### `Dispatchers`

Dispatchersは、データレイヤーからのデータをTealiumエンドポイントに送信するモジュールです。現在利用可能なディスパッチャーは以下の通りです：

| ディスパッチャー名 | TealiumConfig参照 |
| --- | --- |
| `Collect` | `Dispatchers.Collect`|
| `RemoteCommands` | `Dispatchers.RemoteCommands`|
| `TagManagement` | `Dispatchers.TagManagement`|

少なくとも1つのディスパッチャーが必要です。ディスパッチャーが指定されていない場合、トラッキングは行われません。


### `Expiry`

プロパティの有効期限を構成するための有効期限を定義します。

例：

```dart
Expiry.session
```

利用可能な有効期限オプション：

| 値 | 説明 |
| :-- | :-- |
| `Expiry.session` (デフォルト)| 現在のアクティブセッションの寿命 |
| `Expiry.forever` | アプリがインストールされている間は期限切れにならない |
| `Expiry.untilRestart` | アプリが再起動するまで |

### `LogLevel`

`loglevel`プロパティを構成し、記録される情報の量を制御します。

利用可能なログレベル：

| 値 | 説明 |
| --- | --- |
| `LogLevel.DEV` | アプリケーションの進行を強調する情報イベント |
| `LogLevel.QA` | アプリケーションのデバッグに使用されるデバッグレベルのイベント |
| `LogLevel.PROD` | 重大なエラーや失敗などのエラーイベント |
| `LogLevel.SILENT` | ログなし（デフォルト） |

例：

```dart
LogLevel.DEV
```
### `TealiumEnvironment`

環境は、デフォルトの3つの環境（Dev、QA、Prod）またはTealiumが公開する任意のカスタム環境のいずれかです。これらの環境の中から一つを選択してください。

例:

```dart
TealiumEnvironment.dev
```

| 値 | 説明 |
| --- | --- |
| `TealiumEnvironment.dev` | 開発 |
| `TealiumEnvironment.qa` | QA/UAT |
| `TealiumEnvironment.prod` | 本番 |

### `visitorIdentityKey`

データレイヤーで指定された `visitorIdentityKey` に訪問切り替えを有効にするために使用されます。