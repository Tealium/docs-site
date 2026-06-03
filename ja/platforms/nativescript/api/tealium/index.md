---
title: Tealium
description: Tealiumクラスは、すべてのモジュールのための主要なAPIエントリーポイントとして機能します。
url: https://docs.tealium.com/ja/platforms/nativescript/api/tealium/
---
## クラス: `Tealium`

以下は、NativeScriptプラグインの`Tealium`クラスで一般的に使用されるメソッドとプロパティをまとめたものです。

| メソッド/プロパティ | 説明 |
| ----- | ------ |
| [`addRemoteCommand()`](#addremotecommand)| リモートコマンドマネージャーにリモートコマンドを追加します |
| [`addData()`](#adddata)| 永続データ保存にデータを追加します |
| [`consentCategories`](#consentcategories)| ユーザーの同意カテゴリを取得または構成します |
| [`consentStatus`](#consentstatus)| ユーザーの同意状態を取得または構成します |
| [`getData()`](#getdata)| データレイヤーからデータを取得します |
| [`gatherTrackData()`](#gathertrackdata)| すべてのコレクターとデータレイヤーからデータを収集します |
| [`initialize()`](#initialize) | 構成パラメータでTealiumを初期化します |
| [`joinTrace()`](#jointrace)| 指定されたIDでトレースに参加します |
| [`leaveTrace()`](#leavetrace)| アクティブなトレースセッションを離れます |
| [`removeData()`](#removedata)| `addData()`を使用して以前に構成された永続データを削除します |
| [`removeRemoteCommand()`](#removeremotecommand) | リモートコマンドマネージャーからリモートコマンドを削除します |
| [`removeVisitorServiceListener()`](#removevisitorservicelistener)| 訪問サービスリスナー/コールバックを削除します |
| [`setVisitorServiceListener()`](#setvisitorservicelistener)| 訪問サービスリスナー/コールバックを定義します |
| [`terminateInstance()`](#terminateinstance)| Tealiumライブラリを無効にし、すべてのモジュール参照を削除します |
| [`track()`](#track)| イベントまたは画面表示を追跡します |
| [`visitorId`](#visitorid) | 現在の訪問IDを取得します |

### `addRemoteCommand()`

リモートコマンドマネージャーにリモートコマンドを追加します。

```javascript
Tealium.addRemoteCommand(id, callback);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `id` | `String` | タグ構成からのリモートコマンドIDの名前 | `&#34;test_command&#34;` |
| `callback` | `Function ` | リモートコマンドからの応答を受け取った後に実行されるコールバック関数。コールバックはタグマッピングからのキー値ペアのペイロードを返します。 | (例を参照) |

例:

```javascript
Tealium.addRemoteCommand(&#39;mycommand&#39;, (result: any): void =&gt; {
	console.log(result[&#34;payload&#34;][&#34;command_id&#34;]);            // &#34;mycommand&#34;をログに記録
	console.log(result[&#34;payload&#34;][&#34;my_remote_command_key&#34;]); // キー&#34;my_remote_command_key&#34;の値をログに記録
});
```

### `addData()`

指定された[有効期限](/ja/platforms/nativescript/api/tealium-config/#expiry)のために永続データ保存にデータを追加します。

```javascript
Tealium.addData(data, expiry);
```
| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `data` | `Object` | 文字列のキーと、値が文字列または文字列の配列であるキー値ペアのマップ | `{&#34;persistent_key2&#34; : &#34;persistent_val2&#34;}` |
| `expiry` | [`Expiry`](/ja/platforms/nativescript/api/tealium-config/#expiry) | データを永続させる時間の長さ | `Expiry.forever` |

例:

```javascript
let data: Map&lt;string, any&gt; = new Map([[&#39;test_session_data&#39;, &#39;test&#39;]]);
data.set(&#39;my_test_value&#39;, 1);
data[&#39;my_test_value&#39;] = 1;
Tealium.addData(data, Expiry.session);
```

#### `Expiry`

プロパティの有効期限を構成するための有効期限を定義します。

利用可能な有効期限オプションは次のとおりです：

| 値 | 説明 |
| :-- | :-- |
| `Expiry.session` (デフォルト)| 現在のセッションの終了時に期限切れになります |
| `Expiry.forever` | アプリがインストールされている間は期限切れになりません |
| `Expiry.untilRestart` | デバイスが再起動されると期限切れになります |

### `consentCategories`

ユーザーの同意カテゴリを取得または構成します。

ユーザーの同意カテゴリを構成するには：

```javascript
Tealium.consentCategories = categories
```

ユーザーの同意カテゴリを取得するには：  
```javascript
let categories = Tealium.consentCategories
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `categories` | `ConsentCategories[]` | ユーザー同意カテゴリの配列 | `[ConsentCategories.email, ConsentCategories.personalization]` |

例:

```javascript
Tealium.consentCategories = [ConsentCategories.analytics, ConsentCategories.email];
```

利用可能な同意カテゴリは次のとおりです：

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
| `cookieMatch` | クッキーマッチ |
| `misc` | その他 |

### `consentStatus`

ユーザーの同意状態を取得または構成します。デフォルトは`.unknown`で、変更されるまでその状態です。

ユーザーの同意状態を構成するには：  
```javascript
Tealium.consentStatus = status;
```

ユーザーの同意状態を取得するには：  
```javascript
let status = Tealium.consentStatus
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `status` | `ConsentStatus` | ユーザーの同意状態 | `ConsentStatus.consented` |

例:

```javascript
Tealium.consentStatus = ConsentStatus.consented;
```

利用可能な同意状態は次のとおりです：

| 値 | 説明 |
| --- | --- |
| `.consented` | 同意済み |
| `.notConsented` | 同意していない |
| `.unknown` | 不明 |

### `getData()`
データレイヤーから`any`型のデータを取得します。

```javascript
let data = Tealium.getData(key);
```
| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `key` | `String` | 取得するデータのキー | `&#34;KEY&#34;` |

```javascript
let data: Tealium.getData(&#34;KEY&#34;)
```

### `initialize()`

他のメソッドを呼び出す前にTealiumを初期化します。

```javascript
Tealium.initialize(config);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `config` | [`TealiumConfig`](/ja/platforms/nativescript/api/tealium-config/#tealiumconfig) | Tealiumの構成パラメータ | (例を参照) |

例:

```javascript
let config: TealiumConfig =
{
	account: &#39;ACCOUNT&#39;,
	profile: &#39;PROFILE&#39;,
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

指定されたIDでトレースに参加します。Tealium Customer Data Hubの[Trace]()機能について詳しくはこちらをご覧ください。

```javascript
Tealium.joinTrace(id);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `id` | `String` | データソースキーから取得したトレースID | `abc123xy` |

例:

```javascript
Tealium.joinTrace(&#34;abc123xy&#34;);
```

### `leaveTrace()`

`leaveTrace()`メソッドが呼ばれるまで、トレースはアプリセッションの間アクティブなままです。これにより、以前に参加したトレースを離れ、訪問セッションが終了します。

```javascript
Tealium.leaveTrace();
```


### `removeData()`
`Tealium.addData()`を使用して以前に構成された永続データを削除します。

```javascript
Tealium.removeData(keys);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `keys` | `String[]` | キー名の配列  | `[&#34;foo&#34;, &#34;bar&#34;]` |

例:

```javascript
Tealium.removeData([&#34;foo&#34;, &#34;bar&#34;]);
```

### `gatherTrackData()`
すべてのコレクターとデータレイヤーからすべてのデータを収集します。

例:
```javascript
Tealium.gatherTrackData((response: Map&lt;string, any&gt;): void =&gt; {				
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
| `id` | `String` | 削除するコマンドIDの名前 | `&#34;test_command&#34;` |

例:

```javascript
Tealium.removeRemoteCommand(&#34;test_command&#34;);
```

### `setVisitorServiceListener()`
訪問プロファイルが更新されたときに実行するコールバックを定義します。更新された[`VisitorProfile`](/ja/platforms/nativescript/api/tealium-config/#visitorprofile)はコールバックレスポンスで提供されます。

VisitorServiceモジュールはTealium Customer Data Hubの[Data Layer Enrichment]()機能を実装しています。

このモジュールの使用は、Tealium AudienceStreamのライセンスを持っていて、モバイルアプリケーションで訪問プロファイルを使用してユーザーエクスペリエンスを向上させたい場合に推奨されます。AudienceStreamのライセンスがない場合、訪問プロファイルが返されないため、このモジュールの使用は推奨されません。

```javascript
Tealium.setVisitorServiceListener(callback);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `callback` | `Function` | 更新された訪問プロファイルが返された後に実行するコード | (例を参照) |

次の例では、訪問のオーディエンスとバッジをコンソールにログします：

```javascript
Tealium.setVisitorServiceListener(profile =&gt; {
    console.log(profile[&#34;audiences&#34;]);
    console.log(profile[&#34;badges&#34;]);
});
```

### `terminateInstance()`

Tealiumライブラリを無効にし、すべてのモジュール参照を削除します。必要に応じて新しいTealiumインスタンスを作成して再有効化します。

```javascript
Tealium.terminateInstance();
```

### `track()`

オプショナルな関連データを持つ画面表示またはイベントを追跡します。

```
tealium?.track(tealEvent)
```

| パラメータ | 型  | 説明 | 
|:-----------|:------|:------------|
| `tealEvent` | string | [TealiumDispatch](/ja/platforms/nativescript/api/tealium-config/#dispatchers) で、イベント名を `tealium_event` 属性として渡し、オプショナルなイベントデータオブジェクトを含みます。 |

イベントを追跡するには、`track()` メソッドに [`TealiumEvent`](#class-tealiumevent) のインスタンスを渡します：

```javascript
let tealEvent = new TealiumEvent(
	&#34;cart_add&#34;, 
	new Map([
		[
			&#34;customer_id&#34;: &#34;abc123&#34;, 
			&#34;product_id&#34;: [&#34;PROD123&#34;, &#34;PROD456&#34;], 
			&#34;product_price&#34;: [4.00, 6.00]
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

## インターフェース: `TealiumDispatch`

追跡するディスパッチのタイプを定義するインターフェースです。次のクラスが `TealiumDispatch` を実装しています：

### クラス: `TealiumEvent`

ユーザーの画面とのやり取りまたは画面表示を追跡するには、[`Track()`](#track) メソッドに `TealiumEvent(tealiumEvent, dataLayer)` のインスタンスを渡します。`TealiumEvent` はイベント名を含み、追跡コールで `tealium_event` として表示され、オプショナルなデータ辞書が含まれます。

```javascript
let tealEvent = new TealiumEvent(tealiumEvent, eventData);
Tealium.track(tealEvent);
```

| パラメータ  | 型    | 説明      | 
|:------------|:--------|:-----------------|
| `tealiumEvent` | `string` | イベント名で、`tealium_event` 属性として渡されます。 |
| `eventData` | `&lt;string, object&gt;` | オプショナル。イベントに送信されるキーと値の形式のデータ。 | 

例:

```javascript
let tealEvent = new TealiumEvent(
	&#34;cart_add&#34;, 
	new Map([
		[
			&#34;customer_id&#34;: &#34;abc123&#34;, 
			&#34;product_id&#34;: [&#34;PROD123&#34;, &#34;PROD456&#34;], 
			&#34;product_price&#34;: [4.00, 6.00]
		]
	])
);
Tealium.track(tealEvent);
```

### クラス: `TealiumView`

画面表示を追跡するには、[`Track()`](#track) メソッドに `TealiumView(tealiumEvent, dataLayer)` のインスタンスを渡します。`TealiumView` はビュー名を含み、追跡コールで `tealium_event` として表示され、オプショナルなデータ辞書が含まれます。

```javascript
let screenView = new TealiumEvent(tealiumEvent, eventData);
Tealium.track(screenView);
```

| パラメータ  | 型    | 説明      | 
|:------------|:--------|:-----------------|
| `tealiumEvent`  | `string`| イベント名で、`tealium_event` 属性として渡されます。          | 
| `eventData` | `Dictionary&lt;string, object&gt;` | オプショナル。イベントに送信されるキーと値の形式のデータ。 | 

例:

```javascript
let screenView = new TealiumView(
	&#39;purchase&#39;, 
	new Map([
		[
			&#39;customer_id&#39;, &#39;abc123&#39;, 
			&#39;order_total&#39;, 10.00, 
			&#39;product_id&#39;, [&#34;PROD123&#34;, &#34;PROD456&#34;], 
			&#39;order_id&#39;: &#34;0123456789&#34;
		]
	])
);
Tealium.track(screenView);
```
