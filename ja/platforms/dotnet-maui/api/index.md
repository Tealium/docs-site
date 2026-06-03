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
        public string CommandId =&gt; &#34;my_remote_command&#34;;
        public string Description =&gt; &#34;私のリモートコマンドの説明&#34;;
        public string Path =&gt; null;
        public string Url =&gt; null;

        public void Dispose()
        {
            //
        }

        public void HandleResponse(IRemoteCommandResponse response)
        {
            var str = response.Payload.GetValueForKey&lt;String&gt;(&#34;key&#34;);
            if (str == &#34;&#34;)
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
void AddToDataLayer(IDictionary&lt;string, object&gt; data, Expiry expiry);
```

| パラメータ | タイプ | 説明 |
|:-----------|:-----|:------------|
| `data`     | `IDictionary&lt;string, object&gt;` | 文字列のキーと値がプリミティブまたはコレクションであるキー値ペアの IDictionary |
| `expiry`   | [`Expiry`](#expiry)           | データを保持する時間の長さ|

```csharp
tealium.AddToDataLayer(new Dictionary&lt;string, object&gt; {
  { &#34;user_language&#34;, lang }
}, Expiry.Forever);
```

### `ClearStoredVisitorIds()`

保存されている訪問IDをクリアし、新しいものを生成します。主に法的コンプライアンスのために使用されます。

訪問IDは、データレイヤーに `visitorIdentityKey` という構成が含まれている場合、その構成に基づいて引き続き保存されます。

```csharp
tealium.ClearStoredVisitorIds();
```

保存をクリアした後、現在のアイデンティティと共に新しくリセットされた `visitorId` を保存しないようにするためには、アイデンティティキーを事前にデータレイヤーから削除する必要があります（[`RemoveFromDataLayer()`](#removefromdatalayer)を参照）。

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
tealium.GatherTrackData(data =&gt; {
    foreach (var entry in data)
    {
        System.Diagnostics.Debug.WriteLine($&#34;key ({entry.Key}) - value: {Stringify(entry.Value)}&#34;);
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
string myString = (string)tealium.GetFromDataLayer(&#34;user_language&#34;);
```

### `GetConsentCategories()`

ユーザーが同意したカテゴリのリストを取得します。

```csharp
List&lt;ConsentCategory&gt;? GetConsentCategories();
```

例:

```csharp
tealium.GetConsentCategories().ForEach((c) =&gt;
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

指定されたIDでトレースに参加します。Tealium Customer Data Hub の [Trace]() 機能について詳しくはこちらをご覧ください。

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
void RemoveFromDataLayer(ICollection&lt;string&gt; keys);
```

| パラメータ | タイプ                  | 説明             |
|:-----------|:----------------------|:------------------------|
| `keys`     | `ICollection&lt;String&gt;` | キー名のコレクション |
  
```csharp
tealium.RemoveFromDataLayer(new string[] { &#34;key1&#34;, &#34;key2&#34; });
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
tealium.RemoveRemoteCommand(&#34;firebase&#34;);
```

### `ResetVisitorId()`

訪問IDをリセットし、新しいIDを生成します。

```csharp
tealium.ResetVisitorId();
```

### `SetConsentCategories()`

ユーザーが同意したカテゴリのリストを構成します。[`ConsentCategory`](#consentcategory)を使用します。

```csharp
void SetConsentCategories(List&lt;ConsentCategory&gt; categories);
```

| パラメータ   | 型                      | 説明                        |
|:-------------|:------------------------|:----------------------------|
| `categories` | `List&lt;ConsentCategory&gt;` | ユーザー同意カテゴリのリスト |

```csharp
tealium.SetConsentCategories(new List&lt;ConsentManager.ConsentCategory&gt;()
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
tealium.SetConsentExpiryListener(() =&gt;
{
    System.Diagnostics.Debug.WriteLine(&#34;Consent Expired&#34;);
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

訪問プロファイルが更新されたときに実行するコールバック関数を構成します。更新された[`VisitorProfile`](#instance-ivisitorprofile)がコールバックの応答で提供されます。[`visitorServiceEnabled`](/ja/platforms/dotnet-maui/install/#config)が `true` に構成されている場合に使用します。

Tealium AudienceStreamのライセンスを持っていて、モバイルアプリケーションでユーザー体験を向上させるために訪問プロファイルを使用したい場合にこの機能を使用します。

```csharp
void SetVisitorServiceListener(Action callback);
```

| パラメータ   | 型       | 説明                                          |
|:-------------|:---------|:----------------------------------------------|
| `callback  ` | `Action` | 訪問プロファイルが取得されたときの実行コード |

```csharp
tealium.SetVisitorServiceListener((visitorProfile) =&gt;
{
    System.Diagnostics.Debug.WriteLine(&#34;Visitor Updated&#34;);
    System.Diagnostics.Debug.WriteLine($&#34;Visitor: {visitorProfile}&#34;);
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
tealium.Track(new TealiumEvent(&#34;cart_add&#34;, new Dictionary&lt;string, object&gt; {
    { &#34;customer_id&#34;, &#34;abc123&#34; }, 
    { &#34;product_id&#34;, new[] {&#34;PROD123&#34;, &#34;PROD456&#34;} },
    { &#34;product_price&#34;, new[] {4.00, 6.00} }
}));
```
## クラス: `TealiumConfig`

以下は、`TealiumConfig` クラスのプロパティをまとめたものです。

| パラメータ | 型 | 説明 | 例 |
|:----------|:----|:-----------|:-------|
| `account` | `String` | (必須) Tealiumアカウント名 | `&#34;companyXYZ&#34;` |
| `profile` | `String` | (必須) Tealiumプロファイル名 | `&#34;main&#34;` |
| `environment` | [`Environment`](#environment) | (必須) Tealium環境名 | `Environment.dev` |
| `dataSource` | `String` | CDHデータソースキー | `&#34;abc123&#34;` |
| `collectors` | `Collectors[]` | (必須) Tealiumライブラリを初期化するための[`Collectors`](#collectors)のリストを構成 | `[Collectors.AppData]` |
| `dispatchers` | `Dispatchers[]` | (必須) Tealiumライブラリを初期化するための[`Dispatchers`](#dispatchers)のリストを構成 | `[Dispatchers.Collect]` |
| `customVisitorId` | `String` | カスタム訪問IDを構成 | `&#34;ALK2398LSDKJ3289SLKJ3298SLKJ3&#34;` |
| `memoryReportingEnabled` | `Boolean` | デバイスデータモジュールでのメモリレポートを有効または無効にする（デフォルト: 無効）。 | `true` |
| `overrideCollectDomain` | `String` | Tealium Collect URLのドメインを上書き。[ファーストパーティドメイン](/ja/iq-tag-management/administration/first-party-domains/manage/)で使用。 | `&#34;your-domain.com&#34;` |
| `overrideCollectProfile` | `String` | Tealium Collectプロファイルを上書きして、異なるTealiumプロファイルにデータを送信。 | `&#34;custom-profile&#34;` |
| `overrideCollectURL` | `String` | Tealium Collect URLを上書きして、異なるエンドポイントにデータを送信。イベントバッチ機能を使用する場合は、`overrideCollectBatchURL`プロパティも上書き。 | `&#34;https://custom-domain.com/event&#34;` |
| `overrideCollectBatchURL` | `String` | Tealium CollectバッチURLを上書きして、異なるエンドポイントにデータを送信。 | `&#34;https://custom-domain.com/batch-event&#34;` |
| `overrideLibrarySettingsURL` | `String` | 公開構成URLを上書き。 | `&#34;https://custom-domain.com/mobile.html&#34;` |
| `overrideTagManagementURL` | `String` | タグ管理モジュールで使用されるデフォルトURLを上書き。Tealium JavaScriptファイルを自己ホスティングする場合に必要。 | `&#34;https://custom-domain.com/path/env/utag.js&#34;` |
| `deepLinkTrackingEnabled` | `Boolean` | [標準ディープリンクの自動追跡](/ja/platforms/getting-started-mobile/deep-linking/#readout)を有効または無効にする。例えば、Facebookや他のソースからのアプリへのリンクやQRトレースも含む（デフォルト: 有効）。 | `false` |
| `qrTraceEnabled` | `Boolean` | [QRトレース](/ja/platforms/getting-started-mobile/trace/#how-it-works)を有効または無効にする（デフォルト: 有効）。 | `false` |
| `loglevel` | [`LogLevel`](#loglevel) | ログレベルプロパティを構成し、ログに記録される情報の量を制御する（デフォルト: サイレント）。 | `LogLevel.dev` |
| `consentExpiry` | [`ConsentExpiry`](#consentexpiry) | ユーザーの同意構成の有効期限を構成する。（ポリシーに依存するデフォルト値） | `ConsentExpiry(90, TimeUnit.days)` |
| `consentLoggingEnabled` | `Boolean` | [同意ログ記録]()機能を有効にする。これにより、すべての同意ステータス変更が監査目的でTealium Customer Data Hubに送信される（デフォルト: 有効）。 | `true` |
| `consentPolicy` | [`ConsentPolicy`](#consentpolicy) | 同意ポリシーを構成する。例えば、CCPAやGDPR。このプロパティが構成されている場合のみ、Consent Managerが有効になる。 | `ConsentPolicy.gdpr` |
| `lifecycleAutotrackingEnabled` | `Boolean` | ライフサイクル自動追跡を有効または無効にする（デフォルト: 有効）。 | `false` |
| `useRemoteLibrarySettings` | `Boolean` | [モバイル公開構成]()を有効または無効にする（デフォルト: 有効）。Tealium iQタグ管理でモバイル公開構成を構成するか、この機能を無効にする。 | `false` |
| `visitorServiceEnabled` | `Boolean` | [データレイヤーエンリッチメントAPI]()を使用して訪問プロファイルの自動取得を有効または無効にする（デフォルト: 無効）。 | `true` |
| `remoteCommands` | `RemoteCommand[]` | インスタンスが準備完了時に追加する[RemoteCommand](#RemoteCommand)オブジェクトのリストを構成する。 | `[{ id: &#34;hello-world&#34;, callback: (payload) =&gt; { console.log(&#34;hello-world: &#34; &#43; JSON.stringify(payload)); } }]` |
| `overrideConsentCategoriesKey` | `String` | 同意カテゴリイベント属性の名前を上書きする。サーバーサイドの同意の自動適用を無効にする方法について詳しくは[こちら]()を参照。（デフォルト: `consent_categories`） | `consent_categories_granted` |
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
    new List&lt;Collectors&gt; {
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
    new List&lt;Dispatchers&gt; {
        Dispatchers.Collect, Dispatchers.RemoteCommands
    }
    // ...
);
```

利用可能なディスパッチャーは以下の通りです:

* `Dispatchers.Collect`
* `Dispatchers.RemoteCommands`
* `Dispatchers.TagManagement`

少なくとも1つのディスパッチャーが必要です。

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
| `ArraysOfBooleans`| `IDictionary&lt;string, IList&lt;bool&gt;&gt;`                | `id: &#34;5129&#34;, value: [true,false,true,true]`                |
| `ArraysOfNumbers` | `IDictionary&lt;string, IList&lt;double&gt;&gt;`              | `id: &#34;57&#34;, value: [4.82125, 16.8, 0.5714285714285714]`     |
| `ArraysOfStrings` | `IDictionary&lt;string, IList&lt;string&gt;&gt;`              | `id: &#34;5213&#34;, value: [&#34;green shirts&#34;, &#34;green shirts&#34;, &#34;blue shirts&#34;]` |
| `Audiences`       | `IDictionary&lt;string, string&gt;`                     | `id: &#34;tealiummobile_demo_103&#34;, value: &#34;iOS Users&#34;`         |
| `Badges`          | `IDictionary&lt;string, bool&gt;`                       | `id: &#34;2815&#34;, value: true`                                  |
| `Booleans`        | `IDictionary&lt;string, bool&gt;`                       | `id: &#34;4868&#34;, value: true`                                  |
| `CurrentVisit`    | `ICurrentVisit`                                    |                                                            |
| `Dates`           | `IDictionary&lt;string, long&gt;`                       | `id: &#34;22&#34;, value: 1567120112000`                           |
| `Numbers`         | `IDictionary&lt;string, double&gt;`                     | `id: &#34;5728&#34;, value: 4.82125`                               |
| `SetOfStrings`    | `IDictionary&lt;string, ISet&lt;string&gt;&gt;`               | `id: &#34;5211&#34;, value: [&#34;green shirts&#34;, &#34;red shirts&#34;, &#34;blue shirts&#34;]`   |
| `Strings`         | `IDictionary&lt;string, string&gt;`                     | `id: &#34;5380&#34;, value: &#34;green shirts&#34;`                        |
| `Tallies`         | `IDictionary&lt;string, IDictionary&lt;string, double&gt;&gt;`| `&#34;57&#34;: [[&#34;category 1&#34;: 2.0], &#34;category 2&#34;: 1.0]]`          |

### `ICurrentVisit`

現在の訪問に関連する属性を含むオブジェクトです。

| パラメーター       | プロパティ                                          | 値                                                         |
|:------------------|:--------------------------------------------------|:-----------------------------------------------------------|
| `ArraysOfBooleans`| `IDictionary&lt;string, IList&lt;bool&gt;&gt;`                | `id: &#34;5129&#34;, value: [true,false,true,true]`                |
| `ArraysOfNumbers` | `IDictionary&lt;string, IList&lt;double&gt;&gt;`              | `id: &#34;57&#34;, value: [4.82125, 16.8, 0.5714285714285714]`     |
| `ArraysOfStrings` | `IDictionary&lt;string, IList&lt;string&gt;&gt;`              | `id: &#34;5213&#34;, value: [&#34;green shirts&#34;, &#34;green shirts&#34;, &#34;blue shirts&#34;]` |
| `Booleans`        | `IDictionary&lt;string, bool&gt;`                       | `id: &#34;4868&#34;, value: true`                                  |
| `Dates`           | `IDictionary&lt;string, long&gt;`                       | `id: &#34;22&#34;, value: 1567120112000`                           |
| `Numbers`         | `IDictionary&lt;string, double&gt;`                     | `id: &#34;5728&#34;, value: 4.82125`                               |
| `SetOfStrings`    | `IDictionary&lt;string, ISet&lt;string&gt;&gt;`               | `id: &#34;5211&#34;, value: [&#34;green shirts&#34;, &#34;red shirts&#34;, &#34;blue shirts&#34;]`   |
| `Strings`         | `IDictionary&lt;string, string&gt;`                     | `id: &#34;5380&#34;, value: &#34;green shirts&#34;`                        |
| `Tallies`         | `IDictionary&lt;string, IDictionary&lt;string, double&gt;&gt;`| `&#34;57&#34;: [[&#34;category 1&#34;: 2.0], &#34;category 2&#34;: 1.0]]`          |
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
| `eventData`   | `Dictionary&lt;string, object&gt;`   | （オプション）イベントに送信されるキーと値の形式のデータ。 |

例：

```csharp
tealium.Track(new TealiumEvent(&#34;cart_add&#34;, new Dictionary&lt;string, object&gt; {
    { &#34;customer_id&#34;, &#34;abc123&#34; }, 
    { &#34;product_id&#34;, new[] {&#34;PROD123&#34;, &#34;PROD456&#34;} },
    { &#34;product_price&#34;, new[] {4.00, 6.00} }
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
| `eventData`   | `Dictionary&lt;string, object&gt;`   | （オプション）イベントに送信されるキーと値の形式のデータ。 |

例：

```csharp
tealium.Track(new TealiumView(&#34;purchase&#34;, new Dictionary&lt;string, object&gt; {
    { &#34;customer_id&#34;, &#34;abc123&#34; },
    { &#34;order_total&#34;, 10.00 },
    { &#34;product_id&#34;, new[] {&#34;PROD123&#34;, &#34;PROD456&#34;} },
    { &#34;order_id&#34;, &#34;0123456789&#34; }
}));
```
