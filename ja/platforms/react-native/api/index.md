---
title: APIリファレンス
description: React Native向けにTealiumが提供するクラスとメソッドのリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/react-native/api/
---
## クラス：`Tealium`

以下は、React Nativeライブラリの`Tealium`クラスでよく使用されるメソッドの概要です。

| メソッド                                                    | 説明                                                                    |
|:------------------------------------------------------------|:------------------------------------------------------------------------|
| [`addRemoteCommand()`](#addRemoteCommand)                   | リモートコマンドマネージャーにリモートコマンドを追加します              |
| [`addData()`](#addData)                                     | 永続データレイヤーにデータを追加します                                  |
| [`gatherTrackData()`](#gatherTrackData)                     | コレクターとデータレイヤーからすべてのトラッキングデータを収集します    |
| [`getData()`](#getData)                                     | データレイヤーから指定された値を取得します                              |
| [`getConsentCategories()`](#getConsentCategories)           | ユーザーが同意したカテゴリーを取得します                                |
| [`getConsentStatus()`](#getConsentStatus)                   | ユーザーの同意ステータスを取得します                                    |
| [`getSessionId()`](#getSessionId)                           | 現在の`tealium_session_id`を取得します                                  |
| [`getVisitorId()`](#getVisitorId)                           | 現在の訪問IDを取得します                                              |
| [`initialize()`](#initialize)                               | 構成パラメータを使用してTealiumを初期化します                           |
| [`joinTrace()`](#joinTrace)                                 | 指定されたIDのトレースに参加します                                      |
| [`leaveTrace()`](#leaveTrace)                               | アクティブなトレースセッションから退出します                            |
| [`removeData()`](#removeData)                               | `addData()`を使用して以前に構成した永続データを削除します                |
| [`removeRemoteCommand()`](#removeRemoteCommand)             | リモートコマンドマネージャーからリモートコマンドを削除します            |
| [`setConsentCategories()`](#setConsentCategories)           | ユーザーの同意カテゴリーを構成します                                    |
| [`setConsentExpiryListener()`](#setConsentExpiryListener)   | 同意の有効期限切れリスナー／コールバックを構成します                    |
| [`setConsentStatus()`](#setConsentStatus)                   | ユーザーの同意ステータスを構成します                                    |
| [`setVisitorServiceListener()`](#setVisitorServiceListener) | 訪問サービスのリスナー／コールバックを定義します                      |
| [`terminateInstance()`](#terminateInstance)                 | Tealiumインスタンスを無効化して破棄します                               |
| [`track()`](#track)                                         | イベントまたは画面表示をトラッキングします                              |

### `addRemoteCommand()`

リモートコマンドマネージャーにリモートコマンドを追加します。

```javascript
Tealium.addRemoteCommand(id, callback);
```

| パラメータ | 型          | 説明                                                                                                                                                              | 例               |
|:-----------|:------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-----------------|
| `id`       | `String`    | タグ構成に含まれるコマンドIDの名前                                                                                                                                | `"test_command"` |
| `callback` | `Function ` | リモートコマンドから応答を受信した後に実行するコールバック関数。コールバックは、タグマッピングから取得したキーと値のペアをペイロードとして返します。              | （例を参照）     |

例：

```javascript
Tealium.addRemoteCommand("firebase", payload => {

  var eventName = payload["firebase_event_name"];
  var eventProperties = payload["firebase_event_properties"];

  analytics.logEvent(eventName, eventProperties);
});
```

### `addData()`

指定された有効期限で永続データ保存にデータを追加します。

```javascript
Tealium.addData(data, expiry);
```

| パラメータ | 型                  | 説明                                                                                              | 例                                        |
|:-----------|:--------------------|:--------------------------------------------------------------------------------------------------|:------------------------------------------|
| `data`     | `Object`            | キーと値のペアで構成されるJSONオブジェクト。キーは文字列で、値は文字列または文字列の配列です      | `{"persistent_key2" : "persistent_val2"}` |
| `expiry`   | [`Expiry`](#expiry) | データを永続化する期間                                                                            | `Expiry.forever`                          |

### コレクター

コレクターは、デバイスから補足情報を収集し、Tealium Customer Data Hubへ送信される前にデータレイヤーへ追加するモジュールです。一部のコレクターはコアライブラリに含まれていますが、それ以外はオプションで、個別のモジュールとしてインストールされます。

次の表に、利用可能なコレクターを示します。デフォルトのコレクターは、コレクター名の横に`*`を付けて示しています。

| コレクター名     | TealiumConfigリファレンス   |
|:-----------------|:----------------------------|
| `AppData`*       | `Collectors.AppData`        |
| `Connectivity`*  | `Collectors.Connectivity`   |
| `Device`         | `Collectors.Device`         |
| `Lifecycle`      | `Collectors.Lifecycle`      |
| `VisitorService` | `Collectors.VisitorService` |

以下で説明するように、これらのモジュールは[`TealiumConfig`](#tealiumconfig)の`collectors`プロパティを使用して有効または無効にします。

### ConsentExpiry

同意構成の有効期限を定義します。

| パラメータ | 型         | 説明                       | 例              |
|:-----------|:-----------|:---------------------------|:----------------|
| `time`     | `Number`   | 有効期限が切れるまでの時間 | `90`            |
| `unit`     | `TimeUnit` | 有効期限までの時間単位     | `TimeUnit.days` |

例：

`ConsentExpiry(90, TimeUnit.days)`

#### TimeUnit

| 値       | 説明 |
|:---------|:-----|
| .minutes | 分   |
| .hours   | 時間 |
| .months  | 月   |
| .days    | 日   |

### ConsentPolicy

準拠する同意ポリシーを定義します。[`TealiumConfig`](#tealiumconfig)オブジェクトに同意ポリシーが定義されていない場合、同意マネージャーは無効になります。

例：

`ConsentPolicy.gdpr`

| 値    | 説明 |
|:------|:-----|
| .gdpr | GDPR |
| .ccpa | CCPA |

### ディスパッチャー

ディスパッチャーは、データレイヤーからTealiumエンドポイントへデータを送信するモジュールです。現在、次のディスパッチャーを利用できます。

| ディスパッチャー名 | TealiumConfigリファレンス    |
|:-------------------|:-----------------------------|
| `Collect`          | `Dispatchers.Collect`        |
| `RemoteCommands`   | `Dispatchers.RemoteCommands` |
| `TagManagement`    | `Dispatchers.TagManagement`  |


<blockquote>
少なくとも1つのディスパッチャーが必要です。ディスパッチャーを指定しない場合、データはどこにも送信されません。
</blockquote>

### 有効期限

カスタムデータの有効期限を定義します。

例：

`Expiry.session`

| パラメータ | 型         | 説明                         | 例              |
|:-----------|:-----------|:-----------------------------|:----------------|
| `time`     | `Number`   | 有効期限が切れるまでの時間   | `90`            |
| `unit`     | `TimeUnit` | 有効期限が切れるまでの時間単位 | `TimeUnit.days` |

例：

`ConsentExpiry(90, TimeUnit.days)`

#### TimeUnit

| 値       | 説明 |
|:---------|:-----|
| .minutes | 分   |
| .hours   | 時間 |
| .months  | 月   |
| .days    | 日   |

### `gatherTrackData()`

Collector とデータレイヤーからすべてのトラッキングデータを収集します。

```javascript
Tealium.gatherTrackData(callback);
```

| パラメータ | 型         | 説明 | 例 |
|:-----------|:-----------|:-----|:---|
| `callback` | `Function` | 取得した値を使用するためのコールバック関数。コールバックは JSON オブジェクトを返します。 | （例を参照） |

例：

```javascript
Tealium.gatherTrackData(value => {
   console.log("Track data: " + JSON.stringify(value))
});
```

### `getData()`

永続データレイヤーから指定されたキーの値を取得し、コールバック関数の形式で返します。

```javascript
Tealium.getData(key, callback);
```

| パラメータ | 型         | 説明                                           | 例           |
|:-----------|:-----------|:-----------------------------------------------|:-------------|
| `key`      | `String`   | データレイヤーから取得するキー                 | （例を参照） |
| `callback` | `Function` | 取得したキーの値を使用するためのコールバック関数 | （例を参照） |

例：

```javascript
Tealium.getData('test_session_key', value => {
   console.log("Value: " + value)
});
```

### `getConsentCategories()`

ユーザーが同意したカテゴリを取得します。

```javascript
Tealium.getConsentCategories(callback);
```

| パラメータ | 型         | 説明                                           | 例           |
|:-----------|:-----------|:-----------------------------------------------|:-------------|
| `callback` | `Function` | 同意カテゴリを使用するためのコールバック関数   | （例を参照） |

例：

```javascript
Tealium.getConsentCategories(categories => {
    console.log("Consent Categories: " + categories)
});
```

### `getConsentStatus()`

ユーザーの同意ステータスを取得し、コールバック関数の形式で返します。

```javascript
Tealium.getConsentStatus(callback);
```

| パラメータ | 型         | 説明                                           | 例           |
|:-----------|:-----------|:-----------------------------------------------|:-------------|
| `callback` | `Function` | 同意ステータスを使用するためのコールバック関数 | （例を参照） |

例：

```javascript
Tealium.getConsentStatus(status => {
    console.log("Consent Status: " + status)
});
```

### `getSessionId()`

現在のセッション ID を取得し、コールバック関数の形式で返します。

```javascript
Tealium.getSessionId(callback);
```

| パラメータ | 型         | 説明                                         | 例           |
|:-----------|:-----------|:---------------------------------------------|:-------------|
| `callback` | `Function` | セッション ID を使用するためのコールバック関数 | （例を参照） |

例：

```javascript
Tealium.getSessionId(value => {
    console.log("Sesssion ID: " + value)
});
```

### `getVisitorId()`

ユーザーの訪問 ID を取得し、コールバック関数の形式で返します。

```javascript
Tealium.getVisitorId(callback);
```

| パラメータ | 型         | 説明                                       | 例           |
|:-----------|:-----------|:-------------------------------------------|:-------------|
| `callback` | `Function` | 訪問 ID を使用するためのコールバック関数 | （例を参照） |

例：

```javascript
Tealium.getVisitorId(value => {
    console.log("Visitor ID: " + value)
});
```

### `initialize()`

ほかのメソッドを呼び出す前に Tealium を初期化します。

```javascript
Tealium.initialize(config);
```

| パラメータ | 型                                | 説明                                                   | 例           |
|:-----------|:----------------------------------|:-------------------------------------------------------|:-------------|
| `config`   | [`TealiumConfig`](#tealiumconfig) | Tealium の構成パラメータ                               | （例を参照） |
| `callback` | `Function`                        | （任意）Tealium インスタンスの準備完了後に実行するコールバック関数 | （例を参照） |

例：

```javascript
let config: TealiumConfig =
{
	account: 'tealiummobile',
	profile: 'demo',
	environment: TealiumEnvironment.dev,
	dispatchers: [Dispatchers.Collect,
	 			  Dispatchers.TagManagement,
	  			  Dispatchers.RemoteCommands],
	collectors: [Collectors.AppData,
				 Collectors.DeviceData,
				 Collectors.Lifecycle,
				 Collectors.Connectivity],
	consentLoggingEnabled: true,
	consentPolicy: ConsentPolicy.gdpr,
	visitorServiceEnabled: true
};

Tealium.initialize(config, success => {
    if (!success) {
        // error creating instance.
    }
    // do something on-ready
});
```

### `joinTrace()`

指定した ID のトレースに参加します。Tealium Customer Data Hub の[トレース](https://docs.tealium.com/manage-traces/)機能について詳しく説明します。

```javascript
Tealium.joinTrace(id);
```

| パラメータ | 型       | 説明                         | 例         |
|:-----------|:---------|:-----------------------------|:-----------|
| `id`       | `String` | CDH から取得したトレース ID  | `abc123xy` |

### `leaveTrace()`

トレースは、`leaveTrace()` メソッドが呼び出されるまでアプリセッション中はアクティブなままです。このメソッドを呼び出すと、以前に参加したトレースから離脱し、訪問セッションが終了します。

```javascript
Tealium.leaveTrace();
```

### LogLevel

ログに記録する情報量を制御するログレベルプロパティを、次のいずれかの値に構成します。

| 値        | 説明                                                   |
|:----------|:-------------------------------------------------------|
| `.dev`    | アプリケーションの進行状況を示す情報イベント         |
| `.qa`     | アプリケーションのデバッグに使用するデバッグレベルのイベント |
| `.prod`   | 重大なエラーや障害などのエラーイベント               |
| `.silent` | ログを記録しない（デフォルト）                         |

例：

`LogLevel.dev`

### `setConsentCategories()`

ユーザーの同意カテゴリを構成します。カテゴリを構成するには、文字列の配列を渡します。`ConsentStatus` が `.consented` に構成されるまでは、デフォルトで空の配列になります。同意ステータスが `.consented` で、`setConsentCategories()` メソッドでカテゴリが指定されていない場合は、すべてのカテゴリが構成されます。

```javascript
Tealium.setConsentCategories(categories);
```

| パラメータ   | 型                    | 説明                         | 例                                                             |
|:-------------|:----------------------|:-----------------------------|:---------------------------------------------------------------|
| `categories` | `ConsentCategories[]` | ユーザー同意カテゴリの配列   | `[ConsentCategories.email, ConsentCategories.personalization]` |

例：

```javascript
Tealium.setConsentCategories([ConsentCategories.analytics, ConsentCategories.email]);
```
#### ConsentCategories

| 値                | 説明               |
|:------------------|:-------------------|
| `analytics`       | 分析               |
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
| `cookieMatch`     | Cookie Match       |
| `misc`            | その他             |

### `setConsentExpiryListener()`

ユーザーの同意構成が [`ConsentExpiry`](#consentexpiry) に従って期限切れになった後に実行するコールバックを定義します。

```javascript
Tealium.setConsentExpiryListener(callback);
```

| パラメータ | 型         | 説明                                     | 例         |
|:-----------|:-----------|:-----------------------------------------|:-----------|
| `callback` | `Function` | 同意の期限切れ後に実行するコード         | （例を参照） |

例：

```javascript
Tealium.setConsentExpiryListener(() => {
    console.log("Consent Expired");
});
```

### `setConsentStatus()`

ユーザーの同意ステータスを構成します。変更されるまでは、デフォルトで `.unknown` です。

```javascript
Tealium.setConsentStatus(status);
```

| パラメータ | 型              | 説明                     | 例                        |
|:-----------|:----------------|:-------------------------|:--------------------------|
| `status`   | `ConsentStatus` | ユーザーの同意ステータス | `ConsentStatus.consented` |

例：

```javascript
Tealium.setConsentStatus(ConsentStatus.consented);
```

#### ConsentStatus

| 値              | 説明       |
|:----------------|:-----------|
| `.consented`    | 同意済み   |
| `.notConsented` | 未同意     |
| `.unknown`      | 不明       |

### `setVisitorServiceListener()`

訪問プロファイルが更新されたときに実行するコールバックを定義します。更新された [`VisitorProfile`](#visitorprofile) は、コールバックのレスポンスで提供されます。

VisitorService モジュールは、Tealium Customer Data Hub の[データレイヤーエンリッチメント](https://docs.tealium.com/about-data-layer-enrichment/)機能を実装します。

Customer Data Platform（CDP）のライセンスを取得しており、訪問プロファイルを使用してモバイルアプリケーションのユーザーエクスペリエンスを向上させる場合は、このモジュールの使用を推奨します。Customer Data Platform（CDP）のライセンスを取得していない場合、訪問プロファイルは返されないため、このモジュールの使用は推奨されません。

```javascript
Tealium.setVisitorServiceListener(callback);
```

| パラメータ | 型         | 説明                                               | 例           |
|:-----------|:-----------|:---------------------------------------------------|:-------------|
| `callback` | `Function` | 更新された訪問プロファイルが返された後に実行するコード | （例を参照） |

例：

```javascript
Tealium.setVisitorServiceListener(profile => {
    console.log(JSON.stringify(profile["audiences"]));
});
```

### `removeData()`

以前に `Tealium.setPersistentData()` を使用して構成した永続データを削除します。

```javascript
Tealium.removeData(keys);
```

| パラメータ | 型         | 説明             | 例               |
|:-----------|:-----------|:-----------------|:-----------------|
| `keys`     | `String[]` | キー名の配列     | `["foo", "bar"]` |

### `removeRemoteCommand()`

リモートコマンドマネージャーからリモートコマンドを削除します。

```javascript
Tealium.removeRemoteCommand(id);
```

| パラメータ | 型       | 説明                           | 例               |
|:-----------|:---------|:-------------------------------|:-----------------|
| `id`       | `String` | 削除するコマンドIDの名前       | `"test_command"` |

例：

```javascript
Tealium.removeRemoteCommand("firebase");
```

### TealiumEnvironment

環境には、3つのデフォルト環境（Dev、QA、Prod）のいずれか、またはTealiumがパブリッシュする任意のカスタム環境を指定できます。これらの環境から1つを選択します。

例：

`TealiumEnvironment.dev`

| 値      | 説明       |
|:--------|:-----------|
| `.dev`  | 開発       |
| `.qa`   | QA/UAT     |
| `.prod` | 本番       |
### TealiumConfig

以下に、`TealiumConfig` クラスのプロパティをまとめます。

| パラメータ                     | 型                                          | 説明                                                                                                                                                                                                                                                 | 例                                                                                                            |
|:-------------------------------|:--------------------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:--------------------------------------------------------------------------------------------------------------|
| `account`                      | `String`                                    | （必須）Tealium アカウント名                                                                                                                                                                                                                         | `"companyXYZ" `                                                                                               |
| `profile`                      | `String`                                    | （必須）Tealium プロファイル名                                                                                                                                                                                                                       | `"main"`                                                                                                      |
| `environment`                  | [`TealiumEnvironment`](#tealiumenvironment) | （必須）Tealium 環境名                                                                                                                                                                                                                               | `"TealiumEnvironment.dev"`                                                                                    |
| `dataSource`                   | `String`                                    | CDH データソースキー                                                                                                                                                                                                                                 | `"abc123"`                                                                                                    |
| `collectors`                   | `Collectors[]`                              | （必須）Tealium ライブラリの初期化に使用する [`Collectors`](#collectors) のリストを構成します。                                                                                                                                                       | `[Collectors.AppData]`                                                                                        |
| `dispatchers`                  | `Dispatchers[]`                             | （必須）Tealium ライブラリの初期化に使用する [`Dispatchers`](#dispatchers) のリストを構成します。                                                                                                                                                     | `[Dispatchers.Collect]`                                                                                       |
| `customVisitorId`              | `String`                                    | カスタム訪問 ID を構成します。                                                                                                                                                                                                                     | `ALK2398LSDKJ3289SLKJ3298SLKJ3`                                                                               |
| `memoryReportingEnabled`       | `Boolean`                                   | DeviceData モジュールのメモリレポートを有効または無効にします（デフォルト：無効）。                                                                                                                                                                  | `true`                                                                                                        |
| `overrideCollectURL`           | `String`                                    | Tealium Collect URL を上書きし、別のエンドポイントにデータを送信します。イベントバッチ処理機能を使用する場合は、`overrideCollectBatchURL` プロパティも上書きしてください。                                                                           | `https://custom-domain.com/event`                                                                             |
| `overrideCollectBatchURL`      | `String`                                    | Tealium Collect のバッチ URL を上書きし、別のエンドポイントにデータを送信します。                                                                                                                                                                    | `https://custom-domain.com/batch-event`                                                                       |
| `overrideCollectProfile`       | `String`                                    | Tealium Collect プロファイルを上書きし、別の Tealium プロファイルにデータを送信します。                                                                                                                                                              | `custom-profile`                                                                                              |
| `overrideCollectDomain`        | `String`                                    | Tealium Collect URL のドメイン名を上書きし、別のエンドポイントにデータを送信します。                                                                                                                                                                 | `custom-domain`                                                                                               |
| `overrideLibrarySettingsURL`   | `String`                                    | パブリッシュ構成 URL を上書きします。                                                                                                                                                                                                                | `https://custom-domain.com/mobile.html`                                                                       |
| `overrideTagManagementURL`     | `String`                                    | Tag Management モジュールで使用されるデフォルト URL を上書きします。Tealium JavaScript ファイルをセルフホスティングする場合に必要です。                                                                                                              | `https://custom-domain.com/path/env/utag.js`                                                                  |
| `deepLinkTrackingEnabled`      | `Boolean`                                   | Facebook やその他のソースからアプリへのリンクなど、[標準ディープリンクの自動トラッキング](https://docs.tealium.com/ja/platforms/getting-started-mobile/deep-linking/#readout)および QR トレースを有効または無効にします（デフォルト：有効）。                                     | `false`                                                                                                       |
| `qrTraceEnabled`               | `Boolean`                                   | [QRトレース](https://docs.tealium.com/ja/platforms/getting-started-mobile/trace/#how-it-works)を有効または無効にします。（デフォルト：有効）                                                                                                                                                           | `false`                                                                                                       |
| `loglevel`                     | [`LogLevel`](#loglevel)                     | 記録する情報量を制御するログレベルプロパティを構成します。（デフォルト：サイレント）                                                                                                                                                                | `LogLevel.dev`                                                                                                |
| `consentExpiry`                | [`ConsentExpiry`](#consentexpiry)           | ユーザーの同意構成の有効期限を構成します。（デフォルトはポリシーによって異なります）                                                                                                                                                                     | `ConsentExpiry(90, TimeUnit.days)`                                                                            |
| `consentLoggingEnabled`        | `Boolean`                                   | 監査を目的として、すべての同意ステータスの変更をTealium Customer Data Hubに送信する[同意ログ](https://docs.tealium.com/consent-change-event-specifications/)機能を有効にします。（デフォルト：有効）   | true                                                                                                          |
| `consentPolicy`                | [`ConsentPolicy`](#consentpolicy)           | CCPAやGDPRなどの同意ポリシーを構成します。このプロパティが構成されている場合にのみ、同意マネージャーが有効になります。                                                                                                                                                        | `ConsentPolicy.gdpr`                                                                                          |
| `lifecycleAutotrackingEnabled` | `Boolean`                                   | ライフサイクルの自動トラッキングを有効または無効にします。（デフォルト：有効）                                                                                                                                                                                             | `false`                                                                                                       |
| `useRemoteLibrarySettings`     | `Boolean`                                   | [モバイルパブリッシュ構成](https://docs.tealium.com/create-mobile-profile/)を有効または無効にします。（デフォルト：有効）モバイルパブリッシュ構成は、タグ管理で構成するか、この機能を無効にします。 | `false`                                                                                                       |
| `visitorServiceEnabled`        | `Boolean`                                   | [データレイヤーエンリッチメントAPI](https://docs.tealium.com/data-layer-enrichment-api/)を使用した訪問プロファイルの自動取得を有効または無効にします。（デフォルト：無効）                                | `true`                                                                                                        |
| `sessionCountingEnabled`       | `Boolean`                                   | タグ管理アカウントのセッションカウントを有効または無効にします。Tealium JavaScriptファイルをセルフホスティングしている場合は、`false`に構成します。（デフォルト：有効）                                                                                                            | `false`                                                                                                        |
| `remoteCommands`               | `RemoteCommand[]`                           | インスタンスの準備が完了したときに追加する[RemoteCommand](#RemoteCommand)オブジェクトのリストを構成します                                                                                                                                                                    | `[{ id: "hello-world", callback: (payload) => { console.log("hello-world: " + JSON.stringify(payload)); } }]` |


### `terminateIntance()`

Tealiumライブラリを無効にし、すべてのモジュール参照を削除します。必要に応じて、新しいTealiumインスタンスを作成して再度有効にします。

`Tealium.terminateIntance();`

### `track()`

`TealiumEvent`または`TealiumView`ディスパッチを使用してイベントをトラッキングします。

`Tealium.track(dispatch);`

| パラメータ | 型      | 説明      | 
|:-----------|:----------|:-----------------|
| `tealEvent` | [`TealiumDispatch`](#tealiumdispatch) | イベント名とデータレイヤーを含むTealiumディスパッチ | 

```javascript
let tealEvent = new TealiumEvent(
    'cart_add', 
    {
        "customer_id": "abc123", 
        "product_id": ["PROD123", "PROD456"], 
        "product_price": [4.00, 6.00]
    }
);
Tealium.track(tealEvent);
```
### VisitorProfile

訪問プロファイルは、各属性のわかりやすい名前を含むオブジェクトです。訪問属性タイプと訪問属性タイプを区別できる `currentVisit` プロパティがあります。添字を使用して、ID から各属性値にアクセスします。属性が存在しない場合は `null` が返されます。例については、以下の一覧を参照してください。

**属性タイプ**

| パラメータ         | プロパティ                                                                                                       | 値                                                                                                                             |
|:-------------------|:-----------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------|
| `arraysOfBooleans` | ID：String、値：Boolean[]                                                                                     | `id: "5129", value: [true,false,true,true]`                                                                                       |
| `arraysOfNumbers`  | ID：String、値：Number[]                                                                                      | `id: "57", value: [4.82125, 16.8, 0.5714285714285714]`                                                                            |
| `arraysOfStrings`  | ID：String、値：String[]                                                                                      | `id: "5213", value: ["green shirts", "green shirts", "blue shirts"]`                                                              |
| `audiences`        | ID：String、値：String                                                                                        | `id: "tealiummobile\_demo\_103", value: "iOS Users"`                                                                              |
| `badges`           | ID：String、値：Boolean                                                                                       | `id: "2815", value: true`                                                                                                         |
| `booleans`         | ID：String、値：Boolean                                                                                       | `id: "4868", value: true`                                                                                                         |
| `currentVisit`     | 現在の訪問の visitorProfile に関するすべての属性。現在の訪問プロファイルにはオーディエンスまたはバッジは含まれません。 | `TealiumCurrentVisitProfile(dates: ["5376": 1567536668080, "10": 1567536668000], booleans: ["4530": true], numbers: ["32": 3.8])` |
| `dates`            | ID：String、値：Number                                                                                        | `id: "22", value: 1567120112000`                                                                                                  |
| `numbers`          | ID：String、値：Number                                                                                        | `id: "5728", value: 4.82125`                                                                                                      |
| `setOfStrings`     | ID：String、値：Set(String)                                                                                   | `id: "5211", value: ["green shirts", "red shirts", "blue shirts"]`                                                                |
| `strings`          | ID：String、値：String                                                                                        | `id: "5380", value: "green shirts"`                                                                                               |
| `tallies`          | ID：String、値：Object                                                                                        | `"57": [["category 1": 2.0], "category 2": 1.0]]`                                                                                 |
| `tallyValue`       | ID：String、値：Number                                                                                        | `["category 1": 2.0]`                                                                                                             |

### RemoteCommand

構成済みの Remote Command を定義するインターフェースです。

| 値      | 説明                                        |
|:-----------|:---------------------------------------------------|
| `id`       | RemoteCommand の一意の識別子名   |
| `path`     | （任意）マッピングに使用するローカルファイル          |
| `url`      | （任意）マッピングに使用するリモートファイル         |
| `callback` | （任意）RemoteCommand のコールバック関数 |

パスと URL は任意ですが、いずれか一方のみを指定するか、タグ管理のタグによってマッピングが処理される場合は両方とも省略してください。

React Native アプリのスコープ内でコマンドを処理する場合は、コールバックを指定します。ハンドラーがすでにネイティブ側で登録されている場合は、コールバックを省略してください。

次の例は、JavaScript で処理されるコマンド用のローカルマッピングファイルです。   
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

## インターフェース：`TealiumDispatch`

トラッキング対象のイベントタイプを定義するインターフェースです。次のクラスが `TealiumDispatch` を実装します。

### クラス：`TealiumEvent`

画面上でのユーザー操作をトラッキングするには、`TealiumEvent(tealiumEvent, dataLayer)` のインスタンスを [`track()`](#track) メソッドに渡します。`TealiumEvent` は、トラッキング呼び出しで `tealium_event` として表示されるイベント名と、任意のイベントデータオブジェクトで構成されます。

```javascript
let tealEvent = TealiumEvent(tealiumEvent, {eventData})
tealium?.track(tealEvent)
```

| パラメータ  | タイプ    | 説明      |
|:------------|:--------|:-----------------|
| `tealiumEvent` | `string` | `tealium_event` 属性として渡されるイベント名  |
| `eventData` | `object` | （任意）イベントとともにキーと値の形式で送信するデータ。 | 

例：

```javascript
let tealEvent = new TealiumEvent(
    'cart_add', 
    {
        "customer_id": "abc123", 
        "product_id": ["PROD123", "PROD456"], 
        "product_price": [4.00, 6.00]
    }
);
Tealium.track(tealEvent);
```

### クラス：`TealiumView`

画面表示をトラッキングするには、`TealiumView(tealiumEvent, dataLayer)` のインスタンスを [`Track()`](#track) メソッドに渡します。`TealiumView` は、トラッキング呼び出しで `tealium_event` として表示されるビュー名と、任意のデータディクショナリで構成されます。

```swift
let screenView = TealiumView(tealiumEvent, {eventData})
tealium?.track(screenView)
```

| パラメータ  | タイプ    | 説明      | 例    |
|:------------|:--------|:-----------------|:-----------|
| `tealiumEvent`  | `string`                     | ビューイベントまたは画面の `tealium_event` 名。          | `purchase`                                                 |
| `eventData` | `Dictionary<string, object>` | （任意）イベントとともにキーと値の形式で送信するデータ。 | `'purchase', {"customer_id", "abc123", "order_total": 10.00, "product_id": ["PROD123", "PROD456"], "order_id": "0123456789"}` |

例：

```javascript
let screenView = new TealiumView(
    'purchase', 
    {
        "customer_id": "abc123", 
        "order_total": 10.00, 
        "product_id": ["PROD123", "PROD456"], 
        "order_id": "0123456789"
    }
);
Tealium.track(screenView);
```