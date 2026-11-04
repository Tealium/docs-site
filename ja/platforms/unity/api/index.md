---
title: APIリファレンス
description: Unity向けにTealiumが提供するクラスとメソッドのリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/unity/api/
---
## クラス：`Tealium`

以下に、Unityライブラリの`Tealium`クラスでよく使用されるメソッドをまとめます。

| メソッド                                                    | 説明                                                                          |
|:------------------------------------------------------------|:------------------------------------------------------------------------------|
| [`AddRemoteCommand()`](#addRemoteCommand)                   | リモートコマンドマネージャーにリモートコマンドを追加します。                  |
| [`AddToDataLayer()`](#addtodatalayer)                       | 永続データレイヤーにデータを追加します。                                      |
| [`GatherTrackData()`](#gathertrackdata)                     | コレクターとデータレイヤーからすべてのトラッキングデータを収集します。        |
| [`GetFromDataLayer()`](#getfromdatalayer)                   | データレイヤーから指定された値を取得します。                                  |
| [`GetConsentCategories()`](#getConsentCategories)           | ユーザーが同意したカテゴリーを取得します。                                    |
| [`GetConsentStatus()`](#getConsentStatus)                   | ユーザーの同意ステータスを取得します。                                        |
| [`GetVisitorId()`](#getVisitorId)                           | 現在の訪問IDを取得します。                                                   |
| [`Initialize()`](#initialize)                               | 構成パラメータを使用してTealiumを初期化します。                                |
| [`JoinTrace()`](#joinTrace)                                 | 指定されたIDのトレースに参加します。                                          |
| [`LeaveTrace()`](#leaveTrace)                               | アクティブなトレースから離脱し、訪問セッションを終了します。                |
| [`RemoveFromDataLayer()`](#removefromdatalayer)             | `AddToDataLayer()`を使用して以前に構成した永続データを削除します。             |
| [`RemoveRemoteCommand()`](#removeRemoteCommand)             | リモートコマンドマネージャーからリモートコマンドを削除します。                |
| [`SetConsentCategories()`](#setConsentCategories)           | ユーザーの同意カテゴリーを構成します。                                        |
| [`SetConsentExpiryListener()`](#setConsentExpiryListener)   | 同意の有効期限切れリスナーまたはコールバックを構成します。                    |
| [`SetConsentStatus()`](#setConsentStatus)                   | ユーザーの同意ステータスを構成します。                                        |
| [`SetVisitorServiceListener()`](#setVisitorServiceListener) | 訪問サービスのリスナーまたはコールバックを構成します。                      |
| [`Terminate()`](#terminate)                                 | Tealiumインスタンスを無効化して破棄します。                                    |
| [`Track()`](#track)                                         | ユーザーによるゲームまたはゲームビューの操作をトラッキングします。            |

### `AddRemoteCommand()`

リモートコマンドマネージャーにリモートコマンドを追加します。

```javascript
TealiumUnityPlugin.AddRemoteCommand(id, callback);
```

| パラメータ | 型               | 説明                                                                                                                                               | 例               |
|:-----------|:-----------------|:---------------------------------------------------------------------------------------------------------------------------------------------------|:-----------------|
| `id`       | `string`         | タグ構成のコマンドID名。                                                                                                                           | `"test_command"` |
| `callback` | `Action<string>` | リモートコマンドからレスポンスを受信した後に実行するコールバック関数。コールバックは、タグマッピングから取得したキーと値のペアのペイロードを返します。 | （例を参照）     |

例：

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

指定された有効期限に従って、永続データ保存にデータを追加します。

```javascript
TealiumUnityPlugin.AddToDataLayer(data, expiry);
```

| パラメータ | 型                           | 説明                                                                                                          | 例                                                  |
|:-----------|:-----------------------------|:--------------------------------------------------------------------------------------------------------------|:----------------------------------------------------|
| `data`     | `Dictionary<string, object>` | キーと値のペアからなるJSONオブジェクト。キーは文字列で、値は文字列または文字列の配列です。                    | `new Dictionary<string, object> {{"KEY", "VALUE"}}` |
| `expiry`   | [`Expiry`](#expiry)          | データを永続化する期間。                                                                                      | `Expiry.Forever`                                    |

### `Collectors`

コレクターは、デバイスから補足情報を収集し、Tealium Customer Data Hubへ送信される前にデータレイヤーへ追加するモジュールです。一部のコレクターはコアライブラリに含まれていますが、その他のコレクターはオプションであり、個別のモジュールとしてインストールされます。

次の表に、利用可能なコレクターを示します。デフォルトのコレクターには、コレクター名の横に`*`が付いています。

| コレクター名     | `TealiumConfig`リファレンス |
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

| パラメータ | 型         | 説明                         | 例              |
|:-----------|:-----------|:-----------------------------|:----------------|
| `time`     | `Number`   | 有効期限が切れるまでの時間。 | `90`            |
| `unit`     | `TimeUnit` | 有効期限までの時間単位。     | `TimeUnit.Days` |

例：

```javascript
new ConsentExpiry(90, TimeUnit.Days)
```

#### TimeUnit

時間単位の値は次のとおりです。

| 値                      | 説明                 |
|:------------------------|:---------------------|
| `ConsentExpiry.Minutes` | 分単位の時間です。   |
| `ConsentExpiry.Hours`   | 時間単位の時間です。 |
| `ConsentExpiry.Months`  | 月単位の時間です。   |
| `ConsentExpiry.Days`    | 日単位の時間です。   |

### `ConsentPolicy`

準拠する同意ポリシーを定義します。[`TealiumConfig`](#class-tealiumconfig)オブジェクトに同意ポリシーが定義されていない場合、同意マネージャーは無効になります。

| 値                   | 説明                     |
|:---------------------|:-------------------------|
| `ConsentPolicy.GDPR` | GDPR同意ポリシーです。   |
| `ConsentPolicy.CCPA` | CCPA同意ポリシーです。   |

例：

```javascript
ConsentPolicy.GDPR
```
### `Dispatchers`

ディスパッチャーは、データレイヤーから Tealium エンドポイントへデータを送信するモジュールです。現在、次のディスパッチャーを使用できます。

| ディスパッチャー名 | `TealiumConfig` の参照値     |
|:-------------------|:-----------------------------|
| `Collect`          | `Dispatchers.Collect`        |
| `RemoteCommands`   | `Dispatchers.RemoteCommands` |
| `TagManagement`    | `Dispatchers.TagManagement`  |


<blockquote>
少なくとも 1 つのディスパッチャーが必要です。ディスパッチャーが指定されていない場合、データはデータレイヤーに送信されません。
</blockquote>


### `Expiry`

カスタムデータの有効期限を定義します。

| 値             | 説明                                                   |
|:---------------|:-------------------------------------------------------|
| `Session`      | 現在アクティブなセッションが継続している間。           |
| `UntilRestart` | アプリが再起動されるまで。                             |
| `Forever`      | アプリが削除されるまでの、アプリの存続期間全体。       |

例：

```javascript
Expiry.session
```

### `GatherTrackData()`

コレクターおよびデータレイヤーからすべてのトラッキングデータを収集します。

```javascript
Tealium.GatherTrackData(callback);
```

| パラメータ | 型         | 説明                                                                                     | 例       |
|:-----------|:-----------|:-----------------------------------------------------------------------------------------|:---------|
| `callback` | `Function` | トラッキングデータを受け取り、処理するためのコールバック関数。JSON オブジェクトを返します。 | （例を参照） |

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

永続データレイヤーから指定したキーの値を取得し、コールバック関数の形式で返します。

```javascript
TealiumUnityPlugin.GetFromDataLayer(key);
```

| パラメータ | 型                                                                   | 説明                                     |
|:-----------|:---------------------------------------------------------------------|:-----------------------------------------|
| `key`      | `string`                                                             | データレイヤーから取得するキー。         |
| `callback` | Returns an `object` type that needs to be cast to the expected type. | データレイヤーのキーに対応する値。       |

例：

```bash
string? stringValue =
    (string)TealiumUnityPlugin.GetFromDataLayer("test_string");
```

### `GetConsentCategories()`

ユーザーが同意したカテゴリーを取得します。

```javascript
TealiumUnityPlugin.GetConsentCategories();
```

| 戻り値の型                | 説明                                                       |
|:--------------------------|:-----------------------------------------------------------|
| `List<ConsentCategories>` | ユーザーが同意した `ConsentCategories` のリスト。          |

例：

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

| 戻り値の型      | 説明                         |
|:----------------|:-----------------------------|
| `ConsentStatus` | ユーザーの同意ステータス。   |

例：

```javascript
TealiumLogger.Log("Consent Status: "
    + TealiumUnityPlugin.GetConsentStatus().Value);
```

### `GetVisitorId()`

ユーザーの訪問 ID を取得します。

```javascript
TealiumUnityPlugin.GetVisitorId()
```

| 戻り値の型 | 説明                    |
|:-----------|:------------------------|
| `string`   | Tealium の訪問 ID。   |

例：

```javascript
TealiumLogger.Log("Visitor Id: " + TealiumUnityPlugin.GetVisitorId())
```

### `Initialize()`

ほかのメソッドを呼び出す前に Tealium を初期化します。必要に応じて、Tealium の初期化完了後に実行される `Action<bool>` コールバックを渡します。

```javascript
TealiumUnityPlugin.Initialize(config, callback);
```

| パラメータ | 型                                      | 説明                                                                                     |
|:-----------|:----------------------------------------|:-----------------------------------------------------------------------------------------|
| `config`   | [`TealiumConfig`](#class-tealiumconfig) | Tealium の構成パラメータ。                                                               |
| `callback` | `Action<bool>`                          | Tealium の初期化に成功した場合は `true`、エラーが発生した場合は `false` を返します。      |

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

指定した ID のトレースに参加します。Tealium Customer Data Hub の [Trace](https://docs.tealium.com/manage-traces/) 機能について詳しく説明します。

```javascript
TealiumUnityPlugin.JoinTrace(id);
```

| パラメータ | 型       | 説明                              | 例         |
|:-----------|:---------|:----------------------------------|:-----------|
| `id`       | `string` | CDH から取得したトレース ID。     | `abc123xy` |

### `LeaveTrace()`

アクティブなトレースから離脱し、訪問セッションを終了します。トレースは、このメソッドが呼び出されるまで、アプリセッションの継続中はアクティブな状態を維持します。

```javascript
TealiumUnityPlugin.LeaveTrace();
```

### `LogLevel`

ログに記録する情報量を制御するログレベルプロパティを、次のいずれかの値に構成します。

| 値                | 説明                                                         |
|:------------------|:-------------------------------------------------------------|
| `LogLevel.Dev`    | アプリケーションの進行状況を示す情報イベント。               |
| `LogLevel.Qa`     | アプリケーションのデバッグに使用するデバッグレベルのイベント。 |
| `LogLevel.Prod`   | 重大なエラーや障害などのエラーイベント。                     |
| `LogLevel.Silent` | ログを記録しません（デフォルト）。                           |

例：

```javascript
LogLevel.Dev
```

### `SetConsentCategories()`

ユーザーの同意カテゴリーを構成します。カテゴリーを構成するには、文字列の配列を渡します。`ConsentStatus` が `.Consented` に構成されるまでは、デフォルトで空の配列です。同意ステータスが `.Consented` で、`SetConsentCategories()` メソッドによってカテゴリーが指定されていない場合は、すべてのカテゴリーが構成されます。

```javascript
TealiumUnityPlugin.setConsentCategories(categories);
```

| パラメータ   | 型                        | 説明                           | 例                                                             |
|:-------------|:--------------------------|:-------------------------------|:---------------------------------------------------------------|
| `categories` | `List<ConsentCategories>` | ユーザー同意カテゴリーの配列   | `[ConsentCategories.email, ConsentCategories.personalization]` |

例：

```javascript
TealiumUnityPlugin.SetConsentCategories(new List<ConsentCategories>(){ConsentCategories.Analytics, ConsentCategories.Email});
```
#### ConsentCategories

| 値                | 説明                                 |
|:------------------|:-------------------------------------|
| `Analytics`       | 分析の同意カテゴリ。                 |
| `Affiliates`      | アフィリエイトの同意カテゴリ。       |
| `DisplayAds`      | ディスプレイ広告の同意カテゴリ。     |
| `Email`           | メールの同意カテゴリ。               |
| `Personalization` | パーソナライゼーションの同意カテゴリ。 |
| `Search`          | 検索の同意カテゴリ。                 |
| `Social`          | ソーシャルの同意カテゴリ。           |
| `BigData`         | ビッグデータの同意カテゴリ。         |
| `Mobile`          | モバイルの同意カテゴリ。             |
| `Engagement`      | エンゲージメントの同意カテゴリ。     |
| `Monitoring`      | モニタリングの同意カテゴリ。         |
| `Crm`             | CRMの同意カテゴリ。                  |
| `Cdp`             | CDPの同意カテゴリ。                  |
| `CookieMatch`     | Cookie Matchの同意カテゴリ。         |
| `Misc`            | その他の同意カテゴリ。               |

### `SetConsentExpiryListener()`

ユーザーの同意構成が[`ConsentExpiry`](#consentexpiry)に従って期限切れになった後に実行するコールバックを定義します。Tealiumが完全に初期化されるように、このリスナーを初期化コールバック内で定義することを推奨します。

```javascript
TealiumUnityPlugin.SetConsentExpiryListener(callback);
```

| パラメータ | 型       | 説明                                 |
|:-----------|:---------|:-------------------------------------|
| `callback` | `Action` | 同意の期限切れ後に実行するコード。   |

例：

```javascript
TealiumUnityPlugin.SetConsentExpiryListener(()
    => TealiumLogger.Log("Consent Expired!!"));
```

### `SetConsentStatus()`

ユーザーの同意ステータスを構成します。デフォルトは`.Unknown`です。

```javascript
TealiumUnityPlugin.SetConsentStatus(status);
```

| パラメータ | 型              | 説明                       | 例                        |
|:-----------|:----------------|:---------------------------|:--------------------------|
| `status`   | `ConsentStatus` | ユーザーの同意ステータス。 | `ConsentStatus.Consented` |

例：

```javascript
TealiumUnityPlugin.SetConsentStatus(ConsentStatus.Consented);
```

#### `ConsentStatus`

| 値              | 説明                           |
|:----------------|:-------------------------------|
| `.Consented`    | 同意済みの同意ステータス。     |
| `.NotConsented` | 未同意の同意ステータス。       |
| `.Unknown`      | 不明な同意ステータス。         |

### `SetVisitorServiceListener()`

訪問プロファイルが更新されたときに実行するコールバックを定義します。更新された[`VisitorProfile`](#visitorprofile)はコールバックのレスポンスで提供されます。

VisitorServiceモジュールは、Tealium Customer Data Hubの[データレイヤーエンリッチメント](https://docs.tealium.com/about-data-layer-enrichment/)機能を実装します。

Customer Data Platform（CDP）のライセンスを保有し、訪問プロファイルを使用してモバイルアプリケーションのユーザーエクスペリエンスを向上させる場合は、このモジュールの使用を推奨します。Customer Data Platform（CDP）のライセンスを保有していない場合、訪問プロファイルは返されないため、このモジュールの使用は推奨されません。

```javascript
TealiumUnityPlugin.setVisitorServiceListener(callback);
```

| パラメータ | 型                                   | 説明                                                   |
|:-----------|:-------------------------------------|:-------------------------------------------------------|
| `callback` | `Action<Dictionary<string, object>>` | 更新された訪問プロファイルが返された後に実行するコード。 |

例：

```javascript
TealiumUnityPlugin.setVisitorServiceListener((profile) => {
  string? serializedProfile = JsonConvert.SerializeObject(profile);
  if (serializedProfile != null) {
      TealiumLogger.Log(serializedProfile);
  }
});
```

### `RemoveFromDataLayer()`

以前に`TealiumUnityPlugin.AddToDataLayer()`を使用して構成した永続データを削除します。

```javascript
TealiumUnityPlugin.RemoveFromDataLayer(keys);
```

| パラメータ | 型             | 説明             | 例                                 |
|:-----------|:---------------|:-----------------|:-----------------------------------|
| `keys`     | `List<string>` | キー名の配列。   | `new List<string>(){"foo", "bar"}` |

### `RemoveRemoteCommand()`

リモートコマンドマネージャーからリモートコマンドを削除します。

```javascript
TealiumUnityPlugin.RemoveRemoteCommand(id);
```

| パラメータ | 型       | 説明                                 | 例             |
|:-----------|:---------|:-------------------------------------|:---------------|
| `id`       | `string` | 削除するコマンドIDの名前。           | `test_command` |

例：

```javascript
TealiumUnityPlugin.RemoveRemoteCommand("firebase");
```

### `Track()`

ゲームまたはゲームビューに対するユーザーの操作をトラッキングします。

```javascript
TealiumUnityPlugin.Track(dispatch);
```

| パラメータ | 型                                              | 説明                                               | 例                             |
|:-----------|:------------------------------------------------|:---------------------------------------------------|:-------------------------------|
| `dispatch` | [`TealiumDispatch`](#interface-tealiumdispatch) | イベント名とデータレイヤーを含むTealiumディスパッチ。 | `TealiumEvent("button_click")` |

ゲームイベントをトラッキングするには、[`TealiumEvent`](#class-tealiumevent)オブジェクトを作成し、`track()`メソッドに渡します。

```javascript
TealiumEvent event = TealiumEvent('GAME_EVENT_NAME', new Dictionary<string, object> {{"KEY", "VALUE"}});
TealiumUnityPlugin.Track(event);
```

ゲームの画面表示をトラッキングするには、[`TealiumView`](#class-tealiumview)オブジェクトを作成し、`track()`メソッドに渡します。  

```javascript
TealiumView view = new TealiumView("VIEW_NAME", new Dictionary<string, object> {{"KEY", "VALUE"}})
TealiumUnityPlugin.Track(view);
```

### `Terminate()`

Tealiumライブラリを無効にし、すべてのモジュール参照を削除します。必要な場合は、新しいTealiumインスタンスを作成して再度有効にします。

```javascript
TealiumUnityPlugin.Terminate();
```
### `VisitorProfile`

訪問プロファイルは、各属性のわかりやすい名前を含むオブジェクトです。訪問属性と訪問属性のタイプを区別できる `currentVisit` プロパティがあります。添字を使用して、ID から各属性値にアクセスします。属性が存在しない場合は、`null` が返されます。

**属性タイプ**

| パラメーター       | プロパティ                                                                                                              | 値                                                                                                                                |
|:-------------------|:------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------|
| `arraysOfBooleans` | id: `string`、value: `bool`                                                                                             | id: "5129" value: [true,false,true,true]                                                                                           |
| `arraysOfNumbers`  | id: `string`、value: `double[]`                                                                                         | `id: "57", value: [4.82125, 16.8, 0.5714285714285714]`                                                                            |
| `arraysOfStrings`  | id: `string`、value: `string[]`                                                                                         | `id: "5213", value: ["green shirts", "green shirts", "blue shirts"]`                                                              |
| `audiences`        | id: string、value: string                                                                                               | `id: "tealiummobile\_demo\_103", value: "iOS Users"`                                                                              |
| `badges`           | id: `string`、value: `bool`                                                                                             | `id: "2815", value: true`                                                                                                         |
| `booleans`         | id: `string`、value: `bool`                                                                                             | `id: "4868", value: true`                                                                                                         |
| `currentVisit`     | 現在の訪問の visitorProfile に含まれるすべての属性。現在の訪問プロファイルには、オーディエンスまたはバッジは含まれません。 | `TealiumCurrentVisitProfile(dates: ["5376": 1567536668080, "10": 1567536668000], booleans: ["4530": true], numbers: ["32": 3.8])` |
| `dates`            | id: `string`、value: `int`                                                                                              | `id: "22", value: 1567120112000`                                                                                                  |
| `numbers`          | id: `string`、value: `double`                                                                                           | `id: "5728", value: 4.82125`                                                                                                      |
| `setOfStrings`     | id: `string`、value: `string[]`                                                                                         | `id: "5211", value: ["green shirts", "red shirts", "blue shirts"]`                                                                |
| `string`           | id: `string`、value: `string`                                                                                           | `id: "5380", value: "green shirts"`                                                                                               |
| `tallies`          | id: `string`、value: `Dictionary<string, float>`                                                                        | `"57": [["category 1": 2.0], "category 2": 1.0]]`                                                                                 |
| `tallyValue`       | id: `string`、value: `float`                                                                                            | `["category 1": 2.0]`                                                                                                             |
## クラス：`TealiumConfig`

以下に、`TealiumConfig` クラスのプロパティの概要を示します。

| パラメータ                     | 型                                                | 説明                                                                                                                                                                                                                                                  | 例                                           |
|:-------------------------------|:--------------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------|
| `account`                      | `string`                                          | （必須）Tealium アカウント名。                                                                                                                                                                                                                             | `companyXYZ`                                 |
| `profile`                      | `string`                                          | （必須）Tealium プロファイル名。                                                                                                                                                                                                                             | `main`                                       |
| `environment`                  | [`TealiumEnvironment`](#class-tealiumenvironment) | （必須）Tealium 環境名。                                                                                                                                                                                                                         | `TealiumEnvironment.Dev`                     |
| `dataSource`                   | `string`                                          | CDH データソースキー。                                                                                                                                                                                                                                         | `abc123`                                     |
| `collectors`                   | `List<Collectors>`                                | （必須）Tealium ライブラリの初期化に使用する [`Collectors`](#collectors) のリストを構成します。                                                                                                                                                              | `new List<Collectors>(){Collectors.AppData}` |
| `dispatchers`                  | `List<Dispatchers>`                               | （必須）Tealium ライブラリの初期化に使用する [`Dispatchers`](#dispatchers) のリストを構成します。                                                                                                                                                            | `new List<Collectors>(){Dispatchers.Collec}` |
| `customVisitorId`              | `string`                                          | カスタム訪問 ID を構成します。                                                                                                                                                                                                                                    | `ALK2398LSDKJ3289SLKJ3298SLKJ3`              |
| `memoryReportingEnabled`       | `bool`                                            | DeviceData モジュールのメモリレポートを有効または無効にします（デフォルト：無効）。                                                                                                                                                                           | `true`                                       |
| `overrideCollectURL`           | `string`                                          | Tealium Collect URL を上書きし、別のエンドポイントにデータを送信します。イベントバッチ処理機能を使用する場合は、`overrideCollectBatchURL` プロパティも上書きしてください。                                                                                           | `https://custom-domain.com/event`            |
| `overrideCollectBatchURL`      | `string`                                          | Tealium Collect のバッチ URL を上書きし、別のエンドポイントにデータを送信します。                                                                                                                                                                                | `https://custom-domain.com/batch-event`      |
| `overrideCollectProfile`       | `String`                                          | Tealium Collect プロファイルを上書きし、別の Tealium プロファイルにデータを送信します。
| `custom-profile`                                                                                              |
| `overrideLibrarySettingsURL`   | `string`                                          | 公開構成 URL を上書きします。                                                                                                                                                                                                                          | `https://custom-domain.com/mobile.html`      |
| `overrideTagManagementURL`     | `string`                                          | Tag Management モジュールで使用されるデフォルト URL を上書きします。Tealium JavaScript ファイルをセルフホスティングする場合に必要です。                                                                                                                           | `https://custom-domain.com/path/env/utag.js` |
| `deepLinkTrackingEnabled`      | `bool`                                            | Facebook やその他のソースからアプリへのリンクなど、[標準ディープリンクの自動トラッキング](https://docs.tealium.com/ja/platforms/getting-started-mobile/deep-linking/#readout)と QR Trace を有効または無効にします（デフォルト：有効）。                                          | `false`                                      |
| `qrTraceEnabled`               | `bool`                                            | [QR Trace](https://docs.tealium.com/ja/platforms/getting-started-mobile/trace/#how-it-works) を有効または無効にします（デフォルト：有効）。                                                                                                                                                            | `false`                                      |
| `loglevel`                     | [`LogLevel`](#loglevel)                           | ログに記録される情報量を制御するログレベルプロパティを構成します（デフォルト：サイレント）。                                                                                                                                                                | `LogLevel.dev`                               |
| `consentExpiry`                | [`ConsentExpiry`](#consentexpiry)                 | ユーザーの同意構成の有効期限を構成します（デフォルトはポリシーによって異なります）。                                                                                                                                                                      | `ConsentExpiry(90, TimeUnit.days)`           |
| `consentLoggingEnabled`        | `bool`                                            | 監査のためにすべての同意ステータスの変更を Tealium Customer Data Hub に送信する、[同意ログ](https://docs.tealium.com/consent-change-event-specifications/)機能を有効にします（デフォルト：有効）。    | `true`                                       |
| `consentPolicy`                | [`ConsentPolicy`](#consentpolicy)                 | 同意ポリシーを CCPA または GDPR に構成します。このプロパティが構成されている場合にのみ、同意マネージャーが有効になります。                                                                                                                                                     | `ConsentPolicy.GDPR`                         |
| `lifecycleAutotrackingEnabled` | `bool`                                            | ライフサイクルの自動トラッキングを有効または無効にします（デフォルト：有効）。                                                                                                                                                                                              | `false`                                      |
| `useRemoteLibrarySettings`     | `bool`                                            | [モバイルパブリッシュ構成](https://docs.tealium.com/create-mobile-profile/)を有効または無効にします（デフォルト：有効）。タグ管理でモバイルパブリッシュ構成を構成するか、この機能を無効にしてください。 | `false`                                      |
| `visitorServiceEnabled`        | `bool`                                            | [データレイヤーエンリッチメントAPI](https://docs.tealium.com/data-layer-enrichment-api/)を使用した訪問プロファイルの自動取得を有効または無効にします（デフォルト：無効）。                                | `true`                                       |
| `sessionCountingEnabled`       | `Boolean`                                   | タグ管理アカウントのセッションカウントを有効または無効にします。Tealium JavaScriptファイルをセルフホスティングしている場合は、これを`false`に構成してください（デフォルト：有効）。                                                                                                            | `false`                                                                                                        |


## クラス：`TealiumEnvironment`

`TealiumEnvironment`は、3つのデフォルト環境（Dev、QA、Prod）のいずれか、またはTealiumのパブリッシュ先となるカスタム環境です。

例：

```javascript
TealiumEnvironment.Dev
```

次の環境を使用できます。

| 値      | 説明         |
|:--------|:-------------|
| `.Dev`  | 開発環境。   |
| `.Qa`   | QAまたはUAT環境。 |
| `.Prod` | 本番環境。   |


## インターフェース：`TealiumDispatch`

トラッキングするディスパッチのタイプを定義するインターフェースです。次のクラスが`TealiumDispatch`を実装しています。

### クラス：`TealiumEvent`

ゲームまたはゲームビューに対するユーザーの操作をトラッキングするには、`TealiumEvent(eventName, dataLayer)`のインスタンスを[`Track()`](#track)メソッドに渡します。`TealiumEvent`は、トラッキング呼び出しで`tealium_event`として表示されるイベント名と、任意のデータディクショナリで構成されます。

```javascript
TealiumEvent(viewName, dataLayer)
```

| パラメータ  | 型                           | 説明                                   | 例                                                                                                |
|:------------|:-----------------------------|:---------------------------------------|:--------------------------------------------------------------------------------------------------|
| `eventName` | `string`                     | ゲームイベントの名前。                 | `level_completed`                                                                                 |
| `dataLayer` | `Dictionary<string, object>` | （任意）イベントとともに送信するデータ。 | `new Dictionary<string, object> {{"user_id", "gamer123"}, {"level": 2}, {"total_points": 17500}}` |

例：

```javascript
TealiumEvent event = TealiumEvent('EVENT_NAME',
    new Dictionary<string, object> {{"KEY", "VALUE"}});
TealiumUnityPlugin.Track(event);
```

### クラス：`TealiumView`

ゲーム内の画面ビューをトラッキングするには、`TealiumView(viewName, dataLayer)`のインスタンスを[`Track()`](#track)メソッドに渡します。`TealiumView`は、トラッキング呼び出しで`tealium_event`として表示されるビュー名と、任意のデータディクショナリで構成されます。

```javascript
TealiumView(viewName, dataLayer)
```

| パラメータ  | 型                           | 説明                                   | 例                                                           |
|:------------|:-----------------------------|:---------------------------------------|:-------------------------------------------------------------|
| `viewName`  | `string`                     | ゲーム内のビューまたは画面の名前。     | `login_view`                                                 |
| `dataLayer` | `Dictionary<string, object>` | （任意）イベントとともに送信するデータ。 | `new Dictionary<string, object> {{"customer_id", "abc123"}}` |

例：

```javascript
TealiumView view = new TealiumView("VIEW_NAME",
    new Dictionary<string, object> {{"KEY", "VALUE"}})
TealiumUnityPlugin.Track(view);
```