---
title: Tealium
description: Tealium クラスは、すべてのモジュールに対するメイン API エントリーポイントとして機能します。
url: https://docs.tealium.com/ja/platforms/flutter/api/tealium/
---
## クラス：`Tealium`

以下に、Flutter の `Tealium` クラスでよく使用されるメソッドの概要を示します。

| メソッド | 説明 |
| ----- | ------ |
| [`addCustomRemoteCommand()`](#addcustomremotecommand)| リモートコマンドマネージャーにリモートコマンドのコールバックを追加します。 |
| [`addRemoteCommand()`](#addremotecommand)| リモートコマンドマネージャーにリモートコマンドを追加します。 |
| [`addToDataLayer()`](#addtodatalayer) | 永続データレイヤーにデータを追加します。 |
| [`clearStoredVisitorIds()`](#clearstoredvisitorids) | 以前に保存されたすべての訪問 ID とハッシュ化された顧客識別子を消去します。その結果、新しい訪問 ID が生成され、アクティブな訪問 ID になります。 |
| [`gatherTrackData()`](#gathertrackdata) | すべてのコレクターとデータレイヤーからデータを収集します。 |
| [`getFromDataLayer()`](#getfromdatalayer) | 永続データレイヤー内の指定されたキーの値を取得します。 |
| [`getConsentCategories()`](#getconsentcategories) | ユーザーが同意したカテゴリーを取得します。 |
| [`getConsentStatus()`](#getconsentstatus) | ユーザーの同意ステータスを取得します。 |
| [`getVisitorId()`](#getvisitorid) | ユーザーの訪問 ID を取得します。 |
| [`initialize()`](#initialize) | 構成パラメーターを使用して Tealium を初期化します。 |
| [`joinTrace()`](#jointrace) | 指定された ID のトレースに参加します。 |
| [`leaveTrace()`](#leavetrace) | 以前に参加したトレースから離脱し、訪問セッションを終了します。 |
| [`removeFromDataLayer()`](#removefromdatalayer) | `addToDataLayer()` を使用して以前に構成された、永続データのキーと値のペアのリストを削除します。 |
| [`removeRemoteCommand()`](#removeremotecommand) | リモートコマンドマネージャーからリモートコマンドを削除します。 |
| [`resetVisitorId()`](#resetvisitorid) | ユーザーの新しい訪問 ID を生成します。 |
| [`setConsentCategories()`](#setconsentcategories) | ユーザーの同意カテゴリーを構成します。 |
| [`setConsentExpiryListener()`](#setconsentexpirylistener) | 同意期限切れのリスナー／コールバックを構成します。 |
| [`setConsentStatus()`](#setconsentstatus) | ユーザーの同意ステータスを構成します。 |
| [`setVisitorIdListener()`](#setvisitoridlistener) | `visitorId` の変更を監視するリスナーを追加します。 |
| [`setVisitorServiceListener()`](#setvisitorservicelistener) | 訪問サービスのリスナー／コールバックを構成します。 |
| [`terminateInstance()`](#terminateinstance) | Tealium ライブラリを無効にしてすべてのモジュール参照を削除することにより、Tealium インスタンスを終了します。 |
| [`track()`](#track) | イベントまたは画面表示をトラッキングします。 |

### `addCustomRemoteCommand()`

Tag Management のタグを基盤とするカスタムリモートコマンドを、リモートコマンドマネージャーに追加します。

```dart
Tealium.addCustomRemoteCommand(id, callback);
```

| パラメーター | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `id` | `String` | タグ構成に含まれるコマンド ID の名前 | `"test_command"` |
| `callback` | `Function ` | リモートコマンドからレスポンスを受信した後に実行するコールバック関数。コールバックは、タグマッピングから得られたキーと値のペアをペイロードとして返します。 | （例を参照） |

例：

```dart
Tealium.addCustomRemoteCommand('CUSTOM_COMMAND_ID', (payload) {
  print(JsonEncoder().convert(payload));
});
```

### `addRemoteCommand()`

リモートコマンドマネージャーにリモートコマンドを追加します。

```dart
Tealium.addRemoteCommand(remoteCommand);
```

| パラメーター | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `remoteCommand` | `RemoteCommand` | パス、URL、または WebView のいずれかで構成された構築済みのリモートコマンド。 | 以下の例を参照してください。 |

例：

```dart
Tealium.addRemoteCommand(RemoteCommand(TealiumFirebase.commandName, path: "firebase.json")); // local
Tealium.addRemoteCommand(RemoteCommand(TealiumFirebase.commandName, url: "www.tealium.com/path_to_remote_command/firebase.json")); // remote
Tealium.addRemoteCommand(RemoteCommand(TealiumFirebase.commandName)); // webview
```

### `addToDataLayer()`

指定された有効期限で、永続データレイヤーにデータを追加します。

```dart
Tealium.addToDataLayer(data, expiry);
```

| パラメーター | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `data` | `Map<String, Object>` | キーと値のペアで構成される JSON オブジェクト。キーは文字列で、値は文字列または文字列の配列です。 | `{'persistent_key' : 'persistent_val'}` |
| `expiry` | `Expiry` | データを保持する期間 | `Expiry.forever` |

### `clearStoredVisitorIds()`

以前に保存されたすべての訪問 ID とハッシュ化された顧客識別子を消去します。その結果、新しい訪問 ID が生成され、アクティブな訪問 ID になります。

```dart
Tealium.clearStoredVisitorIds();
```


### `getFromDataLayer()`

永続データレイヤー内の指定されたキーの値を、コールバック関数として取得します。

```dart
Tealium.getFromDataLayer(key);
```

| パラメーター | 型 | 説明 |
|-----------|-------------| ---- |
| `key` | `String` | データレイヤーから取得するキー |
| `N/A` | `Future<dynamic>` | `Tealium.dataLayer` から値が正常に取得されると Future が完了します。 |

例：

```dart
Tealium.getFromDataLayer('key')
    .then((value) => print('Value From data layer: $value'));
```


### `getConsentCategories()`

ユーザーが同意したカテゴリーを取得します。

```dart
Tealium.getConsentCategories();
```

| パラメーター | 型 | 説明 |
|-----------|-------------| ---- |
| `N/A` | `Future<List<dynamic>>` | `Tealium.ConsentManager` から同意カテゴリーが正常に取得されると Future が完了します。 |

例：

```dart
Tealium.getConsentCategories()
  .then((categories) =>
      print('Consent Categories: ' + categories.join(",")));
```


### `getConsentStatus()`

ユーザーの同意ステータスをコールバック関数として取得します。

```dart
Tealium.getConsentStatus();
```

| パラメーター | 型 | 説明 |
|-----------|-------------| ---- |
| `N/A` | `Future<String>` | `Tealium.ConsentManager` から同意ステータスが正常に取得されると Future が完了します。 |

例：

```dart
Tealium.getConsentStatus()
  .then((status) => print('Consent Status: $status'));
```

### `getVisitorId()`

ユーザーの訪問 ID を取得します。

```dart
Tealium.getVisitorId();
```

| パラメーター | 型 | 説明 |
|-----------|-------------| ---- |
| `N/A` | `Future<String>` | `Tealium.visitorId` が正常に取得されると Future が値を返します。 |

例：

```dart
final visitorId = await Tealium.getVisitorId();
```

### `initialize()`

他のメソッドを呼び出す前に Tealium を初期化します。

```dart
Tealium.initialize(config);
```

| パラメーター | 型 | 説明 |
|-----------|-------------| ---- |
| `config`  | `TealiumConfig` | 構成 |
| `N/A` | `Future<void>` | Tealium が正常に初期化されると Future が完了します。失敗した場合は `PlatformException` をスローします。 |


例：

```dart
final config = TealiumConfig(
    'ACCOUNT',
    'PROFILE',
    TealiumEnvironment.dev,
    [Collectors.AppData, Collectors.DeviceData, Collectors.Lifecycle, Collectors.Connectivity],
    [Dispatchers.Collect, Dispatchers.TagManagement, Dispatchers.RemoteCommands],
    loglevel: LogLevel.DEV,
    consentLoggingEnabled: true,
    consentPolicy: ConsentPolicy.GDPR,
    visitorServiceEnabled: true);

try {
    await Tealium.initialize(config);
    Tealium.setConsentStatus(ConsentStatus.consented);
    Tealium.setConsentExpiryListener(() => print('Consent Expired'));
} on PlatformException catch (e) {
    print('Tealium initialization error: ${e.message}');
}
```


### `joinTrace()`

指定された ID のトレースに参加します。詳しくは、[トレース](https://docs.tealium.com/ja/platforms/getting-started-mobile/trace/)を参照してください。

```dart
Tealium.joinTrace(id);
```

| パラメーター | 型 | 説明 | 例 |
|-----------|-------------| ---- | ------- |
| `id` | `String` | CDH から取得したトレース ID | `"abc123xy"` |

### `leaveTrace()`

以前に参加したトレースから離脱し、訪問セッションを終了します。このメソッドが呼び出されるまで、アプリセッションの間はトレースがアクティブな状態に保たれます。

```dart
Tealium.leaveTrace();
```
### `removeFromDataLayer()`

以前に `Tealium.addToDataLayer()` を使用して構成した永続データを削除します。

```dart
Tealium.removeFromDataLayer(keys);
```

| パラメータ | 型 | 説明 | 例 |
|-----------|-------------| ---- | ------- |
| `keys` | `List<String>` | キー名の配列 | `["key1", "key2"]` |

### `removeRemoteCommand()`

リモートコマンドマネージャーからリモートコマンドを削除します。

```dart
Tealium.removeRemoteCommand(id);
```

| パラメータ | 型 | 説明 | 例 |
|-----------|-------------| ---- | ------- |
| `id` | `String` | 削除するコマンド ID の名前 | `"test_command"` |

例：

```dart
Tealium.removeRemoteCommand('test_command');
```

### `resetVisitorId()`

ユーザーの新しい訪問 ID を生成します。

```dart
Tealium.resetVisitorId();
```

### `setConsentCategories()`

ユーザーの同意カテゴリを構成します。カテゴリを構成するには、文字列の配列を渡します。`ConsentStatus` が `ConsentStatus.consented` に構成されるまでは、デフォルトは空の配列です。同意ステータスが `ConsentStatus.consented` で、`setConsentCategories()` メソッドでカテゴリが指定されていない場合は、すべてのカテゴリが構成されます。

```dart
Tealium.setConsentCategories(categories);
```

| パラメータ | 型 | 説明 | 例 |
|-----------|-------------| ---- | ------- |
| `categories` | `List<ConsentCategories>` | ユーザー同意カテゴリの配列 | `[ConsentCategories.email, ConsentCategories.personalization]` |

例：

```dart
Tealium.setConsentCategories([ConsentCategories.analytics, ConsentCategories.email]);
```

#### 同意カテゴリ

以下の同意カテゴリを使用できます。

| 値 | 説明 |
| ----- | ----------- |
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
| `cookieMatch` | Cookie マッチ |
| `misc` | その他 |

### `setConsentExpiryListener()`

`ConsentExpiry` に基づいてユーザーの同意構成が期限切れになった後に実行するコールバックを構成します。

```dart
Tealium.setConsentExpiryListener(callback);
```

| パラメータ | 型 | 説明 |
|-----------|-------------| ---- |
| `callback` | `Function` | 同意の期限切れ後に実行するコード |

```dart
Tealium.setConsentExpiryListener(() => print('Consent Expired'));
```

### `setConsentStatus()`

ユーザーの同意ステータスを構成します。ステータスが更新されるまで、デフォルトは `ConsentStatus.unknown` です。

```dart
Tealium.setConsentStatus(status);
```

| パラメータ | 型 | 説明 |
|-----------|-------------| ---- |
| `status` | `ConsentStatus` | 同意ステータス |

例：

```dart
Tealium.setConsentStatus(ConsentStatus.consented);
```

#### 同意ステータス

以下の同意ステータスを使用できます。

| 値 | 説明 |
| ----- | ----------- |
| `ConsentStatus.consented` | 同意済み |
| `ConsentStatus.notConsented` | 未同意 |
| `ConsentStatus.unknown` | 不明 |

### `setVisitorIdListener()`

訪問 ID が変更されたときに実行するコールバックを構成します。

```dart
Tealium.setVisitorIdListener(callback);
```

| パラメータ | 型 | 説明 |
|-----------|-------------| ---- |
| `callback` | `Function` | 更新された `visitorId` を使用して実行するコード。 |

例：

```dart
Tealium.setVisitorIdListener((newVisitorId) => print(newVisitorId));
```

### `setVisitorServiceListener()`

訪問プロファイルが更新されたときに実行するコールバックを構成します。更新された `VisitorProfile` は、コールバックのレスポンスで提供されます。

VisitorService モジュールは、Tealium Customer Data Hub の[データレイヤーエンリッチメント](https://docs.tealium.com/about-data-layer-enrichment/)機能を実装します。

Customer Data Platform（CDP）のライセンスがあり、訪問プロファイルを使用してモバイルアプリケーションのユーザーエクスペリエンスを向上させる場合は、このモジュールの使用を推奨します。Customer Data Platform（CDP）のライセンスがない場合、訪問プロファイルが返されないため、このモジュールの使用は推奨されません。

```dart
Tealium.setVisitorServiceListener(callback);
```

| パラメータ | 型 | 説明 |
|-----------|-------------| ---- |
| `callback` | `Function` | 更新された訪問プロファイルが返された後に実行するコード |

例：

```dart
Tealium.setVisitorServiceListener((profile) {
    print(JsonEncoder().convert(profile));
});
```

### `terminateInstance()`

Tealium ライブラリを無効にし、すべてのモジュール参照を削除して、Tealium インスタンスを終了します。必要な場合は、新しい Tealium インスタンスを作成して再度有効にします。

```dart
Tealium.terminateInstance();
```

### `track()`

オプションのイベントデータとともに、画面表示またはイベントをトラッキングします。

```dart
Tealium.track(tealEvent);
```

| パラメータ | 型 | 説明 |
|-----------|-------------| ---- |
| `tealEvent` | `TealiumDispatch` | イベント名とイベントデータを含む Tealium ディスパッチ。 |

画面表示またはイベントをトラッキングするには、[`TealiumView`](#class-tealiumview) または [`TealiumEvent`](#class-tealiumevent) のインスタンスを `track()` メソッドに渡します。

```dart
final tealEvent = TealiumEvent(
  'cart_add', 
  {
    'customer_id': 'abc123', 
    'product_id': ["PROD123", "PROD456"], 
    'product_price': [4.00, 6.00]
  }
);
Tealium.track(tealEvent);
```

### `gatherTrackData()`

すべてのコレクターとデータレイヤーからすべてのデータを収集します。

例：

```dart
Tealium.gatherTrackData()
  .then((data) => print('Gather track data: $data'));
```

## インターフェイス：`TealiumDispatch`

トラッキングするディスパッチの種類を定義するインターフェイスです。以下のクラスが `TealiumDispatch` を実装しています。

### クラス：`TealiumEvent`

ユーザーによる画面の操作または画面表示をトラッキングするには、`TealiumEvent(eventName, dataLayer)` のインスタンスを [`track()`](#track) メソッドに渡します。`TealiumEvent` は、トラッキング呼び出しに `tealium_event` として表示されるイベント名と、オプションのデータディクショナリで構成されます。

```dart
final tealEvent = TealiumEvent(eventName, dataLayer);
Tealium.track(tealEvent);
```

| パラメータ | 型 | 説明 |
|:------------|:--------|:-----------------|
| `eventName` | `String` | `tealium_event` 属性として渡されるイベント名。 |
| `dataLayer` | `Map<String, Object>` | （オプション）イベントとともにキーと値の形式で送信するデータ。 |

例：

```dart
final tealEvent = TealiumEvent(
  'cart_add', 
  {
    'customer_id': 'abc123', 
    'product_id': ["PROD123", "PROD456"], 
    'product_price': [4.00, 6.00]
  }
);
Tealium.track(tealEvent);
```

### クラス：`TealiumView`

画面表示をトラッキングするには、`TealiumView(viewName, dataLayer)` のインスタンスを [`track()`](#track) メソッドに渡します。`TealiumView` は、トラッキング呼び出しに `tealium_event` として表示されるビュー名と、オプションのデータオブジェクトで構成されます。

```dart
final screenView = TealiumView(viewName, dataLayer);
Tealium.track(screenView);
```

| パラメータ | 型 | 説明 |
|:------------|:--------|:-----------------|
| `viewName` | `String` | `tealium_event` 属性として渡されるビュー名。 |
| `dataLayer` | `Map<String, Object>` | （オプション）イベントとともにキーと値の形式で送信するデータ。 |

例：

```dart
final screenView = TealiumView(
  'purchase', 
  {
    'customer_id': 'abc123', 
    'order_total': 10.00, 
    'product_id': ["PROD123", "PROD456"], 
    'order_id': '0123456789'
  }
);
Tealium.track(screenView);
```