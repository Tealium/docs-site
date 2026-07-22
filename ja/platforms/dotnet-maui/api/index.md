---
title: API リファレンス
description: Tealium の .NET MAUI 用クラスとメソッドのリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/dotnet-maui/api/
---
## クラス: `Tealium`

Tealium .NET MAUI ライブラリの `Tealium` クラスのメソッドと定数。

### `AddRemoteCommand()`

リモートコマンドマネージャーにリモートコマンドを追加します。

```csharp
void AddRemoteCommand(IRemoteCommand remoteCommand);
```

| パラメータ          | タイプ             | 説明                                                                                      |
|:----------------|:-----------------|:-------------------------------------------------------------------------------------------------|
| `remoteCommand` | `IRemoteCommand` | IRemoteCommand インターフェースの実装で、必要なリモートコマンドのプロパティを提供します。 |

例:

```csharp
public class MyRemoteCommand : IRemoteCommand
    {
        public string CommandId => "my_remote_command";
        public string Description => "私のリモートコマンドの説明";
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

指定された有効期限で永続的なデータ保存にデータを追加します。

```csharp
void AddToDataLayer(IDictionary<string, object> data, Expiry expiry);
```

| パラメータ | タイプ | 説明 |
|:-----------|:-----|:------------|
| `data`     | `IDictionary<string, object>` | 文字列のキーと値がプリミティブまたはコレクションであるキー値ペアの IDictionary |
| `expiry`   | [`Expiry`](#expiry)           | データを保持する時間の長さ|

```csharp
tealium.AddToDataLayer(new Dictionary<string, object> {
  { "user_language", lang }
}, Expiry.Forever);
```

### `ClearStoredVisitorIds()`

保存されている訪問IDをクリアし、新しいものを生成します。主に法的コンプライアンスのために使用されます。

訪問IDは、データレイヤーに `visitorIdentityKey` という構成が含まれている場合、その構成に基づいて引き続き保存されます。

```csharp
tealium.ClearStoredVisitorIds();
```


<blockquote>
保存をクリアした後、現在のアイデンティティと共に新しくリセットされた `visitorId` を保存しないようにするためには、アイデンティティキーを事前にデータレイヤーから削除する必要があります（[`RemoveFromDataLayer()`](#removefromdatalayer)を参照）。
</blockquote>


### ConsentCategory

同意カテゴリの値。[`GetConsentCategories`](#getconsentcategories) および [`SetConsentCategories`](#setconsentcategories) で使用します。

同意カテゴリは以下の通りです:

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

同意ステータスの値。[`SetConsentStatus()`](#setconsentstatus)で使用します。

| 値                                       | 説明   |
|:--------------------------------------------|:--------------|
| `ConsentManager.ConsentStatus.Consented`    | 同意済み     |
| `ConsentManager.ConsentStatus.NotConsented` | 同意していない |
| `ConsentManager.ConsentStatus.Unknown`      | 不明       |

### Environment

環境は、デフォルトの3つの環境（Dev、QA、Prod）のいずれか、または公開するカスタム環境です。

| 値              | 説明 |
|:-------------------|:------------|
| `Environment.dev`  | 開発 |
| `Environment.qa`   | QA/UAT      |
| `Environment.prod` | 本番  |

### Expiry

永続的または揮発性データの有効期限を定義します。[`AddToDataLayer()`](#addtodatalayer)で使用します。

| 値                 | 説明                                  |
|:----------------------|:---------------------------------------------|
| `Expiry.Session`      | 現在のアクティブセッションの長さ。    |
| `Expiry.UntilRestart` | 次の再起動までの時間の長さ。   |
| `Expiry.Forever`      | アプリが削除されるまでの時間の長さ。 |

### `GatherTrackData()`

コレクターやデータレイヤーからすべてのトラックデータを収集します。

```csharp
GatherTrackData(callback);
```

| パラメータ | タイプ       | 説明                                          | 例       |
|:-----------|:-----------|:-----------------------------------------------------|:--------------|
| `callback` | `Function` | キーの取得値を使用するコールバック関数。コールバックは JSON オブジェクトを返します。 | (例を参照) |

例:

```csharp
tealium.GatherTrackData(data => {
    foreach (var entry in data)
    {
        System.Diagnostics.Debug.WriteLine($"key ({entry.Key}) - value: {Stringify(entry.Value)}");
    }
});
```

### `GetFromDataLayer()`

永続的なデータレイヤーで指定されたキーの値を取得します。

```csharp
object? GetFromDataLayer(string key);
```

| パラメータ | タイプ     | 説明                         |
|:-----------|:---------|:------------------------------------|
| `key`      | `String` | データレイヤーから取得するキー |

```csharp
string myString = (string)tealium.GetFromDataLayer("user_language");
```

### `GetConsentCategories()`

ユーザーが同意したカテゴリのリストを取得します。

```csharp
List<ConsentCategory>? GetConsentCategories();
```

例:

```csharp
tealium.GetConsentCategories().ForEach((c) =>
{
    if (c == ConsentManager.ConsentCategory.Analytics)
    {
        // Analytics に同意済み
    }
});
```

### `GetConsentStatus()`

ユーザーの同意の現在の状態を取得します。[`ConsentStatus`](#consentstatus) 値を返します。

```csharp
ConsentStatus GetConsentStatus();
```

例:

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

ユーザーの訪問IDを取得し、コールバック関数の形で返します。

```csharp
string? visitorId = tealium.GetVisitorId();
```

### `JoinTrace()`

指定されたIDでトレースに参加します。Tealium Customer Data Hub の [Trace](https://docs.tealium.com/manage-traces/) 機能について詳しくはこちらをご覧ください。

```csharp
tealium.JoinTrace(id);
```

| パラメータ | タイプ     | 説明 | 例    |
|:-----------|:---------|:------------|:-----------|
| `id`       | `String` | トレースID    | `abc123xy` |

### `LeaveTrace()`

`leaveTrace()` メソッドが呼ばれるまで、トレースはアプリセッションの間有効です。このメソッドは以前に参加したトレースを離れ、訪問セッションを終了します。

```csharp
tealium.LeaveTrace();
```

### `RemoveFromDataLayer()`

以前に [`AddToDataLayer()`](#addtodatalayer) を使用して構成された永続的なデータを削除します。

```csharp
void RemoveFromDataLayer(ICollection<string> keys);
```

| パラメータ | タイプ                  | 説明             |
|:-----------|:----------------------|:------------------------|
| `keys`     | `ICollection<String>` | キー名のコレクション |
  
```csharp
tealium.RemoveFromDataLayer(new string[] { "key1", "key2" });
```
### `RemoveRemoteCommand()`

リモートコマンドマネージャーからリモートコマンドを削除します。

```csharp
void RemoveRemoteCommand(string id);
```

| パラメータ | 型       | 説明                            |
|:-----------|:---------|:--------------------------------|
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

ユーザーが同意したカテゴリのリストを構成します。[`ConsentCategory`](#consentcategory)を使用します。

```csharp
void SetConsentCategories(List<ConsentCategory> categories);
```

| パラメータ   | 型                      | 説明                        |
|:-------------|:------------------------|:----------------------------|
| `categories` | `List<ConsentCategory>` | ユーザー同意カテゴリのリスト |

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

| パラメータ   | 型       | 説明                             |
|:-------------|:---------|:---------------------------------|
| `callback  ` | `Action` | 同意が期限切れになったときのコード |

```csharp
tealium.SetConsentExpiryListener(() =>
{
    System.Diagnostics.Debug.WriteLine("Consent Expired");
});
```

### `SetConsentStatus()`

ユーザーの同意状態を構成します。デフォルト値は構成されるまで `.Unknown` です。

```csharp
void SetConsentStatus(ConsentStatus status);
```

| パラメータ | 型              | 説明                                                              |
|:-----------|:----------------|:------------------------------------------------------------------|
| `status  ` | `ConsentStatus` | ユーザーの同意状態。[ConsentManager.ConsentStatus](#consentstatus)を参照。 |

```csharp
tealium.SetConsentStatus(ConsentManager.ConsentStatus.NotConsented);
```

### `SetVisitorServiceListener()`

訪問プロファイルが更新されたときに実行するコールバック関数を構成します。更新された[`VisitorProfile`](#instance-ivisitorprofile)がコールバックの応答で提供されます。[`visitorServiceEnabled`](https://docs.tealium.com/ja/platforms/dotnet-maui/install/#config)が `true` に構成されている場合に使用します。

Tealium AudienceStreamのライセンスを持っていて、モバイルアプリケーションでユーザー体験を向上させるために訪問プロファイルを使用したい場合にこの機能を使用します。

```csharp
void SetVisitorServiceListener(Action callback);
```

| パラメータ   | 型       | 説明                                          |
|:-------------|:---------|:----------------------------------------------|
| `callback  ` | `Action` | 訪問プロファイルが取得されたときの実行コード |

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

オプションのイベントデータを含む画面表示またはイベントを追跡します。

```csharp
tealium.Track(tealiumEvent);
```

| パラメータ     | 型                          | 説明                                      |
|:---------------|:----------------------------|:------------------------------------------|
| `tealiumEvent` | `TealiumView` or `TealiumEvent` | イベント名とオプショナルデータを含むディスパッチオブジェクト |

イベントを追跡するには、`track()`メソッドに[`TealiumView`](#class-tealiumview)または[`TealiumEvent`](#class-tealiumevent)のインスタンスを渡します：

```csharp
tealium.Track(new TealiumEvent("cart_add", new Dictionary<string, object> {
    { "customer_id", "abc123" }, 
    { "product_id", new[] {"PROD123", "PROD456"} },
    { "product_price", new[] {4.00, 6.00} }
}));
```
## クラス: `TealiumConfig`

以下は、`TealiumConfig` クラスのプロパティをまとめたものです。

| パラメータ | 型 | 説明 | 例 |
|:----------|:----|:-----------|:-------|
| `account` | `String` | (必須) Tealiumアカウント名 | `"companyXYZ"` |
| `profile` | `String` | (必須) Tealiumプロファイル名 | `"main"` |
| `environment` | [`Environment`](#environment) | (必須) Tealium環境名 | `Environment.dev` |
| `dataSource` | `String` | CDHデータソースキー | `"abc123"` |
| `collectors` | `Collectors[]` | (必須) Tealiumライブラリを初期化するための[`Collectors`](#collectors)のリストを構成 | `[Collectors.AppData]` |
| `dispatchers` | `Dispatchers[]` | (必須) Tealiumライブラリを初期化するための[`Dispatchers`](#dispatchers)のリストを構成 | `[Dispatchers.Collect]` |
| `customVisitorId` | `String` | カスタム訪問IDを構成 | `"ALK2398LSDKJ3289SLKJ3298SLKJ3"` |
| `memoryReportingEnabled` | `Boolean` | デバイスデータモジュールでのメモリレポートを有効または無効にする（デフォルト: 無効）。 | `true` |
| `overrideCollectDomain` | `String` | Tealium Collect URLのドメインを上書き。[ファーストパーティドメイン](https://docs.tealium.com/ja/iq-tag-management/administration/first-party-domains/manage/)で使用。 | `"your-domain.com"` |
| `overrideCollectProfile` | `String` | Tealium Collectプロファイルを上書きして、異なるTealiumプロファイルにデータを送信。 | `"custom-profile"` |
| `overrideCollectURL` | `String` | Tealium Collect URLを上書きして、異なるエンドポイントにデータを送信。イベントバッチ機能を使用する場合は、`overrideCollectBatchURL`プロパティも上書き。 | `"https://custom-domain.com/event"` |
| `overrideCollectBatchURL` | `String` | Tealium CollectバッチURLを上書きして、異なるエンドポイントにデータを送信。 | `"https://custom-domain.com/batch-event"` |
| `overrideLibrarySettingsURL` | `String` | 公開構成URLを上書き。 | `"https://custom-domain.com/mobile.html"` |
| `overrideTagManagementURL` | `String` | タグ管理モジュールで使用されるデフォルトURLを上書き。Tealium JavaScriptファイルを自己ホスティングする場合に必要。 | `"https://custom-domain.com/path/env/utag.js"` |
| `deepLinkTrackingEnabled` | `Boolean` | [標準ディープリンクの自動追跡](https://docs.tealium.com/ja/platforms/getting-started-mobile/deep-linking/#readout)を有効または無効にする。例えば、Facebookや他のソースからのアプリへのリンクやQRトレースも含む（デフォルト: 有効）。 | `false` |
| `qrTraceEnabled` | `Boolean` | [QRトレース](https://docs.tealium.com/ja/platforms/getting-started-mobile/trace/#how-it-works)を有効または無効にする（デフォルト: 有効）。 | `false` |
| `loglevel` | [`LogLevel`](#loglevel) | ログレベルプロパティを構成し、ログに記録される情報の量を制御する（デフォルト: サイレント）。 | `LogLevel.dev` |
| `consentExpiry` | [`ConsentExpiry`](#consentexpiry) | ユーザーの同意構成の有効期限を構成する。（ポリシーに依存するデフォルト値） | `ConsentExpiry(90, TimeUnit.days)` |
| `consentLoggingEnabled` | `Boolean` | [同意ログ記録](https://docs.tealium.com/consent-change-event-specifications/)機能を有効にする。これにより、すべての同意ステータス変更が監査目的でTealium Customer Data Hubに送信される（デフォルト: 有効）。 | `true` |
| `consentPolicy` | [`ConsentPolicy`](#consentpolicy) | 同意ポリシーを構成する。例えば、CCPAやGDPR。このプロパティが構成されている場合のみ、Consent Managerが有効になる。 | `ConsentPolicy.gdpr` |
| `lifecycleAutotrackingEnabled` | `Boolean` | ライフサイクル自動追跡を有効または無効にする（デフォルト: 有効）。 | `false` |
| `useRemoteLibrarySettings` | `Boolean` | [モバイル公開構成](https://docs.tealium.com/creating-a-mobile-profile/)を有効または無効にする（デフォルト: 有効）。Tealium iQタグ管理でモバイル公開構成を構成するか、この機能を無効にする。 | `false` |
| `visitorServiceEnabled` | `Boolean` | [データレイヤーエンリッチメントAPI](https://docs.tealium.com/data-layer-enrichment-api/)を使用して訪問プロファイルの自動取得を有効または無効にする（デフォルト: 無効）。 | `true` |
| `remoteCommands` | `RemoteCommand[]` | インスタンスが準備完了時に追加する[RemoteCommand](#RemoteCommand)オブジェクトのリストを構成する。 | `[{ id: "hello-world", callback: (payload) => { console.log("hello-world: " + JSON.stringify(payload)); } }]` |
| `overrideConsentCategoriesKey` | `String` | 同意カテゴリイベント属性の名前を上書きする。サーバーサイドの同意の自動適用を無効にする方法について詳しくは[こちら](https://docs.tealium.com/server-side-consent-management/)を参照。（デフォルト: `consent_categories`） | `consent_categories_granted` |
| `visitorIdentityKey` | `String` | 訪問の切り替えをサポートし、アプリの複数のユーザーを識別する共有キーを指定するために使用。 | `user_profile_id` |

### Collectors

Collectorsは、デバイスから追加情報を収集し、データレイヤーに追加してからTealium Customer Data Hubに送信するモジュールです。いくつかのコレクターはコアライブラリに含まれており、他のコレクターは別のモジュールとしてオプションでインストールされます。

以下の表は、利用可能なコレクターをリストしています。デフォルトのコレクターはコレクター名の隣に `*` が付けられています。

| コレクター名 | TealiumConfig参照 |
|:----------------|:--------------------------|
| `AppData`* | `Collectors.AppData` |
| `Connectivity`* | `Collectors.Connectivity` |
| `Device` | `Collectors.Device` |
| `Lifecycle` | `Collectors.Lifecycle` |

これらのモジュールは、[`TealiumConfig`](#class-tealiumconfig)で構成された`Collectors`プロパティを使用して有効または無効にされます。

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

[`TealiumConfig`](#class-tealiumconfig)オブジェクト上で同意構成の有効期限を構成します。

| パラメータ | 型 | 説明 |
|:-----------|:-----------|:-----------|
| `time` | `Number` | 有効期限までの時間。 |
| `unit` | `TimeUnit` | 有効期限までの時間単位。`TimeUnit.Minutes`, `TimeUnit.Hours`, `TimeUnit.Days`, `TimeUnit.Months`のいずれか |

```csharp
TealiumConfig config = new TealiumConfig(
  //...
  consentExpiry = new TimeUnit(90, TimeUnit.Days)),
  //...
);
```

### ConsentPolicy

[`TealiumConfig`](#class-tealiumconfig)オブジェクトで使用する同意ポリシーを構成します。同意ポリシーが構成されていない場合、同意マネージャーは無効です。

```csharp
TealiumConfig config = new TealiumConfig(
  //...
  consentPolicy = ConsentPolicy.GDPR,
  //...
);
```

同意値:

* `ConsentPolicy.GDPR`
* `ConsentPolicy.CCPA`

### Dispatchers

Dispatchersは、データをTealiumエンドポイントに送信するモジュールです。これらは[`TealiumConfig`](#class-tealiumconfig)オブジェクトに構成されます。

```csharp
TealiumConfig tealConfig = new TealiumConfig(
    // ...
    new List<Dispatchers> {
        Dispatchers.Collect, Dispatchers.RemoteCommands
    }
    // ...
);
```

利用可能なディスパッチャーは以下の通りです:

* `Dispatchers.Collect`
* `Dispatchers.RemoteCommands`
* `Dispatchers.TagManagement`


<blockquote>
少なくとも1つのディスパッチャーが必要です。
</blockquote>


### LogLevel

ログレベルプロパティを構成し、ログに記録される情報の量を制御します。以下の値のいずれかに構成します:

| 値 | 説明 |
|:------------------|:--------------------------------------------------------------------|
| `LogLevel.dev` | アプリケーションの進行を強調する情報イベント |
| `LogLevel.qa` | アプリケーションのデバッグに使用されるデバッグレベルのイベント |
| `LogLevel.prod` | 重大なエラーや障害などのエラーイベント |
| `LogLevel.silent` | ログなし（デフォルト） |
## `IRemoteCommand`

リモートコマンドを構成するためのインターフェースを定義します。

| 値             | 説明                                                       |
|:--------------|:------------------------------------------------------------|
| `CommandId`   | リモートコマンドの一意の識別子名                            |
| `Description` | （オプション）リモートコマンドの一意の識別子名               |
| `Path`        | （オプション）マッピングに使用するローカルファイル           |
| `Url`         | （オプション）マッピングに使用するリモートファイル           |

## `IVisitorProfile`

（[`TealiumConfig.visitorServiceEnabled`](#class-tealiumconfig)で使用します。）

訪問プロファイルオブジェクトには、訪問サービスから返される訪問属性が含まれています。`currentVisit`プロパティには現在の訪問に関連する属性が含まれています。サブスクリプトを使用してIDで各属性値にアクセスします。属性が存在しない場合は`null`が返されます。

| パラメーター       | プロパティ                                          | 値                                                         |
|:------------------|:--------------------------------------------------|:-----------------------------------------------------------|
| `ArraysOfBooleans`| `IDictionary<string, IList<bool>>`                | `id: "5129", value: [true,false,true,true]`                |
| `ArraysOfNumbers` | `IDictionary<string, IList<double>>`              | `id: "57", value: [4.82125, 16.8, 0.5714285714285714]`     |
| `ArraysOfStrings` | `IDictionary<string, IList<string>>`              | `id: "5213", value: ["green shirts", "green shirts", "blue shirts"]` |
| `Audiences`       | `IDictionary<string, string>`                     | `id: "tealiummobile_demo_103", value: "iOS Users"`         |
| `Badges`          | `IDictionary<string, bool>`                       | `id: "2815", value: true`                                  |
| `Booleans`        | `IDictionary<string, bool>`                       | `id: "4868", value: true`                                  |
| `CurrentVisit`    | `ICurrentVisit`                                    |                                                            |
| `Dates`           | `IDictionary<string, long>`                       | `id: "22", value: 1567120112000`                           |
| `Numbers`         | `IDictionary<string, double>`                     | `id: "5728", value: 4.82125`                               |
| `SetOfStrings`    | `IDictionary<string, ISet<string>>`               | `id: "5211", value: ["green shirts", "red shirts", "blue shirts"]`   |
| `Strings`         | `IDictionary<string, string>`                     | `id: "5380", value: "green shirts"`                        |
| `Tallies`         | `IDictionary<string, IDictionary<string, double>>`| `"57": [["category 1": 2.0], "category 2": 1.0]]`          |

### `ICurrentVisit`

現在の訪問に関連する属性を含むオブジェクトです。

| パラメーター       | プロパティ                                          | 値                                                         |
|:------------------|:--------------------------------------------------|:-----------------------------------------------------------|
| `ArraysOfBooleans`| `IDictionary<string, IList<bool>>`                | `id: "5129", value: [true,false,true,true]`                |
| `ArraysOfNumbers` | `IDictionary<string, IList<double>>`              | `id: "57", value: [4.82125, 16.8, 0.5714285714285714]`     |
| `ArraysOfStrings` | `IDictionary<string, IList<string>>`              | `id: "5213", value: ["green shirts", "green shirts", "blue shirts"]` |
| `Booleans`        | `IDictionary<string, bool>`                       | `id: "4868", value: true`                                  |
| `Dates`           | `IDictionary<string, long>`                       | `id: "22", value: 1567120112000`                           |
| `Numbers`         | `IDictionary<string, double>`                     | `id: "5728", value: 4.82125`                               |
| `SetOfStrings`    | `IDictionary<string, ISet<string>>`               | `id: "5211", value: ["green shirts", "red shirts", "blue shirts"]`   |
| `Strings`         | `IDictionary<string, string>`                     | `id: "5380", value: "green shirts"`                        |
| `Tallies`         | `IDictionary<string, IDictionary<string, double>>`| `"57": [["category 1": 2.0], "category 2": 1.0]]`          |
| `TotalEventCount` | `int`                                             | `42`                                                       |
| `CreatedAt`       | `long`                                            | `1638236024`                                               |

## インターフェース: `TealiumDispatch`

追跡するディスパッチのタイプを定義するインターフェースです。以下のクラスが`TealiumDispatch`を実装しています：

### クラス: `TealiumEvent`

ユーザーの画面とのインタラクションを追跡するには、`TealiumEvent(tealiumEvent, dataLayer)`のインスタンスを[`Track()`](#track)メソッドに渡します。`TealiumEvent`は、追跡コールに`tealium_event`として表示されるイベント名と、オプションのデータ辞書で構成されています。

```csharp
tealium.Track(new TealiumEvent(tealiumEvent, eventData));
```

| パラメーター    | タイプ                          | 説明                                      |
|:--------------|:-------------------------------|:-----------------------------------------|
| `tealiumEvent`| `string`                       | `tealium_event`として渡されるイベント名。 |
| `eventData`   | `Dictionary<string, object>`   | （オプション）イベントに送信されるキーと値の形式のデータ。 |

例：

```csharp
tealium.Track(new TealiumEvent("cart_add", new Dictionary<string, object> {
    { "customer_id", "abc123" }, 
    { "product_id", new[] {"PROD123", "PROD456"} },
    { "product_price", new[] {4.00, 6.00} }
}));
```

### クラス: `TealiumView`

画面ビューを追跡するには、`TealiumView(tealiumEvent, dataLayer)`のインスタンスを[`Track()`](#track)メソッドに渡します。`TealiumView`は、追跡コールに`tealium_event`として表示されるビュー名と、オプションのデータ辞書で構成されています。

```csharp
tealium.Track(new TealiumView(tealiumEvent, eventData));
```

| パラメーター    | タイプ                          | 説明                                      |
|:--------------|:-------------------------------|:-----------------------------------------|
| `tealiumEvent`| `string`                       | `tealium_event`として渡されるビューイベントまたは画面の名前。 |
| `eventData`   | `Dictionary<string, object>`   | （オプション）イベントに送信されるキーと値の形式のデータ。 |

例：

```csharp
tealium.Track(new TealiumView("purchase", new Dictionary<string, object> {
    { "customer_id", "abc123" },
    { "order_total", 10.00 },
    { "product_id", new[] {"PROD123", "PROD456"} },
    { "order_id", "0123456789" }
}));
```
