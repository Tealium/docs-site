---
title: API リファレンス
description: TealiumのUnity用クラスとメソッドのリファレンスガイドです。
url: https://docs.tealium.com/ja/platforms/unity/api/
---
## クラス: `Tealium`

以下は、Unityライブラリ用の`Tealium`クラスの一般的に使用されるメソッドをまとめたものです。

| メソッド                                                      | 説明                                                                   |
|:------------------------------------------------------------|:------------------------------------------------------------------------------|
| [`AddRemoteCommand()`](#addRemoteCommand)                   | リモートコマンドマネージャーにリモートコマンドを追加します。                          |
| [`AddToDataLayer()`](#addtodatalayer)                       | 永続データレイヤーにデータを追加します。                                           |
| [`GatherTrackData()`](#gathertrackdata)                     | コレクターとデータレイヤーからすべてのトラックデータを収集します。                         |
| [`GetFromDataLayer()`](#getfromdatalayer)                   | データレイヤーから指定された値を取得します。                                   |
| [`GetConsentCategories()`](#getConsentCategories)           | ユーザーの同意したカテゴリを取得します。                                         |
| [`GetConsentStatus()`](#getConsentStatus)                   | ユーザーの同意状態を取得します。                                               |
| [`GetVisitorId()`](#getVisitorId)                           | 現在の訪問IDを取得します。                                                  |
| [`Initialize()`](#initialize)                               | 構成パラメータでTealiumを初期化します。                            |
| [`JoinTrace()`](#joinTrace)                                 | 指定されたIDでトレースに参加します。                                              |
| [`LeaveTrace()`](#leaveTrace)                               | アクティブなトレースを離れ、訪問セッションを終了します。                          |
| [`RemoveFromDataLayer()`](#removefromdatalayer)             | `AddToDataLayer()`を使用して以前に構成された永続データを削除します。 |
| [`RemoveRemoteCommand()`](#removeRemoteCommand)             | リモートコマンドマネージャーからリモートコマンドを削除します。                     |
| [`SetConsentCategories()`](#setConsentCategories)           | ユーザーの同意カテゴリを構成します。                                        |
| [`SetConsentExpiryListener()`](#setConsentExpiryListener)   | 同意期限が切れたときのリスナーまたはコールバックを構成します。                                |
| [`SetConsentStatus()`](#setConsentStatus)                   | ユーザーの同意状態を構成します。                                            |
| [`SetVisitorServiceListener()`](#setVisitorServiceListener) | 訪問サービスのリスナーまたはコールバックを構成します。                                |
| [`Terminate()`](#terminate)                                 | Tealiumインスタンスを無効にして破棄します。                                   |
| [`Track()`](#track)                                         | ユーザーのゲームやゲームビューとのインタラクションをトラックします。                        |

### `AddRemoteCommand()`

リモートコマンドマネージャーにリモートコマンドを追加します。

```javascript
TealiumUnityPlugin.AddRemoteCommand(id, callback);
```

| パラメータ | 型             | 説明                                                                                                                                                     | 例          |
|:-----------|:-----------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------|:-----------------|
| `id`       | `string`         | タグ構成からのコマンドIDの名前です。                                                                                                              | `"test_command"` |
| `callback` | `Action<string>` | リモートコマンドからの応答を受け取った後に実行するコールバック関数です。タグマッピングからのキーと値のペアのペイロードを返します。 | (例を参照)    |

例:

```swift
TealiumUnityPlugin.AddRemoteCommand("firebase", (payload) => {

  string? eventName = (string)payload["firebase_event_name"];
  Dictionary<string, object>? eventProperties =
      (Dictionary<string, object>)payload["firebase_event_properties"];

  if (eventName != null) {
    analytics().logEvent(eventName, eventProperties);
  }
});
```

### `AddToDataLayer()`

指定された有効期限で永続データ保存にデータを追加します。

```javascript
TealiumUnityPlugin.AddToDataLayer(data, expiry);
```

| パラメータ | 型                         | 説明                                                                                                    | 例                                             |
|:-----------|:-----------------------------|:---------------------------------------------------------------------------------------------------------------|:----------------------------------------------------|
| `data`     | `Dictionary<string, object>` | 文字列のキーと文字列または文字列の配列の値を持つキーと値のペアのJSONオブジェクトです。 | `new Dictionary<string, object> {{"KEY", "VALUE"}}` |
| `expiry`   | [`Expiry`](#expiry)          | データを永続させる時間の長さです。                                                                  | `Expiry.Forever`                                    |

### `Collectors`

コレクターは、デバイスから補足情報を収集し、それをデータレイヤーに追加してからTealium Customer Data Hubに送信します。いくつかのコレクターはコアライブラリに含まれており、他のコレクターは別のモジュールとしてインストールされています。

以下の表は、利用可能なコレクターをリストしています。デフォルトのコレクターはコレクター名の隣に`*`が付けられています。

| コレクター名   | `TealiumConfig` 参照   |
|:-----------------|:----------------------------|
| `AppData`*       | `Collectors.AppData`        |
| `Connectivity`*  | `Collectors.Connectivity`   |
| `Device`         | `Collectors.Device`         |
| `Lifecycle`      | `Collectors.Lifecycle`      |
| `VisitorService` | `Collectors.VisitorService` |

### `ConsentExpiry`

同意構成の有効期限を定義します。

```javascript
ConsentExpiry(time, unit)
```

| パラメータ | 型       | 説明                           | 例         |
|:-----------|:-----------|:--------------------------------------|:----------------|
| `time`     | `Number`   | 有効期限までの時間です。 | `90`            |
| `unit`     | `TimeUnit` | 有効期限までの時間単位です。   | `TimeUnit.Days` |

例:

```javascript
new ConsentExpiry(90, TimeUnit.Days)
```

#### TimeUnit

以下は時間単位の値です：

| 値                   | 説明               |
|:------------------------|:--------------------------|
| `ConsentExpiry.Minutes` | 分単位の時間です。 |
| `ConsentExpiry.Hours`   | 時間単位の時間です。   |
| `ConsentExpiry.Months`  | 月単位の時間です。  |
| `ConsentExpiry.Days`    | 日単位の時間です。    |

### `ConsentPolicy`

遵守すべき同意ポリシーを定義します。[`TealiumConfig`](#class-tealiumconfig)オブジェクトに同意ポリシーが定義されていない場合、同意マネージャーは無効になります。

| 値                | 説明              |
|:---------------------|:-------------------------|
| `ConsentPolicy.GDPR` | GDPR同意ポリシーです。 |
| `ConsentPolicy.CCPA` | CCPA同意ポリシーです。 |

例:

```javascript
ConsentPolicy.GDPR
```
### `Dispatchers`

ディスパッチャーは、データレイヤーからのデータをTealiumエンドポイントに送信するモジュールです。現在利用可能なディスパッチャーは以下の通りです：

| ディスパッチャー名  | `TealiumConfig` 参照    |
|:-----------------|:-----------------------------|
| `Collect`        | `Dispatchers.Collect`        |
| `RemoteCommands` | `Dispatchers.RemoteCommands` |
| `TagManagement`  | `Dispatchers.TagManagement`  |


<blockquote>
少なくとも1つのディスパッチャーが必要です。ディスパッチャーが指定されていない場合、データはデータレイヤーに送信されません。
</blockquote>


### `Expiry`

カスタムデータの有効期限を定義します。

| 値              | 説明                                            |
|:---------------|:-------------------------------------------------------|
| `Session`      | 現在のアクティブセッションの寿命。            |
| `UntilRestart` | アプリが再起動するまで。                                |
| `Forever`      | アプリが削除されるまでのアプリの寿命。 |

例：

```javascript
Expiry.session
```

### `GatherTrackData()`
コレクターとデータレイヤーからすべてのトラックデータを収集します。

```javascript
Tealium.GatherTrackData(callback);
```

| パラメータ | タイプ       | 説明                                          | 例       |
|:-----------|:-----------|:-----------------------------------------------------|:--------------|
| `callback` | `Function` | トラッキングデータを受け取り処理するコールバック関数。コールバックはJSONオブジェクトを返します。 | (例を参照) |

例：

```javascript
Tealium.GatherTrackData(callback => {
  string? serializedPayload = JsonConvert.SerializeObject(callback);
  if (serializedPayload != null) {
      TealiumLogger.Log($"Track Data: {serializedPayload}");
  }
});
```

### `GetFromDataLayer()`

永続データレイヤーで指定されたキーの値を取得し、コールバック関数の形で返します。

```javascript
TealiumUnityPlugin.GetFromDataLayer(key);
```

| パラメータ | タイプ                                                                 | 説明                          |
|:-----------|:---------------------------------------------------------------------|:-------------------------------------|
| `key`      | `string`                                                             | データレイヤーから取得するキー。 |
| `callback` | 期待されるタイプにキャストする必要がある`object`タイプを返します。 | データレイヤーキーからの値。           |

例：

```bash
string? stringValue =
    (string)TealiumUnityPlugin.GetFromDataLayer("test_string");
```

### `GetConsentCategories()`

ユーザーの同意したカテゴリを取得します。

```javascript
TealiumUnityPlugin.GetConsentCategories();
```

| 戻り値のタイプ               | 説明                                                     |
|:--------------------------|:----------------------------------------------------------------|
| `List<ConsentCategories>` | ユーザーが同意した`ConsentCategories`のリスト。 |

例：

```javascript
List<string> categories = TealiumUnityPlugin.GetConsentCategories();
TealiumLogger.Log("Consent Categories: ");
categories.ForEach(category => TealiumLogger.Log(category.Value + " "));
```


### `GetConsentStatus()`

ユーザーの同意状態を取得します。

```javascript
TealiumUnityPlugin.GetConsentStatus();
```

| 戻り値のタイプ     | 説明                |
|:----------------|:---------------------------|
| `ConsentStatus` | ユーザーの同意状態。 |
例：

```javascript
TealiumLogger.Log("Consent Status: "
    + TealiumUnityPlugin.GetConsentStatus().Value);
```

### `GetVisitorId()`

ユーザーの訪問IDを取得します。

```javascript
TealiumUnityPlugin.GetVisitorId()
```

| 戻り値のタイプ | 説明             |
|:------------|:------------------------|
| `string`    | Tealium訪問ID。 |

例：

```javascript
TealiumLogger.Log("Visitor Id: " + TealiumUnityPlugin.GetVisitorId())
```

### `Initialize()`

他のメソッドを呼び出す前にTealiumを初期化します。オプションで、Tealiumの初期化が完了した後に実行される`Action<bool>`コールバックを渡すことができます。

```javascript
TealiumUnityPlugin.Initialize(config, callback);
```

| パラメータ | タイプ                                    | 説明                                                                                  |
|:-----------|:----------------------------------------|:---------------------------------------------------------------------------------------------|
| `config`   | [`TealiumConfig`](#class-tealiumconfig) | Tealiumの構成パラメータ。                                                            |
| `callback` | `Action<bool>`                          | Tealiumの初期化が成功した場合は`true`、エラーが発生した場合は`false`を返します。 |

例：

```javascript
private TealiumConfig config =
      new TealiumConfig("tealiummobile",
      "demo",
      TealiumEnvironment.DEV,
      new List<Dispatchers> {
        Dispatchers.TagManagement,
        Dispatchers.Collect,
        Dispatchers.RemoteCommands },
      new List<Collectors> {
        Collectors.AppData,
        Collectors.DeviceData,
        Collectors.Lifecycle,
        Collectors.Connectivity },
      consentPolicy: ConsentPolicy.GDPR,
      consentExpiry: new ConsentExpiry(10, TimeUnit.Minutes));

TealiumUnityPlugin.Initialize(config, success => {
    if (success) {
        TealiumLogger.Log("TealiumUnityPlugin Initialized");
        TealiumUnityPlugin.SetConsentStatus(ConsentStatus.Consented);
        TealiumUnityPlugin.SetConsentExpiryListener(() =>
            TealiumLogger.Log("Consent Expired!!"));
    } else {
        TealiumLogger.Log("TealiumUnityPlugin Failed to Initialize");
    }
});
```

### `JoinTrace()()`

指定されたIDでトレースに参加します。Tealium Customer Data Hubの[Trace](https://docs.tealium.com/manage-traces/)機能について詳しくはこちらをご覧ください。

```javascript
TealiumUnityPlugin.JoinTrace(id);
```

| パラメータ | タイプ     | 説明                      | 例    |
|:-----------|:---------|:---------------------------------|:-----------|
| `id`       | `string` | CDHから取得したトレースID。 | `abc123xy` |

### `LeaveTrace()`

アクティブなトレースを離れ、訪問セッションを終了します。このメソッドが呼ばれるまでのアプリセッションの間、トレースはアクティブのままです。

```javascript
TealiumUnityPlugin.LeaveTrace();
```

### `LogLevel`

ログレベルプロパティを構成し、どの程度の情報がログに記録されるかを以下の値のいずれかに制御します：

| 値             | 説明                                                          |
|:------------------|:---------------------------------------------------------------------|
| `LogLevel.Dev`    | アプリケーションの進行を強調する情報イベント。 |
| `LogLevel.Qa`     | アプリケーションのデバッグに使用されるデバッグレベルのイベント。                |
| `LogLevel.Prod`   | 致命的なエラーや失敗などのエラーイベント。                   |
| `LogLevel.Silent` | ログなし（デフォルト）。                                                |

例：

```javascript
LogLevel.Dev
```

### `SetConsentCategories()`

ユーザーの同意カテゴリを構成します。カテゴリの配列を渡して構成します。デフォルトは空の配列で、`ConsentStatus`が`.Consented`に構成されるまでです。同意状態が`.Consented`であり、`SetConsentCategories()`メソッドでカテゴリが指定されていない場合、すべてのカテゴリが構成されます。

```javascript
TealiumUnityPlugin.setConsentCategories(categories);
```

| パラメータ   | タイプ                      | 説明                      | 例                                                        |
|:-------------|:--------------------------|:---------------------------------|:---------------------------------------------------------------|
| `categories` | `List<ConsentCategories>` | ユーザーの同意カテゴリの配列 | `[ConsentCategories.email, ConsentCategories.personalization]` |

例：

```javascript
TealiumUnityPlugin.SetConsentCategories(new List<ConsentCategories>(){ConsentCategories.Analytics, ConsentCategories.Email});
```
#### ConsentCategories

| Value             | Description                       |
|:------------------|:----------------------------------|
| `Analytics`       | アナリティクス同意カテゴリー       |
| `Affiliates`      | アフィリエイト同意カテゴリー      |
| `DisplayAds`      | ディスプレイ広告同意カテゴリー    |
| `Email`           | メール同意カテゴリー              |
| `Personalization` | パーソナライゼーション同意カテゴリー |
| `Search`          | 検索同意カテゴリー                |
| `Social`          | ソーシャル同意カテゴリー          |
| `BigData`         | ビッグデータ同意カテゴリー        |
| `Mobile`          | モバイル同意カテゴリー            |
| `Engagement`      | エンゲージメント同意カテゴリー    |
| `Monitoring`      | モニタリング同意カテゴリー        |
| `Crm`             | CRM同意カテゴリー                 |
| `Cdp`             | CDP同意カテゴリー                 |
| `CookieMatch`     | クッキーマッチ同意カテゴリー      |
| `Misc`            | その他同意カテゴリー              |

### `SetConsentExpiryListener()`

ユーザーの同意構成が期限切れになった後に実行するコールバックを定義します。[`ConsentExpiry`](#consentexpiry)に従っています。このリスナーはTealiumが完全に初期化されることを保証するために、初期化コールバックで定義することを推奨します。

```javascript
TealiumUnityPlugin.SetConsentExpiryListener(callback);
```

| Parameters | Type     | Description                                |
|:-----------|:---------|:-------------------------------------------|
| `callback` | `Action` | 同意が期限切れになった後に実行するコード。 |

例:

```javascript
TealiumUnityPlugin.SetConsentExpiryListener(()
    => TealiumLogger.Log("Consent Expired!!"));
```

### `SetConsentStatus()`

ユーザーの同意ステータスを構成します。デフォルトは `.Unknown` です。

```javascript
TealiumUnityPlugin.SetConsentStatus(status);
```

| Parameters | Type            | Description              | Example                   |
|:-----------|:----------------|:-------------------------|:--------------------------|
| `status`   | `ConsentStatus` | ユーザーの同意ステータス。 | `ConsentStatus.Consented` |

例:

```javascript
TealiumUnityPlugin.SetConsentStatus(ConsentStatus.Consented);
```

#### `ConsentStatus`

| Value           | Description                   |
|:----------------|:------------------------------|
| `.Consented`    | 同意済みの同意ステータス。     |
| `.NotConsented` | 同意していない同意ステータス。 |
| `.Unknown`      | 不明な同意ステータス。         |

### `SetVisitorServiceListener()`

訪問プロファイルが更新されたときに実行するコールバックを定義します。更新された[`VisitorProfile`](#visitorprofile)はコールバックレスポンスで提供されます。

Tealium Customer Data Hubの[Data Layer Enrichment](https://docs.tealium.com/about-data-layer-enrichment/)機能を実装するVisitorServiceモジュールです。

このモジュールは、Tealium AudienceStreamのライセンスを持っており、モバイルアプリケーションで訪問プロファイルを使用してユーザーエクスペリエンスを向上させたい場合に使用することを推奨します。AudienceStreamのライセンスがない場合、訪問プロファイルが返されないため、このモジュールの使用は推奨されません。

```javascript
TealiumUnityPlugin.setVisitorServiceListener(callback);
```

| Parameters | Type                                 | Description                                                    |
|:-----------|:-------------------------------------|:---------------------------------------------------------------|
| `callback` | `Action<Dictionary<string, object>>` | 更新された訪問プロファイルが返された後に実行するコード。 |

例:

```javascript
TealiumUnityPlugin.setVisitorServiceListener((profile) => {
  string? serializedProfile = JsonConvert.SerializeObject(profile);
  if (serializedProfile != null) {
      TealiumLogger.Log(serializedProfile);
  }
});
```

### `RemoveFromDataLayer()`

`TealiumUnityPlugin.AddToDataLayer()`を使用して以前に構成された永続データを削除します。

```javascript
TealiumUnityPlugin.RemoveFromDataLayer(keys);
```

| Parameters | Type           | Description         | Example                            |
|:-----------|:---------------|:--------------------|:-----------------------------------|
| `keys`     | `List<string>` | キー名の配列。 | `new List<string>(){"foo", "bar"}` |

### `RemoveRemoteCommand()`

リモートコマンドマネージャーからリモートコマンドを削除します。

```javascript
TealiumUnityPlugin.RemoveRemoteCommand(id);
```

| Parameters | Type     | Description                       | Example        |
|:-----------|:---------|:----------------------------------|:---------------|
| `id`       | `string` | 削除するコマンドIDの名前。 | `test_command` |

例:

```javascript
TealiumUnityPlugin.RemoveRemoteCommand("firebase");
```


### `Track()`

ゲームやゲームビューとのユーザーのインタラクションを追跡します。

```javascript
TealiumUnityPlugin.Track(dispatch);
```

| Parameters | Type                                            | Description                                          | Example                        |
|:-----------|:------------------------------------------------|:-----------------------------------------------------|:-------------------------------|
| `dispatch` | [`TealiumDispatch`](#interface-tealiumdispatch) | Tealiumディスパッチでイベント名とデータレイヤーを含む。 | `TealiumEvent("button_click")` |

ゲームイベントを追跡するには、[`TealiumEvent`](#class-tealiumevent)オブジェクトを作成し、`track()`メソッドに渡します：

```javascript
TealiumEvent event = TealiumEvent('GAME_EVENT_NAME', new Dictionary<string, object> {{"KEY", "VALUE"}});
TealiumUnityPlugin.Track(event);
```

ゲーム画面ビューを追跡するには、[`TealiumView`](#class-tealiumview)オブジェクトを作成し、`track()`メソッドに渡します：

```javascript
TealiumView view = new TealiumView("VIEW_NAME", new Dictionary<string, object> {{"KEY", "VALUE"}})
TealiumUnityPlugin.Track(view);
```

### `Terminate()`

Tealiumライブラリを無効にし、すべてのモジュール参照を削除します。必要に応じて新しいTealiumインスタンスを作成することで再度有効にします。

```javascript
TealiumUnityPlugin.Terminate();
```
### `VisitorProfile`

訪問プロファイルは、各属性に対してフレンドリーな名前が含まれているオブジェクトです。`currentVisit`プロパティを使用して、訪問または訪問属性のタイプを区別できます。サブスクリプトを使用してIDで各属性値にアクセスします。属性が存在しない場合、`null`が返されます。

**属性タイプ**

| パラメータ           | プロパティ                                                                                                       | 値                                                                                                                             |
|:-------------------|:-----------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------|
| `arraysOfBooleans` | id: `string`, value: `bool`                                                                                      | id: "5129" value: [true,false,true,true]                                                                                         |
| `arraysOfNumbers`  | id: `string`, value: `double[]`                                                                                  | `id: "57", value: [4.82125, 16.8, 0.5714285714285714]`                                                                            |
| `arraysOfStrings`  | id: `string`, value: `string[]`                                                                                  | `id: "5213", value: ["green shirts", "green shirts", "blue shirts"]`                                                              |
| `audiences`        | id: string, value: string                                                                                        | `id: "tealiummobile\_demo\_103", value: "iOS Users"`                                                                              |
| `badges`           | id: `string`, value: `bool`                                                                                      | `id: "2815", value: true`                                                                                                         |
| `booleans`         | id: `string`, value: `bool`                                                                                      | `id: "4868", value: true`                                                                                                         |
| `currentVisit`     | 現在の訪問の訪問プロファイルのすべての属性。現在の訪問プロファイルにはAudiencesやBadgesは含まれません。 | `TealiumCurrentVisitProfile(dates: ["5376": 1567536668080, "10": 1567536668000], booleans: ["4530": true], numbers: ["32": 3.8])` |
| `dates`            | id: `string`, value: `int`                                                                                       | `id: "22", value: 1567120112000`                                                                                                  |
| `numbers`          | id: `string`, value: `double`                                                                                    | `id: "5728", value: 4.82125`                                                                                                      |
| `setOfStrings`     | id: `string`, value: `string[]`                                                                                  | `id: "5211", value: ["green shirts", "red shirts", "blue shirts"]`                                                                |
| `string`           | id: `string`, value: `string`                                                                                    | `id: "5380", value: "green shirts"`                                                                                               |
| `tallies`          | id: `string`, value: `Dictionary<string, float>`                                                                 | `"57": [["category 1": 2.0], "category 2": 1.0]]`                                                                                 |
| `tallyValue`       | id: `string`, value: `float`                                                                                     | `["category 1": 2.0]`                                                                                                             |
## クラス: `TealiumConfig`

以下は、`TealiumConfig` クラスのプロパティをまとめたものです。

| パラメータ                         | タイプ                                              | 説明                                                                                                                                                                                                                                                         | 例                                            |
|:-----------------------------------|:----------------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------|
| `account`                          | `string`                                            | (必須) Tealiumアカウント名。                                                                                                                                                                                                                                 | `companyXYZ`                                 |
| `profile`                          | `string`                                            | (必須) Tealiumプロファイル名。                                                                                                                                                                                                                               | `main`                                       |
| `environment`                      | [`TealiumEnvironment`](#class-tealiumenvironment)   | (必須) Tealium環境名。                                                                                                                                                                                                                                       | `TealiumEnvironment.Dev`                     |
| `dataSource`                       | `string`                                            | CDHデータソースキー。                                                                                                                                                                                                                                        | `abc123`                                     |
| `collectors`                       | `List<Collectors>`                                  | (必須) Tealiumライブラリを初期化するための[`Collectors`](#collectors)のリストを構成します。                                                                                                                                                                 | `new List<Collectors>(){Collectors.AppData}` |
| `dispatchers`                      | `List<Dispatchers>`                                 | (必須) Tealiumライブラリを初期化するための[`Dispatchers`](#dispatchers)のリストを構成します。                                                                                                                                                               | `new List<Collectors>(){Dispatchers.Collec}` |
| `customVisitorId`                  | `string`                                            | カスタム訪問IDを構成します。                                                                                                                                                                                                                              | `ALK2398LSDKJ3289SLKJ3298SLKJ3`              |
| `memoryReportingEnabled`           | `bool`                                              | DeviceDataモジュールでのメモリレポートを有効または無効にします（デフォルト：無効）。                                                                                                                                                                        | `true`                                       |
| `overrideCollectURL`               | `string`                                            | 異なるエンドポイントにデータを送信するためにTealium Collect URLを上書きします。イベントバッチ機能を使用する場合は、`overrideCollectBatchURL`プロパティも上書きしてください。                                                                             | `https://custom-domain.com/event`            |
| `overrideCollectBatchURL`          | `string`                                            | 異なるエンドポイントにデータを送信するためにTealium CollectバッチURLを上書きします。                                                                                                                                                                         | `https://custom-domain.com/batch-event`      |
| `overrideCollectProfile`           | `String`                                            | 異なるTealiumプロファイルにデータを送信するためにTealium Collectプロファイルを上書きします。                                                                                                                                                                 | `custom-profile`                             |
| `overrideLibrarySettingsURL`       | `string`                                            | 公開構成URLを上書きします。                                                                                                                                                                                                                                  | `https://custom-domain.com/mobile.html`      |
| `overrideTagManagementURL`         | `string`                                            | タグ管理モジュールで使用されるデフォルトURLを上書きします。これは、Tealium JavaScriptファイルを自己ホスティングする場合に必要です。                                                                                                                         | `https://custom-domain.com/path/env/utag.js` |
| `deepLinkTrackingEnabled`          | `bool`                                              | Facebookやその他のソースからのアプリへのリンクなど、[標準的なディープリンクの自動追跡](https://docs.tealium.com/ja/platforms/getting-started-mobile/deep-linking/#readout)を有効または無効にします（デフォルト：有効）。                                                               | `false`                                      |
| `qrTraceEnabled`                   | `bool`                                              | [QRトレース](https://docs.tealium.com/ja/platforms/getting-started-mobile/trace/#how-it-works)を有効または無効にします（デフォルト：有効）。                                                                                                                                             | `false`                                      |
| `loglevel`                         | [`LogLevel`](#loglevel)                             | ログレベルプロパティを構成し、どれだけの情報がログに記録されるかを制御します（デフォルト：サイレント）。                                                                                                                                                     | `LogLevel.dev`                               |
| `consentExpiry`                    | [`ConsentExpiry`](#consentexpiry)                   | ユーザーの同意構成の有効期限を構成します（ポリシーに依存するデフォルト値）。                                                                                                                                                                                | `ConsentExpiry(90, TimeUnit.days)`           |
| `consentLoggingEnabled`            | `bool`                                              | [同意ログ記録](https://docs.tealium.com/consent-change-event-specifications/)機能を有効にし、すべての同意ステータス変更を監査目的でTealium Customer Data Hubに送信します（デフォルト：有効）。                                                                      | `true`                                       |
| `consentPolicy`                    | [`ConsentPolicy`](#consentpolicy)                   | 同意ポリシーをCCPAまたはGDPRに構成します。このプロパティが構成されている場合のみ、同意マネージャーが有効になります。                                                                                                                                         | `ConsentPolicy.GDPR`                         |
| `lifecycleAutotrackingEnabled` | `bool`                                            | ライフサイクル自動追跡を有効または無効にします（デフォルト：有効）。                                                                                                                                                                                              | `false`                                      |
| `useRemoteLibrarySettings`     | `bool`                                            | [モバイル公開構成](https://docs.tealium.com/create-mobile-profile/)を有効または無効にします（デフォルト：有効）。Tealium iQタグ管理でモバイル公開構成を構成するか、この機能を無効にします。 | `false`                                      |
| `visitorServiceEnabled`        | `bool`                                            | [データレイヤーエンリッチメントAPI](https://docs.tealium.com/data-layer-enrichment-api/)を使用して訪問プロファイルの自動取得を有効または無効にします（デフォルト：無効）。                                | `true`                                       |
| `sessionCountingEnabled`       | `Boolean`                                   | Tealium iQアカウントのセッションカウントを有効または無効にします。TealiumのJavaScriptファイルを自己ホスティングしている場合は、これを`false`に構成します（デフォルト：有効）。                                                                                                            | `false`                                                                                                        |

## クラス: `TealiumEnvironment`

`TealiumEnvironment`は、デフォルトの環境（Dev、QA、Prod）のうちの1つ、またはTealiumが公開するカスタム環境です。

例:

```javascript
TealiumEnvironment.Dev
```

利用可能な環境は以下の通りです:

| 値       | 説明                  |
|:--------|:---------------------|
| `.Dev`  | 開発環境。             |
| `.Qa`   | QAまたはUAT環境。     |
| `.Prod` | 本番環境。             |

## インターフェース: `TealiumDispatch`

追跡するディスパッチのタイプを定義するインターフェースです。以下のクラスが`TealiumDispatch`を実装しています:

### クラス: `TealiumEvent`

ゲームやゲームビューとのユーザーのインタラクションを追跡するには、[`Track()`](#track)メソッドに`TealiumEvent(eventName, dataLayer)`のインスタンスを渡します。`TealiumEvent`は、追跡呼び出しに`tealium_event`として表示されるイベント名と、オプションのデータ辞書で構成されています。

```javascript
TealiumEvent(viewName, dataLayer)
```

| パラメータ  | タイプ                         | 説明                                | 例                                                                                           |
|:------------|:-----------------------------|:-----------------------------------|:--------------------------------------------------------------------------------------------|
| `eventName` | `string`                     | ゲームイベントの名前。              | `level_completed`                                                                           |
| `dataLayer` | `Dictionary<string, object>` | (オプション) イベントに送信されるデータ。 | `new Dictionary<string, object> {{"user_id", "gamer123"}, {"level": 2}, {"total_points": 17500}}` |

例:

```javascript
TealiumEvent event = TealiumEvent('EVENT_NAME',
    new Dictionary<string, object> {{"KEY", "VALUE"}});
TealiumUnityPlugin.Track(event);
```

### クラス: `TealiumView`

ゲーム内の画面ビューを追跡するには、[`Track()`](#track)メソッドに`TealiumView(viewName, dataLayer)`のインスタンスを渡します。`TealiumView`は、追跡呼び出しに`tealium_event`として表示されるビュー名と、オプションのデータ辞書で構成されています。

```javascript
TealiumView(viewName, dataLayer)
```

| パラメータ  | タイプ                         | 説明                                | 例                                                      |
|:------------|:-----------------------------|:-----------------------------------|:---------------------------------------------------------|
| `viewName`  | `string`                     | ゲーム内のビューまたは画面の名前。  | `login_view`                                             |
| `dataLayer` | `Dictionary<string, object>` | (オプション) イベントに送信されるデータ。 | `new Dictionary<string, object> {{"customer_id", "abc123"}}` |

例:

```javascript
TealiumView view = new TealiumView("VIEW_NAME",
    new Dictionary<string, object> {{"KEY", "VALUE"}})
TealiumUnityPlugin.Track(view);
```