---
title: Tealium
description: Tealiumクラスは、すべてのモジュールのための主要なAPIエントリーポイントとして機能します。
url: https://docs.tealium.com/ja/platforms/flutter-v2/api/tealium/
---
<blockquote>
これはFlutter用Tealiumの以前のバージョン（2.x）です。最新バージョンについては、[Flutter用Tealium](https://docs.tealium.com/ja/platforms/flutter/)をご覧ください。
</blockquote>


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
| [`initialize()`](#initialize) | 構成パラメーターでTealiumを初期化します |
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
| `id` | `String` | タグ構成からのコマンドIDの名前 | `"test_command"` |
| `callback` | `Function ` | リモートコマンドからの応答を受け取った後に実行するコールバック関数。コールバックはタグマッピングからのキー値ペアのペイロードを返します。 | (例を参照) |

例:

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

| パラメータ | タイプ | 説明 | 例 |
| --- | --- | --- | --- |
| `remoteCommand` | `RemoteCommand` | パス、URL、またはWebView構成を持つ事前に構築されたリモートコマンド。 | 下記の例を参照。 |

例:

```dart
Tealium.addRemoteCommand(RemoteCommand(TealiumFirebase.commandName, path: "firebase.json")); // local
Tealium.addRemoteCommand(RemoteCommand(TealiumFirebase.commandName, url: "www.tealium.com/path_to_remote_command/firebase.json")); // remote
Tealium.addRemoteCommand(RemoteCommand(TealiumFirebase.commandName)); // webview
```

### `addToDataLayer()`

指定された有効期限のために永続的なデータレイヤーにデータを追加します。

```dart
Tealium.addToDataLayer(data, expiry);
```

| パラメータ | タイプ | 説明 | 例 |
| --- | --- | --- | --- |
| `data` | `Map<String, Object>` | 文字列がキーであり、値が文字列または文字列の配列であるキー値ペアのJSONオブジェクト | `{'persistent_key' : 'persistent_val'}` |
| `expiry` | `Expiry` | データを永続させる時間の長さ | `Expiry.forever` |

### `clearStoredVisitorIds()`

以前に保存されたすべての訪問IDとハッシュ化された顧客識別子をクリアします。

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
| `N/A` | `Future<dynamic>` | `Tealium.dataLayer`から値が正常に取得された後にFutureが成功します |

例:

```dart
Tealium.getFromDataLayer('key')
    .then((value) => print('データレイヤーからの値: $value'));
```


### `getConsentCategories()`

ユーザーの同意したカテゴリを取得します。

```dart
Tealium.getConsentCategories();
```

| パラメータ | タイプ | 説明 |
|-----------|-------------| ---- |
| `N/A` | `Future<List<dynamic>>` | `Tealium.ConsentManager`から同意カテゴリが正常に取得された後にFutureが完了します |

例:

```dart
Tealium.getConsentCategories()
  .then((categories) =>
      print('同意カテゴリ: ' + categories.join(",")));
```


### `getConsentStatus()`

ユーザーの同意状態をコールバック関数として取得します。

```dart
Tealium.getConsentStatus();
```

| パラメータ | タイプ | 説明 |
|-----------|-------------| ---- |
| `N/A` | `Future<String>` | `Tealium.ConsentManager`から同意状態が正常に取得された後にFutureが完了します |

例:

```dart
Tealium.getConsentStatus()
  .then((status) => print('同意状態: $status'));
```

### `getVisitorId()`

ユーザーの訪問IDをコールバック関数として取得します。

```dart
Tealium.getVisitorId();
```

| パラメータ | タイプ | 説明 |
|-----------|-------------| ---- |
| `N/A` | `Future<String>` | `Tealium.visitorId`が正常に取得された後にFutureが返されます |

### `initialize()`

他のメソッドを呼び出す前にTealiumを初期化します。

```dart
Tealium.initialize(config);
```

| パラメータ | タイプ | 説明 |
|-----------|-------------| ---- |
| `config`  | `TealiumConfig` | 構成 |
| `N/A` | `Future<bool>` | Tealiumの初期化が成功した後にFutureが完了します |


例:

```dart
final config = TealiumConfig(
    'ACCOUNT',
    'PROFILE',
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
    print('Tealiumが初期化されました');
    Tealium.setConsentStatus(ConsentStatus.consented);
    Tealium.setConsentExpiryListener(() => print('同意が期限切れになりました'));
});
```


### `joinTrace()`

指定されたIDでトレースに参加します。[Trace](https://docs.tealium.com/ja/platforms/getting-started-mobile/trace/)についてもっと学びましょう。

```dart
Tealium.joinTrace(id);
```

| パラメータ | タイプ | 説明 |  例 |
|-----------|-------------| ---- | ------- |
| `id` | `String` | CDHから取得したトレースID |  `"abc123xy"` |

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
| `keys` | `List<String>` | キー名の配列 |  `["key1", "key2"]` |

### `removeRemoteCommand()`

リモートコマンドマネージャーからリモートコマンドを削除します。

```dart
Tealium.removeRemoteCommand(id);
```

| パラメータ | 型 | 説明 |  例 |
|-----------|-------------| ---- | ------- |
| `id` | `String` | 削除するコマンドIDの名前 |  `"test_command"` |

例:

```dart
Tealium.removeRemoteCommand('test_command');
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
| `categories` | `List<ConsentCategories>` | ユーザーの同意カテゴリの配列 | `[ConsentCategories.email, ConsentCategories.personalization]` |

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

ユーザーの同意構成が期限切れになった後に実行するコールバックを構成します。

```dart
Tealium.setConsentExpiryListener(callback);
```

| パラメータ | 型 | 説明 |
|-----------|-------------| ---- |
| `callback`  | `Function` | 同意が期限切れになった後に実行するコード |

```dart
Tealium.setConsentExpiryListener(() {
    print('Consent Expired');
});
```

### `setConsentStatus()`

ユーザーの同意ステータスを構成します。デフォルトは`ConsentStatus.unknown`で、ステータスが更新されるまでです。

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