---
title: TealiumConfig
description: Android（Kotlin）向けにTealiumが提供するTealiumConfigクラスおよびメソッドのリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium-config/
---
## クラス：`TealiumConfig`

`TealiumConfig`クラスは、メインの`Tealium`クラスの構成オプションを構成するためのメソッドを提供します。以下では、Kotlin向けの`TealiumConfig`クラスで一般的に使用されるメソッドとプロパティについて説明します。また、有効化されている個別のモジュールによって、TealiumConfigクラスに独自の拡張機能が提供される場合があります。これらについては、各モジュールのドキュメントを参照してください。

| メソッド／プロパティ                                                        | 説明                                                                                         |
|:----------------------------------------------------------------------------|:---------------------------------------------------------------------------------------------|
| [`adobeVisitorAuthState`](#adobevisitorauthstate)                           | 訪問の現在の認証状態を構成します。 |
| [`adobeVisitorCustomVisitorId`](#adobevisitorcustomvisitorid)               | 初期化時に既知である場合、既知の訪問IDをAdobe ECIDに構成します。今後ECIDが変更された場合は、`linkECIDToKnownIdentifier`を呼び出して訪問IDを更新します。 |
| [`adobeVisitorDataProviderId`](#adobevisitordataproviderid)                 | Adobeから提供されるデータプロバイダーIDを構成します。このIDは、ECIDを既知のIDにリンクする際に必要です。 |
| [`adobeVisitorExistingEcid`](#adobevisitorexistingecid)                     | 新しいECIDをリクエストする代わりに、Adobe SDKなどの以前のインストールから取得した既存のECIDを使用するように構成します。 |
| [`adobeVisitorOrgId`](#adobevisitororgid)                                   | `@`部分を含むAdobe Org IDの文字列です。 |
| [`adobeVisitorRetries`](#adobevisitorretries)                               | リクエストが失敗するまでに許容される無効な訪問IDの再試行回数です。失敗した場合でも、ECIDなしでトラッキング呼び出しが送信されます。 |
| [`autoTrackingBlocklistFilename`](#autotrackingblocklistfilename)           | ローカルブロックリストファイルの名前を構成します。 |
| [`autoTrackingBlocklistUrl`](#autotrackingblocklisturl)                     | リモートブロックリストファイルのURLを構成します。 |
| [`autoTrackingCollectorDelegate`](#autotrackingcollectordelegate)           | 自動的にトラッキングされるアクティビティに対して実行されるグローバルデリゲートを構成します。 |
| [`autoTrackingMode`](#autoTrackingBlocklistFilename)                        | AutoTrackingモジュールのトラッキングモードを構成します。 |
| [`consentExpiry`](#consentexpiry)                                           | ユーザーの同意選択の有効期限を構成します。 |
| [`consentManagerEnabled`](#consentmanagerenabled)                           | 同意管理機能を有効または無効にするためのオプションの`Boolean`です。 |
| [`consentManagerPolicy`](#consentmanagerpolicy)                             | 準拠する同意機能を決定するためのオプションの`ConsentPolicy`です。 |
| [`consentManagerLoggingEnabled`](#consentmanagerloggingenabled)             | 同意変更のログ記録を有効または無効にするためのオプションの`Boolean`です。 |
| [`consentManagerLoggingUrl`](#consentmanagerloggingurl)                     | 同意ログの更新先を指定するオプションの`String`です。 |
| [`consentManagerLoggingProfile`](#consentmanagerloggingprofile)             | Tealium Collectがデータを送信するプロファイルを上書きするためのオプションの`String`です。 |
| [`deepLinkTrackingEnabled`](#deeplinktrackingenabled)                       | ディープリンクの自動トラッキングを有効または無効にします。 |
| [`existingVisitorId`](#existingvisitorid)                                   | 独自の一意の識別子を構成し、`tealium_visitor_id`に保存します。 |
| [`hostedDataLayerMaxCacheTimeMinutes`](#hosteddatalayermaxcachetimeminutes) | ホステッドデータレイヤーのデータに有効期限を構成します。 |
| [`hostedDataLayerEventMappings`](#hosteddatalayereventmappings)             | データレイヤーIDを検索する際にホステッドデータレイヤーモジュールが使用するイベントマッピングを構成します。 |
| [`logLevel`](#loglevel)                                                     | ログに記録する情報量を制御するログレベルプロパティを構成します。 |
| [`remoteAPIEnabled`](#remoteapienabled)                                     | `remote_api`イベントを有効または無効にします。DispatchQueueモジュールを使用している場合、RemoteCommandsモジュールに必要です。 |
| [`sessionCountingEnabled`](#sessioncountingenabled)                         | タグ管理アカウントのセッションカウントを無効にします。Tealium JavaScriptファイルをセルフホスティングする場合に使用してください。 |
| [`TealiumConfig`](#tealiumconfig)                                           | `TealiumConfig`のインスタンスを作成するコンストラクターメソッドです。 |
| [`timedEventTriggers`](#timedeventtriggers)                                 | 時間指定イベントを自動的にトラッキングするための`EventTrigger`オブジェクトのリストです。 |
| [`useRemoteLibrarySettings`](#useremotelibrarysettings)                     | [モバイルパブリッシュ構成](https://docs.tealium.com/create-mobile-profile/)を有効または無効にするためのオプションの`Boolean`です（デフォルト：無効）。タグ管理でモバイルパブリッシュ構成を構成するか、この機能を無効にしてください。 |

### `adobeVisitorAuthState`

訪問の現在の認証状態を構成します。

例：

```java
config.adobeVisitorAuthState = AdobeAuthState.AUTH_STATE_AUTHENTICATED
config.adobeVisitorAuthState = AdobeAuthState.AUTH_STATE_LOGGED_OUT
config.adobeVisitorAuthState = AdobeAuthState.AUTH_STATE_UNKNOWN
```

### `adobeVisitorCustomVisitorId`

初期化時に既知である場合、既知の訪問IDをAdobe ECIDに構成します。今後ECIDが変更された場合は、[`linkECIDToKnownIdentifier`](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium/#linkecidtoknownidentifier)を呼び出して訪問IDを更新します。

```java
config.adobeVisitorCustomVisitorId = "20381482060927465156359999806251989655"
```
### `adobeVisitorDataProviderId`

既知の ID に ECID をリンクする際に必要となる、Adobe から提供されたデータプロバイダー ID を構成します。

```java
config.adobeVisitorDataProviderId = "01"
```

### `adobeVisitorExistingEcid`

新しい ECID をリクエストする代わりに、Adobe SDK などの以前のインストール環境で使用していた既存の ECID を構成します。

例：

```java
config.adobeVisitorExistingEcid = "20381482060927465156359999806251989655"
```

### `adobeVisitorOrgId`

`@` 部分を含む Adobe Org ID の文字列です。Org ID が指定されていない場合、モジュールは初期化されず、訪問 ID は取得されません。トラッキング呼び出しは、Adobe ECID なしで通常どおり続行されます。

```java
config.adobeVisitorOrgId = STRING_VALUE
```

例：

```java
config.adobeVisitorOrgId = "1A2A111A111150AA0A110A12@AdobeOrg"
```

### `adobeVisitorRetries`

リクエストが失敗するまでに許容される、無効な訪問 ID に対する再試行回数です。リクエストが失敗した場合でも、トラッキング呼び出しは ECID なしで送信されます。

例：

```java
config.adobeVisitorRetries = 5
```

### `autoTrackingBlocklistFilename`

[AutoTracking モジュール](https://docs.tealium.com/ja/platforms/android-kotlin/module-list/autotracking/#block-list)で使用します。

自動トラッキングから除外するアクティビティのリストを含む、JSON 形式のブロックリストファイル名を構成します。このファイルは Android の `assets` ディレクトリに配置する必要があります。

```kotlin
config.autoTrackingBlocklistFilename = "autotracking-blocklist.json"
```

### `autoTrackingBlocklistUrl`

[AutoTracking モジュール](https://docs.tealium.com/ja/platforms/android-kotlin/module-list/autotracking/#block-list)で使用します。

自動トラッキングから除外するアクティビティのリストを含む、JSON 形式のブロックリストファイルの URL を構成します。

```kotlin
config.autoTrackingBlocklistUrl = "https://example.com/autotracking-blocklist.json"
```

### `autoTrackingCollectorDelegate`

[AutoTracking モジュール](https://docs.tealium.com/ja/platforms/android-kotlin/module-list/autotracking/#custom-data)で使用します。

[AutoTracking モジュール](https://docs.tealium.com/ja/platforms/android-kotlin/module-list/autotracking/)によってトラッキングされるアクティビティに対して実行されるグローバルデリゲートを構成します。特定のアクティビティに含めるデータをカスタマイズするには、このデリゲートを編集します。

```kotlin
config.autoTrackingCollectorDelegate = myCollectorDelegate
```

### `autoTrackingMode`

[AutoTracking モジュール](https://docs.tealium.com/ja/platforms/android-kotlin/module-list/autotracking/)のトラッキングレベルを構成します。

* `FULL`  
`@Autotracked(track=false)` が付与されたものを除く、すべてのアクティビティをトラッキングします。
* `ANNOTATED`  
`@Autotracked` が付与されたアクティビティのみをトラッキングします。
* `NONE`  
すべての自動トラッキングを無効にします（アプリのデバッグビルドまたは開発ビルド用）。

```kotlin
config.autoTrackingMode = AutoTrackingMode.FULL
```

### `Collectors`

コレクターは、デバイスから補足情報を収集し、Tealium Customer Data Hub に送信される前にデータレイヤーへ追加するモジュールです。一部のコレクターはコアライブラリに含まれていますが、その他はオプションであり、個別のモジュールとしてインストールされます。

次の表は、使用可能なコレクターの一覧です。デフォルトのコレクターは、コレクター名の横にある `*` で示されています。

| コレクター名  | TealiumConfig の参照   |
|:----------------|:--------------------------|
| `AdobeVisitor`  | `Collectors.AdobeVisitor` |
| `AppData`*      | `Collectors.AppData`      |
| `Connectivity`* | `Collectors.Connectivity` |
| `Device`        | `Collectors.Device`       |
| `Lifecycle`     | `Collectors.Lifecycle`    |

これらのモジュールは、[`TealiumConfig`](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium-config/) の `collectors` プロパティを使用して有効または無効にします。

次の例では、現在使用しているコレクターのリストに追加します。

```java
val config = TealiumConfig(collectors = mutableSetOf(Collectors.AdobeVisitor))
```

### `consentExpiry`

ユーザーが選択した同意構成の有効期限を構成します。このプロパティは、Tealium を初期化する前に構成してください。同意構成のデフォルトの有効期間は次のとおりです。

- CCPA：395 日
- GDPR：365 日

次の例では、同意の有効期限を 90 日に構成します。

```java
config.consentExpiry = ConsentExpiry(90, TimeUnit.DAYS)
```

### `consentManagerEnabled`

ConsentManager モジュールを有効にするかどうかを構成します。また、`consentManagerPolicy` を使用してポリシーを構成する必要があります。

```java
config.consentManagerEnabled = true  // enable
```

### `consentManagerPolicy`

アプリ内で準拠する `ConsentPolicy` を構成します。このポリシーは、関連する法的要件に従って、SDK 全体でディスパッチをキューに追加するか、破棄するかを制御します。

```java
config.consentManagerPolicy = ConsentPolicy.GDPR
```

### `consentManagerLoggingEnabled`

同意構成の変更を記録するために、リモートサーバーへ送信する必要があるかどうかを構成します。

```java
config.consentManagerLoggingEnabled = true
```

### `consentManagerLoggingProfile`

Tealium Collect がデータを送信するプロファイルを上書きします。

```java
config.consentManagerLoggingProfile = "us-mobile"
```

### `consentManagerLoggingUrl`

同意構成の変更を記録するときに使用する URL を構成します。

```java
config.consentManagerLoggingUrl = url
```

### `deepLinkTrackingEnabled`

Facebook やその他のソースからアプリへのリンクなど、標準的なディープリンクおよび QR Trace の自動トラッキングを有効または無効にします。デフォルトでは有効です。

```java
config.deepLinkTrackingEnabled = true
```

### `existingVisitorId`

`tealium_visitor_id` のデータレイヤー値を構成します。独自の一意な識別子がある場合に使用します。

```java
config.existingVisitorId = "8243d23b56d5488571027547bc72d93"
```

### `hostedDataLayerMaxCacheTimeMinutes`

ホステッドデータレイヤーのデータに有効期限を構成します。このプロパティが構成されていない場合、ホステッドデータレイヤーの項目はデフォルトで 7 日間保持され、この期間が経過すると Tealium から再度ダウンロードされます。

```java
hostedDataLayerMaxCacheTimeMinutes = 30
```


<blockquote>
ホステッドデータレイヤーが頻繁に更新される場合、値を小さく構成するとネットワークリクエストが増加し、バッテリー駆動時間に影響する可能性があります。
</blockquote>


### `hostedDataLayerEventMappings`

ホステッドデータレイヤーモジュールがデータレイヤー ID を取得するときに使用する、ホステッドデータレイヤーのキー（ルックアップ変数）を構成します。キーは、ディスパッチの `tealium_event` キーに含まれる値です。

```java
hostedDataLayerEventMappings = mapOf("pdp" to "product_id")
```

### `logLevel`

記録する情報量を制御するログレベルプロパティを構成します。このプロパティを構成すると、`TealiumConfig` の `environment` プロパティに基づくデフォルト値が上書きされます。

ログレベルを次のいずれかの値に構成します。

| ログレベル | ログアクティビティの説明                                                                       |
|:----------|:-----------------------------------------------------------------------------------------------|
| `DEV`     | アプリケーションのデバッグに使用するデバッグレベルのイベント（開発環境での使用を推奨）。|
| `QA`      | アプリケーションの進行状況を示す情報イベント。|
| `PROD`    | 重大なエラーや障害などのエラーイベント。|
| `SILENT`  | ログを記録しません。|

```java
config.logLevel = LogLevel.DEV
```


<blockquote>
開発ログは、Android Studio で LogCat を使用して表示します。本番環境のログは、Android デバイスを接続し、LogCat アプリを使用して表示します。
</blockquote>


### `remoteAPIEnabled`

`remote_api` イベントを有効または無効にします。DispatchQueue モジュールを使用している場合、RemoteCommands モジュールに必要です。デフォルトは `false` です。

```swift
config.remoteAPIEnabled = true
```

### `sessionCountingEnabled`

タグ管理アカウントのセッションカウントを無効にします。Tealium JavaScript ファイルをセルフホスティングしている場合に使用します。デフォルトは `true` です。

```swift
config.sessionCountingEnabled = false
```
### `TealiumConfig`

`TealiumConfig` インスタンスを作成するコンストラクターメソッドです。

```java
val config = TealiumConfig(
      application,
      account,
      profile,
      environment);
```

`TealiumConfig` インスタンスは、次のパラメータを使用して構成されます。

| パラメータ      | 型             | 説明                          | 例                 |
|:--------------|:--------------|:-----------------------------|:-------------------|
| `application` | `Application` | アプリケーションのインスタンス | `applicationObj`   |
| `account`     | `String`      | Tealium アカウント名           | `"companyXYZ"`     |
| `profile`     | `String`      | Tealium プロファイル名          | `"main"`           |
| `environment` | `String`      | Tealium 環境名                 | `Environment.PROD` |

次に例を示します。

```java
// Assuming execution is within Application.onCreate()
val config = TealiumConfig(this, "ACCOUNT_NAME", "PROFILE_NAME", Environment.PROD)

// Add required Dispatchers
config.dispatchers.addAll(setOf(CollectDispatcher, TagManagementDispatcher))

// Add required Modules
config.modules.add(VisitorService)

// Automatic tracking mode
config.autoTrackingMode = AutoTrackingMode.FULL // (FULL, ANNOTATED, NONE)
```

### `timedEventTriggers`

時間指定イベントを自動的にトラッキングするための `EventTrigger` オブジェクトのリストです。

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

`EventTrigger` のパラメータは次のとおりです。  

| パラメータ         | 型        | 説明                                                                    |
|:-------------------|:----------|:------------------------------------------------------------------------|
| `start_event`      | `String`  | 時間指定イベントを開始する `TealiumEvent` の名前                           |
| `stop_event`       | `String`  | 時間指定イベントを停止する `TealiumEvent` の名前                           |
| `timed_event_name` | `String?` | （任意）時間指定イベントの名前（デフォルト：`"start_event::stop_event"`） |

### `useRemoteLibrarySettings`

[モバイルパブリッシュ構成](https://docs.tealium.com/create-mobile-profile/)を有効または無効にするための任意の `Boolean` 値です（デフォルト：無効）。タグ管理でモバイルパブリッシュ構成を構成するか、この機能を無効にします。

```swift
config.useRemoteLibrarySettings = true
```