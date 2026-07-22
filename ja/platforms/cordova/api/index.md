---
title: API リファレンス
description: TealiumのCordova用クラスとメソッドのリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/cordova/api/
---
## クラス: `Tealium`

以下は、Cordovaの`Tealium`クラスでよく使用されるメソッドをまとめたものです。

| メソッド                                                      | 説明                                                                        |
|:------------------------------------------------------------|:-----------------------------------------------------------------------------------|
| [`addRemoteCommand()`](#addremotecommand)                   | リモートコマンドマネージャーにリモートコマンドを追加します。                               |
| [`addData()`](#adddata)                                     | 永続データレイヤーにデータを追加します。                                                |
| [`gatherTrackData()`](#gathertrackdata)                     | コレクターとデータレイヤーからすべてのトラックデータを収集します。                             |
| [`getData()`](#getdata)                                     | データレイヤーから指定された値を取得します。                                   |
| [`getConsentCategories()`](#getconsentcategories)           | ユーザーの同意したカテゴリを取得します。                                         |
| [`getConsentStatus()`](#getconsentwtatus)                   | ユーザーの同意状態を取得します。                                               |
| [`getVisitorId()`](#getvisitorid)                           | 現在の訪問IDを取得します。                                                  |
| [`initialize()`](#initialize)                               | 構成パラメータでTealiumを初期化します。                                 |
| [`joinTrace()`](#joinTrace)                                 | 指定されたIDでトレースに参加します。                                                   |
| [`leaveTrace()`](#leavetrace)                               | アクティブなトレースセッションを離れます。                                                       |
| [`removeData()`](#removedata)                               | 以前に[`addData()`](#adddata)を使用して構成された永続データを削除します。 |
| [`removeRemoteCommand()`](#removeremotecommand)             | リモートコマンドマネージャーからリモートコマンドを削除します。                          |
| [`setConsentCategories()`](#setconsentcategories)           | ユーザーの同意カテゴリを構成します。                                             |
| [`setConsentExpiryListener()`](#setconsentexpirylistener)   | 同意期限が切れたときのリスナーまたはコールバックを構成します。                                     |
| [`setConsentStatus()`](#setconsentstatus)                   | ユーザーの同意状態を構成します。                                                 |
| [`setVisitorServiceListener()`](#setvisitorservicelistener) | 訪問サービスリスナーまたはコールバックを定義します。                                  |
| [`terminateInstance()`](#terminateinstance)                 | Tealiumインスタンスを無効にして破棄します。                                        |
| [`track()`](#track)                                         | イベントまたは画面表示をトラックします。                                                      |

### `addRemoteCommand()`

リモートコマンドマネージャーにリモートコマンドを追加します。

```javascript
tealium.addRemoteCommand(id, callback);
```

| パラメータ | タイプ        | 説明                                                                                                                                                     | 例          |
|:-----------|:------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------|:-----------------|
| `id`       | `String`    | タグ構成からのコマンドIDの名前                                                                                                               | `"test_command"` |
| `callback` | `Function ` | リモートコマンドからの応答を受け取った後に実行するコールバック関数。このコールバックはタグマッピングからのキーと値のペアのペイロードを返します。 | (例を参照)    |

例:

```javascript
tealium.addRemoteCommand("firebase", (payload) => {

  var eventName = payload["firebase_event_name"];
  var eventProperties = payload["firebase_event_properties"];

  analytics.logEvent(eventName, eventProperties);
});
```

### `addData()`
指定された有効期限のために永続データ保存にデータを追加します。

```javascript
tealium.addData(data, expiry);
```
| パラメータ | タイプ                | 説明                                                                                                   | 例                                   |
|:-----------|:--------------------|:--------------------------------------------------------------------------------------------------------------|:------------------------------------------|
| `data`     | `Object`            | 文字列のキーと、値が文字列または文字列の配列であるキーと値のペアのJSONオブジェクト | `{"persistent_key2" : "persistent_val2"}` |
| `expiry`   | [`Expiry`](#expiry) | データを永続させる時間の長さ                                                                  | `Expiry.forever`                          |

### コレクター

コレクターは、デバイスから追加情報を収集し、Tealium Customer Data Hubに送信される前にデータレイヤーに追加するモジュールです。いくつかのコレクターはコアライブラリに含まれていますが、他のコレクターは別のモジュールとしてオプションでインストールされます。

以下の表は、利用可能なコレクターをリストしています。デフォルトのコレクターはコレクター名の隣に`*`が付けられています。

| コレクター名  | TealiumConfig 参照   |
|:----------------|:--------------------------|
| `AppData`*      | `Collectors.AppData`      |
| `Connectivity`* | `Collectors.Connectivity` |
| `Device`        | `Collectors.Device`       |
| `Lifecycle`     | `Collectors.Lifecycle`    |

これらのモジュールは、構成オブジェクトの`collectors`プロパティを使用して有効または無効にされ、定数値は`window.tealium.utils.Collectors`から利用可能です。

### ConsentExpiry

同意構成の有効期限を定義します

| パラメータ | タイプ       | 説明                          | 例         |
|:-----------|:-----------|:-------------------------------------|:----------------|
| `time`     | `Number`   | 有効期限までの時間 | `90`            |
| `unit`     | `TimeUnit` | 有効期限までの時間単位   | `TimeUnit.days` |

例:

```javascript
var ConsentExpiry = tealium.utils.ConsentExpiry
var TimeUnit = tealium.utils.TimeUnit
ConsentExpiry.create(90, TimeUnit.days)
```

#### TimeUnit

| 値    | 説明 |
|:---------|:------------|
| .minutes | 分     |
| .hours   | 時間       |
| .months  | 月      |
| .days    | 日        |

### ConsentPolicy

遵守すべき同意ポリシーを定義します。`config`オブジェクトに同意ポリシーが定義されていない場合、同意マネージャーは無効になります。定数は`window.tealium.utils.ConsentPolicy`から利用可能です。

例:

```javascript
var ConsentPolicy = tealium.utils.ConsentPolicy
var gdpr = ConsentPolicy.gdpr
```

| 値 | 説明 |
|:------|:------------|
| .gdpr | GDPR        |
| .ccpa | CCPA        |

### ディスパッチャー

ディスパッチャーは、データレイヤーからのデータをTealiumエンドポイントに送信するモジュールです。現在利用可能なディスパッチャーは以下の通りです - 定数は`window.tealium.utils.Dispatchers`から利用可能です。

| ディスパッチャー名  | TealiumConfig 参照      |
|:-----------------|:-----------------------------|
| `Collect`        | `Dispatchers.Collect`        |
| `RemoteCommands` | `Dispatchers.RemoteCommands` |
| `TagManagement`  | `Dispatchers.TagManagement`  |


<blockquote>
少なくとも1つのディスパッチャーが必要です。ディスパッチャーが指定されていない場合、データはどこにも送信されません。
</blockquote>

### 有効期限

カスタムデータの有効期限を定義します。

例：

```javascript
Expiry.session
```

| 値              | 説明                                       |
|:----------------|:-------------------------------------------|
| `session`       | 現在のアクティブセッションの寿命。         |
| `untilRestart`  | アプリが再起動するまで。                   |
| `forever`       | アプリの寿命が終了するまで、削除されるまで。|

例：

```javascript
var Expiry = tealium.utils.Expiry
var session = Expiry.session
```

### `gatherTrackData()`

コレクターやデータレイヤーからすべてのトラックデータを収集します。

```javascript
tealium.gatherTrackData(callback)
```

| パラメータ | タイプ       | 説明                                          |
|:-----------|:-----------|:---------------------------------------------|
| `callback` | `Function` | トラックデータオブジェクトを使用するコールバック関数 |

例：

```javascript
  tealium.gatherTrackData(function(data) {
    console.log(data)
  });
```

### `getData()`

永続データレイヤーで指定されたキーの値を取得し、コールバック関数の形で返します。

```javascript
tealium.getData(key, callback);
```

| パラメータ | タイプ       | 説明                                          |
|:-----------|:-----------|:---------------------------------------------|
| `key`      | `String`   | データレイヤーから取得するキー                  |
| `callback` | `Function` | キーの取得値を使用するコールバック関数           |

例：

```javascript
tealium.getData(key, function(data) {
  console.log(data)
});
```

### `getConsentCategories()`
ユーザーの同意したカテゴリを取得します。

```javascript
tealium.getConsentCategories(callback);
```

| パラメータ | タイプ       | 説明                                     |
|:-----------|:-----------|:----------------------------------------|
| `callback` | `Function` | 同意カテゴリを使用するコールバック関数     |

例：

```javascript
tealium.getConsentCategories(categories => {
    console.log("Consent Categories: " + categories)
});
```

### `getConsentStatus()`
ユーザーの訪問IDを取得し、コールバック関数の形で返します。

```javascript
tealium.getConsentStatus(callback);
```

| パラメータ | タイプ       | 説明                                 |
|:-----------|:-----------|:------------------------------------|
| `callback` | `Function` | 同意状態を使用するコールバック関数     |

例：

```javascript
tealium.getConsentStatus(function(categories) {
  console.log("Consent Status: " + status)
})
```

### `getVisitorId()`
ユーザーの訪問IDを取得し、コールバック関数の形で返します。

```javascript
tealium.getVisitorId(callback);
```

| パラメータ | タイプ       | 説明                             | 例             |
|:-----------|:-----------|:--------------------------------|:--------------|
| `callback` | `Function` | 訪問IDを使用するコールバック関数 | (例を参照)     |

例：

```javascript
tealium.getVisitorId(function(visitorId) {
  console.log("VisitorId: " + visitorId)
})
```

### `initialize()`

他のメソッドを呼び出す前にTealiumを初期化します。

```javascript
tealium.initialize(config);
```

| パラメータ | タイプ                              | 説明                                                      | 例             |
|:-----------|:----------------------------------|:---------------------------------------------------------|:--------------|
| `config`   | [`TealiumConfig`](#tealiumconfig) | Tealiumの構成パラメータ                                   | (例を参照)     |
| `callback` | `Function`                        | (オプション) Tealiumインスタンスが準備完了後のコールバック関数 | (例を参照)     |

例：

```javascript
let Environment = tealium.utils.Environment;
let Collectors = tealium.utils.Collectors;
let Dispatchers = tealium.utils.Dispatchers;
let ConsentPolicy = tealium.utils.ConsentPolicy;
let Expiry = tealium.utils.Expiry;

let config = {
    account: 'tealiummobile',
    profile: 'demo',
    environment: Environment.dev,
    dispatchers: [
        Dispatchers.Collect,
        Dispatchers.TagManagement,
        Dispatchers.RemoteCommands
    ],
    collectors: [
        Collectors.AppData,
        Collectors.DeviceData,
        Collectors.Lifecycle,
        Collectors.Connectivity
    ],
    consentLoggingEnabled: true,
    // consentExpiry: {
    //     'time': 10,
    //     'unit': 'days'
    // },
    // consentPolicy: ConsentPolicy.gdpr,
    lifecycleAutotrackingEnabled: true,
    batchingEnabled: false,
    visitorServiceEnabled: true,
    useRemoteLibrarySettings: false
};

window.tealium.initialize(config, function(success) {
    console.log("Init was: " + success)
    if(success) {
        tealium.setVisitorServiceListener(logVisitorUpdated)
        tealium.setConsentExpiryListener(logConsentExpired)
        tealium.addRemoteCommand("hello-world", logRemoteCommand)
    }
})
```

### `joinTrace()`

指定されたIDでトレースに参加します。Tealium Customer Data Hubの[Trace](https://docs.tealium.com/manage-traces/)機能について詳しくはこちらをご覧ください。

```javascript
tealium.joinTrace(id);
```

| パラメータ | タイプ     | 説明                     | 例          |
|:-----------|:---------|:------------------------|:-----------|
| `id`       | `String` | CDHから取得したトレースID | `abc123xy` |

### `leaveTrace()`

`leaveTrace()`メソッドが呼ばれるまで、アプリセッションの間トレースはアクティブのままです。このメソッドは以前に参加したトレースを離れ、訪問セッションを終了します。

```javascript
tealium.leaveTrace();
```

### ログレベル

ログレベルプロパティを構成し、どの程度の情報がログに記録されるかを制御します。次の値のいずれかに構成します：

| 値                 | 説明                                                         |
|:------------------|:------------------------------------------------------------|
| `LogLevel.dev`    | アプリケーションの進行を強調する情報イベント                   |
| `LogLevel.qa`     | アプリケーションのデバッグに使用されるデバッグレベルのイベント   |
| `LogLevel.prod`   | 重大なエラーや失敗などのエラーイベント                         |
| `LogLevel.silent` | ログなし（デフォルト）                                        |

例：

`LogLevel.dev`

### `setConsentCategories()`
ユーザーの同意カテゴリを構成します。カテゴリの配列を渡して構成します。デフォルトは空の配列で、`ConsentStatus`が`.consented`に構成されるまでです。同意状態が`.consented`で、`setConsentCategories()`メソッドでカテゴリが指定されていない場合、すべてのカテゴリが構成されます。

```javascript
tealium.setConsentCategories(categories);
```

| パラメータ     | タイプ                  | 説明                       | 例                                                                |
|:-------------|:----------------------|:--------------------------|:-----------------------------------------------------------------|
| `categories` | `ConsentCategories[]` | ユーザーの同意カテゴリの配列 | `[ConsentCategories.email, ConsentCategories.personalization]` |

例：

```javascript
var ConsentCategories = tealium.utils.ConsentCategories;

tealium.setConsentCategories([ConsentCategories.analytics, ConsentCategories.email]);
```

#### 同意カテゴリ

| 値                 | 説明             |
|:------------------|:----------------|
| `analytics`       | アナリティクス   |
| `affiliates`      | アフィリエイト   |
| `displayAds`      | ディスプレイ広告 |
| `email`           | メール           |
| `personalization` | パーソナライゼーション |
| `search`          | 検索             |
| `social`          | ソーシャル       |
| `bigData`         | ビッグデータ     |
| `mobile`          | モバイル         |
| `engagement`      | エンゲージメント |
| `monitoring`      | モニタリング     |
| `crm`             | CRM             |
| `cdp`             | CDP             |
| `cookieMatch`     | クッキーマッチ   |
| `misc`            | その他           |
### `setConsentExpiryListener()`
ユーザーの同意構成の有効期限が切れた後に実行するコールバックを定義します。[`ConsentExpiry`](#consentexpiry)に従います。

```javascript
tealium.setConsentExpiryListener(callback);
```

| パラメータ | タイプ       | 説明                               |
|:-----------|:-----------|:----------------------------------|
| `callback` | `Function` | 同意の有効期限が切れた後に実行するコード |

例:

```javascript
tealium.setConsentExpiryListener(() => {
    print("Consent Expired");
});
```

### `setConsentStatus()`

ユーザーの同意状態を構成します。デフォルトは変更されるまで `.unknown` です。

```javascript
tealium.setConsentStatus(status);
```

| パラメータ | タイプ     | 説明             | 例                          |
|:-----------|:---------|:----------------|:--------------------------|
| `status`   | `String` | ユーザーの同意状態 | `ConsentStatus.consented` |

例:

```javascript
var ConsentStatus = window.tealium.utils.ConsentStatus

tealium.setConsentStatus(ConsentStatus.consented);
```

#### ConsentStatus

| 値               | 説明                        |
|:----------------|:-------------------------------|
| `.consented`    | ユーザーが同意しています。            |
| `.notConsented` | ユーザーが同意していません。        |
| `.unknown`      | ユーザーが同意しているか不明です。 |

### `setVisitorServiceListener()`
訪問プロファイルが更新されたときに実行するコールバックを定義します。更新された[`VisitorProfile`](#visitorprofile)がコールバックの応答で提供されます。

VisitorServiceモジュールはTealium Customer Data Hubの[Data Layer Enrichment](https://docs.tealium.com/enable-data-layer-enrichment/)機能を実装しています。

このモジュールの使用は、Tealium AudienceStreamのライセンスを持っており、モバイルアプリケーションで訪問プロファイルを使用してユーザーエクスペリエンスを向上させたい場合に推奨されます。AudienceStreamのライセンスがない場合、訪問プロファイルが返されないため、このモジュールの使用は推奨されません。

```javascript
tealium.setVisitorServiceListener(callback);
```

| パラメータ | タイプ       | 説明                                                   |
|:-----------|:-----------|:------------------------------------------------------|
| `callback` | `Function` | 更新された訪問プロファイルが返された後に実行するコード |

例:

```javascript
tealium.setVisitorServiceListener((profile) => {
    console.log(JSON.stringify(profile));
});
```

### `removeData()`
以前に `tealium.addData()` を使用して構成された永続的なデータを削除します。

```javascript
tealium.removeData(keys);
```

| パラメータ | タイプ              | 説明        | 例              |
|:-----------|:------------------|:-----------|:-----------------|
| `keys`     | `Array (Strings)` | キー名の配列 | `["foo", "bar"]` |

### `removeRemoteCommand()`

リモートコマンドマネージャーからリモートコマンドを削除します。

```javascript
tealium.removeRemoteCommand(id);
```

| パラメータ | タイプ     | 説明                      | 例              |
|:-----------|:---------|:-------------------------|:-----------------|
| `id`       | `String` | 削除するコマンドIDの名前 | `"test_command"` |

例:

```javascript
tealium.removeRemoteCommand("firebase");
```

### TealiumEnvironment

環境はデフォルトの三つの環境（Dev, QA, Prod）またはTealiumが公開する任意のカスタム環境のいずれかです。これらの環境の中から選択します。定数は `window.tealium.utils.Environment` から利用可能です。

例:

```javascript
Environment.dev
```

| 値       | 説明         |
|:--------|:------------|
| `.dev`  | 開発         |
| `.qa`   | QA/UAT      |
| `.prod` | 本番         |
### 構成

以下は、`config` オプションとそのキーのプロパティをまとめたものです。

| パラメーター                     | タイプ                                        | 説明                                                                                                                                                                                                                                                 | 例                                                                                                       |
|:-------------------------------|:--------------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:--------------------------------------------------------------------------------------------------------------|
| `account`                      | `String`                                    | （必須）Tealiumアカウント名                                                                                                                                                                                                                             | `"companyXYZ" `                                                                                               |
| `profile`                      | `String`                                    | （必須）Tealiumプロファイル名                                                                                                                                                                                                                             | `"main"`                                                                                                      |
| `environment`                  | [`TealiumEnvironment`](#tealiumenvironment) | （必須）Tealium環境名                                                                                                                                                                                                                         | `"Environment.dev"`                                                                                           |
| `dataSource`                   | `String`                                    | CDHデータソースキー                                                                                                                                                                                                                                         | `"abc123"`                                                                                                    |
| `collectors`                   | `Collectors[]`                              | （必須）Tealiumライブラリを初期化するための[`Collectors`](#collectors)のリストを構成します                                                                                                                                                              | `[Collectors.AppData]`                                                                                        |
| `dispatchers`                  | `Dispatchers[]`                             | （必須）Tealiumライブラリを初期化するための[`Dispatchers`](#dispatchers)のリストを構成します                                                                                                                                                            | `[Dispatchers.Collect]`                                                                                       |
| `customVisitorId`              | `String`                                    | カスタム訪問IDを構成します                                                                                                                                                                                                                                    | `ALK2398LSDKJ3289SLKJ3298SLKJ3`                                                                               |
| `memoryReportingEnabled`       | `Boolean`                                   | DeviceDataモジュールでメモリレポートを有効または無効にします（デフォルト：無効）。                                                                                                                                                                          | `true`                                                                                                        |
| `overrideCollectURL`           | `String`                                    | Tealium Collect URLをオーバーライドして、データを別のエンドポイントに送信します。イベントバッチ機能を使用する場合は、`overrideCollectBatchURL`プロパティもオーバーライドしてください。                                                                                          | `https://custom-domain.com/event`                                                                             |
| `overrideCollectBatchURL`      | `String`                                    | Tealium CollectバッチURLをオーバーライドして、データを別のエンドポイントに送信します。                                                                                                                                                                               | `https://custom-domain.com/batch-event`                                                                       |
| `overrideCollectProfile`       | `String`                                    | Tealium Collectプロファイルをオーバーライドして、データを別のTealiumプロファイルに送信します。                                                                                                                                                                          | `custom-profile`                                                                                              |
| `overrideCollectDomain`        | `String`                                    | Tealium Collect URLのドメイン名をオーバーライドして、データを別のエンドポイントに送信します。                                                                                                                                                                  | `custom-domain`                                                                                               |
| `overrideLibrarySettingsURL`   | `String`                                    | 公開構成URLをオーバーライドします。                                                                                                                                                                                                                         | `https://custom-domain.com/mobile.html`                                                                       |
| `overrideTagManagementURL`     | `String`                                    | タグ管理モジュールで使用されるデフォルトURLをオーバーライドします。これは、TealiumのJavaScriptファイルを自己ホスティングする場合に必要です。                                                                                                                          | `https://custom-domain.com/path/env/utag.js`                                                                  |
| `deepLinkTrackingEnabled`      | `Boolean`                                   | [標準的なディープリンクの自動追跡](https://docs.tealium.com/ja/platforms/getting-started-mobile/deep-linking/#readout)を有効または無効にします。これには、FacebookなどのソースからアプリへのリンクやQRトレースも含まれます（デフォルト：有効）。                                        | `false`                                                                                                       |
| `qrTraceEnabled`               | `Boolean`                                   | [QRトレース](https://docs.tealium.com/ja/platforms/getting-started-mobile/trace/#how-it-works)を有効または無効にします（デフォルト：有効）。                                                                                                                                                           | `false`                                                                                                       |
| `loglevel`                     | [`LogLevel`](#loglevel)                     | ログレベルプロパティを構成し、ログに記録される情報の量を制御します（デフォルト：silent）                                                                                                                                                                | `LogLevel.dev`                                                                                                |
| `consentExpiry`                | [`ConsentExpiry`](#consentexpiry)           | ユーザーの同意の有効期限を構成します。（ポリシーに依存するデフォルト値）                                                                                                                                                                     | `ConsentExpiry(90, TimeUnit.days)`                                                                            |
| `consentLoggingEnabled`        | `Boolean`                                   | [同意ログ記録](https://docs.tealium.com/consent-change-event-specifications/)機能を有効にし、すべての同意状態の変更をTealium Customer Data Hubに送信して監査目的で使用します。（デフォルト：有効）   | true                                                                                                          |
| `consentPolicy`                | [`ConsentPolicy`](#consentpolicy)           | 同意ポリシー（CCPAまたはGDPRなど）を構成します。このプロパティが構成されている場合にのみ、Consent Managerが有効になります。                                                                                                                                                        | `ConsentPolicy.gdpr`                                                                                          |
| `lifecycleAutotrackingEnabled` | `Boolean`                                   | ライフサイクル自動追跡を有効または無効にします。（デフォルト：有効）                                                                                                                                                                                             | `false`                                                                                                       |
| `useRemoteLibrarySettings`     | `Boolean`                                   | [モバイル公開構成](https://docs.tealium.com/creating-a-mobile-profile/)を有効または無効にします（デフォルト：有効）。Tealium iQタグ管理でモバイル公開構成を構成するか、この機能を無効にします。 | `false`                                                                                                       |
| `visitorServiceEnabled`        | `Boolean`                                   | [Data Layer Enrichment API](https://docs.tealium.com/data-layer-enrichment-api/)を使用して訪問プロファイルの自動取得を有効または無効にします（デフォルト：無効）。                                | `true`                                                                                                        |
| `remoteCommands`               | `RemoteCommand[]`                           | インスタンスが準備完了時に追加する[RemoteCommand](#RemoteCommand)オブジェクトのリストを構成します。                                                                                                                                                                    | `[{ id: "hello-world", callback: (payload) => { console.log("hello-world: " + JSON.stringify(payload)); } }]` |
| `sessionCountingEnabled`       | `Boolean`                                   | Tealium iQアカウントのセッションカウントを有効または無効にします。TealiumのJavaScriptファイルを自己ホスティングしている場合は、これを`false`に構成します。（デフォルト：有効）                                                                                                 | `false`                                                                                                       |

### Dispatch

追跡するディスパッチのタイプを定義するインターフェースです。

#### View

画面ビューを追跡するには、`viewName`とオプションの`dataLayer`を持つオブジェクトを[`track()`](#track)メソッドに渡します。これらは手動で供給するか、`tealium.utils.Dispatch.view(viewName, dataLayer)`のユーティリティメソッドを介して供給することができます。

```javascript
var Dispatch = tealium.utils.Dispatch;
var screenView = Dispatch.view(tealiumEvent, eventData);
tealium.track(screenView);
```

| パラメータ  | タイプ    | 説明      | 
|:------------|:--------|:-----------------|
| `tealiumEvent` | `string` | `tealium_event`属性として渡されるイベント名。  | 
| `eventData` | `<string, object>` | オプション。キーと値の形式でイベントに送信されるデータ。 | 

```javascript
var Dispatch = tealium.utils.Dispatch;

var screenView = Dispatch.view(
  'purchase', 
  {
    "customer_id": "abc123", 
    "order_total": 10.00, 
    "product_id": ["PROD123", "PROD456"], 
    "order_id": "0123456789"
  }
);
tealium.track(screenView);

// 以下と同等です
tealium.track({
  type: "view",
  viewName: "purchase",
  dataLayer: {
    "customer_id": "abc123", 
    "order_total": 10.00, 
    "product_id": ["PROD123", "PROD456"], 
    "order_id": "0123345789"
  }
})
```

#### Event

ビュー以外のイベントを追跡するには、`eventName`とオプションの`eventData`を持つオブジェクトを[`track()`](#track)メソッドに渡します。これらは手動で供給するか、`tealium.utils.Dispatch.event(eventName, dataLayer)`のユーティリティメソッドを介して供給することができます。

```javascript
var Dispatch = tealium.utils.Dispatch;
var tealiumEvent= Dispatch.view(tealiumEvent, eventData);
tealium.track(tealiumEvent);
```

| パラメータ  | タイプ    | 説明      | 
|:------------|:--------|:-----------------|
| `tealiumEvent`  | `string`| `tealium_event`属性として渡されるイベント名。 | 
| `eventData` | `Dictionary<string, object>` | オプション。キーと値の形式でイベントに送信されるデータ。 | 

```javascript
var Dispatch = tealium.utils.Dispatch
var tealEvent = Dispatch.event(
  "cart_add", 
  {
    "customer_id": "abc123", 
    "product_id": ["PROD123", "PROD456"], 
    "product_price": [4.00, 6.00]
  }
)
tealium.track(tealEvent)

// 以下と同等です
tealium.track({
  type: "event",
  eventName: "cart_add",
  dataLayer: {
    "customer_id": "abc123", 
    "product_id": ["PROD123", "PROD456"], 
    "product_price": [4.00, 6.00]
  }
})
```

### `terminateIntance()`

Tealiumライブラリを無効にし、すべてのモジュール参照を削除します。必要に応じて新しいTealiumインスタンスを作成して再度有効にしてください。

```javascript
tealium.terminateIntance();
```

### `track()`

画面ビューまたはイベントをオプションの関連データとともに追跡します。

```javascript
tealium.track(tealiumEvent)
```

| パラメータ | タイプ     | 説明| 
|:-----------|:---------|:------------|
| `tealiumEvent` | `Object` | イベント名を`tealium_event`属性として持ち、オプションのイベントデータオブジェクトを持つTealium [`Dispatch`](#dispatch)。 | 

イベントを追跡するには、[`TealiumEvent`](#event)オブジェクトを`track()`メソッドに渡します：

```javascript
var Dispatch = tealium.utils.Dispatch
var tealEvent = Dispatch.event(
  "cart_add", 
  {
    "customer_id": "abc123", 
    "product_id": ["PROD123", "PROD456"], 
    "product_price": [4.00, 6.00]
  }
)
tealium.track(tealEvent)

// 以下と同等です
tealium.track({
  type: "event",
  eventName: "cart_add",
  dataLayer: {
    "customer_id": "abc123", 
    "product_id": ["PROD123", "PROD456"], 
    "product_price": [4.00, 6.00]
  }
})
```
### VisitorProfile

訪問プロファイルは、各属性に対してフレンドリーな名前を含むオブジェクトです。`currentVisit`プロパティを使用して、訪問/訪問属性タイプを区別できます。サブスクリプトを使用してIDで各属性値にアクセスします。属性が存在しない場合は`null`が返されます。以下のリストを参照してください。

**属性タイプ**

| パラメータ           | プロパティ                                                                                                       | 値                                                                                                                             |
|:-------------------|:-----------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------|
| `arraysOfBooleans` | id: String, value: Boolean[]                                                                                     | `id: "5129", value: [true,false,true,true]`                                                                                       |
| `arraysOfNumbers`  | id: String, value: Number[]                                                                                      | `id: "57", value: [4.82125, 16.8, 0.5714285714285714]`                                                                            |
| `arraysOfStrings`  | id: String, value: String[]                                                                                      | `id: "5213", value: ["green shirts", "green shirts", "blue shirts"]`                                                              |
| `audiences`        | id: String, value: String                                                                                        | `id: "tealiummobile\_demo\_103", value: "iOS Users"`                                                                              |
| `badges`           | id: String, value: Boolean                                                                                       | `id: "2815", value: true`                                                                                                         |
| `booleans`         | id: String, value: Boolean                                                                                       | `id: "4868", value: true`                                                                                                         |
| `currentVisit`     | 現在の訪問の訪問プロファイルのすべての属性。現在の訪問プロファイルにはAudiencesやBadgesは含まれません。 | `TealiumCurrentVisitProfile(dates: ["5376": 1567536668080, "10": 1567536668000], booleans: ["4530": true], numbers: ["32": 3.8])` |
| `dates`            | id: String, value: Number                                                                                        | `id: "22", value: 1567120112000`                                                                                                  |
| `numbers`          | id: String, value: Number                                                                                        | `id: "5728", value: 4.82125`                                                                                                      |
| `setOfStrings`     | id: String, value: Set(String)                                                                                   | `id: "5211", value: ["green shirts", "red shirts", "blue shirts"]`                                                                |
| `strings`          | id: String, value: String                                                                                        | `id: "5380", value: "green shirts"`                                                                                               |
| `tallies`          | id: String, value: Object                                                                                        | `"57": [["category 1": 2.0], "category 2": 1.0]]`                                                                                 |
| `tallyValue`       | id: String, value: Number                                                                                        | `["category 1": 2.0]`                                                                                                             |

### RemoteCommand

リモートコマンドを定義するインターフェース

| 値          | 説明                                                      |
|:-----------|:---------------------------------------------------------|
| `id`       | リモートコマンドの一意の識別名                            |
| `path`     | (オプション) マッピングに使用するローカルファイル         |
| `url`      | (オプション) マッピングに使用するリモートファイル         |
| `callback` | (オプション) リモートコマンドのコールバック関数           |

パスとURLはオプションですが、どちらか一方のみを提供するか、Tealium iQタグ管理でタグによってマッピングが処理される場合は両方を省略します。

コマンドがReact Nativeアプリの範囲内で処理される場合はコールバックを提供します。ハンドラが既にネイティブに登録されている場合はコールバックを省略します。

以下の例は、Javascriptによって処理されるコマンドのローカルマッピングファイルです：
```javascript
let localCommand: RemoteCommand = {
    id: "hello-world",
    path: "hello-mappings.json",
    callback: (payload) => {
        //...
    }
}
```

以下の例は、ネイティブに処理されるコマンドのリモートマッピングファイルです：
```javascript
let remoteNativeCommand: RemoteCommand = {
    id: "hello-world",
    url: "https://you.domain.com/hello-mappings.json"
}
```


