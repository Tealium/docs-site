---
title: TealiumConfig
description: Tealiumクラスの構成オプションを構成するためのクラス。個々のモジュールは、有効になっている場合、`TealiumConfig`クラスの拡張を提供します。
url: https://docs.tealium.com/ja/platforms/flutter/api/tealium-config/
---
## `TealiumConfig`

以下は、`TealiumConfig`クラスのプロパティをまとめたものです。

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `account` | `String` | (必須) Tealiumアカウント名 | `companyXYZ`|
| `batchingEnabled` | `bool` | イベントバッチ処理を有効または無効にします（デフォルト：無効） | `false` |
| `collectors` | `List<Collectors>` | (必須) Tealiumライブラリを初期化するための[`Collectors`](#collectors)のリストを構成します | `[Collectors.AppData]` |
| `consentExpiry`| [`ConsentExpiry`](#consentexpiry) | ユーザーの同意構成の有効期限を構成します（デフォルトはポリシーに依存します） | `ConsentExpiry(90, TimeUnit.DAYS)` |
| `consentLoggingEnabled` | `bool` | [同意ログ記録](https://docs.tealium.com/consent-change-event-specifications/)機能を有効にし、すべての同意状態の変更を監査目的でTealium Customer Data Hubに送信します（デフォルト：有効） | `true` |
| `consentPolicy`| [`ConsentPolicy`](#consentpolicy) | 同意ポリシー（CCPAまたはGDPRなど）を構成します。このプロパティが構成されている場合のみ、同意マネージャーが有効になります。 | `ConsentPolicy.GDPR` |
| `customVisitorId` | `String` | カスタム訪問IDを構成します | `ALK2398LSDKJ3289SLKJ3298SLKJ3`|
| `dataSource` | `String` | CDHデータソースキー |`abc123` |
| `deepLinkTrackingEnabled` | `bool` | [標準ディープリンクの自動追跡](https://docs.tealium.com/ja/platforms/getting-started-mobile/deep-linking/#readout)を有効または無効にします。Facebookなどの他のソースからのアプリへのリンクやQRトレースを含みます（デフォルト：有効） | `false` |
| `dispatchers` | `List<Dispatchers>` | (必須) Tealiumライブラリを初期化するための[`Dispatchers`](#dispatchers)のリストを構成します| `[Dispatchers.Collect]` |
| `environment` | [`TealiumEnvironment`](#tealiumenvironment) | (必須) Tealium環境名 |  `TealiumEnvironment.dev` |
| `lifecycleAutotrackingEnabled` | `bool` | ライフサイクル自動追跡を有効または無効にします（デフォルト：有効） | `false` |
| `loglevel`| [`LogLevel`](#loglevel) | ログレベルプロパティを構成し、どの程度の情報がログに記録されるかを制御します（デフォルト：サイレント） | `LogLevel.DEV` |
| `memoryReportingEnabled` | `bool` | DeviceDataモジュールでのメモリ報告を有効または無効にします（デフォルト：無効） | `true` |
| `overrideCollectBatchURL` | `String` | Tealium CollectバッチURLを上書きして、データを別のエンドポイントに送信します | `https://example.com/batch-event` |
| `overrideCollectDomain` | `String` | Tealium Collectドメインを上書きします | `"custom-domain.example.com"` |
| `overrideCollectProfile` | `String` | トラッキングデータで送信されるTealiumプロファイルを上書きします。 | `custom-profile` |
| `overrideCollectURL` | `String` | Tealium Collect URLを上書きして、データを別のエンドポイントに送信します。イベントバッチ処理機能を使用する場合は、`overrideCollectBatchURL`プロパティも上書きしてください。 | `https://example.com/event` |
| `overrideLibrarySettingsURL` | `String` | 公開構成URLを上書きします。 | `https://example.com/mobile.html` |
| `overrideTagManagementURL` | `String` | タグ管理モジュールで使用されるデフォルトURLを上書きします。Tealium JavaScriptファイルを自己ホスティングしている場合に必要です | `https://example.com/mobile.html` |
| `profile` | `String` | (必須) Tealiumプロファイル名 | `main` |
| `qrTraceEnabled` | `bool` | [QRトレース](https://docs.tealium.com/ja/platforms/getting-started-mobile/trace/#how-it-works)を有効または無効にします（デフォルト：有効） | `false` |
| `remoteCommands` | `List<RemoteCommand>` | 初期化中に追加するリモートコマンドのリスト | `[RemoteCommand("firebase", path: "firebase.json")]` |
| `sessionCountingEnabled` | `bool` | Tealium iQアカウントのセッションカウントを有効または無効にします。Tealium JavaScriptファイルを自己ホスティングしている場合に使用します（デフォルト：有効） | `false` |
| `useRemoteLibrarySettings`| `bool` | [モバイル公開構成](https://docs.tealium.com/creating-a-mobile-profile/)を有効または無効にします（デフォルト：有効）。iQタグ管理でモバイル公開構成を構成するか、機能を無効にします。 | `false` |
| [`visitorIdentityKey`](#visitoridentitykey) | `String` | 顧客識別子を表すデータレイヤーキーを指定します。このキーを使用して[訪問の切り替え](https://docs.tealium.com/ja/platforms/getting-started-mobile/identity-resolution/#visitor-switching)を有効にすることができます。 | |
| `visitorServiceEnabled`| `bool` | [データレイヤーエンリッチメントAPI](https://docs.tealium.com/data-layer-enrichment-api/)を使用して訪問プロファイルの自動取得を有効または無効にします（デフォルト：無効） | `true` |
| `webViewLoggingEnabled` | `bool` | WebViewコンソールログを有効または無効にします（デフォルト：無効） | `true` |


### `Collectors`

Collectorsは、デバイスから追加情報を収集し、データレイヤーに追加してからTealium Customer Data Hubに送信するモジュールです。いくつかのコレクターはコアライブラリに含まれており、他のコレクターは別のモジュールとしてオプションでインストールされます。

利用可能なコレクターを以下の表に示します：

| コレクター名 | TealiumConfig参照 |
| --- | --- |
| `AppData` (デフォルト) | `Collectors.AppData`|
| `Connectivity` (デフォルト) | `Collectors.Connectivity`|
| `DeviceData` | `Collectors.DeviceData`|
| `Lifecycle` | `Collectors.Lifecycle`|

これらのモジュールは、[`TealiumConfig`](https://docs.tealium.com/ja/platforms/flutter/api/tealium-config/)の`collectors`プロパティを使用して有効または無効にされます。


### `ConsentExpiry`

ユーザーの同意構成の有効期限を定義します。

| パラメータ | 型 | 説明 | 例 |
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
| `TimeUnit.MONTHS`| 月|


### `ConsentPolicy`

同意ポリシーを定義します。[`TealiumConfig`](https://docs.tealium.com/ja/platforms/flutter/api/tealium-config/)オブジェクトに同意ポリシーが定義されていない場合、同意マネージャーは無効になります。

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


<blockquote>
少なくとも1つのディスパッチャーが必要です。ディスパッチャーが指定されていない場合、トラッキングは行われません。
</blockquote>



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
| `Expiry.forever` | アプリがインストールされている間は決して期限切れになりません |
| `Expiry.untilRestart` | アプリが再起動するまで |

### `LogLevel`

`loglevel`プロパティを構成し、どの程度の情報がログに記録されるかを制御します。

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

データレイヤーで指定された `visitorIdentityKey` を使用して訪問の切り替えを可能にします。