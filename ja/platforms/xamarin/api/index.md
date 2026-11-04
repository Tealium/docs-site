---
title: APIリファレンス
description: Xamarin向けにTealiumが提供するクラスとメソッドのリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/xamarin/api/
---
## クラス：`Tealium`

Tealium Xamarinライブラリの`Tealium`クラスで使用できるメソッドと定数です。

### `AddRemoteCommand()`

リモートコマンドマネージャーにリモートコマンドを追加します。

```csharp
void AddRemoteCommand(IRemoteCommand remoteCommand);
```

| パラメータ      | 型               | 説明                                                                                  |
|:----------------|:-----------------|:--------------------------------------------------------------------------------------|
| `remoteCommand` | `IRemoteCommand` | 必要なリモートコマンドプロパティを提供する、IRemoteCommandインターフェイスの実装です。 |

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

指定した有効期限に従って、永続データ保存にデータを追加します。

```csharp
void AddToDataLayer(IDictionary<string, object> data, Expiry expiry);
```

| パラメータ | 型                                 | 説明                                                                       |
|:-----------|:-----------------------------------|:---------------------------------------------------------------------------|
| `data`     | `IDictionary<string, object>`      | キーが文字列、値がプリミティブまたはコレクションであるキーと値のペアのIDictionary |
| `expiry`   | [`Expiry`](#expiry)                | データを保持する期間                                                       |

```csharp
tealium.AddToDataLayer(new Dictionary<string, object> {
  { "user_language", lang }
}, Expiry.Forever);
```

### `ClearStoredVisitorIds()`

保存されている訪問IDを消去し、新しいIDを生成します。主に法令遵守のために使用します。

データレイヤーに`visitorIdentityKey`で指定されたキーが含まれている場合、構成値`visitorIdentityKey`に基づいて訪問IDの保存が継続されます。

```csharp
tealium.ClearStoredVisitorIds();
```


<blockquote>
保存の消去後、リセットされた新しい`visitorId`を現在のIDとともに保存しないようにするには、事前にIDキーをデータレイヤーから削除する必要があります（[`RemoveFromDataLayer()`](#removefromdatalayer)を参照）。
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

環境は、3つのデフォルト環境（Dev、QA、Prod）のいずれか、またはパブリッシュ先として指定したカスタム環境です。

| 値                 | 説明     |
|:-------------------|:---------|
| `Environment.dev`  | 開発     |
| `Environment.qa`   | QA/UAT   |
| `Environment.prod` | 本番     |

### Expiry

永続データまたは揮発性データの有効期限を定義します。[`AddToDataLayer()`](#addtodatalayer)で使用します。

| 値                    | 説明                                 |
|:----------------------|:-------------------------------------|
| `Expiry.Session`      | 現在アクティブなセッションの期間です。 |
| `Expiry.UntilRestart` | 次回の再起動までの期間です。           |
| `Expiry.Forever`      | アプリが削除されるまでの期間です。     |


### `GetFromDataLayer()`

永続データレイヤーから、指定したキーの値を取得します。

```csharp
object? GetFromDataLayer(string key);
```

| パラメータ | 型       | 説明                                 |
|:-----------|:---------|:-------------------------------------|
| `key`      | `String` | データレイヤーから取得するキー       |

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

ユーザーの訪問IDを取得します。

```csharp
string? visitorId = tealium.GetVisitorId();
```

### `JoinTrace()`

指定したIDのトレースに参加します。Tealium Customer Data Hubの[トレース](https://docs.tealium.com/manage-traces/)機能について詳しく確認してください。

```csharp
tealium.JoinTrace(id);
```

| パラメータ | 型       | 説明       | 例         |
|:-----------|:---------|:-----------|:-----------|
| `id`       | `String` | トレースID | `abc123xy` |

### `LeaveTrace()`

トレースは、`leaveTrace()`メソッドが呼び出されるまで、アプリセッション中はアクティブなまま維持されます。このメソッドを呼び出すと、以前に参加したトレースから退出し、訪問セッションを終了します。

```csharp
tealium.LeaveTrace();
```

### `RemoveFromDataLayer()`

以前に[`AddToDataLayer()`](#addtodatalayer)を使用して構成した永続データを削除します。

```csharp
void RemoveFromDataLayer(ICollection<string> keys);
```

| パラメータ | 型                    | 説明               |
|:-----------|:----------------------|:-------------------|
| `keys`     | `ICollection<String>` | キー名のコレクション |
  
```csharp
tealium.RemoveFromDataLayer(new string[] { "key1", "key2" });
```

### `RemoveRemoteCommand()`

リモートコマンドマネージャーからリモートコマンドを削除します。

```csharp
void RemoveRemoteCommand(string id);
```

| パラメータ | 型       | 説明                             |
|:-----------|:---------|:---------------------------------|
| `id`       | `String` | 削除するコマンドIDの名前         |

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

| パラメーター | 型                      | 説明                               |
|:-------------|:------------------------|:-----------------------------------|
| `categories` | `List<ConsentCategory>` | ユーザー同意カテゴリーのリストです。 |

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

| パラメーター | 型       | 説明                                      |
|:-------------|:---------|:------------------------------------------|
| `callback  ` | `Action` | 同意の有効期限が切れたときに実行するコードです。 |
  
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

| パラメーター | 型              | 説明                                                                       |
|:-------------|:----------------|:---------------------------------------------------------------------------|
| `status  `   | `ConsentStatus` | ユーザーの同意ステータスです。[ConsentManager.ConsentStatus](#consentstatus) を参照してください。 |

```csharp
tealium.SetConsentStatus(ConsentManager.ConsentStatus.NotConsented);
```

### `SetVisitorServiceListener()`
訪問プロファイルが更新されたときに実行するコールバック関数を構成します。更新された [`VisitorProfile`](#instance-ivisitorprofile) は、コールバックの応答で提供されます。[`visitorServiceEnabled`](https://docs.tealium.com/ja/platforms/xamarin/install/#config) が `true` に構成されている場合に使用します。

Customer Data Platform（CDP）のライセンスを取得しており、訪問プロファイルを使用してモバイルアプリケーションのユーザーエクスペリエンスを向上させる場合は、この機能を使用してください。

```csharp
void SetVisitorServiceListener(Action callback);
```

| パラメーター | 型       | 説明                                             |
|:-------------|:---------|:-------------------------------------------------|
| `callback  ` | `Action` | 訪問プロファイルが取得されたときに実行するコードです。 |
  
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

`TealiumEvent` または `TealiumView` のディスパッチを使用してイベントをトラッキングします。

```csharp
tealium.Track(tealEvent);
```

| パラメーター | 型       | 説明                                                                    |
|:-------------|:---------|:------------------------------------------------------------------------|
| `tealEvent`  | `string` | `tealium_event` 属性として渡されるイベント名と、任意のイベントデータオブジェクトです。 |

イベントをトラッキングするには、[`TealiumEvent`](#class-tealiumevent) オブジェクトを作成し、`track()` メソッドに渡します。

```csharp
tealium.Track(new TealiumEvent("cart_add", new Dictionary<string, object> {
    { "customer_id", "abc123" }, 
    { "product_id", ["PROD123", "PROD456"] },
    { "product_price", [4.00, 6.00] }
}));
```

## クラス：`TealiumConfig`

以下に、`TealiumConfig` クラスのプロパティの概要を示します。

| パラメーター | 型 | 説明 | 例 |
|:----------|:----|:-----------|:-------|
| `account` | `String` | （必須）Tealiumアカウント名 | `"companyXYZ" ` |
| `profile` | `String` | （必須）Tealiumプロファイル名 | `"main"` |
| `environment` | [`Environment`](#environment) | （必須）Tealium環境名 | `Environment.dev` |
| `dataSource` | `String` | CDHデータソースキー | `"abc123"` |
| `collectors` | `Collectors[]` | （必須）Tealiumライブラリの初期化に使用する [`Collectors`](#collectors) のリストを構成します | `[Collectors.AppData]` |
| `dispatchers` | `Dispatchers[]` | （必須）Tealiumライブラリの初期化に使用する [`Dispatchers`](#dispatchers) のリストを構成します | `[Dispatchers.Collect]` |
| `customVisitorId` | `String` | カスタム訪問IDを構成します | `"ALK2398LSDKJ3289SLKJ3298SLKJ3"` |
| `memoryReportingEnabled` | `Boolean` | DeviceDataモジュールのメモリレポートを有効または無効にします（デフォルト：無効）。 | `true` |
| `overrideCollectDomain` | `String` | Tealium Collect URLのドメインを上書きします。[ファーストパーティドメイン](https://docs.tealium.com/ja/iq-tag-management/administration/first-party-domains/manage/)で使用します。 | `"your-domain.com"` |
| `overrideCollectURL` | `String` | Tealium Collect URLを上書きし、別のエンドポイントにデータを送信します。イベントバッチ処理機能を使用する場合は、`overrideCollectBatchURL` プロパティも上書きしてください。 | `"https://custom-domain.com/event"` |
| `overrideCollectBatchURL` | `String` | Tealium CollectバッチURLを上書きし、別のエンドポイントにデータを送信します。 | `"https://custom-domain.com/batch-event"` |
| `overrideLibrarySettingsURL` | `String` | パブリッシュ構成URLを上書きします。 | `"https://custom-domain.com/mobile.html"` |
| `overrideTagManagementURL` | `String` | タグ管理モジュールで使用されるデフォルトURLを上書きします。Tealium JavaScriptファイルをセルフホスティングする場合に必要です。 | `"https://custom-domain.com/path/env/utag.js"` |
| `deepLinkTrackingEnabled` | `Boolean` | Facebookなどのソースからアプリへのリンクを含む[標準ディープリンクの自動トラッキング](https://docs.tealium.com/ja/platforms/getting-started-mobile/deep-linking/#readout)とQRトレースを有効または無効にします（デフォルト：有効）。 | `false` |
| `qrTraceEnabled` | `Boolean` | [QRトレース](https://docs.tealium.com/ja/platforms/getting-started-mobile/trace/#how-it-works)を有効または無効にします（デフォルト：有効）。 | `false` |
| `loglevel` | [`LogLevel`](#loglevel) | ログに記録する情報量を制御するログレベルプロパティを構成します（デフォルト：サイレント）。 | `LogLevel.dev` |
| `consentExpiry` | [`ConsentExpiry`](#consentexpiry) | ユーザーの同意構成の有効期限を構成します（デフォルトはポリシーに依存します）。 | `ConsentExpiry(90, TimeUnit.days)` |
| `consentLoggingEnabled` | `Boolean` | 監査目的で同意ステータスのすべての変更をTealium Customer Data Hubに送信する、[同意ログ](https://docs.tealium.com/consent-change-event-specifications/)機能を有効にします（デフォルト：有効）。 | `true` |
| `consentPolicy` | [`ConsentPolicy`](#consentpolicy) | CCPAやGDPRなどの同意ポリシーを構成します。同意マネージャーは、このプロパティが構成されている場合にのみ有効になります。 | `ConsentPolicy.gdpr` |
| `lifecycleAutotrackingEnabled` | `Boolean` | ライフサイクルの自動トラッキングを有効または無効にします（デフォルト：有効）。 | `false` |
| `useRemoteLibrarySettings` | `Boolean` | [モバイルパブリッシュ構成](https://docs.tealium.com/create-mobile-profile/)を有効または無効にします（デフォルト：有効）。タグ管理でモバイルパブリッシュ構成を構成するか、この機能を無効にします。 | `false` |
| `visitorServiceEnabled` | `Boolean` | [データレイヤーエンリッチメントAPI](https://docs.tealium.com/data-layer-enrichment-api/)を使用した訪問プロファイルの自動取得を有効または無効にします（デフォルト：無効）。 | `true` |
| `remoteCommands` | `RemoteCommand[]` | インスタンスの準備が完了したときに追加する [RemoteCommand](#RemoteCommand) オブジェクトのリストを構成します | `[{ id: "hello-world", callback: (payload) => { console.log("hello-world: " + JSON.stringify(payload)); } }]` |
| `overrideConsentCategoriesKey` | `String` | 同意カテゴリーのイベント属性名を上書きします。サーバーサイド同意のカスタム適用をサポートするために使用します。[サーバーサイド同意の自動適用の無効化](https://docs.tealium.com/server-side-consent-management/)について詳しく確認してください（デフォルト：`consent_categories`）。 | `consent_categories_granted` |
| `visitorIdentityKey` | `String` | 訪問の切り替えをサポートし、アプリの複数ユーザーを識別する共有キーを指定するために使用します。 | `user_profile_id` |
### コレクター

コレクターは、デバイスから補足情報を収集し、Tealium Customer Data Hub に送信される前にデータレイヤーへ追加するモジュールです。一部のコレクターはコアライブラリに含まれていますが、その他はオプションであり、個別のモジュールとしてインストールされます。

次の表に、利用可能なコレクターを示します。デフォルトのコレクターは、コレクター名の横に `*` を付けて示しています。

| コレクター名  | TealiumConfig の参照   |
|:----------------|:--------------------------|
| `AppData`*      | `Collectors.AppData`      |
| `Connectivity`* | `Collectors.Connectivity` |
| `Device`        | `Collectors.Device`       |
| `Lifecycle`     | `Collectors.Lifecycle`    |

これらのモジュールは、[`TealiumConfig`](#class-tealiumconfig) に構成される `Collectors` プロパティを使用して有効化または無効化します。

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

[`TealiumConfig`](#class-tealiumconfig) オブジェクトで、同意構成の有効期限を構成します。

| パラメータ | 型       | 説明 |
|:-----------|:-----------|:-----------|
| `time`     | `Number`   | 有効期限が切れるまでの時間です。 |
| `unit`     | `TimeUnit` | 有効期限が切れるまでの時間の単位です。`TimeUnit.Minutes`、`TimeUnit.Hours`、`TimeUnit.Days`、`TimeUnit.Months` のいずれかです。 |

```csharp
TealiumConfig config = new TealiumConfig(
  //...
  consentExpiry = new TimeUnit(90, TimeUnit.Days)),
  //...
);
```

### ConsentPolicy

[`TealiumConfig`](#class-tealiumconfig) オブジェクトで使用する同意ポリシーを構成します。同意ポリシーが構成されていない場合、同意マネージャーは無効になります。

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

### ディスパッチャー

ディスパッチャーは、Tealium エンドポイントにデータを送信するモジュールです。これらは [`TealiumConfig`](#class-tealiumconfig) オブジェクトで構成します。

```csharp
TealiumConfig tealConfig = new TealiumConfig(
    // ...
    new List<Dispatchers> {
        Dispatchers.Collect, Dispatchers.RemoteCommands
    }
    // ...
);
```

次のディスパッチャーを利用できます。

* `Dispatchers.Collect`
* `Dispatchers.RemoteCommands`
* `Dispatchers.TagManagement`


<blockquote>
少なくとも 1 つのディスパッチャーが必要です。
</blockquote>


### LogLevel

ログに記録する情報量を制御するログレベルプロパティを、次のいずれかの値に構成します。

| 値                | 説明 |
|:------------------|:--------------------------------------------------------------------|
| `LogLevel.dev`    | アプリケーションの進行状況を示す情報イベント |
| `LogLevel.qa`     | アプリケーションのデバッグに使用するデバッグレベルのイベント |
| `LogLevel.prod`   | 重大なエラーや障害などのエラーイベント |
| `LogLevel.silent` | ログを記録しない（デフォルト） |


## `IRemoteCommand`

構成済みリモートコマンドを定義するインターフェイスです。

| 値            | 説明 |
|:--------------|:------------------------------------------------------------|
| `CommandId`   | RemoteCommand の一意の識別子名 |
| `Description` | （任意）RemoteCommand の一意の識別子名 |
| `Path`        | （任意）マッピングに使用するローカルファイル |
| `Url`         | （任意）マッピングに使用するリモートファイル |

## `IVisitorProfile`

（[`TealiumConfig.visitorServiceEnabled`](#class-tealiumconfig) とともに使用します。）

訪問プロファイルオブジェクトには、訪問サービスから返された訪問属性が含まれます。`currentVisit` プロパティには、現在の訪問をスコープとする属性が含まれます。添字を使用し、ID によって各属性値にアクセスします。属性が存在しない場合は、`null` が返されます。


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
| `Strings`          | `IDictionary<string, string>`                       | `id: "5380", value: "green shirts"`                                  |
| `Tallies`          | `IDictionary<string, IDictionary<string, double>>` | `"57": [["category 1": 2.0], "category 2": 1.0]]`                    |

### `ICurrentVisit`

現在の訪問をスコープとする属性を含むオブジェクトです。

| パラメータ | プロパティ | 値 |
|:----------|:----------|:-----|
| `ArraysOfBooleans` | `IDictionary<string, IList<bool>>`                 | `id: "5129", value: [true,false,true,true]`                          |
| `ArraysOfNumbers`  | `IDictionary<string, IList<double>>`               | `id: "57", value: [4.82125, 16.8, 0.5714285714285714]`               |
| `ArraysOfStrings`  | `IDictionary<string, IList<string>>`               | `id: "5213", value: ["green shirts", "green shirts", "blue shirts"]` |
| `Booleans`         | `IDictionary<string, bool>`                        | `id: "4868", value: true`                                            |
| `Dates`            | `IDictionary<string, long>`                        | `id: "22", value: 1567120112000`                                     |
| `Numbers`          | `IDictionary<string, double>`                      | `id: "5728", value: 4.82125`                                         |
| `SetOfStrings`     | `IDictionary<string, ISet<string>>`                | `id: "5211", value: ["green shirts", "red shirts", "blue shirts"]`   |
| `Strings`          | `IDictionary<string, string>`                       | `id: "5380", value: "green shirts"`                                  |
| `Tallies`          | `IDictionary<string, IDictionary<string, double>>` | `"57": [["category 1": 2.0], "category 2": 1.0]]`                    |
| `TotalEventCount`  | `int`                                              | `42`                                                                 |
| `CreatedAt`        | `long`                                             | `1638236024`                                                         |

## インターフェイス：`TealiumDispatch`

トラッキングするディスパッチの種類を定義するインターフェイスです。次のクラスが `TealiumDispatch` を実装します。
### クラス：`TealiumEvent`

画面上でのユーザー操作または画面表示をトラッキングするには、`TealiumEvent(tealiumEvent, dataLayer)` のインスタンスを [`Track()`](#track) メソッドに渡します。`TealiumEvent` は、トラッキング呼び出しで `tealium_event` として使用されるイベント名と、任意のデータディクショナリで構成されます。

```csharp
tealium.Track(new TealiumEvent("tealiumEvent", new Dictionary<string, object> {
    eventData
}));
```

| パラメータ | 型 | 説明 |
|:------------|:--------|:-----------------|
| `tealiumEvent` | `string` | `tealium_event` 属性として渡されるイベント名。 |
| `eventData` | `Dictionary<string, object>` | （任意）イベントとともにキーと値の形式で送信するデータ。 |

例：

```csharp
tealium.Track(new TealiumEvent("cart_add", new Dictionary<string, object> {
    { "customer_id", "abc123" }, 
    { "product_id", ["PROD123", "PROD456"] },
    { "product_price", [4.00, 6.00] }
}));
```

### クラス：`TealiumView`

画面表示をトラッキングするには、`TealiumView(tealiumEvent, dataLayer)` のインスタンスを [`Track()`](#track) メソッドに渡します。`TealiumView` は、トラッキング呼び出しで `tealium_event` として使用されるビュー名と、任意のデータディクショナリで構成されます。

```csharp
tealium.Track(new TealiumView("tealiumEvent", new Dictionary<string, object> {
    eventData
}));
```

| パラメータ | 型 | 説明 |
|:------------|:--------|:-----------------|
| `tealiumEvent` | `string` | `tealium_event` 属性として渡されるイベント名。 |
| `eventData` | `Dictionary<string, object>` | （任意）イベントとともにキーと値の形式で送信するデータ。 |

例：

```csharp
tealium.Track(new TealiumView("purchase", new Dictionary<string, object> {
    { "customer_id", "abc123" },
    { "order_total", 10.00 },
    { "product_id", ["PROD123", "PROD456"] },
    { "order_id", "0123456789" }
}));
```