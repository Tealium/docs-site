---
title: APIリファレンス
description: Cordova向けにTealiumが提供するクラスとメソッドのリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/cordova/api/
---
## クラス：`Tealium`

以下に、Cordovaの`Tealium`クラスでよく使用されるメソッドの概要を示します。

| メソッド                                                    | 説明                                                                                     |
|:------------------------------------------------------------|:-----------------------------------------------------------------------------------------|
| [`addRemoteCommand()`](#addremotecommand)                   | リモートコマンドマネージャーにリモートコマンドを追加します。                             |
| [`addData()`](#adddata)                                     | 永続データレイヤーにデータを追加します。                                                 |
| [`gatherTrackData()`](#gathertrackdata)                     | コレクターとデータレイヤーからすべてのトラッキングデータを収集します。                   |
| [`getData()`](#getdata)                                     | データレイヤーから指定された値を取得します。                                             |
| [`getConsentCategories()`](#getconsentcategories)           | ユーザーが同意したカテゴリーを取得します。                                               |
| [`getConsentStatus()`](#getconsentwtatus)                   | ユーザーの同意ステータスを取得します。                                                   |
| [`getVisitorId()`](#getvisitorid)                           | 現在の訪問IDを取得します。                                                             |
| [`initialize()`](#initialize)                               | 構成パラメータを使用してTealiumを初期化します。                                          |
| [`joinTrace()`](#joinTrace)                                 | 指定されたIDのトレースに参加します。                                                     |
| [`leaveTrace()`](#leavetrace)                               | アクティブなトレースセッションから退出します。                                           |
| [`removeData()`](#removedata)                               | [`addData()`](#adddata)を使用して以前に構成された永続データを削除します。                |
| [`removeRemoteCommand()`](#removeremotecommand)             | リモートコマンドマネージャーからリモートコマンドを削除します。                           |
| [`setConsentCategories()`](#setconsentcategories)           | ユーザーの同意カテゴリーを構成します。                                                   |
| [`setConsentExpiryListener()`](#setconsentexpirylistener)   | 同意の有効期限切れリスナーまたはコールバックを構成します。                               |
| [`setConsentStatus()`](#setconsentstatus)                   | ユーザーの同意ステータスを構成します。                                                   |
| [`setVisitorServiceListener()`](#setvisitorservicelistener) | 訪問サービスのリスナーまたはコールバックを定義します。                                 |
| [`terminateInstance()`](#terminateinstance)                 | Tealiumインスタンスを無効化して破棄します。                                              |
| [`track()`](#track)                                         | イベントまたは画面表示をトラッキングします。                                             |

### `addRemoteCommand()`

リモートコマンドマネージャーにリモートコマンドを追加します。

```javascript
tealium.addRemoteCommand(id, callback);
```

| パラメータ | 型          | 説明                                                                                                                                                           | 例               |
|:-----------|:------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------|:-----------------|
| `id`       | `String`    | タグ構成にあるコマンドIDの名前                                                                                                                                | `"test_command"` |
| `callback` | `Function ` | リモートコマンドからレスポンスを受信した後に実行するコールバック関数。コールバックは、タグマッピングから取得したキーと値のペアのペイロードを返します。       | （例を参照）     |

例：

```javascript
tealium.addRemoteCommand("firebase", (payload) => {

  var eventName = payload["firebase_event_name"];
  var eventProperties = payload["firebase_event_properties"];

  analytics.logEvent(eventName, eventProperties);
});
```

### `addData()`
指定した有効期限で永続データ保存にデータを追加します。

```javascript
tealium.addData(data, expiry);
```

| パラメータ | 型                  | 説明                                                                                                      | 例                                        |
|:-----------|:--------------------|:----------------------------------------------------------------------------------------------------------|:------------------------------------------|
| `data`     | `Object`            | キーが文字列で、値が文字列または文字列の配列であるキーと値のペアのJSONオブジェクト                       | `{"persistent_key2" : "persistent_val2"}` |
| `expiry`   | [`Expiry`](#expiry) | データを永続化する期間                                                                                    | `Expiry.forever`                          |

### コレクター

コレクターは、デバイスから補足情報を収集し、その情報がTealium Customer Data Hubに送信される前にデータレイヤーへ追加するモジュールです。一部のコレクターはコアライブラリに含まれていますが、その他は任意で個別のモジュールとしてインストールします。

以下の表に、使用可能なコレクターを示します。デフォルトのコレクターは、コレクター名の横にある`*`で示されています。

| コレクター名    | TealiumConfigリファレンス   |
|:----------------|:----------------------------|
| `AppData`*      | `Collectors.AppData`        |
| `Connectivity`* | `Collectors.Connectivity`   |
| `Device`        | `Collectors.Device`         |
| `Lifecycle`     | `Collectors.Lifecycle`      |

これらのモジュールは、構成オブジェクトの`collectors`プロパティを使用して有効または無効にします。定数値は`window.tealium.utils.Collectors`から使用できます。

### ConsentExpiry

同意構成の有効期限を定義します。

| パラメータ | 型         | 説明                   | 例              |
|:-----------|:-----------|:-----------------------|:----------------|
| `time`     | `Number`   | 有効期限までの時間     | `90`            |
| `unit`     | `TimeUnit` | 有効期限までの時間単位 | `TimeUnit.days` |

例：

```javascript
var ConsentExpiry = tealium.utils.ConsentExpiry
var TimeUnit = tealium.utils.TimeUnit
ConsentExpiry.create(90, TimeUnit.days)
```

#### TimeUnit

| 値       | 説明 |
|:---------|:-----|
| .minutes | 分   |
| .hours   | 時間 |
| .months  | 月   |
| .days    | 日   |

### ConsentPolicy

準拠する同意ポリシーを定義します。`config`オブジェクトに同意ポリシーが定義されていない場合、同意マネージャーは無効になります。定数は`window.tealium.utils.ConsentPolicy`から使用できます。

例：

```javascript
var ConsentPolicy = tealium.utils.ConsentPolicy
var gdpr = ConsentPolicy.gdpr
```

| 値    | 説明 |
|:------|:-----|
| .gdpr | GDPR |
| .ccpa | CCPA |

### ディスパッチャー

ディスパッチャーは、データレイヤーのデータをTealiumエンドポイントに送信するモジュールです。現在、以下のディスパッチャーを使用できます。定数は`window.tealium.utils.Dispatchers`から使用できます。

| ディスパッチャー名 | TealiumConfigリファレンス      |
|:-------------------|:-------------------------------|
| `Collect`          | `Dispatchers.Collect`          |
| `RemoteCommands`   | `Dispatchers.RemoteCommands`   |
| `TagManagement`    | `Dispatchers.TagManagement`    |


<blockquote>
少なくとも1つのディスパッチャーが必要です。ディスパッチャーが指定されていない場合、データはどこにも送信されません。
</blockquote>

### Expiry

カスタムデータの有効期限を定義します。

例：

```javascript
Expiry.session
```

| 値             | 説明                                             |
|:---------------|:-------------------------------------------------|
| `session`      | 現在アクティブなセッションの存続期間。           |
| `untilRestart` | アプリが再起動するまで。                          |
| `forever`      | 削除されるまでのアプリの存続期間。                |

例：

```javascript
var Expiry = tealium.utils.Expiry
var session = Expiry.session
```

### `gatherTrackData()`

コレクターおよびデータレイヤーからすべてのトラッキングデータを収集します。

```javascript
tealium.gatherTrackData(callback)
```

| パラメータ | 型         | 説明                                                   |
|:-----------|:-----------|:-------------------------------------------------------|
| `callback` | `Function` | トラッキングデータオブジェクトを使用するコールバック関数 |

例：

```javascript
  tealium.gatherTrackData(function(data) {
    console.log(data)
  });
```

### `getData()`

永続データレイヤーから指定したキーの値を取得し、コールバック関数を介して返します。

```javascript
tealium.getData(key, callback);
```

| パラメータ | 型         | 説明                                               |
|:-----------|:-----------|:---------------------------------------------------|
| `key`      | `String`   | データレイヤーから取得するキー                     |
| `callback` | `Function` | キーに対応する取得値を使用するコールバック関数     |

例：

```javascript
tealium.getData(key, function(data) {
  console.log(data)
});
```

### `getConsentCategories()`

ユーザーが同意したカテゴリーを取得します。

```javascript
tealium.getConsentCategories(callback);
```

| パラメータ | 型         | 説明                                       |
|:-----------|:-----------|:-------------------------------------------|
| `callback` | `Function` | 同意カテゴリーを使用するコールバック関数   |

例：

```javascript
tealium.getConsentCategories(categories => {
    console.log("Consent Categories: " + categories)
});
```

### `getConsentStatus()`

ユーザーの訪問 ID を取得し、コールバック関数を介して返します。

```javascript
tealium.getConsentStatus(callback);
```

| パラメータ | 型         | 説明                                     |
|:-----------|:-----------|:-----------------------------------------|
| `callback` | `Function` | 同意ステータスを使用するコールバック関数 |

例：

```javascript
tealium.getConsentStatus(function(categories) {
  console.log("Consent Status: " + status)
})
```

### `getVisitorId()`

ユーザーの訪問 ID を取得し、コールバック関数を介して返します。

```javascript
tealium.getVisitorId(callback);
```

| パラメータ | 型         | 説明                                      | 例         |
|:-----------|:-----------|:------------------------------------------|:-----------|
| `callback` | `Function` | 訪問 ID を使用するコールバック関数      | （例を参照） |

例：

```javascript
tealium.getVisitorId(function(visitorId) {
  console.log("VisitorId: " + visitorId)
})
```

### `initialize()`

他のメソッドを呼び出す前に Tealium を初期化します。

```javascript
tealium.initialize(config);
```

| パラメータ | 型                                | 説明                                                     | 例           |
|:-----------|:----------------------------------|:---------------------------------------------------------|:-------------|
| `config`   | [`TealiumConfig`](#tealiumconfig) | Tealium の構成パラメータ                                 | （例を参照） |
| `callback` | `Function`                        | （任意）Tealium インスタンスの準備完了後に実行するコールバック関数 | （例を参照） |

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

指定した ID のトレースに参加します。Tealium Customer Data Hub の[トレース](https://docs.tealium.com/manage-traces/)機能について詳しくご覧ください。

```javascript
tealium.joinTrace(id);
```

| パラメータ | 型       | 説明                                  | 例         |
|:-----------|:---------|:--------------------------------------|:-----------|
| `id`       | `String` | CDH から取得したトレース ID           | `abc123xy` |

### `leaveTrace()`

トレースは、`leaveTrace()` メソッドが呼び出されるまで、アプリのセッション中はアクティブな状態を維持します。このメソッドを呼び出すと、以前参加したトレースから退出し、訪問セッションが終了します。

```javascript
tealium.leaveTrace();
```

### LogLevel

ログに記録する情報量を制御するログレベルプロパティを、次のいずれかの値に構成します。

| 値                | 説明                                               |
|:------------------|:---------------------------------------------------|
| `LogLevel.dev`    | アプリケーションの進行状況を示す情報イベント     |
| `LogLevel.qa`     | アプリケーションのデバッグに使用するデバッグレベルのイベント |
| `LogLevel.prod`   | 重大なエラーや障害などのエラーイベント             |
| `LogLevel.silent` | ログを記録しない（デフォルト）                     |

例：

`LogLevel.dev`

### `setConsentCategories()`

ユーザーの同意カテゴリーを構成します。カテゴリーを構成するには、文字列の配列を渡します。`ConsentStatus` が `.consented` に構成されるまでは、デフォルトで空の配列です。同意ステータスが `.consented` で、`setConsentCategories()` メソッドによってカテゴリーが指定されていない場合は、すべてのカテゴリーが構成されます。

```javascript
tealium.setConsentCategories(categories);
```

| パラメータ   | 型                    | 説明                             | 例                                                             |
|:-------------|:----------------------|:---------------------------------|:---------------------------------------------------------------|
| `categories` | `ConsentCategories[]` | ユーザー同意カテゴリーの配列     | `[ConsentCategories.email, ConsentCategories.personalization]` |

例：

```javascript
var ConsentCategories = tealium.utils.ConsentCategories;

tealium.setConsentCategories([ConsentCategories.analytics, ConsentCategories.email]);
```

#### ConsentCategories

| 値                | 説明               |
|:------------------|:-------------------|
| `analytics`       | アナリティクス     |
| `affiliates`      | アフィリエイト     |
| `displayAds`      | ディスプレイ広告   |
| `email`           | メール             |
| `personalization` | パーソナライゼーション |
| `search`          | 検索               |
| `social`          | ソーシャル         |
| `bigData`         | ビッグデータ       |
| `mobile`          | モバイル           |
| `engagement`      | エンゲージメント   |
| `monitoring`      | モニタリング       |
| `crm`             | CRM                |
| `cdp`             | CDP                |
| `cookieMatch`     | Cookie マッチ      |
| `misc`            | その他             |
### `setConsentExpiryListener()`
ユーザーの同意構成が [`ConsentExpiry`](#consentexpiry) に従って期限切れになった後に実行するコールバックを定義します。

```javascript
tealium.setConsentExpiryListener(callback);
```

| パラメータ | 型         | 説明                                 |
|:-----------|:-----------|:-------------------------------------|
| `callback` | `Function` | 同意の期限切れ後に実行するコード     |

例：

```javascript
tealium.setConsentExpiryListener(() => {
    print("Consent Expired");
});
```

### `setConsentStatus()`

ユーザーの同意ステータスを構成します。変更されるまでは、デフォルトで `.unknown` です。

```javascript
tealium.setConsentStatus(status);
```

| パラメータ | 型       | 説明                       | 例                        |
|:-----------|:---------|:---------------------------|:--------------------------|
| `status`   | `String` | ユーザーの同意ステータス   | `ConsentStatus.consented` |

例：

```javascript
var ConsentStatus = window.tealium.utils.ConsentStatus

tealium.setConsentStatus(ConsentStatus.consented);
```

#### ConsentStatus

| 値              | 説明                                 |
|:----------------|:-------------------------------------|
| `.consented`    | ユーザーは同意しています。           |
| `.notConsented` | ユーザーは同意していません。         |
| `.unknown`      | ユーザーが同意したか不明です。       |

### `setVisitorServiceListener()`
訪問プロファイルが更新されたときに実行するコールバックを定義します。更新された [`VisitorProfile`](#visitorprofile) は、コールバックのレスポンスとして渡されます。

VisitorService モジュールは、Tealium Customer Data Hub の[データレイヤーエンリッチメント](https://docs.tealium.com/about-data-layer-enrichment/)機能を実装します。

Customer Data Platform（CDP）のライセンスがあり、訪問プロファイルを使用してモバイルアプリケーションのユーザーエクスペリエンスを向上させる場合は、このモジュールの使用を推奨します。Customer Data Platform（CDP）のライセンスがない場合、訪問プロファイルは返されないため、このモジュールの使用は推奨されません。

```javascript
tealium.setVisitorServiceListener(callback);
```

| パラメータ | 型         | 説明                                               |
|:-----------|:-----------|:---------------------------------------------------|
| `callback` | `Function` | 更新された訪問プロファイルが返された後に実行するコード |

例：

```javascript
tealium.setVisitorServiceListener((profile) => {
    console.log(JSON.stringify(profile));
});
```

### `removeData()`
以前に `tealium.addData()` を使用して構成した永続データを削除します。

```javascript
tealium.removeData(keys);
```

| パラメータ | 型                | 説明                 | 例               |
|:-----------|:------------------|:---------------------|:-----------------|
| `keys`     | `Array (Strings)` | キー名の配列         | `["foo", "bar"]` |

### `removeRemoteCommand()`

リモートコマンドマネージャーからリモートコマンドを削除します。

```javascript
tealium.removeRemoteCommand(id);
```

| パラメータ | 型       | 説明                               | 例               |
|:-----------|:---------|:-----------------------------------|:-----------------|
| `id`       | `String` | 削除するコマンド ID の名前         | `"test_command"` |

例：

```javascript
tealium.removeRemoteCommand("firebase");
```

### TealiumEnvironment

環境には、3 つのデフォルト環境（Dev、QA、Prod）のいずれか、または Tealium のパブリッシュ先となる任意のカスタム環境を指定できます。これらの環境から 1 つを選択します。定数は `window.tealium.utils.Environment` から利用できます。

例：

```javascript
Environment.dev
```

| 値      | 説明       |
|:--------|:-----------|
| `.dev`  | 開発       |
| `.qa`   | QA/UAT     |
| `.prod` | 本番       |
### 構成

以下に、`config` オプションのプロパティとそのキーの概要を示します。

| パラメータ                     | 型                                          | 説明                                                                                                                                                                                                                                                        | 例                                                                                                            |
|:-------------------------------|:--------------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:--------------------------------------------------------------------------------------------------------------|
| `account`                      | `String`                                    | （必須）Tealiumのアカウント名                                                                                                                                                                                                                               | `"companyXYZ" `                                                                                               |
| `profile`                      | `String`                                    | （必須）Tealiumのプロファイル名                                                                                                                                                                                                                             | `"main"`                                                                                                      |
| `environment`                  | [`TealiumEnvironment`](#tealiumenvironment) | （必須）Tealiumの環境名                                                                                                                                                                                                                                     | `"Environment.dev"`                                                                                           |
| `dataSource`                   | `String`                                    | CDHデータソースキー                                                                                                                                                                                                                                         | `"abc123"`                                                                                                    |
| `collectors`                   | `Collectors[]`                              | （必須）Tealiumライブラリの初期化に使用する[`Collectors`](#collectors)のリストを構成します                                                                                                                                                                  | `[Collectors.AppData]`                                                                                        |
| `dispatchers`                  | `Dispatchers[]`                             | （必須）Tealiumライブラリの初期化に使用する[`Dispatchers`](#dispatchers)のリストを構成します                                                                                                                                                                | `[Dispatchers.Collect]`                                                                                       |
| `customVisitorId`              | `String`                                    | カスタム訪問IDを構成します                                                                                                                                                                                                                                | `ALK2398LSDKJ3289SLKJ3298SLKJ3`                                                                               |
| `memoryReportingEnabled`       | `Boolean`                                   | DeviceDataモジュールでメモリレポートを有効または無効にします（デフォルト：無効）。                                                                                                                                                                          | `true`                                                                                                        |
| `overrideCollectURL`           | `String`                                    | Tealium Collect URLをオーバーライドして、別のエンドポイントにデータを送信します。イベントバッチ処理機能を使用する場合は、`overrideCollectBatchURL`プロパティもオーバーライドしてください。                                                                  | `https://custom-domain.com/event`                                                                             |
| `overrideCollectBatchURL`      | `String`                                    | Tealium CollectのバッチURLをオーバーライドして、別のエンドポイントにデータを送信します。                                                                                                                                                                    | `https://custom-domain.com/batch-event`                                                                       |
| `overrideCollectProfile`       | `String`                                    | Tealium Collectプロファイルをオーバーライドして、別のTealiumプロファイルにデータを送信します。                                                                                                                                                              | `custom-profile`                                                                                              |
| `overrideCollectDomain`        | `String`                                    | Tealium Collect URL内のドメイン名をオーバーライドして、別のエンドポイントにデータを送信します。                                                                                                                                                            | `custom-domain`                                                                                               |
| `overrideLibrarySettingsURL`   | `String`                                    | パブリッシュ構成URLをオーバーライドします。                                                                                                                                                                                                                 | `https://custom-domain.com/mobile.html`                                                                       |
| `overrideTagManagementURL`     | `String`                                    | Tag Managementモジュールで使用されるデフォルトURLをオーバーライドします。Tealium JavaScriptファイルをセルフホスティングする場合に必要です。                                                                                                                 | `https://custom-domain.com/path/env/utag.js`                                                                  |
| `deepLinkTrackingEnabled`      | `Boolean`                                   | Facebookやその他のソースからアプリへのリンクなど、[標準ディープリンクの自動トラッキング](https://docs.tealium.com/ja/platforms/getting-started-mobile/deep-linking/#readout)とQRトレースを有効または無効にします。（デフォルト：有効）                                                  | `false`                                                                                                       |
| `qrTraceEnabled`               | `Boolean`                                   | [QRトレース](https://docs.tealium.com/ja/platforms/getting-started-mobile/trace/#how-it-works)を有効または無効にします。（デフォルト：有効）                                                                                                                                            | `false`                                                                                                       |
| `loglevel`                     | [`LogLevel`](#loglevel)                     | ログに記録する情報量を制御するログレベルプロパティを構成します（デフォルト：silent）                                                                                                                                                                | `LogLevel.dev`                                                                                                |
| `consentExpiry`                | [`ConsentExpiry`](#consentexpiry)           | ユーザーの同意構成の有効期限を構成します（デフォルトはポリシーによって異なります）                                                                                                                                                                     | `ConsentExpiry(90, TimeUnit.days)`                                                                            |
| `consentLoggingEnabled`        | `Boolean`                                   | 監査を目的として、同意ステータスのすべての変更をTealium Customer Data Hubに送信する[同意ログ](https://docs.tealium.com/consent-change-event-specifications/)機能を有効にします（デフォルト：有効）   | true                                                                                                          |
| `consentPolicy`                | [`ConsentPolicy`](#consentpolicy)           | CCPAやGDPRなどの同意ポリシーを構成します。このプロパティが構成されている場合にのみ、同意マネージャーが有効になります。                                                                                                                                                        | `ConsentPolicy.gdpr`                                                                                          |
| `lifecycleAutotrackingEnabled` | `Boolean`                                   | ライフサイクルの自動トラッキングを有効または無効にします（デフォルト：有効）                                                                                                                                                                                             | `false`                                                                                                       |
| `useRemoteLibrarySettings`     | `Boolean`                                   | [モバイルパブリッシュ構成](https://docs.tealium.com/create-mobile-profile/)を有効または無効にします（デフォルト：有効）。タグ管理でモバイルパブリッシュ構成を構成するか、この機能を無効にしてください。 | `false`                                                                                                       |
| `visitorServiceEnabled`        | `Boolean`                                   | [データレイヤーエンリッチメントAPI](https://docs.tealium.com/data-layer-enrichment-api/)を使用した訪問プロファイルの自動取得を有効または無効にします（デフォルト：無効）                                | `true`                                                                                                        |
| `remoteCommands`               | `RemoteCommand[]`                           | インスタンスの準備が完了したときに追加する[RemoteCommand](#RemoteCommand)オブジェクトのリストを構成します                                                                                                                                                                    | `[{ id: "hello-world", callback: (payload) => { console.log("hello-world: " + JSON.stringify(payload)); } }]` |
| `sessionCountingEnabled`       | `Boolean`                                   | タグ管理アカウントのセッションカウントを有効または無効にします。Tealium JavaScriptファイルをセルフホスティングしている場合は、これを`false`に構成してください（デフォルト：有効）                                                                                                 | `false`                                                                                                       |

### ディスパッチ

トラッキングするディスパッチのタイプを定義するインターフェイスです。

#### ビュー

画面ビューをトラッキングするには、`viewName`と任意の`dataLayer`を持つオブジェクトを[`track()`](#track)メソッドに渡します。これらは手動で指定するか、`tealium.utils.Dispatch.view(viewName, dataLayer)`のユーティリティメソッドを使用して指定できます。

```javascript
var Dispatch = tealium.utils.Dispatch;
var screenView = Dispatch.view(tealiumEvent, eventData);
tealium.track(screenView);
```

| パラメータ  | 型    | 説明      | 
|:------------|:--------|:-----------------|
| `tealiumEvent` | `string` | `tealium_event`属性として渡されるイベント名です。  | 
| `eventData` | `<string, object>` | （任意）イベントとともに送信するキーバリュー形式のデータです。 | 


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

// the following is equivalent
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

#### イベント

ビュー以外のイベントをトラッキングするには、`eventName`と任意の`eventData`を持つオブジェクトを[`track()`](#track)メソッドに渡します。これらは手動で指定するか、`tealium.utils.Dispatch.event(eventName, dataLayer)`のユーティリティメソッドを使用して指定できます。

```javascript
var Dispatch = tealium.utils.Dispatch;
var tealiumEvent= Dispatch.view(tealiumEvent, eventData);
tealium.track(tealiumEvent);
```

| パラメータ  | 型    | 説明      | 
|:------------|:--------|:-----------------|
| `tealiumEvent`  | `string`| `tealium_event`属性として渡されるイベント名です。 | 
| `eventData` | `Dictionary<string, object>` | （任意）イベントとともに送信するキーバリュー形式のデータです。 | 

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

// the following is equivalent
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

Tealiumライブラリを無効にし、すべてのモジュール参照を削除します。必要に応じて、新しいTealiumインスタンスを作成して再度有効にします。

```javascript
tealium.terminateIntance();
```

### `track()`

画面ビューまたはイベントを、任意の関連データとともにトラッキングします。

```javascript
tealium.track(tealiumEvent)
```

| パラメータ | 型     | 説明| 
|:-----------|:---------|:------------|
| `tealiumEvent` | `Object` | `tealium_event`属性として渡されるイベント名と、任意のイベントデータオブジェクトを持つTealium [`Dispatch`](#dispatch)です。 | 

イベントをトラッキングするには、[`TealiumEvent`](#event)オブジェクトを`track()`メソッドに渡します。

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

// the following is equivalent
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

訪問プロファイルは、各属性のわかりやすい名前を含むオブジェクトです。訪問属性と訪問属性のタイプを区別するための `currentVisit` プロパティがあります。添字を使用し、IDで各属性値にアクセスします。属性が存在しない場合は、`null` が返されます。例については、以下の一覧を参照してください。

**属性タイプ**

| パラメータ         | プロパティ                                                                                                       | 値                                                                                                                             |
|:-------------------|:-----------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------|
| `arraysOfBooleans` | ID: String、値: Boolean[]                                                                                     | `id: "5129", value: [true,false,true,true]`                                                                                       |
| `arraysOfNumbers`  | ID: String、値: Number[]                                                                                      | `id: "57", value: [4.82125, 16.8, 0.5714285714285714]`                                                                            |
| `arraysOfStrings`  | ID: String、値: String[]                                                                                      | `id: "5213", value: ["green shirts", "green shirts", "blue shirts"]`                                                              |
| `audiences`        | ID: String、値: String                                                                                        | `id: "tealiummobile\_demo\_103", value: "iOS Users"`                                                                              |
| `badges`           | ID: String、値: Boolean                                                                                       | `id: "2815", value: true`                                                                                                         |
| `booleans`         | ID: String、値: Boolean                                                                                       | `id: "4868", value: true`                                                                                                         |
| `currentVisit`     | 現在の訪問のvisitorProfileに含まれるすべての属性。現在の訪問プロファイルには、オーディエンスまたはバッジは含まれません。 | `TealiumCurrentVisitProfile(dates: ["5376": 1567536668080, "10": 1567536668000], booleans: ["4530": true], numbers: ["32": 3.8])` |
| `dates`            | ID: String、値: Number                                                                                        | `id: "22", value: 1567120112000`                                                                                                  |
| `numbers`          | ID: String、値: Number                                                                                        | `id: "5728", value: 4.82125`                                                                                                      |
| `setOfStrings`     | ID: String、値: Set(String)                                                                                   | `id: "5211", value: ["green shirts", "red shirts", "blue shirts"]`                                                                |
| `strings`          | ID: String、値: String                                                                                        | `id: "5380", value: "green shirts"`                                                                                               |
| `tallies`          | ID: String、値: Object                                                                                        | `"57": [["category 1": 2.0], "category 2": 1.0]]`                                                                                 |
| `tallyValue`       | ID: String、値: Number                                                                                        | `["category 1": 2.0]`                                                                                                             |


### RemoteCommand

構成済みのRemote Commandを定義するインターフェースです。

| 値      | 説明                                        |
|:-----------|:---------------------------------------------------|
| `id`       | RemoteCommandの一意の識別名   |
| `path`     | （任意）マッピングに使用するローカルファイル          |
| `url`      | （任意）マッピングに使用するリモートファイル         |
| `callback` | （任意）RemoteCommandのコールバック関数 |

パスとURLは任意ですが、指定する場合はいずれか一方のみを指定してください。タグ管理のタグによってマッピングを処理する場合は、両方とも省略します。

React Nativeアプリのスコープ内でコマンドを処理する場合は、コールバックを指定します。ハンドラーがすでにネイティブ側で登録されている場合は、コールバックを省略します。

次の例は、JavaScriptで処理されるコマンド用のローカルマッピングファイルです。   
```javascript
let localCommand: RemoteCommand = {
    id: "hello-world",
    path: "hello-mappings.json",
    callback: (payload) => {
        //...
    }
}
```

次の例は、ネイティブ側で処理されるコマンド用のリモートマッピングファイルです。   
```javascript
let remoteNativeCommand: RemoteCommand = {
    id: "hello-world",
    url: "https://you.domain.com/hello-mappings.json"
}
```