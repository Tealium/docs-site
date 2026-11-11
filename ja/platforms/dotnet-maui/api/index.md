---
title: APIリファレンス
description: Tealiumが.NET MAUI向けに提供するクラスとメソッドのリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/dotnet-maui/api/
---
## クラス：`Tealium`

Tealium .NET MAUIライブラリの`Tealium`クラスで使用できるメソッドと定数について説明します。

### `AddRemoteCommand()`

リモートコマンドをリモートコマンドマネージャーに追加します。

```csharp
void AddRemoteCommand(IRemoteCommand remoteCommand);
```

| パラメータ      | 型               | 説明                                                                                             |
|:----------------|:-----------------|:-------------------------------------------------------------------------------------------------|
| `remoteCommand` | `IRemoteCommand` | 必須のリモートコマンドプロパティを提供する、IRemoteCommandインターフェイスの実装。 |

例：

```csharp
public class MyRemoteCommand : IRemoteCommand
    {
        public string CommandId => "my_remote_command";
        public string Description => "description of my remote command";
        public string Path => null;
        public string Url => null;

        public void Dispose()
        {
            //
        }

        public void HandleResponse(IRemoteCommandResponse response)
        {
            var str = response.Payload.GetValueForKey<String>("key");
            if (str == "")
            {
                // etc
            }
        }
    }

tealium.AddRemoteCommand(new MyRemoteCommand());
```

### `AddToDataLayer()`

指定された有効期限で、永続データ保存にデータを追加します。

```csharp
void AddToDataLayer(IDictionary<string, object> data, Expiry expiry);
```

