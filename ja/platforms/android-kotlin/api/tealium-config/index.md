---
title: TealiumConfig
description: TealiumのAndroid（Kotlin）向けTealiumConfigクラスとメソッドのリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium-config/
---
## クラス: `TealiumConfig`

`TealiumConfig`クラスは、メインの`Tealium`クラスの構成オプションを構成するためのメソッドを提供します。以下のドキュメントでは、Kotlin向けの`TealiumConfig`クラスの一般的に使用されるメソッドとプロパティをまとめています。個々のモジュールは、有効になっている場合に`TealiumConfig`クラスの拡張機能を提供する場合があります。これらは関連するモジュールのドキュメントに記載されています。

| メソッド/プロパティ                                                             | 説明                                                                                  |
|:----------------------------------------------------------------------------|:---------------------------------------------------------------------------------------------|
| [`adobeVisitorAuthState`](#adobevisitorauthstate)                           | 訪問の現在の認証状態を構成します。                                                                                                                           |
| [`adobeVisitorCustomVisitorId`](#adobevisitorcustomvisitorid)               | Adobe ECIDに既知の訪問IDを構成します。初期化時に既知のECIDが変更された場合は、`linkECIDToKnownIdentifier`を呼び出して訪問IDを更新します。 |
| [`adobeVisitorDataProviderId`](#adobevisitordataproviderid)                 | ECIDを既知のIDにリンクする際に必要な、Adobeから提供されるデータプロバイダIDを構成します。                                                                              |
| [`adobeVisitorExistingEcid`](#adobevisitorexistingecid)                     | 新しいECIDを要求する代わりに、以前のインストールから使用する既存のECID（Adobe SDKなど）を構成します。                                                         |
| [`adobeVisitorOrgId`](#adobevisitororgid)                                   | `@`を含むAdobe Org IDを含む文字列を構成します。                                                                                                                    |
| [`adobeVisitorRetries`](#adobevisitorretries)                               | ECIDがない場合にリクエストが失敗する前に許可される無効な訪問IDのリトライ回数を構成します。ECIDがない場合でもトラッキングコールが送信されるようになります。                                      |
| [`autoTrackingBlocklistFilename`](#autotrackingblocklistfilename)           | ローカルのブロックリストファイルの名前を構成します。                                                  |
| [`autoTrackingBlocklistUrl`](#autotrackingblocklisturl)                     | リモートのブロックリストファイルのURLを構成します。                                                  |
| [`autoTrackingCollectorDelegate`](#autotrackingcollectordelegate)           | 自動トラッキングされるアクティビティのために実行されるグローバルデリゲートを構成します。                 |
| [`autoTrackingMode`](#autoTrackingBlocklistFilename)                        | AutoTrackingモジュールのトラッキングモードを構成します。                                          |
| [`consentExpiry`](#consentexpiry)                                           | ユーザーの同意選択の有効期限を構成します。                                                                                                                              |
| [`consentManagerEnabled`](#consentmanagerenabled)                           | 同意管理機能を有効化/無効化するためのオプションの`Boolean`値です。                                                                                                           |
| [`consentManagerPolicy`](#consentmanagerpolicy)                             | 適用する同意ポリシーを構成するためのオプションの`ConsentPolicy`です。                                                                                                  |
| [`consentManagerLoggingEnabled`](#consentmanagerloggingenabled)             | 同意の変更のログ記録を有効化/無効化するためのオプションの`Boolean`値です。                                                                                                                 |
| [`consentManagerLoggingUrl`](#consentmanagerloggingurl)                     | 同意のログ記録の更新先のためのオプションの`String`です。                                                                                                            |
| [`consentManagerLoggingProfile`](#consentmanagerloggingprofile)             | Tealium Collectがデータを送信するプロファイルを上書きするためのオプションの`String`です。                                                                                                            |
| [`deepLinkTrackingEnabled`](#deeplinktrackingenabled)                       | ディープリンクの自動トラッキングを有効化/無効化します。                                                                                                                            |
| [`existingVisitorId`](#existingvisitorid)                                   | 独自の一意の識別子を構成します。                                                                                                                            |
| [`hostedDataLayerMaxCacheTimeMinutes`](#hosteddatalayermaxcachetimeminutes) | ホストされたデータレイヤーデータの有効期限を構成します。                                                                                                                                |
| [`hostedDataLayerEventMappings`](#hosteddatalayereventmappings)             | ホストされたデータレイヤーモジュールがデータレイヤーIDを検索する際に使用するイベントマッピングを構成します。                                                                                     |
| [`logLevel`](#loglevel)                                                     | ログレベルを構成します。                                                                                                      |
| [`remoteAPIEnabled`](#remoteapienabled)                                     | `remote_api`イベントを有効化/無効化します。DispatchQueueモジュールを使用している場合は必須です。                                     |
| [`sessionCountingEnabled`](#sessioncountingenabled)                         | Tealium iQアカウントのセッションカウントを無効化します。TealiumのJavaScriptファイルを自己ホストしている場合に使用します。                                        |
| [`TealiumConfig`](#tealiumconfig)                                           | `TealiumConfig`のインスタンスを作成するコンストラクタメソッドです。                                                                                                                      |

### `adobeVisitorAuthState`

訪問の現在の認証状態を構成します。

例:

```java
config.adobeVisitorAuthState = AdobeAuthState.AUTH_STATE_AUTHENTICATED
config.adobeVisitorAuthState = AdobeAuthState.AUTH_STATE_LOGGED_OUT
config.adobeVisitorAuthState = AdobeAuthState.AUTH_STATE_UNKNOWN
```

### `adobeVisitorCustomVisitorId`

Adobe ECIDに既知の訪問IDを構成します。初期化時に既知のECIDが変更された場合は、[`linkECIDToKnownIdentifier`](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium/#linkecidtoknownidentifier)を呼び出して訪問IDを更新します。

```java
config.adobeVisitorCustomVisitorId = "20381482060927465156359999806251989655"
```

### `adobeVisitorDataProviderId`

ECIDを既知のIDにリンクする際に必要な、Adobeから提供されるデータプロバイダIDを構成します。

```java
config.adobeVisitorDataProviderId = "01"
```

### `adobeVisitorExistingEcid`

新しいECIDを要求する代わりに、以前のインストールから使用する既存のECID（Adobe SDKなど）を構成します。

例:

```java
config.adobeVisitorExistingEcid = "20381482060927465156359999806251989655"
```

### `adobeVisitorOrgId`

`@`を含むAdobe Org IDを含む文字列を構成します。Org IDが提供されていない場合、モジュールは初期化されず、Adobe ECIDは取得されません。Adobe ECIDなしでトラッキングコールは通常どおりに続行されます。

```java
config.adobeVisitorOrgId = STRING_VALUE
```

例:

```java
config.adobeVisitorOrgId = "1A2A111A111150AA0A110A12@AdobeOrg"
```

### `adobeVisitorRetries`

ECIDがない場合にリクエストが失敗する前に許可される無効な訪問IDのリトライ回数を構成します。ECIDがない場合でもトラッキングコールが送信されるようになります。

例:

```java
config.adobeVisitorRetries = 5
```

### `autoTrackingBlocklistFilename`

[AutoTrackingモジュール](https://docs.tealium.com/ja/platforms/android-kotlin/module-list/autotracking/#block-list)で使用するための構成です。

自動トラッキングから除外するアクティビティのリストを含むJSON形式のブロックリストファイルの名前を構成します。ファイルはAndroidの`assets`ディレクトリに配置する必要があります。

```kotlin
config.autoTrackingBlocklistFilename = "autotracking-blocklist.json"
```

### `autoTrackingBlocklistUrl`

[AutoTrackingモジュール](https://docs.tealium.com/ja/platforms/android-kotlin/module-list/autotracking/#block-list)で使用するための構成です。

自動トラッキングから除外するアクティビティのリストを含むJSON形式のブロックリストファイルのURLを構成します。

```kotlin
config.autoTrackingBlocklistUrl = "https://example.com/autotracking-blocklist.json"
```

### `autoTrackingCollectorDelegate`

[AutoTrackingモジュール](https://docs.tealium.com/ja/platforms/android-kotlin/module-list/autotracking/#custom-data)で使用するための構成です。

自動トラッキングモジュールによってトラッキングされるアクティビティのために実行されるグローバルデリゲートを構成します。特定のアクティビティに含まれるデータをカスタマイズするために、このデリゲートを編集します。

```kotlin
config.autoTrackingCollectorDelegate = myCollectorDelegate
```

### `autoTrackingMode`

[AutoTrackingモジュール](https://docs.tealium.com/ja/platforms/android-kotlin/module-list/autotracking/#custom-data)のトラッキングモードを構成します。

* `FULL`  
`@Autotracked(track=false)`で注釈が付けられていないすべてのアクティビティをトラッキングします。
* `ANNOTATED`  
`@Autotracked`で注釈が付けられたアクティビティのみをトラッキングします。
* `NONE`  
すべての自動トラッキングを無効にします（デバッグまたは開発ビルドの場合に使用します）。

```kotlin
config.autoTrackingMode = AutoTrackingMode.FULL
```

### `Collectors`

Collectorsは、デバイスから補足情報を収集し、Tealium Customer Data Hubに送信する前にデータレイヤーに追加するモジュールです。一部のCollectorsはコアライブラリに含まれており、他のものはオプションとして別のモジュールとしてインストールされます。

以下の表は、利用可能なCollectorsの一覧です。デフォルトのCollectorsは、コレクター名の横に`*`が付いています。

| Collector名  | TealiumConfigリファレンス   |
|:----------------|:--------------------------|
| `AdobeVisitor`  | `Collectors.AdobeVisitor` |
| `AppData`*      | `Collectors.AppData`      |
| `Connectivity`* | `Collectors.Connectivity` |
| `Device`        | `Collectors.Device`       |
| `Lifecycle`     | `Collectors.Lifecycle`    |

これらのモジュールは、[`TealiumConfig`](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium-config/)の`collectors`プロパティを使用して有効または無効にできます。

以下の例は、使用しているCollectorsのリストに追加する方法です:

```java
val config = TealiumConfig(collectors = mutableSetOf(Collectors.AdobeVisitor))
```

### `consentExpiry`

ユーザーの同意選択の有効期限を構成します。Tealiumの初期化前にこのプロパティを構成します。同意選択のデフォルトの有効期限は次のとおりです:

- CCPA: 395日
- GDPR: 365日

以下は、同意の有効期限を90日に構成する例です。

```java
config.consentExpiry = ConsentExpiry(90, TimeUnit.DAYS)
```

### `consentManagerEnabled`

ConsentManagerモジュールが有効かどうかを構成します。`consentManagerPolicy`を構成する必要もあります。

```java
config.consentManagerEnabled = true  // 有効化
```

### `consentManagerPolicy`

アプリ内で適用される`ConsentPolicy`を構成します。このポリシーは、関連する法的要件に従ってSDK内でDispatchesがキューに入れられ、破棄されるかどうかを制御します。

```java
config.consentManagerPolicy = ConsentPolicy.GDPR
```

### `consentManagerLoggingEnabled`

同意の変更をリモートサーバーに送信して記録するかどうかを構成します。

```java
config.consentManagerLoggingEnabled = true
```

### `consentManagerLoggingProfile`

データを送信するTealium Collectのプロファイルを上書きします。

```java
config.consentManagerLoggingProfile = "us-mobile"
```

### `consentManagerLoggingUrl`

同意のログ記録の更新先のURLを構成します。

```java
config.consentManagerLoggingUrl = url
```

### `deepLinkTrackingEnabled`

FacebookなどのソースからアプリへのリンクやQRトレースなどの標準的なディープリンクの自動トラッキングを有効化または無効化します。デフォルトで有効化されています。

```java
config.deepLinkTrackingEnabled = true
```

### `existingVisitorId`

`tealium_visitor_id`のデータレイヤー値を構成します。独自の一意の識別子を持っている場合に使用します。

```java
config.existingVisitorId = "8243d23b56d5488571027547bc72d93"
```

### `hostedDataLayerMaxCacheTimeMinutes`

ホストされたデータレイヤーデータの有効期限を構成します。このプロパティが構成されていない場合、ホストされたデータレイヤーアイテムはデフォルトで7日間保持され、この期間が経過するとTealiumから再ダウンロードされます。

```java
hostedDataLayerMaxCacheTimeMinutes = 30
```


<blockquote>
ホストされたデータレイヤーが頻繁に更新される場合、より低い値を構成するとネットワークリクエストが増えるため、バッテリー寿命に影響する可能性があります。
</blockquote>


### `hostedDataLayerEventMappings`

ホストされたデータレイヤーモジュールがデータレイヤーIDを検索する際に使用するイベントマッピングを構成します。キーはディスパッチの`tealium_event`キーの値です。

```java
hostedDataLayerEventMappings = mapOf("pdp" to "product_id")
```

### `logLevel`

ログレベルプロパティを構成して、ログに記録される情報の量を制御します。このプロパティを構成すると、`TealiumConfig`の`environment`プロパティからのデフォルト値が上書きされます。

ログレベルを次のいずれかの値に構成します:

| ログレベル | ログのアクティビティの説明                                                                       |
|:----------|:-----------------------------------------------------------------------------------------------|
| `DEV`     | アプリケーションのデバッグに使用されるデバッグレベルのイベント（開発環境で推奨）。|
| `QA`      | アプリケーションの進行状況を示す情報イベント。                        |
| `PROD`    | クリティカルなエラーや障害などのエラーイベント。                                             |
| `SILENT`  | ログを出力しません。                                                                                    |


```java
config.logLevel = LogLevel.DEV
```


<blockquote>
Android StudioのLogCatを使用して開発ログを表示します。Androidデバイスに接続してLogCatアプリで本番ログを表示します。
</blockquote>


### `remoteAPIEnabled`

`remote_api`イベントを有効化または無効化します。DispatchQueueモジュールを使用している場合は必須です。デフォルトは`false`です。

```swift
config.remoteAPIEnabled = true
```

### `sessionCountingEnabled`

Tealium iQアカウントのセッションカウントを無効化します。TealiumのJavaScriptファイルを自己ホストしている場合に使用します。デフォルトは`true`です。

```swift
config.sessionCountingEnabled = false
```

### `TealiumConfig`

`TealiumConfig`のインスタンスを作成するコンストラクタメソッドです。

```java
val config = TealiumConfig(
      application,
      account,
      profile,
      environment);
```

`TealiumConfig`インスタンスは、次のパラメータで構成されます:

| パラメータ    | タイプ          | 説明              | 例            |
|:--------------|:--------------|:-------------------------|:-------------------|
| `application` | `Application` | アプリケーションインスタンス | `applicationObj`   |
| `account`     | `String`      | Tealiumアカウント名     | `"companyXYZ"`     |
| `profile`     | `String`      | Tealiumプロファイル名     | `"main"`           |
| `environment` | `String`      | Tealium環境名 | `Environment.PROD` |

以下は例です:

```java
// Application.onCreate()内で実行されていると仮定します
val config = TealiumConfig(this, "ACCOUNT_NAME", "PROFILE_NAME", Environment.PROD)

// 必要なDispatchersを追加
config.dispatchers.addAll(setOf(CollectDispatcher, TagManagementDispatcher))

// 必要なModulesを追加
config.modules.add(VisitorService)

// 自動トラッキングモード
config.autoTrackingMode = AutoTrackingMode.FULL // (FULL, ANNOTATED, NONE)
```

### `timedEventTriggers`

タイムドイベントを自動的にトラッキングするための`EventTrigger`オブジェクトのリストです。

```kotlin
val config = TealiumConfig(…).apply {
  timedEventTriggers = mutableListOf(
     EventTrigger.forEventName(
       start_event,
       stop_event,
       timed_event_name)
  )  
}
```

以下は`EventTrigger`のパラメータです:  

| パラメータ          | タイプ      | 説明                                                           |
|:-------------------|:----------|:----------------------------------------------------------------------|
| `start_event`      | `String`  | タイムドイベントを開始するための`TealiumEvent`の名前                   |
| `stop_event`       | `String`  | タイムドイベントを停止するための`TealiumEvent`の名前                   |
| `timed_event_name` | `String?` | (オプション) タイムドイベントの名前（デフォルト: `"start_event::stop_event"`） |


