---
title: APIリファレンス
description: Unity向けのTealiumが提供するクラスとメソッドのリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/unity/api/
---
## クラス: `Tealium`

以下はUnityライブラリの`Tealium`クラスの一般的に使用されるメソッドをまとめたものです。

| メソッド                                                      | 説明                                                                   |
|:------------------------------------------------------------|:------------------------------------------------------------------------------|
| [`AddRemoteCommand()`](#addRemoteCommand)                   | リモートコマンドをリモートコマンドマネージャに追加します。                          |
| [`AddToDataLayer()`](#addtodatalayer)                       | 永続データレイヤーにデータを追加します。                                           |
| [`GatherTrackData()`](#gathertrackdata)                     | コレクタとデータレイヤーからすべてのトラックデータを収集します。                         |
| [`GetFromDataLayer()`](#getfromdatalayer)                   | データレイヤーから指定された値を取得します。                                   |
| [`GetConsentCategories()`](#getConsentCategories)           | ユーザーの同意済みカテゴリを取得します。                                         |
| [`GetConsentStatus()`](#getConsentStatus)                   | ユーザーの同意ステータスを取得します。                                               |
| [`GetVisitorId()`](#getVisitorId)                           | 現在の訪問者IDを取得します。                                                  |
| [`Initialize()`](#initialize)                               | 設定パラメータでTealiumを初期化します。                            |
| [`JoinTrace()`](#joinTrace)                                 | 指定されたIDでトレースに参加します。                                              |
| [`LeaveTrace()`](#leaveTrace)                               | アクティブなトレースを終了し、訪問者セッションを終了します。                          |
| [`RemoveFromDataLayer()`](#removefromdatalayer)             | `AddToDataLayer()`を使用して以前に設定された永続データを削除します。 |
| [`RemoveRemoteCommand()`](#removeRemoteCommand)             | リモートコマンドマネージャからリモートコマンドを削除します。                     |
| [`SetConsentCategories()`](#setConsentCategories)           | ユーザーの同意カテゴリを設定します。                                        |
| [`SetConsentExpiryListener()`](#setConsentExpiryListener)   | 同意の有効期限が切れたときのリスナーまたはコールバックを設定します。                                |
| [`SetConsentStatus()`](#setConsentStatus)                   | ユーザーの同意ステータスを設定します。                                            |
| [`SetVisitorServiceListener()`](#setVisitorServiceListener) | 訪問者サービスのリスナーまたはコールバックを設定します。                                |
| [`Terminate()`](#terminate)                                 | Tealiumインスタンスを無効にし、破棄します。                                   |
| [`Track()`](#track)                                         | ユーザーのゲームまたはゲームビューとの相互作用をトラックします。                        |

### `AddRemoteCommand()`

リモートコマンドをリモートコマンドマネージャに追加します。

```javascript
TealiumUnityPlugin.AddRemoteCommand(id, callback);
```

| パラメータ | タイプ             | 説明                                                                                                                                                     | 例          |
|:-----------|:-----------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------|:-----------------|
| `id`       | `string`         | タグの設定からのコマンドIDの名前。                                                                                                              | `"test_command"` |
| `callback` | `Action<string>` | リモートコマンドからのレスポンスを受け取った後に実行するコールバック関数。コールバックは、タグマッピングからのキーバリューペアのペイロードを返します。 | (例を参照)    |

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

指定された有効期間の永続データストレージにデータを追加します。

```javascript
TealiumUnityPlugin.AddToDataLayer(data, expiry);
```

| パラメータ | タイプ                         | 説明                                                                                                    | 例                                             |
|:-----------|:-----------------------------|:-------------------------------------------------------------------------------------------------------|:------------------------------------------------|
| `data`     | `Dictionary<string, object>` | キーが文字列で値が文字列または文字列の配列であるJSONオブジェクト。                                          | `new Dictionary<string, object> {{"KEY", "VALUE"}}` |
| `expiry`   | [`Expiry`](#expiry)          | データを永続化する期間。                                                                                  | `Expiry.Forever`                                    |

### `Collectors`

コレクタは、デバイスから補足情報を収集し、それをTealium Customer Data Hubに送信する前にデータレイヤーに追加するモジュールです。一部のコレクタはコアライブラリに含まれており、他のコレクタはオプションとして別のモジュールとしてインストールされます。

以下の表は利用可能なコレクタの一覧です。デフォルトのコレクタは、コレクタ名の横に `*` が付いています。

| コレクタ名   | `TealiumConfig` リファレンス   |
|:-----------------|:----------------------------|
| `AppData`*       | `Collectors.AppData`        |
| `Connectivity`*  | `Collectors.Connectivity`   |
| `Device`         | `Collectors.Device`         |
| `Lifecycle`      | `Collectors.Lifecycle`      |
| `VisitorService` | `Collectors.VisitorService` |

### `ConsentExpiry`

同意の有効期限を定義します。

```javascript
ConsentExpiry(time, unit)
```

| パラメータ | タイプ       | 説明                           | 例         |
|:-----------|:-----------|:------------------------------|:----------------|
| `time`     | `Number`   | 有効期限までの時間。           | `90`            |
| `unit`     | `TimeUnit` | 有効期限までの時間の単位。     | `TimeUnit.Days` |

例:

```javascript
new ConsentExpiry(90, TimeUnit.Days)
```

#### TimeUnit

以下は時間の単位の値です:

| 値                   | 説明               |
|:------------------------|:--------------------------|
| `ConsentExpiry.Minutes` | 分単位の時間。 |
| `ConsentExpiry.Hours`   | 時間単位の時間。   |
| `ConsentExpiry.Months`  | 月単位の時間。  |
| `ConsentExpiry.Days`    | 日単位の時間。    |

### `ConsentPolicy`

遵守する同意ポリシーを定義します。[`TealiumConfig`](#class-tealiumconfig)オブジェクトで同意ポリシーが定義されていない場合、同意マネージャは無効になります。

| 値                | 説明              |
|:---------------------|:-------------------------|
| `ConsentPolicy.GDPR` | GDPR同意ポリシー。 |
| `ConsentPolicy.CCPA` | CCPA同意ポリシー。 |

例:

```javascript
ConsentPolicy.GDPR
```

### `Dispatchers`

ディスパッチャは、データレイヤーからデータを送信し、Tealiumエンドポイントに送信するモジュールです。以下のディスパッチャが現在利用可能です:

| ディスパッチャ名  | `TealiumConfig` リファレンス    |
|:-----------------|:-----------------------------|
| `Collect`        | `Dispatchers.Collect`        |
| `RemoteCommands` | `Dispatchers.RemoteCommands` |
| `TagManagement`  | `Dispatchers.TagManagement`  |


<blockquote>
少なくとも1つのディスパッチャが必要です。ディスパッチャが指定されていない場合、データはデータレイヤーに送信されません。
</blockquote>


### `Expiry`

カスタムデータの有効期限を定義します。

| 値          | 説明                                            |
|:---------------|:-------------------------------------------------------|
| `Session`      | 現在のアクティブなセッションの寿命。            |
| `UntilRestart` | アプリが再起動するまで。                                |
| `Forever`      | アプリの寿命、アプリが削除されるまで。 |

例:

```javascript
Expiry.session
```

### `GatherTrackData()`
コレクタとデータレイヤーからすべてのトラックデータを収集します。

```javascript
Tealium.GatherTrackData(callback);
```

| パラメータ | タイプ       | 説明                                          | 例       |
|:-----------|:-----------|:---------------------------------------------|:----------|
| `callback` | `Function` | トラッキングデータを受け取り処理するためのコールバック関数。コールバックはJSONオブジェクトを返します。 | (例を参照) |

例:

```javascript
Tealium.GatherTrackData(callback => {
  string? serializedPayload = JsonConvert.SerializeObject(callback);
  if (serializedPayload != null) {
      TealiumLogger.Log($"Track Data: {serializedPayload}");
  }
});
```

### `GetFromDataLayer()`

永続データレイヤーの指定されたキーの値を取得し、コールバック関数の形式で返します。

```javascript
TealiumUnityPlugin.GetFromDataLayer(key);
```

| パラメータ | タイプ                                                                 | 説明                          |
|:-----------|:---------------------------------------------------------------------|:---------------------------------|
| `key`      | `string`                                                             | データレイヤーから取得するキー。 |
| `callback` | 期待されるタイプにキャストする必要がある `object` タイプを返します。 | データレイヤーキーの値。           |

例:

```bash
string? stringValue =
    (string)TealiumUnityPlugin.GetFromDataLayer("test_string");
```

### `GetConsentCategories()`

ユーザーの同意済みカテゴリを取得します。

```javascript
TealiumUnityPlugin.GetConsentCategories();
```

| 戻り値のタイプ               | 説明                                                     |
|:--------------------------|:----------------------------------------------------------------|
| `List<ConsentCategories>` | ユーザーが同意した `ConsentCategories` のリスト。 |

例:

```javascript
List<string> caetgories = TealiumUnityPlugin.GetConsentCategories();
TealiumLogger.Log("Consent Categories: ");
caetgories.ForEach(category => TealiumLogger.Log(category.Value + " "));
```


### `GetConsentStatus()`

ユーザーの同意ステータスを取得します。

```javascript
TealiumUnityPlugin.GetConsentStatus();
```

| 戻り値のタイプ     | 説明                |
|:----------------|:---------------------------|
| `ConsentStatus` | ユーザーの同意ステータス。 |

例:

```javascript
TealiumLogger.Log("Consent Status: "
    + TealiumUnityPlugin.GetConsentStatus().Value);
```

### `GetVisitorId()`

ユーザーの訪問者IDを取得します。

```javascript
TealiumUnityPlugin.GetVisitorId()
```

| 戻り値のタイプ | 説明             |
|:------------|:------------------------|
| `string`    | Tealiumの訪問者ID。 |

例:

```javascript
TealiumLogger.Log("Visitor Id: " + TealiumUnityPlugin.GetVisitorId())
```

### `Initialize()`

他のメソッドを呼び出す前にTealiumを初期化します。オプションで、Tealiumの初期化が完了した後に実行される `Action<bool>` コールバックを渡すこともできます。

```javascript
TealiumUnityPlugin.Initialize(config, callback);
```

| パラメータ | タイプ                                    | 説明                                                                                  |
|:-----------|:----------------------------------------|:-------------------------------------------------------------------------------------|
| `config`   | [`TealiumConfig`](#class-tealiumconfig) | Tealiumの設定パラメータ。                                                            |
| `callback` | `Action<bool>`                          | Tealiumの初期化が成功した場合は `true` 、エラーが発生した場合は `false` を返します。 |


例:

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

指定されたIDでトレースに参加します。Tealium Customer Data Hubの[トレース](https://docs.tealium.com/manage-traces/)機能について詳しくは、ドキュメントを参照してください。

```javascript
TealiumUnityPlugin.JoinTrace(id);
```

| パラメータ | タイプ     | 説明                      | 例    |
|:-----------|:---------|:-------------------------|:-----------|
| `id`       | `string` | CDHから取得したトレースID。 | `abc123xy` |

### `LeaveTrace()`

アクティブなトレースを終了し、訪問者セッションを終了します。このメソッドが呼び出されるまで、トレースはアプリのセッションの間アクティブです。

```javascript
TealiumUnityPlugin.LeaveTrace();
```

### `LogLevel`

ログレベルプロパティを設定します。ログレベルプロパティは、ログに記録される情報の量を制御します。

| 値             | 説明                                                          |
|:------------------|:---------------------------------------------------------------------|
| `LogLevel.Dev`    | アプリケーションの進行状況を示す情報イベント。 |
| `LogLevel.Qa`     | アプリケーションのデバッグに使用されるデバッグレベルのイベント。                |
| `LogLevel.Prod`   | クリティカルなエラーや障害などのエラーイベント。                   |
| `LogLevel.Silent` | ログなし（デフォルト）。                                                |

例:

```javascript
LogLevel.Dev
```

### `SetConsentCategories()`

ユーザーの同意カテゴリを設定します。カテゴリを設定するには、文字列の配列を渡します。デフォルトは空の配列で、`ConsentStatus` が `.Consented` に設定されている場合、`SetConsentCategories()` メソッドでカテゴリが指定されていない場合、すべてのカテゴリが設定されます。

```javascript
TealiumUnityPlugin.setConsentCategories(categories);
```

| パラメータ   | タイプ                      | 説明                                        | 例                                                |
|:-------------|:--------------------------|:-------------------------------------------|:---------------------------------------------------|
| `categories` | `List<ConsentCategories>` | ユーザーの同意カテゴリの配列 | `[ConsentCategories.email, ConsentCategories.personalization]` |

例:

```javascript
TealiumUnityPlugin.SetConsentCategories(new List<ConsentCategories>(){ConsentCategories.Analytics, ConsentCategories.Email});
```

#### ConsentCategories

| 値             | 説明                       |
|:------------------|:----------------------------------|
| `Analytics`       | アナリティクス同意カテゴリ。       |
| `Affiliates`      | アフィリエイト同意カテゴリ。      |
| `DisplayAds`      | ディスプレイ広告同意カテゴリ。     |
| `Email`           | メール同意カテゴリ。           |
| `Personalization` | パーソナライゼーション同意カテゴリ。 |
| `Search`          | 検索同意カテゴリ。          |
| `Social`          | ソーシャル同意カテゴリ。          |
| `BigData`         | ビッグデータ同意カテゴリ。        |
| `Mobile`          | モバイル同意カテゴリ。          |
| `Engagement`      | エンゲージメント同意カテゴリ。      |
| `Monitoring`      | モニタリング同意カテゴリ。      |
| `Crm`             | CRM同意カテゴリ。             |
| `Cdp`             | CDP同意カテゴリ。             |
| `CookieMatch`     | Cookie Match同意カテゴリ。    |
| `Misc`            | その他の同意カテゴリ。            |

### `SetConsentExpiryListener()`

ユーザーの同意設定が有効期限切れになった後に実行するコールバックを定義します。Tealiumが完全に初期化されていることを確認するために、初期化コールバック内でこのリスナーを定義することをお勧めします。

```javascript
TealiumUnityPlugin.SetConsentExpiryListener(callback);
```

| パラメータ | タイプ     | 説明                                |
|:-----------|:---------|:-----------------------------------|
| `callback` | `Action` | 同意が期限切れになった後に実行するコード。 |

例:

```javascript
TealiumUnityPlugin.SetConsentExpiryListener(()
    => TealiumLogger.Log("Consent Expired!!"));
```

### `SetConsentStatus()`

ユーザーの同意ステータスを設定します。デフォルトは `.Unknown` です。

```javascript
TealiumUnityPlugin.SetConsentStatus(status);
```

| パラメータ | タイプ            | 説明              | 例            |
|:-----------|:----------------|:-----------------|:---------------|
| `status`   | `ConsentStatus` | ユーザーの同意ステータス。 | `ConsentStatus.Consented` |

例:

```javascript
TealiumUnityPlugin.SetConsentStatus(ConsentStatus.Consented);
```

#### `ConsentStatus`

| 値           | 説明                    |
|:----------------|:-------------------------------|
| `.Consented`    | 同意済みの同意ステータス。     |
| `.NotConsented` | 同意されていない同意ステータス。 |
| `.Unknown`      | 不明な同意ステータス。          |

### `SetVisitorServiceListener()`

訪問者プロファイルが更新された後に実行するコールバックを定義します。更新された [`VisitorProfile`](#visitorprofile) はコールバック応答で提供されます。

VisitorServiceモジュールは、Tealium Customer Data Hubの[データレイヤーエンリッチメント](https://docs.tealium.com/enable-data-layer-enrichment/)機能を実装しています。

このモジュールの使用は、Tealium AudienceStreamのライセンスを受けており、モバイルアプリケーションでユーザーエクスペリエンスを向上させるために訪問者プロファイルを使用したい場合に推奨されます。AudienceStreamのライセンスを受けていない場合、このモジュールの使用は推奨されません。

```javascript
TealiumUnityPlugin.setVisitorServiceListener(callback);
```

| パラメータ | タイプ                                 | 説明                                                    |
|:-----------|:-------------------------------------|:-------------------------------------------------------|
| `callback` | `Action<Dictionary<string, object>>` | 更新された訪問者プロファイルが返される後に実行するコード。 |

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

`TealiumUnityPlugin.AddToDataLayer()` を使用して以前に設定された永続データを削除します。

```javascript
TealiumUnityPlugin.RemoveFromDataLayer(keys);
```

| パラメータ | タイプ           | 説明         | 例                            |
|:-----------|:---------------|:------------|:-------------------------------|
| `keys`     | `List<string>` | キーの名前の配列。 | `new List<string>(){"foo", "bar"}` |

### `RemoveRemoteCommand()`

リモートコマンドマネージャからリモートコマンドを削除します。

```javascript
TealiumUnityPlugin.RemoveRemoteCommand(id);
```

| パラメータ | タイプ     | 説明                       | 例        |
|:-----------|:---------|:--------------------------|:-----------|
| `id`       | `string` | 削除するコマンドIDの名前。 | `test_command` |

例:

```javascript
TealiumUnityPlugin.RemoveRemoteCommand("firebase");
```


### `Track()`

ユーザーのゲームまたはゲームビューとの相互作用をトラックします。

```javascript
TealiumUnityPlugin.Track(dispatch);
```

| パラメータ | タイプ                                            | 説明                                          | 例                        |
|:-----------|:------------------------------------------------|:---------------------------------------------|:---------------------------|
| `dispatch` | [`TealiumDispatch`](#interface-tealiumdispatch) | イベント名とデータレイヤーを持つTealiumディスパッチ。 | `TealiumEvent("button_click")` |

ゲームイベントをトラックするには、[`TealiumEvent`](#class-tealiumevent) オブジェクトを作成し、`track()` メソッドに渡します:

```javascript
TealiumEvent event = TealiumEvent('GAME_EVENT_NAME', new Dictionary<string, object> {{"KEY", "VALUE"}});
TealiumUnityPlugin.Track(event);
```

ゲーム画面ビューをトラックするには、[`TealiumView`](#class-tealiumview) オブジェクトを作成し、`track()` メソッドに渡します:  

```javascript
TealiumView view = new TealiumView("VIEW_NAME", new Dictionary<string, object> {{"KEY", "VALUE"}})
TealiumUnityPlugin.Track(view);
```

### `Terminate()`

Tealiumライブラリを無効にし、すべてのモジュール参照を削除します。必要に応じて新しいTealiumインスタンスを作成して再度有効にします。

```javascript
TealiumUnityPlugin.Terminate();
```

### `VisitorProfile`

訪問者プロファイルは、各属性のフレンドリーな名前を含むオブジェクトです。`currentVisit` プロパティがあり、訪問者または訪問属性タイプを区別することができます。各属性の値は、サブスクリプトを使用してIDでアクセスできます。属性が存在しない場合は、`null` が返されます。

**属性タイプ**

| パラメータ         | プロパティ                                                                                                       | 値                                                                                                                             |
|:-------------------|:-----------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------|
| `arraysOfBooleans` | id: `string`, value: `bool`                                                                                      | id: "5129" value: [true,false,true,true]                                                                                         |
| `arraysOfNumbers`  | id: `string`, value: `double[]`                                                                                  | `id: "57", value: [4.82125, 16.8, 0.5714285714285714]`                                                                            |
| `arraysOfStrings`  | id: `string`, value: `string[]`                                                                                  | `id: "5213", value: ["green shirts", "green shirts", "blue shirts"]`                                                              |
| `audiences`        | id: string, value: string                                                                                        | `id: "tealiummobile\_demo\_103", value: "iOS Users"`                                                                              |
| `badges`           | id: `string`, value: `bool`                                                                                      | `id: "2815", value: true`                                                                                                         |
| `booleans`         | id: `string`, value: `bool`                                                                                      | `id: "4868", value: true`                                                                                                         |
| `currentVisit`     | 現在の訪問者プロファイルのすべての属性。現在の訪問プロファイルには、AudiencesまたはBadgesは含まれません。 | `TealiumCurrentVisitProfile(dates: ["5376": 1567536668080, "10": 1567536668000], booleans: ["4530": true], numbers: ["32": 3.8])` |
| `dates`            | id: `string`, value: `int`                                                                                       | `id: "22", value: 1567120112000`                                                                                                  |
| `numbers`          | id: `string`, value: `double`                                                                                    | `id: "5728", value: 4.82125`                                                                                                      |
| `setOfStrings`     | id: `string`, value: `string[]`                                                                                  | `id: "5211", value: ["green shirts", "red shirts", "blue shirts"]`                                                                |
| `string`           | id: `string`, value: `string`                                                                                    | `id: "5380", value: "green shirts"`                                                                                               |
| `tallies`          | id: `string`, value: `Dictionary<string, float>`                                                                 | `"57": [["category 1": 2.0], "category 2": 1.0]]`                                                                                 |
| `tallyValue`       | id: `string`, value: `float`                                                                                     | `["category 1": 2.0]`                                                                                                             |

## クラス: `TealiumConfig`

以下は `TealiumConfig` クラスのプロパティの概要です。

| パラメータ                     | タイプ                                              | 説明                                                                                                                                                                                                                                                  | 例                                      |
|:-------------------------------|:--------------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------|
| `account`                      | `string`                                          | (必須) Tealiumアカウント名。                                                                                                                                                                                                                             | `companyXYZ`                                 |
| `profile`                      | `string`                                          | (必須) Tealiumプロファイル名。                                                                                                                                                                                                                             | `main`                                       |
| `environment`                  | [`TealiumEnvironment`](#class-tealiumenvironment) | (必須) Tealium環境名。                                                                                                                                                                                                                         | `TealiumEnvironment.Dev`                     |
| `dataSource`                   | `string`                                          | CDHデータソースキー。                                                                                                                                                                                                                                         | `abc123`                                     |
| `collectors`                   | `List<Collectors>`                                | (必須) Tealiumライブラリを初期化するための [`Collectors`](#collectors) のリストを設定します。                                                                                                                                                              | `new List<Collectors>(){Collectors.AppData}` |
| `dispatchers`                  | `List<Dispatchers>`                               | (必須) Tealiumライブラリを初期化するための [`Dispatchers`](#dispatchers) のリストを設定します。                                                                                                                                                            | `new List<Collectors>(){Dispatchers.Collec}` |
| `customVisitorId`              | `string`                                          | カスタムの訪問者IDを設定します。                                                                                                                                                                                                                                    | `ALK2398LSDKJ3289SLKJ3298SLKJ3`              |
| `memoryReportingEnabled`       | `bool`                                            | デバイスデータモジュールでメモリレポートを有効または無効にします（デフォルト：無効）。                                                                                                                                                                           | `true`                                       |
| `overrideCollectURL`           | `string`                                          | Tealium Collect URLを別のエンドポイントに送信するためにオーバーライドします。イベントバッチング機能を使用している場合は、`overrideCollectBatchURL` プロパティもオーバーライドしてください。                                                                                           | `https://custom-domain.com/event`            |
| `overrideCollectBatchURL`      | `string`                                          | Tealium CollectバッチURLを別のエンドポイントに送信するためにオーバーライドします。                                                                                                                                                                                | `https://custom-domain.com/batch-event`      |
| `overrideCollectProfile`       | `String`                                    | Tealium Collectプロファイルを別のTealiumプロファイルに送信するためにオーバーライドします。
| `custom-profile`                                                                                              |
| `overrideLibrarySettingsURL`   | `string`                                          | パブリッシュ設定URLをオーバーライドします。                                                                                                                                                                                                                          | `https://custom-domain.com/mobile.html`      |
| `overrideTagManagementURL`     | `string`                                          | タグ管理モジュールで使用されるデフォルトのURLをオーバーライドします。Tealium JavaScriptファイルを自己ホストしている場合に必要です。                                                                                                                           | `https://custom-domain.com/path/env/utag.js` |
| `deepLinkTrackingEnabled`      | `bool`                                            | Facebookやその他のソースからアプリへのリンクなど、標準のディープリンクの自動トラッキングを有効または無効にします（デフォルト：有効）。                                                                                                          | `false`                                      |
| `qrTraceEnabled`               | `bool`                                            | [QRトレース](https://docs.tealium.com/ja/platforms/getting-started-mobile/trace/#how-it-works)を有効または無効にします（デフォルト：有効）                                                                                                                                                            | `false`                                      |
| `loglevel`                     | [`LogLevel`](#loglevel)                           | ログレベルプロパティを設定します。ログに記録される情報の量を制御します（デフォルト：silent）。                                                                                                                                                                | `LogLevel.dev`                               |
| `consentExpiry`                | [`ConsentExpiry`](#consentexpiry)                 | ユーザーの同意設定の有効期限を設定します（デフォルトはポリシーに依存します）。                                                                                                                                                                      | `ConsentExpiry(90, TimeUnit.days)`           |
| `consentLoggingEnabled`        | `bool`                                            | 同意の変更イベントをTealium Customer Data Hubに送信して監査目的でログに記録する[同意ログ](https://docs.tealium.com/consent-change-event-specifications/)機能を有効または無効にします（デフォルト：有効）    | `true`                                       |
| `consentPolicy`                | [`ConsentPolicy`](#consentpolicy)                 | CCPAまたはGDPRのいずれかの同意ポリシーを設定します。このプロパティが設定されている場合にのみ同意マネージャが有効になります。                                                                                                                                                     | `ConsentPolicy.GDPR`                         |
| `lifecycleAutotrackingEnabled` | `bool`                                            | ライフサイクルの自動トラッキングを有効または無効にします（デフォルト：有効）。                                                                                                                                                                                              | `false`                                      |
| `useRemoteLibrarySettings`     | `bool`                                            | [モバイルパブリッシュ設定](https://docs.tealium.com/creating-a-mobile-profile/)を有効または無効にします（デフォルト：有効）。Tealium Tag Managementでモバイルパブリッシュ設定を構成するか、機能を無効にします。 | `false`                                      |
| `visitorServiceEnabled`        | `bool`                                            | [データレイヤーエンリッチメントAPI](https://docs.tealium.com/data-layer-enrichment-api/)を使用して訪問者プロファイルを自動的に取得する機能を有効または無効にします（デフォルト：無効）。                                | `true`                                       |
| `sessionCountingEnabled`       | `Boolean`                                   | Tealium iQアカウントのセッションカウントを有効または無効にします。Tealium JavaScriptファイルを自己ホストしている場合は、これを `false` に設定します（デフォルト：有効）                                                                                                            | `false`                                                                                                        |


## クラス: `TealiumEnvironment`

`TealiumEnvironment`は、3つのデフォルト環境（Dev、QA、Prod）のいずれか、またはTealiumが公開するカスタム環境のいずれかです。

例:

```javascript
TealiumEnvironment.Dev
```

以下の環境が利用可能です:

| 値   | 説明              |
|:--------|:-------------------------|
| `.Dev`  | 開発環境。 |
| `.Qa`   | QAまたはUAT環境。   |
| `.Prod` | 本番環境。  |


## インターフェース: `TealiumDispatch`

トラックするディスパッチのタイプを定義するインターフェースです。以下のクラスが `TealiumDispatch` を実装しています:

### クラス: `TealiumEvent`

ユーザーのゲームまたはゲームビューとの相互作用をトラックするには、`TealiumEvent(eventName, dataLayer)` のインスタンスを [`Track()`](#track) メソッドに渡します。`TealiumEvent` は、トラッキングコールで `tealium_event` として表示されるイベント名と、オプションのデータディクショナリで構成されています。

```javascript
TealiumEvent(viewName, dataLayer)
```

| パラメータ  | タイプ                         | 説明                                | 例                                                                                           |
|:------------|:-----------------------------|:-----------------------------------|:--------------------------------------------------------------------------------------------------|
| `eventName` | `string`                     | ゲームイベントの名前。                        | `level_completed`                                                                                 |
| `dataLayer` | `Dictionary<string, object>` | (オプション) イベントと一緒に送信するデータ。 | `new Dictionary<string, object> {{"user_id", "gamer123"}, {"level": 2}, {"total_points": 17500}}` |

例:

```javascript
TealiumEvent event = TealiumEvent('EVENT_NAME',
    new Dictionary<string, object> {{"KEY", "VALUE"}});
TealiumUnityPlugin.Track(event);
```

### クラス: `TealiumView`

ゲーム内の画面ビューをトラックする