| パラメータ | 型 | 説明 |
|:-----------|:-----|:------------|
| `data`     | `IDictionary<string, object>` | キーが文字列、値がプリミティブまたはコレクションであるキーと値のペアのIDictionary |
| `expiry`   | [`Expiry`](#expiry)           | データを保持する期間 |

```csharp
tealium.AddToDataLayer(new Dictionary<string, object> {
  { "user_language", lang }
}, Expiry.Forever);
```

### `ClearStoredVisitorIds()`

保存されている訪問IDをクリアし、新しいIDを生成します。主に法令遵守のために使用します。

データレイヤーに該当するキーが含まれている場合、構成項目`visitorIdentityKey`に基づいて訪問IDの保存が継続されます。

```csharp
tealium.ClearStoredVisitorIds();
```


<blockquote>
保存をクリアした後、リセットされた新しい`visitorId`が現在のIDとともに保存されないようにするには、事前にデータレイヤーからIDキーを削除する必要があります（[`RemoveFromDataLayer()`](#removefromdatalayer)を参照）。
</blockquote>


### ConsentCategory

同意カテゴリの値です。[`GetConsentCategories`](#getconsentcategories)および[`SetConsentCategories`](#setconsentcategories)で使用します。

同意カテゴリは次のとおりです。

* `ConsentManager.ConsentCategory.Analytics`
* `ConsentManager.ConsentCategory.Affiliates`
* `ConsentManager.ConsentCategory.BigData`
* `ConsentManager.ConsentCategory.Cdp`
* `ConsentManager.ConsentCategory.CookieMatch`
* `ConsentManager.ConsentCategory.Crm`
* `ConsentManager.ConsentCategory.DisplayAds`
* `ConsentManager.ConsentCategory.Email`
* `ConsentManager.ConsentCategory.Engagement`
* `ConsentManager.ConsentCategory.Misc`
* `ConsentManager.ConsentCategory.Mobile`
* `ConsentManager.ConsentCategory.Monitoring`
* `ConsentManager.ConsentCategory.Personalization`
* `ConsentManager.ConsentCategory.Search`
* `ConsentManager.ConsentCategory.Social`

### ConsentStatus

同意ステータスの値です。[`SetConsentStatus()`](#setconsentstatus)で使用します。

| 値                                          | 説明       |
|:--------------------------------------------|:-----------|
| `ConsentManager.ConsentStatus.Consented`    | 同意済み   |
| `ConsentManager.ConsentStatus.NotConsented` | 未同意     |
| `ConsentManager.ConsentStatus.Unknown`      | 不明       |

### Environment

環境には、3つのデフォルト環境（Dev、QA、Prod）のいずれか、またはパブリッシュ先として指定した任意のカスタム環境を使用します。

| 値                 | 説明 |
|:-------------------|:-----|
| `Environment.dev`  | 開発 |
| `Environment.qa`   | QA/UAT |
| `Environment.prod` | 本番 |

### Expiry

永続データまたは揮発性データの有効期限を定義します。[`AddToDataLayer()`](#addtodatalayer)で使用します。

| 値                    | 説明                                     |
|:----------------------|:-----------------------------------------|
| `Expiry.Session`      | 現在のアクティブなセッションの継続期間。 |
| `Expiry.UntilRestart` | 次回の再起動までの期間。                 |
| `Expiry.Forever`      | アプリが削除されるまでの期間。           |

### `GatherTrackData()`

Collectorとデータレイヤーからすべてのトラッキングデータを収集します。

```csharp
GatherTrackData(callback);
```

| パラメータ | 型         | 説明                                          | 例       |
|:-----------|:-----------|:-----------------------------------------------------|:--------------|
| `callback` | `Function` | 取得したキーの値を使用するコールバック関数。コールバックはJSONオブジェクトを返します。 | （例を参照） |

例：

```csharp
tealium.GatherTrackData(data => {
    foreach (var entry in data)
    {
        System.Diagnostics.Debug.WriteLine($"key ({entry.Key}) - value: {Stringify(entry.Value)}");
    }
});
```

### `GetFromDataLayer()`

永続データレイヤーから、指定されたキーの値を取得します。

```csharp
object? GetFromDataLayer(string key);
```

| パラメータ | 型       | 説明                                   |
|:-----------|:---------|:---------------------------------------|
| `key`      | `String` | データレイヤーから取得するキー         |

```csharp
string myString = (string)tealium.GetFromDataLayer("user_language");
```

### `GetConsentCategories()`

ユーザーが同意したカテゴリのリストを取得します。

```csharp
List<ConsentCategory>? GetConsentCategories();
```

例：

```csharp
tealium.GetConsentCategories().ForEach((c) =>
{
    if (c == ConsentManager.ConsentCategory.Analytics)
    {
        // consented to Analytics
    }
});
```

### `GetConsentStatus()`

ユーザーの現在の同意状態を取得します。[`ConsentStatus`](#consentstatus)の値を返します。

```csharp
ConsentStatus GetConsentStatus();
```

例：

```csharp
switch (tealium.GetConsentStatus()) {
    case ConsentManager.ConsentStatus.Unknown:
        break;
    case ConsentManager.ConsentStatus.Consented:
        break;
    case ConsentManager.ConsentStatus.NotConsented:
        break;
}
```

### `GetVisitorId()`

ユーザーの訪問IDを取得し、コールバック関数の形式で返します。

```csharp
string? visitorId = tealium.GetVisitorId();
```

### `JoinTrace()`

指定されたIDのトレースに参加します。Tealium Customer Data Hubの[Trace](https://docs.tealium.com/manage-traces/)機能について詳しく確認してください。

```csharp
tealium.JoinTrace(id);
```

| パラメータ | 型       | 説明       | 例         |
|:-----------|:---------|:-----------|:-----------|
| `id`       | `String` | トレースID | `abc123xy` |

### `LeaveTrace()`

トレースは、`leaveTrace()`メソッドが呼び出されるまで、アプリのセッション中はアクティブな状態を維持します。このメソッドを呼び出すと、以前参加したトレースから離脱し、訪問セッションを終了します。

```csharp
tealium.LeaveTrace();
```

### `RemoveFromDataLayer()`

以前に[`AddToDataLayer()`](#addtodatalayer)を使用して構成した永続データを削除します。

```csharp
void RemoveFromDataLayer(ICollection<string> keys);
```

| パラメータ | 型                    | 説明                 |
|:-----------|:----------------------|:---------------------|
| `keys`     | `ICollection<String>` | キー名のコレクション |
  
```csharp
tealium.RemoveFromDataLayer(new string[] { "key1", "key2" });
```
### `RemoveRemoteCommand()`

リモートコマンドマネージャーからリモートコマンドを削除します。

```csharp
void RemoveRemoteCommand(string id);
```

| パラメータ | 型       | 説明                         |
|:-----------|:---------|:-----------------------------|
| `id`       | `String` | 削除するコマンドIDの名前     |

```csharp
tealium.RemoveRemoteCommand("firebase");
```

### `ResetVisitorId()`

訪問IDをリセットし、新しいIDを生成します。

```csharp
tealium.ResetVisitorId();
```

### `SetConsentCategories()`

ユーザーが同意したカテゴリーのリストを構成します。[`ConsentCategory`](#consentcategory) とともに使用します。

```csharp
void SetConsentCategories(List<ConsentCategory> categories);
```

| パラメータ   | 型                      | 説明                               |
|:-------------|:------------------------|:-----------------------------------|
| `categories` | `List<ConsentCategory>` | ユーザー同意カテゴリーのリスト。   |

```csharp
tealium.SetConsentCategories(new List<ConsentManager.ConsentCategory>()
{
    ConsentManager.ConsentCategory.DisplayAds,
    ConsentManager.ConsentCategory.Analytics
});
```

### `SetConsentExpiryListener()`

同意構成の有効期限が切れたときに実行するコールバックメソッドを構成します。

```csharp
void SetConsentExpiryListener(Action callback);
```

| パラメータ  | 型       | 説明                                         |
|:------------|:---------|:---------------------------------------------|
| `callback  ` | `Action` | 同意の有効期限が切れたときに実行するコード。 |
  
```csharp
tealium.SetConsentExpiryListener(() =>
{
    System.Diagnostics.Debug.WriteLine("Consent Expired");
});
```

### `SetConsentStatus()`

ユーザーの同意ステータスを構成します。構成されるまでのデフォルト値は `.Unknown` です。

```csharp
void SetConsentStatus(ConsentStatus status);
```

| パラメータ | 型              | 説明                                                                          |
|:-----------|:----------------|:------------------------------------------------------------------------------|
| `status  ` | `ConsentStatus` | ユーザーの同意ステータス。[ConsentManager.ConsentStatus](#consentstatus) を参照してください。 |

```csharp
tealium.SetConsentStatus(ConsentManager.ConsentStatus.NotConsented);
```

### `SetVisitorServiceListener()`

訪問プロファイルが更新されたときに実行するコールバック関数を構成します。更新された [`VisitorProfile`](#instance-ivisitorprofile) は、コールバックのレスポンスで提供されます。[`visitorServiceEnabled`](https://docs.tealium.com/ja/platforms/dotnet-maui/install/#config) が `true` に構成されている場合に使用します。

Customer Data Platform（CDP）のライセンスがあり、訪問プロファイルを使用してモバイルアプリケーションのユーザーエクスペリエンスを向上させる場合は、この機能を使用します。

```csharp
void SetVisitorServiceListener(Action callback);
```

| パラメータ  | 型       | 説明                                               |
|:------------|:---------|:---------------------------------------------------|
| `callback  ` | `Action` | 訪問プロファイルを取得したときに実行するコード。 |
  
```csharp
tealium.SetVisitorServiceListener((visitorProfile) =>
{
    System.Diagnostics.Debug.WriteLine("Visitor Updated");
    System.Diagnostics.Debug.WriteLine($"Visitor: {visitorProfile}");
});
```

### `TerminateIntance()`

Tealiumライブラリを無効にし、すべてのモジュール参照を削除します。

```csharp
tealium.TerminateIntance();
```

### `Track()`

オプションのイベントデータを使用して、スクリーンビューまたはイベントをトラッキングします。

```csharp
tealium.Track(tealiumEvent);
```

| パラメータ     | 型                                      | 説明                                                                                                 |
|:---------------|:----------------------------------------|:-----------------------------------------------------------------------------------------------------|
| `tealiumEvent` | `TealiumView` または `TealiumEvent`     | イベント名と、イベントとともに送信するオプションデータをキーと値の形式で含むディスパッチオブジェクト。 |

イベントをトラッキングするには、[`TealiumView`](#class-tealiumview) または [`TealiumEvent`](#class-tealiumevent) のインスタンスを `track()` メソッドに渡します。

```csharp
tealium.Track(new TealiumEvent("cart_add", new Dictionary<string, object> {
    { "customer_id", "abc123" }, 
    { "product_id", new[] {"PROD123", "PROD456"} },
    { "product_price", new[] {4.00, 6.00} }
}));
```
## クラス：`TealiumConfig`

以下に、`TealiumConfig`クラスのプロパティをまとめます。

| パラメータ | 型 | 説明 | 例 |
|:----------|:----|:-----------|:-------|
| `account`| `String`| （必須）Tealiumアカウント名 | `"companyXYZ" `|
| `profile`| `String`| （必須）Tealiumプロファイル名 | `"main"`|
| `environment`| [`Environment`](#environment) | （必須）Tealium環境名 | `Environment.dev`|
| `dataSource`| `String`| CDHデータソースキー | `"abc123"`|
| `collectors`| `Collectors[]`| （必須）Tealiumライブラリの初期化に使用する[`Collectors`](#collectors)のリストを構成します | `[Collectors.AppData]`|
| `dispatchers`| `Dispatchers[]`| （必須）Tealiumライブラリの初期化に使用する[`Dispatchers`](#dispatchers)のリストを構成します | `[Dispatchers.Collect]`|
| `customVisitorId`| `String`| カスタム訪問IDを構成します | `"ALK2398LSDKJ3289SLKJ3298SLKJ3"`|
| `memoryReportingEnabled` | `Boolean`| DeviceDataモジュールのメモリレポートを有効または無効にします（デフォルト：無効）。 | `true`|
| `overrideCollectDomain` | `String`| Tealium Collect URLのドメインを上書きします。[ファーストパーティドメイン](https://docs.tealium.com/ja/tag-management/administration/first-party-domains/manage/)で使用します。 | `"your-domain.com"`|
| `overrideCollectProfile` | `String`| データを別のTealiumプロファイルに送信するため、Tealium Collectプロファイルを上書きします。 | `"custom-profile"`|
| `overrideCollectURL` | `String`| データを別のエンドポイントに送信するため、Tealium Collect URLを上書きします。イベントバッチ処理機能を使用する場合は、`overrideCollectBatchURL`プロパティも上書きしてください。 | `"https://custom-domain.com/event"`|
| `overrideCollectBatchURL` | `String`| データを別のエンドポイントに送信するため、Tealium CollectのバッチURLを上書きします。 | `"https://custom-domain.com/batch-event"`|
| `overrideLibrarySettingsURL` | `String`| パブリッシュ構成URLを上書きします。 | `"https://custom-domain.com/mobile.html"`|
| `overrideTagManagementURL` | `String`| Tag Managementモジュールが使用するデフォルトURLを上書きします。Tealium JavaScriptファイルをセルフホスティングする場合に必要です。 | `"https://custom-domain.com/path/env/utag.js"`|
| `deepLinkTrackingEnabled` | `Boolean`| FacebookなどのソースからアプリへのリンクやQR Traceなど、[標準ディープリンクの自動トラッキング](https://docs.tealium.com/ja/platforms/getting-started-mobile/deep-linking/#readout)を有効または無効にします（デフォルト：有効）。 | `false`|
| `qrTraceEnabled` | `Boolean`| [QR Trace](https://docs.tealium.com/ja/platforms/getting-started-mobile/trace/#how-it-works)を有効または無効にします（デフォルト：有効）。 | `false`|
| `loglevel` | [`LogLevel`](#loglevel) | 記録する情報量を制御するログレベルプロパティを構成します（デフォルト：サイレント）。 | `LogLevel.dev`|
| `consentExpiry` | [`ConsentExpiry`](#consentexpiry) | ユーザーの同意構成の有効期限を構成します（デフォルトはポリシーによって異なります）。 | `ConsentExpiry(90, TimeUnit.days)`|
| `consentLoggingEnabled` | `Boolean`| 監査目的ですべての同意ステータス変更をTealium Customer Data Hubに送信する[Consent Logging](https://docs.tealium.com/consent-change-event-specifications/)機能を有効にします（デフォルト：有効）。 | `true`|
| `consentPolicy` | [`ConsentPolicy`](#consentpolicy) | CCPAやGDPRなどの同意ポリシーを構成します。このプロパティが構成されている場合にのみ、同意マネージャーが有効になります。 | `ConsentPolicy.gdpr`|
| `lifecycleAutotrackingEnabled` | `Boolean`| ライフサイクルの自動トラッキングを有効または無効にします（デフォルト：有効）。 | `false`|
| `useRemoteLibrarySettings` | `Boolean`| [Mobile Publish Settings](https://docs.tealium.com/create-mobile-profile/)を有効または無効にします（デフォルト：有効）。Tag ManagementでMobile Publish Settingsを構成するか、この機能を無効にしてください。 | `false`|
| `visitorServiceEnabled` | `Boolean`| [Data Layer Enrichment API](https://docs.tealium.com/data-layer-enrichment-api/)を使用した訪問プロファイルの自動取得を有効または無効にします（デフォルト：無効）。 | `true`|
| `remoteCommands` | `RemoteCommand[]`| インスタンスの準備が整ったときに追加する[RemoteCommand](#RemoteCommand)オブジェクトのリストを構成します | `[{ id: "hello-world", callback: (payload) => { console.log("hello-world: " + JSON.stringify(payload)); } }]` |
| `overrideConsentCategoriesKey` | `String` | 同意カテゴリのイベント属性名を上書きします。サーバー側の同意をカスタム適用する場合に使用します。[サーバー側の同意の自動適用を無効にする方法](https://docs.tealium.com/server-side-consent-management/)について詳しく確認してください（デフォルト：`consent_categories`）。 | `consent_categories_granted` |
| `visitorIdentityKey` | `String` | 訪問の切り替えをサポートし、アプリの複数ユーザーを識別するための共有キーを指定する場合に使用します。 | `user_profile_id` |

### Collectors

Collectorは、デバイスから補足情報を収集し、Tealium Customer Data Hubへ送信する前にデータレイヤーへ追加するモジュールです。一部のCollectorはコアライブラリに含まれていますが、その他はオプションであり、個別のモジュールとしてインストールされます。

次の表に、利用可能なCollectorを示します。デフォルトのCollectorは、名前の横にある`*`で示されています。

| Collector名 | TealiumConfigリファレンス |
|:----------------|:--------------------------|
| `AppData`*      | `Collectors.AppData`      |
| `Connectivity`* | `Collectors.Connectivity` |
| `Device`        | `Collectors.Device`       |
| `Lifecycle`     | `Collectors.Lifecycle`    |

これらのモジュールは、[`TealiumConfig`](#class-tealiumconfig)に構成された`Collectors`プロパティを使用して有効または無効にします。

```csharp
TealiumConfig tealConfig = new TealiumConfig(
    // ...
    new List<Collectors> {
        Collectors.LifeCycle, Collectors.Device
    }
    // ...
);
```

### ConsentExpiry

[`TealiumConfig`](#class-tealiumconfig)オブジェクトで同意構成の有効期限を構成します。

| パラメータ | 型 | 説明 |
|:-----------|:-----------|:-----------|
| `time` | `Number` | 有効期限までの時間。 |
| `unit` | `TimeUnit` | 有効期限までの時間単位。`TimeUnit.Minutes`、`TimeUnit.Hours`、`TimeUnit.Days`、`TimeUnit.Months`のいずれかです。 |

```csharp
TealiumConfig config = new TealiumConfig(
  //...
  consentExpiry = new TimeUnit(90, TimeUnit.Days)),
  //...
);
```

### ConsentPolicy

[`TealiumConfig`](#class-tealiumconfig)オブジェクトで使用する同意ポリシーを構成します。同意ポリシーが構成されていない場合、同意マネージャーは無効になります。

```csharp
TealiumConfig config = new TealiumConfig(
  //...
  consentPolicy = ConsentPolicy.GDPR,
  //...
);
```

同意の値：

* `ConsentPolicy.GDPR`
* `ConsentPolicy.CCPA`

### Dispatchers

Dispatcherは、データをTealiumエンドポイントに送信するモジュールです。これらは[`TealiumConfig`](#class-tealiumconfig)オブジェクトに構成します。

```csharp
TealiumConfig tealConfig = new TealiumConfig(
    // ...
    new List<Dispatchers> {
        Dispatchers.Collect, Dispatchers.RemoteCommands
    }
    // ...
);
```

次のDispatcherを利用できます。

* `Dispatchers.Collect`
* `Dispatchers.RemoteCommands`
* `Dispatchers.TagManagement`


<blockquote>
少なくとも1つのDispatcherが必要です。
</blockquote>


### LogLevel

記録する情報量を制御するログレベルプロパティを、次のいずれかの値に構成します。

| 値 | 説明 |
|:------------------|:--------------------------------------------------------------------|
| `LogLevel.dev` | アプリケーションの進行状況を示す情報イベント |
| `LogLevel.qa` | アプリケーションのデバッグに使用するデバッグレベルのイベント |
| `LogLevel.prod` | 重大なエラーや障害などのエラーイベント |
| `LogLevel.silent` | ログを記録しない（デフォルト） |
## `IRemoteCommand`

構成済みのリモートコマンドを定義するインターフェイスです。

| 値             | 説明                                                        |
|:---------------|:------------------------------------------------------------|
| `CommandId`    | RemoteCommand の一意の識別子名                              |
| `Description`  | （任意）RemoteCommand の一意の識別子名                      |
| `Path`         | （任意）マッピングに使用するローカルファイル                |
| `Url`          | （任意）マッピングに使用するリモートファイル                |

## `IVisitorProfile`

（[`TealiumConfig.visitorServiceEnabled`](#class-tealiumconfig) で使用します。）

訪問プロファイルオブジェクトには、訪問サービスから返された訪問属性が含まれます。`currentVisit` プロパティには、現在の訪問をスコープとする属性が含まれます。添字を使用して、ID ごとに各属性値へアクセスします。属性が存在しない場合は、`null` が返されます。

| パラメータ | プロパティ | 値 |
|:----------|:----------|:-----|
| `ArraysOfBooleans` | `IDictionary<string, IList<bool>>`                 | `id: "5129", value: [true,false,true,true]`                          |
| `ArraysOfNumbers`  | `IDictionary<string, IList<double>>`               | `id: "57", value: [4.82125, 16.8, 0.5714285714285714]`               |
| `ArraysOfStrings`  | `IDictionary<string, IList<string>>`               | `id: "5213", value: ["green shirts", "green shirts", "blue shirts"]` |
| `Audiences`        | `IDictionary<string, string>`                      | `id: "tealiummobile\_demo\_103", value: "iOS Users"`                 |
| `Badges`           | `IDictionary<string, bool>`                        | `id: "2815", value: true`                                            |
| `Booleans`         | `IDictionary<string, bool>`                        | `id: "4868", value: true`                                            |
| `CurrentVisit`     | `ICurrentVisit`                                    |                                                                      |
| `Dates`            | `IDictionary<string, long>`                        | `id: "22", value: 1567120112000`                                     |
| `Numbers`          | `IDictionary<string, double>`                      | `id: "5728", value: 4.82125`                                         |
| `SetOfStrings`     | `IDictionary<string, ISet<string>>`                | `id: "5211", value: ["green shirts", "red shirts", "blue shirts"]`   |
| `Strings`          | `IDictionary<string, string>`                      | `id: "5380", value: "green shirts"`                                  |
| `Tallies`          | `IDictionary<string, IDictionary<string, double>>` | `"57": [["category 1": 2.0], "category 2": 1.0]]`                    |

### `ICurrentVisit`

現在の訪問をスコープとする属性を格納するオブジェクトです。

| パラメータ | プロパティ | 値 |
|:----------|:----------|:-----|
| `ArraysOfBooleans` | `IDictionary<string, IList<bool>>`                 | `id: "5129", value: [true,false,true,true]`                          |
| `ArraysOfNumbers`  | `IDictionary<string, IList<double>>`               | `id: "57", value: [4.82125, 16.8, 0.5714285714285714]`               |
| `ArraysOfStrings`  | `IDictionary<string, IList<string>>`               | `id: "5213", value: ["green shirts", "green shirts", "blue shirts"]` |
| `Booleans`         | `IDictionary<string, bool>`                        | `id: "4868", value: true`                                            |
| `Dates`            | `IDictionary<string, long>`                        | `id: "22", value: 1567120112000`                                     |
| `Numbers`          | `IDictionary<string, double>`                      | `id: "5728", value: 4.82125`                                         |
| `SetOfStrings`     | `IDictionary<string, ISet<string>>`                | `id: "5211", value: ["green shirts", "red shirts", "blue shirts"]`   |
| `Strings`          | `IDictionary<string, string>`                      | `id: "5380", value: "green shirts"`                                  |
| `Tallies`          | `IDictionary<string, IDictionary<string, double>>` | `"57": [["category 1": 2.0], "category 2": 1.0]]`                    |
| `TotalEventCount`  | `int`                                              | `42`                                                                 |
| `CreatedAt`        | `long`                                             | `1638236024`                                                         |


## インターフェイス：`TealiumDispatch`

追跡対象となるディスパッチの種類を定義するインターフェイスです。次のクラスが `TealiumDispatch` を実装します。

### クラス：`TealiumEvent`

ユーザーによる画面上の操作を追跡するには、`TealiumEvent(tealiumEvent, dataLayer)` のインスタンスを [`Track()`](#track) メソッドに渡します。`TealiumEvent` は、追跡呼び出しに `tealium_event` として表示されるイベント名と、任意のデータディクショナリで構成されます。

```csharp
tealium.Track(new TealiumEvent(tealiumEvent, eventData));
```

| パラメータ | 型 | 説明 |
|:------------|:--------|:-----------------|
| `tealiumEvent` | `string` | `tealium_event` 属性として渡されるイベント名。 |
| `eventData` | `Dictionary<string, object>` | （任意）イベントとともにキーと値の形式で送信するデータ。 |

例：

```csharp
tealium.Track(new TealiumEvent("cart_add", new Dictionary<string, object> {
    { "customer_id", "abc123" }, 
    { "product_id", new[] {"PROD123", "PROD456"} },
    { "product_price", new[] {4.00, 6.00} }
}));
```

### クラス：`TealiumView`

画面ビューを追跡するには、`TealiumView(tealiumEvent, dataLayer)` のインスタンスを [`Track()`](#track) メソッドに渡します。`TealiumView` は、追跡呼び出しに `tealium_event` として表示されるビュー名と、任意のデータディクショナリで構成されます。

```csharp
tealium.Track(new TealiumView(tealiumEvent, eventData));
```

| パラメータ | 型 | 説明 |
|:------------|:--------|:-----------------|
| `tealiumEvent` | `string` | ビューイベントまたは画面の `tealium_event` 名。 |
| `eventData` | `Dictionary<string, object>` | （任意）イベントとともにキーと値の形式で送信するデータ。 |

例：

```csharp
tealium.Track(new TealiumView("purchase", new Dictionary<string, object> {
    { "customer_id", "abc123" },
    { "order_total", 10.00 },
    { "product_id", new[] {"PROD123", "PROD456"} },
    { "order_id", "0123456789" }
}));
```