---
title: Tealium
description: Tealiumクラスは、すべてのモジュールのための主要なAPIエントリーポイントとして機能します。
url: https://docs.tealium.com/ja/platforms/flutter-v2/api/tealium/
---これはFlutter用Tealiumの以前のバージョン（2.x）です。最新バージョンについては、[Flutter用Tealium](/ja/platforms/flutter/)をご覧ください。

## クラス: `Tealium`

以下は、Flutterの`Tealium`クラスで一般的に使用されるメソッドをまとめたものです。

| メソッド | 説明 |
| ----- | ------ |
| [`addCustomRemoteCommand()`](#addcustomremotecommand)| リモートコマンドマネージャーにリモートコマンドのコールバックを追加します。 |
| [`addRemoteCommand()`](#addremotecommand)| リモートコマンドマネージャーにリモートコマンドを追加します |
| [`addToDataLayer()`](#addtodatalayer) | 永続的なデータレイヤーにデータを追加します |
| [`clearStoredVisitorIds()`](#clearstoredvisitorids)       | 訪問IDの保存されたキャッシュを削除し、`resetVisitorId`を呼び出します。 |
| [`gatherTrackData()`](#gathertrackdata) | すべてのコレクターとデータレイヤーからデータを収集します |
| [`getFromDataLayer()`](#getfromdatalayer) | 永続的なデータレイヤーで指定されたキーの値を取得します |
| [`getConsentCategories()`](#getconsentcategories) | ユーザーの同意したカテゴリを取得します |
| [`getConsentStatus()`](#getconsentstatus) | ユーザーの同意状態を取得します |
| [`getVisitorId()`](#getvisitorid) | ユーザーの訪問IDを取得します |
| [`initialize()`](#initialize) | Tealiumを構成パラメータで初期化します |
| [`joinTrace()`](#jointrace) | 指定されたIDでトレースに参加します |
| [`leaveTrace()`](#leavetrace) | 以前に参加したトレースを離れ、訪問セッションを終了します |
| [`removeFromDataLayer()`](#removefromdatalayer) | 以前に`addToDataLayer()`を使用して構成された永続的なデータキー値ペアのリストを削除します |
| [`removeRemoteCommand()`](#removeremotecommand) | リモートコマンドマネージャーからリモートコマンドを削除します |
| [`resetVisitorId()`](#resetvisitorid) | ユーザーの新しい訪問IDを生成します。 |
| [`setConsentCategories()`](#setconsentcategories) | ユーザーの同意カテゴリを構成します |
| [`setConsentExpiryListener()`](#setconsentexpirylistener) | 同意期限が切れたときのリスナー/コールバックを構成します |
| [`setConsentStatus()`](#setconsentstatus) | ユーザーの同意状態を構成します |
| [`setVisitorIdListener()`](#setvisitoridlistener) | `visitorId`の変更に関するリスナーを追加します。 |
| [`setVisitorServiceListener()`](#setvisitorservicelistener) | 訪問サービスのリスナー/コールバックを構成します |
| [`terminateInstance()`](#terminateinstance) | Tealiumライブラリを無効にし、すべてのモジュール参照を削除することでTealiumインスタンスを終了します |
| [`track()`](#track) | イベントまたは画面表示をトラックします |

### `addCustomRemoteCommand()`

Tealium iQタグ管理のタグに基づいてリモートコマンドマネージャーにカスタムリモートコマンドを追加します。

```dart
Tealium.addCustomRemoteCommand(id, callback);
```

| パラメータ | タイプ | 説明 | 例 |
| --- | --- | --- | --- |
| `id` | `String` | タグ構成からのコマンドIDの名前 | `&#34;test_command&#34;` |
| `callback` | `Function ` | リモートコマンドからの応答を受け取った後に実行するコールバック関数。コールバックはタグマッピングからのキー値ペアのペイロードを返します。 | (例を参照) |

例:

```dart
Tealium.addCustomRemoteCommand(&#39;CUSTOM_COMMAND_ID&#39;, (payload) {
  print(JsonEncoder().convert(payload));
});
```

### `addRemoteCommand()`

リモートコマンドマネージャーにリモートコマンドを追加します。

```dart
Tealium.addRemoteCommand(remoteCommand);
```

| パラメータ | タイプ | 説明 | 例 |
| --- | --- | --- | --- |
| `remoteCommand` | `RemoteCommand` | パス、URL、またはウェブビュー構成を持つ事前に構築されたリモートコマンド。 | 下記の例を参照。 |

例:

```dart
Tealium.addRemoteCommand(RemoteCommand(TealiumFirebase.commandName, path: &#34;firebase.json&#34;)); // local
Tealium.addRemoteCommand(RemoteCommand(TealiumFirebase.commandName, url: &#34;www.tealium.com/path_to_remote_command/firebase.json&#34;)); // remote
Tealium.addRemoteCommand(RemoteCommand(TealiumFirebase.commandName)); // webview
```

### `addToDataLayer()`

指定された有効期限で永続的なデータレイヤーにデータを追加します。

```dart
Tealium.addToDataLayer(data, expiry);
```

| パラメータ | タイプ | 説明 | 例 |
| --- | --- | --- | --- |
| `data` | `Map&lt;String, Object&gt;` | 文字列のキーと文字列または文字列の配列の値を持つJSONオブジェクト | `{&#39;persistent_key&#39; : &#39;persistent_val&#39;}` |
| `expiry` | `Expiry` | データを永続させる期間 | `Expiry.forever` |

### `clearStoredVisitorIds()`

以前に保存された訪問IDとハッシュ化された顧客識別子をすべてクリアします。

```dart
Tealium.clearStoredVisitorIds();
```

### `getFromDataLayer()`

永続的なデータレイヤーで指定されたキーの値をコールバック関数として取得します。

```dart
Tealium.getFromDataLayer(key);
```

| パラメータ | タイプ | 説明 |
|-----------|-------------| ---- |
| `key` | `String` | データレイヤーから取得するキー|
| `N/A` | `Future&lt;dynamic&gt;` | `Tealium.dataLayer`から値が正常に取得された後にFutureが成功します |

例:

```dart
Tealium.getFromDataLayer(&#39;key&#39;)
    .then((value) =&gt; print(&#39;Value From data layer: $value&#39;));
```


### `getConsentCategories()`

ユーザーの同意したカテゴリを取得します。

```dart
Tealium.getConsentCategories();
```

| パラメータ | タイプ | 説明 |
|-----------|-------------| ---- |
| `N/A` | `Future&lt;List&lt;dynamic&gt;&gt;` | `Tealium.ConsentManager`から同意カテゴリが正常に取得された後にFutureが完了します |

例:

```dart
Tealium.getConsentCategories()
  .then((categories) =&gt;
      print(&#39;Consent Categories: &#39; &#43; categories.join(&#34;,&#34;)));
```


### `getConsentStatus()`

ユーザーの同意状態をコールバック関数として取得します。

```dart
Tealium.getConsentStatus();
```

| パラメータ | タイプ | 説明 |
|-----------|-------------| ---- |
| `N/A` | `Future&lt;String&gt;` | `Tealium.ConsentManager`から同意状態が正常に取得された後にFutureが完了します |

例:

```dart
Tealium.getConsentStatus()
  .then((status) =&gt; print(&#39;Consent Status: $status&#39;));
```

### `getVisitorId()`

ユーザーの訪問IDをコールバック関数として取得します。

```dart
Tealium.getVisitorId();
```

| パラメータ | タイプ | 説明 |
|-----------|-------------| ---- |
| `N/A` | `Future&lt;String&gt;` | `Tealium.visitorId`が正常に取得された後にFutureが返されます |

### `initialize()`

他のメソッドを呼び出す前にTealiumを初期化します。

```dart
Tealium.initialize(config);
```

| パラメータ | タイプ | 説明 |
|-----------|-------------| ---- |
| `config`  | `TealiumConfig` | 構成 |
| `N/A` | `Future&lt;bool&gt;` | Tealiumの初期化が成功した後にFutureが完了します |


例:

```dart
final config = TealiumConfig(
    &#39;ACCOUNT&#39;,
    &#39;PROFILE&#39;,
    TealiumEnvironment.dev,
    [
        Collectors.AppData,
        Collectors.DeviceData,
        Collectors.Lifecycle,
        Collectors.Connectivity,
    ],
    [
        Dispatchers.Collect,
        Dispatchers.TagManagement,
        Dispatchers.RemoteCommands,
    ],
    loglevel: LogLevel.DEV,
    consentLoggingEnabled: true,
    consentPolicy: ConsentPolicy.GDPR,
    visitorServiceEnabled: true);

Tealium.initialize(config).then((_) {
    print(&#39;Tealium Initialized&#39;);
    Tealium.setConsentStatus(ConsentStatus.consented);
    Tealium.setConsentExpiryListener(() =&gt; print(&#39;Consent Expired&#39;));
});
```


### `joinTrace()`

指定されたIDでトレースに参加します。[Trace](/ja/platforms/getting-started-mobile/trace/)についてもっと学びましょう。

```dart
Tealium.joinTrace(id);
```

| パラメータ | タイプ | 説明 |  例 |
|-----------|-------------| ---- | ------- |
| `id` | `String` | CDHから取得したトレースID |  `&#34;abc123xy&#34;` |

### `leaveTrace()`

以前に参加したトレースを離れ、訪問セッションを終了します。このメソッドが呼ばれるまでアプリセッションの間トレースはアクティブのままです。

```dart
Tealium.leaveTrace();
```
### `removeFromDataLayer()`

`addToDataLayer()`を使用して以前に構成された永続的なデータを削除します。

```dart
Tealium.removeFromDataLayer(keys);
```

| パラメータ | 型 | 説明 |  例 |
|-----------|-------------| ---- | ------- |
| `keys` | `List&lt;String&gt;` | キー名の配列 |  `[&#34;key1&#34;, &#34;key2&#34;]` |

### `removeRemoteCommand()`

リモートコマンドマネージャーからリモートコマンドを削除します。

```dart
Tealium.removeRemoteCommand(id);
```

| パラメータ | 型 | 説明 |  例 |
|-----------|-------------| ---- | ------- |
| `id` | `String` | 削除するコマンドIDの名前 |  `&#34;test_command&#34;` |

例:

```dart
Tealium.removeRemoteCommand(&#39;test_command&#39;);
```

### `resetVisitorId()`

ユーザーの新しい訪問IDを生成します。

```dart
Tealium.resetVisitorId();
```

### `setConsentCategories()`

ユーザーの同意カテゴリを構成します。文字列の配列を渡してカテゴリを構成します。デフォルトは、`ConsentStatus`が`ConsentStatus.consented`に構成されるまで空の配列です。同意ステータスが`ConsentStatus.consented`で`setConsentCategories()`メソッドでカテゴリが指定されていない場合、すべてのカテゴリが構成されます。

```dart
Tealium.setConsentCategories(categories);
```

| パラメータ | 型 | 説明 | 例 |
|-----------|-------------| ---- | ------- |
| `categories` | `List&lt;ConsentCategories&gt;` | ユーザーの同意カテゴリの配列 | `[ConsentCategories.email, ConsentCategories.personalization]` |

例:

```dart
Tealium.setConsentCategories([ConsentCategories.analytics, ConsentCategories.email]);
```

#### 同意カテゴリ

以下の同意カテゴリが利用可能です:

| 値 | 説明 |
| ----- | ----------- |
| `analytics` |  アナリティクス |
| `affiliates` |  アフィリエイト |
| `displayAds` | ディスプレイ広告  |
| `email` | メール |
| `personalization` | パーソナライゼーション |
| `search` | 検索 |
| `social`  |  ソーシャル |
| `bigData` | ビッグデータ |
| `mobile` | モバイル  |
| `engagement` | エンゲージメント |
| `monitoring` | モニタリング |
| `crm` | CRM |
| `cdp` | CDP |
| `cookieMatch` | クッキーマッチ |
| `misc` | その他 |

### `setConsentExpiryListener()`

ユーザーの同意構成が`ConsentExpiry`に従って期限切れになった後に実行するコールバックを構成します。

```dart
Tealium.setConsentExpiryListener(callback);
```

| パラメータ | 型 | 説明 |
|-----------|-------------| ---- |
| `callback`  | `Function` | 同意が期限切れになった後に実行するコード |

```dart
Tealium.setConsentExpiryListener(() {
    print(&#39;Consent Expired&#39;);
});
```

### `setConsentStatus()`

ユーザーの同意ステータスを構成します。デフォルトはステータスが更新されるまで`ConsentStatus.unknown`です。

```dart
Tealium.setConsentStatus(status);
```

| パラメータ | 型 | 説明 |
|-----------|-------------| ---- |
| `status`  | `ConsentStatus` | 同意ステータス |

例:

```dart
Tealium.setConsentStatus(ConsentStatus.consented);
```

#### 同意ステータス

以下の同意ステータスが利用可能です:

| 値 | 説明 |
| ----- | ----------- |
| `ConsentStatus.consented` |  同意済み |
| `ConsentStatus.notConsented` |  同意していない |
| `ConsentStatus.unknown` |  不明 |

### `setVisitorIdListener()`

訪問IDが変更されたときに実行するコールバックを構成します。

```dart
Tealium.setVisitorIdListener(callback);
```

| パラメータ | 型 | 説明 |
|-----------|-------------| ---- |
| `callback`  | `Function` | 更新された`visitorId`で実行するコード |

例:

```dart
Tealium.setVisitorIdListener((newVisitorId) {
    print(newVisitorId);
});
```


### `setVisitorServiceListener()`

訪問プロファイルが更新されたときに実行するコールバックを構成します。更新された`VisitorProfile`はコールバックのレスポンスで提供されます。

訪問サービスモジュールはTealium Customer Data Hubの[Data Layer Enrichment]()機能を実装しています。

このモジュールの使用は、Tealium AudienceStreamのライセンスを持っており、訪問プロファイルを使用してモバイルアプリケーションのユーザーエクスペリエンスを向上させたい場合に推奨されます。AudienceStreamのライセンスを持っていない場合、訪問プロファイルが返されないため、このモジュールの使用は推奨されません。

```dart
Tealium.setVisitorServiceListener(callback);
```

| パラメータ | 型 | 説明 |
|-----------|-------------| ---- |
| `callback`  | `Function` | 更新された訪問プロファイルが返された後に実行するコード |

例:

```dart
Tealium.setVisitorServiceListener((profile) {
    print(JsonEncoder().convert(profile));
});
```

### `terminateInstance()`

Tealiumライブラリを無効にし、すべてのモジュール参照を削除することでTealiumインスタンスを終了します。必要に応じて新しいTealiumインスタンスを作成することで再度有効にします。

```dart
Tealium.terminateInstance();
```

### `track()`

オプションのイベントデータを持つ画面表示またはイベントを追跡します。

```dart
Tealium.track(tealEvent);
```

| パラメータ | 型 | 説明 |
|-----------|-------------| ---- |
| `tealEvent` | `TealiumDispatch` | イベント名とイベントデータを持つTealiumディスパッチ。 |

画面表示またはイベントを追跡するには、[`TealiumView`](#class-tealiumview)または[`TealiumEvent`](#class-tealiumevent)のインスタンスを`track()`メソッドに渡します：

```dart
final tealEvent = TealiumEvent(
  &#39;cart_add&#39;,
  {
    &#39;customer_id&#39;: &#39;abc123&#39;,
    &#39;product_id&#39;: [&#34;PROD123&#34;, &#34;PROD456&#34;],
    &#39;product_price&#39;: [4.00, 6.00]
  }
);
Tealium.track(tealEvent);
```

### `gatherTrackData()`

すべてのコレクターとデータレイヤーからすべてのデータを収集します。

例:

```dart
Tealium.gatherTrackData()
  .then((data) =&gt; print(&#39;Gather track data: $data&#39;));
```

## インターフェース: `TealiumDispatch`

追跡するディスパッチのタイプを定義するインターフェースです。以下のクラスが`TealiumDispatch`を実装しています：

### クラス: `TealiumEvent`

ユーザーの画面とのやり取りまたは画面表示を追跡するには、`TealiumEvent(eventName, dataLayer)`のインスタンスを[`track()`](#track)メソッドに渡します。`TealiumEvent`は、追跡コールに`tealium_event`として表示されるイベント名と、オプションのデータ辞書を含みます。

```dart
final tealEvent = TealiumEvent(eventName, dataLayer);
Tealium.track(tealEvent);
```

| パラメータ  | 型    | 説明      |
|:------------|:--------|:-----------------|
| `eventName` | `String` | `tealium_event`属性として渡されるイベント名。  |
| `dataLayer` | `Map&lt;String, Object&gt;` | (オプション) イベントに送信されるキーと値の形式のデータ。 |

例:

```dart
final tealEvent = TealiumEvent(
  &#39;cart_add&#39;,
  {
    &#39;customer_id&#39;: &#39;abc123&#39;,
    &#39;product_id&#39;: [&#34;PROD123&#34;, &#34;PROD456&#34;],
    &#39;product_price&#39;: [4.00, 6.00]
  }
);
Tealium.track(tealEvent);
```

### クラス: `TealiumView`

画面表示を追跡するには、`TealiumView(viewName, dataLayer)`のインスタンスを[`track()`](#track)メソッドに渡します。`TealiumView`は、追跡コールに`tealium_event`として表示されるビュー名と、オプションのデータオブジェクトを含みます。

```dart
final screenView = TealiumView(viewName, dataLayer);
Tealium.track(screenView);
```

| パラメータ  | 型    | 説明      |
|:------------|:--------|:-----------------|
| `viewName`  | `String`| `tealium_event`属性として渡されるビュー名。|
| `dataLayer` | `Map&lt;String, Object&gt;` | (オプション) イベントに送信されるキーと値の形式のデータ。 |

例:

```dart
final screenView = TealiumView(
  &#39;purchase&#39;,
  {
    &#39;customer_id&#39;: &#39;abc123&#39;,
    &#39;order_total&#39;: 10.00,
    &#39;product_id&#39;: [&#34;PROD123&#34;, &#34;PROD456&#34;],
    &#39;order_id&#39;: &#39;0123456789&#39;
  }
);
Tealium.track(screenView);
```