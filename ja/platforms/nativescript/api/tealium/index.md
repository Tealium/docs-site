---
title: Tealium
description: Tealium クラスは、すべてのモジュールに対するメイン API エントリーポイントとして機能します。
url: https://docs.tealium.com/ja/platforms/nativescript/api/tealium/
---

## クラス：`Tealium`

以下は、NativeScript プラグインの `Tealium` クラスでよく使用されるメソッドとプロパティの概要です。

| メソッド／プロパティ | 説明 |
| ----- | ------ |
| [`addRemoteCommand()`](#addremotecommand)| リモートコマンドマネージャーにリモートコマンドを追加します |
| [`addData()`](#adddata)| 永続データ保存にデータを追加します |
| [`consentCategories`](#consentcategories)| ユーザーの同意カテゴリを取得または構成します |
| [`consentStatus`](#consentstatus)| ユーザーの同意ステータスを取得または構成します |
| [`getData()`](#getdata)| データレイヤーからデータを取得します |
| [`gatherTrackData()`](#gathertrackdata)| すべてのコレクターとデータレイヤーからデータを収集します |
| [`initialize()`](#initialize) | 構成パラメータを使用して Tealium を初期化します |
| [`joinTrace()`](#jointrace)| 指定された ID のトレースに参加します |
| [`leaveTrace()`](#leavetrace)| アクティブなトレースセッションから退出します |
| [`removeData()`](#removedata)| `addData()` を使用して以前に構成した永続データを削除します |
| [`removeRemoteCommand()`](#removeremotecommand) | リモートコマンドマネージャーからリモートコマンドを削除します |
| [`removeVisitorServiceListener()`](#removevisitorservicelistener)| Visitor Service のリスナー／コールバックを削除します |
| [`setVisitorServiceListener()`](#setvisitorservicelistener)| Visitor Service のリスナー／コールバックを定義します |
| [`terminateInstance()`](#terminateinstance)| Tealium ライブラリを無効にし、すべてのモジュール参照を削除します |
| [`track()`](#track)| イベントまたは画面表示をトラッキングします |
| [`visitorId`](#visitorid) | 現在の訪問 ID を取得します |

### `addRemoteCommand()`

リモートコマンドマネージャーにリモートコマンドを追加します。

```javascript
Tealium.addRemoteCommand(id, callback);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `id` | `String` | タグ構成にあるリモートコマンド ID の名前 | `"test_command"` |
| `callback` | `Function ` | リモートコマンドからレスポンスを受信した後に実行するコールバック関数。コールバックは、タグマッピングから取得したキーと値のペアを含むペイロードを返します。 | （例を参照） |

例：

```javascript
Tealium.addRemoteCommand('mycommand', (result: any): void => {
	console.log(result["payload"]["command_id"]);            // logs "mycommand"
	console.log(result["payload"]["my_remote_command_key"]); // logs value for key "my_remote_command_key"
});
```

### `addData()`

指定した[有効期限](https://docs.tealium.com/ja/platforms/nativescript/api/tealium-config/#expiry)で、永続データ保存にデータを追加します。

```javascript
Tealium.addData(data, expiry);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `data` | `Object` | キーと値のペアのマップ。キーは文字列で、値は文字列または文字列の配列です | `{"persistent_key2" : "persistent_val2"}` |
| `expiry` | [`Expiry`](https://docs.tealium.com/ja/platforms/nativescript/api/tealium-config/#expiry) | データを永続化する期間 | `Expiry.forever` |

例：

```javascript
let data: Map<string, any> = new Map([['test_session_data', 'test']]);
data.set('my_test_value', 1);
data['my_test_value'] = 1;
Tealium.addData(data, Expiry.session);
```

#### `Expiry`

有効期限があるプロパティを構成する際の有効期限を定義します。

次の有効期限オプションを使用できます。

| 値 | 説明 |
| :-- | :-- |
| `Expiry.session`（デフォルト）| 現在のセッション終了時に期限切れになります |
| `Expiry.forever` | アプリがインストールされている間は期限切れになりません |
| `Expiry.untilRestart` | デバイスの再起動時に期限切れになります |

### `consentCategories`

ユーザーの同意カテゴリを取得または構成します。

ユーザーの同意カテゴリを構成するには、次のようにします。

```javascript
Tealium.consentCategories = categories
```

ユーザーの同意カテゴリを取得するには、次のようにします。  
```javascript
let categories = Tealium.consentCategories
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `categories` | `ConsentCategories[]` | ユーザー同意カテゴリの配列 | `[ConsentCategories.email, ConsentCategories.personalization]` |

例：

```javascript
Tealium.consentCategories = [ConsentCategories.analytics, ConsentCategories.email];
```

次の同意カテゴリを使用できます。

| 値 | 説明 |
| --- | --- |
| `analytics` | アナリティクス |
| `affiliates` | アフィリエイト |
| `displayAds` | ディスプレイ広告 |
| `email` | メール |
| `personalization` | パーソナライゼーション |
| `search` | 検索 |
| `social` | ソーシャル |
| `bigData` | ビッグデータ |
| `mobile` | モバイル |
| `engagement` | エンゲージメント |
| `monitoring` | モニタリング |
| `crm` | CRM |
| `cdp` | CDP |
| `cookieMatch` | Cookie マッチング |
| `misc` | その他 |

### `consentStatus`

ユーザーの同意ステータスを取得または構成します。変更されるまでは、デフォルトで `.unknown` です。

ユーザーの同意ステータスを構成するには、次のようにします。  
```javascript
Tealium.consentStatus = status;
```

ユーザーの同意ステータスを取得するには、次のようにします。  
```javascript
let status = Tealium.consentStatus
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `status` | `ConsentStatus` | ユーザーの同意ステータス | `ConsentStatus.consented` |

例：

```javascript
Tealium.consentStatus = ConsentStatus.consented;
```

次の同意ステータスを使用できます。

| 値 | 説明 |
| --- | --- |
| `.consented` | 同意済み |
| `.notConsented` | 未同意 |
| `.unknown` | 不明 |

### `getData()`

データレイヤーからデータを `any` 型として取得します。

```javascript
let data = Tealium.getData(key);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `key` | `String` | 取得するデータのキー | `"KEY"` |

```javascript
let data: Tealium.getData("KEY")
```

### `initialize()`

他のメソッドを呼び出す前に Tealium を初期化します。

```javascript
Tealium.initialize(config);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `config` | [`TealiumConfig`](https://docs.tealium.com/ja/platforms/nativescript/api/tealium-config/#tealiumconfig) | Tealium の構成パラメータ | （例を参照） |

例：

```javascript
let config: TealiumConfig =
{
	account: 'ACCOUNT',
	profile: 'PROFILE',
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

Tealium.initialize(config);
```

### `joinTrace()`

指定した ID のトレースに参加します。Tealium Customer Data Hub の[トレース](https://docs.tealium.com/manage-traces/)機能について詳しく確認してください。

```javascript
Tealium.joinTrace(id);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `id` | `String` | データソースキーから取得したトレース ID | `abc123xy` |

例：

```javascript
Tealium.joinTrace("abc123xy");
```

### `leaveTrace()`

トレースは、`leaveTrace()` メソッドが呼び出されるまでアプリセッション中はアクティブな状態を維持します。このメソッドを呼び出すと、以前参加したトレースから退出し、訪問セッションが終了します。

```javascript
Tealium.leaveTrace();
```

### `removeData()`

`Tealium.addData()` を使用して以前に構成した永続データを削除します。

```javascript
Tealium.removeData(keys);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `keys` | `String[]` | キー名の配列 | `["foo", "bar"]` |

例：

```javascript
Tealium.removeData(["foo", "bar"]);
```

### `gatherTrackData()`

すべてのコレクターとデータレイヤーからすべてのデータを収集します。

例：
```javascript
Tealium.gatherTrackData((response: Map<string, any>): void => {				
	console.log(response);
});
```
### `removeRemoteCommand()`

リモートコマンドマネージャーからリモートコマンドを削除します。

```javascript
Tealium.removeRemoteCommand(id);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `id ` | `String` | 削除するコマンドIDの名前 | `"test_command"` |

例：

```javascript
Tealium.removeRemoteCommand("test_command");
```

### `setVisitorServiceListener()`

訪問プロファイルが更新されたときに実行するコールバックを定義します。更新された[`VisitorProfile`](https://docs.tealium.com/ja/platforms/nativescript/api/tealium-config/#visitorprofile)は、コールバックのレスポンスで提供されます。

VisitorServiceモジュールは、Tealium Customer Data Hubの[データレイヤーエンリッチメント](https://docs.tealium.com/about-data-layer-enrichment/)機能を実装します。

Customer Data Platform（CDP）のライセンスを保有しており、訪問プロファイルを使用してモバイルアプリケーションのユーザーエクスペリエンスを向上させる場合は、このモジュールの使用を推奨します。Customer Data Platform（CDP）のライセンスを保有していない場合、訪問プロファイルは返されないため、このモジュールの使用は推奨されません。

```javascript
Tealium.setVisitorServiceListener(callback);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `callback` | `Function` | 更新された訪問プロファイルが返されたときに実行するコード | （例を参照） |

次の例では、訪問のオーディエンスとバッジをコンソールに記録します。

```javascript
Tealium.setVisitorServiceListener(profile => {
    console.log(profile["audiences"]);
    console.log(profile["badges"]);
});
```

### `terminateInstance()`

Tealiumライブラリを無効にし、すべてのモジュール参照を削除します。必要な場合は、新しいTealiumインスタンスを作成して再度有効にします。

```javascript
Tealium.terminateInstance();
```

### `track()`

画面表示またはイベントを、オプションの関連データとともにトラッキングします。

```
tealium?.track(tealEvent)
```

| パラメータ | 型 | 説明 |
|:-----------|:------|:------------|
| `tealEvent` | string | イベント名を`tealium_event`属性として渡し、オプションのイベントデータオブジェクトを含む[TealiumDispatch](https://docs.tealium.com/ja/platforms/nativescript/api/tealium-config/#dispatchers)。 |

イベントをトラッキングするには、[`TealiumEvent`](#class-tealiumevent)のインスタンスを`track()`メソッドに渡します。

```javascript
let tealEvent = new TealiumEvent(
	"cart_add", 
	new Map([
		[
			"customer_id": "abc123", 
			"product_id": ["PROD123", "PROD456"], 
			"product_price": [4.00, 6.00]
		]
	])
);
Tealium.track(tealEvent);
```

### `visitorId`

現在の訪問IDを取得します。

```javascript
let visitorId = Tealium.visitorId;
```

## インターフェイス：`TealiumDispatch`

トラッキングするディスパッチの型を定義するインターフェイスです。次のクラスが`TealiumDispatch`を実装します。

### クラス：`TealiumEvent`

ユーザーによる画面操作または画面表示をトラッキングするには、`TealiumEvent(tealiumEvent, dataLayer)`のインスタンスを[`Track()`](#track)メソッドに渡します。`TealiumEvent`は、トラッキング呼び出しで`tealium_event`として表示されるイベント名と、オプションのデータディクショナリで構成されます。

```javascript
let tealEvent = new TealiumEvent(tealiumEvent, eventData);
Tealium.track(tealEvent);
```

| パラメータ | 型 | 説明 |
|:------------|:--------|:-----------------|
| `tealiumEvent` | `string` | `tealium_event`属性として渡されるイベント名 |
| `eventData` | `<string, object>` | （オプション）イベントとともに送信するキーバリュー形式のデータ。 |

例：

```javascript
let tealEvent = new TealiumEvent(
	"cart_add", 
	new Map([
		[
			"customer_id": "abc123", 
			"product_id": ["PROD123", "PROD456"], 
			"product_price": [4.00, 6.00]
		]
	)
);
Tealium.track(tealEvent);
```

### クラス：`TealiumView`

画面表示をトラッキングするには、`TealiumView(tealiumEvent, dataLayer)`のインスタンスを[`Track()`](#track)メソッドに渡します。`TealiumView`は、トラッキング呼び出しで`tealium_event`として表示されるビュー名と、オプションのデータディクショナリで構成されます。

```javascript
let screenView = new TealiumEvent(tealiumEvent, eventData);
Tealium.track(screenView);
```

| パラメータ | 型 | 説明 |
|:------------|:--------|:-----------------|
| `tealiumEvent` | `string` | `tealium_event`属性として渡されるイベント名。 |
| `eventData` | `Dictionary<string, object>` | （オプション）イベントとともに送信するキーバリュー形式のデータ。 |

例：

```javascript
let screenView = new TealiumView(
	'purchase', 
	new Map([
		[
			'customer_id', 'abc123', 
			'order_total', 10.00, 
			'product_id', ["PROD123", "PROD456"], 
			'order_id': "0123456789"
		]
	])
);
Tealium.track(screenView);
```