---
title: TealiumConfig
description: TealiumConfigクラスとTealiumが提供するメソッドのリファレンスガイド（Android Kotlin用）。
url: https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium-config/
---
## クラス: `TealiumConfig`

`TealiumConfig` クラスは、メインの `Tealium` クラスの構成オプションを構成するメソッドを提供します。以下のドキュメントは、Kotlin用の `TealiumConfig` クラスの一般的に使用されるメソッドとプロパティをまとめたものです。個々のモジュールが有効になっている場合、それらのモジュールは `TealiumConfig` クラスの独自の拡張を提供することもあります。これらは関連するモジュールのドキュメントで説明されています。

| メソッド/プロパティ                                                             | 説明                                                                                  |
|:----------------------------------------------------------------------------|:---------------------------------------------------------------------------------------------|
| [`adobeVisitorAuthState`](#adobevisitorauthstate)                           | 訪問の現在の認証状態を構成します。                                                                                                                           |
| [`adobeVisitorCustomVisitorId`](#adobevisitorcustomvisitorid)               | 初期化時に既知のAdobe ECIDがある場合、その訪問IDを構成します。将来ECIDが変更された場合は、[`linkECIDToKnownIdentifier`](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium/#linkecidtoknownidentifier)を呼び出して訪問IDを更新します。 |
| [`adobeVisitorDataProviderId`](#adobevisitordataproviderid)                 | Adobeから提供されるデータプロバイダーIDを構成します。これは、ECIDを既知のIDにリンクする際に必要です。                                                                              |
| [`adobeVisitorExistingEcid`](#adobevisitorexistingecid)                     | 以前のインストールからの既存のECIDを構成します。例えばAdobe SDKの代わりに新しいECIDを要求するのではなく、使用します。                                                         |
| [`adobeVisitorOrgId`](#adobevisitororgid)                                   | `@`部分を含むAdobe Org IDを含む文字列です。                                                                                                                    |
| [`adobeVisitorRetries`](#adobevisitorretries)                               | 無効な訪問IDのリトライが許可される回数を構成します。これにより、ECIDなしでトラッキングコールが送信される前にリクエストが失敗します。                                      |
| [`autoTrackingBlocklistFilename`](#autotrackingblocklistfilename)           | ローカルブロックリストファイルの名前を構成します。                                                  |
| [`autoTrackingBlocklistUrl`](#autotrackingblocklisturl)                     | リモートブロックリストファイルのURLを構成します。                                                  |
| [`autoTrackingCollectorDelegate`](#autotrackingcollectordelegate)           | 自動的に追跡されるアクティビティに対して実行されるグローバルデリゲートを構成します。                 |
| [`autoTrackingMode`](#autoTrackingBlocklistFilename)                        | AutoTrackingモジュールのトラッキングモードを構成します。                                          |
| [`consentExpiry`](#consentexpiry)                                           | ユーザーの同意選択の有効期限を構成します。                                                                                                                              |
| [`consentManagerEnabled`](#consentmanagerenabled)                           | 同意管理機能を有効/無効にするためのオプショナルな `Boolean` を構成します。                                                                                                           |
| [`consentManagerPolicy`](#consentmanagerpolicy)                             | どの同意機能に従うかを決定するためのオプショナルな `ConsentPolicy` を構成します。                                                                                                  |
| [`consentManagerLoggingEnabled`](#consentmanagerloggingenabled)             | 同意変更のログを有効/無効にするためのオプショナルな `Boolean` を構成します。                                                                                                                 |
| [`consentManagerLoggingUrl`](#consentmanagerloggingurl)                     | 同意ログ更新の送信先となるオプショナルな `String` を構成します。                                                                                                            |
| [`consentManagerLoggingProfile`](#consentmanagerloggingprofile)             | Tealium Collectがデータを送信するプロファイルを上書きするためのオプショナルな `String` を構成します。                                                                                                            |
| [`deepLinkTrackingEnabled`](#deeplinktrackingenabled)                       | ディープリンクの自動追跡を有効または無効にします。                                                                                                                            |
| [`existingVisitorId`](#existingvisitorid)                                   | 自分自身の一意の識別子を構成します。これは `tealium_visitor_id` に保存されます。                                                                                                                            |
| [`hostedDataLayerMaxCacheTimeMinutes`](#hosteddatalayermaxcachetimeminutes) | ホストされたデータレイヤーのデータの有効期限を構成します。                                                                                                                                |
| [`hostedDataLayerEventMappings`](#hosteddatalayereventmappings)             | データレイヤーIDを検索する際に使用されるイベントマッピングを構成します。                                                                                     |
| [`logLevel`](#loglevel)                                                     | ログレベルプロパティを構成します。これにより、ログに記録される情報の量が制御されます。                                                                                                      |
| [`remoteAPIEnabled`](#remoteapienabled)                                     | `remote_api` イベントを有効または無効にします。RemoteCommandsモジュールを使用する場合に必要です。                                     |
| [`sessionCountingEnabled`](#sessioncountingenabled)                         | Tealium iQアカウントのセッションカウントを無効にします。Tealium JavaScriptファイルを自己ホスティングする場合に使用してください。                                        |
| [`TealiumConfig`](#tealiumconfig)                                           | `TealiumConfig` のインスタンスを作成するコンストラクターメソッドです。                                                                                                                      |
| [`timedEventTriggers`](#timedeventtriggers)                                 | タイムドイベントを自動的に追跡するための `EventTrigger` オブジェクトのリストです。                                        |
| [`useRemoteLibrarySettings`](#useremotelibrarysettings)                     | [モバイルパブリッシュ構成](https://docs.tealium.com/create-mobile-profile/)を有効または無効にするためのオプショナルな `Boolean` を構成します（デフォルト：無効）。iQタグ管理でモバイルパブリッシュ構成を構成するか、この機能を無効にします。 |

### `adobeVisitorAuthState`

訪問の現在の認証状態を構成します。

例:

```java
config.adobeVisitorAuthState = AdobeAuthState.AUTH_STATE_AUTHENTICATED
config.adobeVisitorAuthState = AdobeAuthState.AUTH_STATE_LOGGED_OUT
config.adobeVisitorAuthState = AdobeAuthState.AUTH_STATE_UNKNOWN
```

### `adobeVisitorCustomVisitorId`

初期化時に既知のAdobe ECIDがある場合、その訪問IDを構成します。将来ECIDが変更された場合は、[`linkECIDToKnownIdentifier`](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium/#linkecidtoknownidentifier)を呼び出して訪問IDを更新します。

```java
config.adobeVisitorCustomVisitorId = "20381482060927465156359999806251989655"
```
### `adobeVisitorDataProviderId`

Adobeから提供されるデータプロバイダーIDを構成します。これは、既知のIDにECIDをリンクする際に必要です。

```java
config.adobeVisitorDataProviderId = "01"
```

### `adobeVisitorExistingEcid`

以前のインストールからの既存のECIDを構成します。例えばAdobe SDKのように、新しいECIDを要求する代わりに使用します。

例：

```java
config.adobeVisitorExistingEcid = "20381482060927465156359999806251989655"
```

### `adobeVisitorOrgId`

Adobe Org IDを含む文字列で、`@`部分を含みます。Org IDが提供されていない場合、モジュールは初期化されず、訪問IDは取得されません。トラッキングコールはAdobe ECIDなしで通常通り続けられます。

```java
config.adobeVisitorOrgId = STRING_VALUE
```

例：

```java
config.adobeVisitorOrgId = "1A2A111A111150AA0A110A12@AdobeOrg"
```

### `adobeVisitorRetries`

無効な訪問IDのリトライが許可される回数を構成します。リクエストが失敗すると、ECIDなしでトラッキングコールが送信されます。

例：

```java
config.adobeVisitorRetries = 5
```

### `autoTrackingBlocklistFilename`

[AutoTrackingモジュール](https://docs.tealium.com/ja/platforms/android-kotlin/module-list/autotracking/#block-list)で使用します。

自動トラッキングから除外するアクティビティのリストを含むJSON形式のブロックリストファイルの名前を構成します。ファイルはAndroidの`assets`ディレクトリに存在する必要があります。

```kotlin
config.autoTrackingBlocklistFilename = "autotracking-blocklist.json"
```

### `autoTrackingBlocklistUrl`

[AutoTrackingモジュール](https://docs.tealium.com/ja/platforms/android-kotlin/module-list/autotracking/#block-list)で使用します。

自動トラッキングから除外するアクティビティのリストを含むJSON形式のブロックリストファイルのURLを構成します。

```kotlin
config.autoTrackingBlocklistUrl = "https://example.com/autotracking-blocklist.json"
```

### `autoTrackingCollectorDelegate`

[AutoTrackingモジュール](https://docs.tealium.com/ja/platforms/android-kotlin/module-list/autotracking/#custom-data)で使用します。

[AutoTrackingモジュール](https://docs.tealium.com/ja/platforms/android-kotlin/module-list/autotracking/)によって追跡されるアクティビティに含まれるデータをカスタマイズするために実行されるグローバルデリゲートを構成します。

```kotlin
config.autoTrackingCollectorDelegate = myCollectorDelegate
```

### `autoTrackingMode`

[AutoTrackingモジュール](https://docs.tealium.com/ja/platforms/android-kotlin/module-list/autotracking/)のトラッキングレベルを構成します。

* `FULL`  
`@Autotracked(track=false)`で注釈されているものを除くすべてのアクティビティを追跡します。
* `ANNOTATED`  
`@Autotracked`で注釈されているアクティビティのみを追跡します。
* `NONE`  
すべての自動トラッキングを無効にします（アプリのデバッグまたは開発ビルド用）。

```kotlin
config.autoTrackingMode = AutoTrackingMode.FULL
```
### `TealiumConfig`

`TealiumConfig` インスタンスを作成するコンストラクタメソッド。

```java
val config = TealiumConfig(
      application,
      account,
      profile,
      environment);
```

以下のパラメータで構成された `TealiumConfig` インスタンス:

| パラメータ      | タイプ          | 説明                  | 例                  |
|:--------------|:--------------|:---------------------|:-------------------|
| `application` | `Application` | アプリケーションインスタンス | `applicationObj`   |
| `account`     | `String`      | Tealiumアカウント名   | `"companyXYZ"`     |
| `profile`     | `String`      | Tealiumプロファイル名 | `"main"`           |
| `environment` | `String`      | Tealium環境名         | `Environment.PROD` |

以下は例です:

```java
// Application.onCreate() 内で実行されると仮定
val config = TealiumConfig(this, "ACCOUNT_NAME", "PROFILE_NAME", Environment.PROD)

// 必要なディスパッチャーを追加
config.dispatchers.addAll(setOf(CollectDispatcher, TagManagementDispatcher))

// 必要なモジュールを追加
config.modules.add(VisitorService)

// 自動追跡モード
config.autoTrackingMode = AutoTrackingMode.FULL // (FULL, ANNOTATED, NONE)
```

### `timedEventTriggers`

タイムドイベントを自動的に追跡するための `EventTrigger` オブジェクトのリスト。

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

以下は `EventTrigger` のパラメータです:

| パラメータ            | タイプ      | 説明                                                           |
|:-------------------|:----------|:--------------------------------------------------------------|
| `start_event`      | `String`  | タイムドイベントを開始する `TealiumEvent` の名前                   |
| `stop_event`       | `String`  | タイムドイベントを停止する `TealiumEvent` の名前                    |
| `timed_event_name` | `String?` | (オプション) タイムドイベントの名前 (デフォルト: `"start_event::stop_event"`) |

### `useRemoteLibrarySettings`

[モバイルパブリッシュ構成](https://docs.tealium.com/create-mobile-profile/) を有効または無効にするためのオプションの `Boolean` (デフォルト: 無効)。iQタグ管理でモバイルパブリッシュ構成を構成するか、機能を無効にします。

```swift
config.useRemoteLibrarySettings = true
```