---
title: API リファレンス
description: TealiumのFlutter用クラスとメソッドのリファレンスガイドです。
url: https://docs.tealium.com/ja/platforms/flutter-v1/api/
---
<blockquote>
これはTealiumのFlutter用の以前のバージョン（1.x）です。最新バージョンについては、[Tealium for Flutter](https://docs.tealium.com/ja/platforms/flutter/)をご覧ください。
</blockquote>


## クラス: `Tealium`

以下は、Flutterの`Tealium`クラスでよく使用されるメソッドをまとめたものです。

| メソッド | 説明 |
| ----- | ------ |
| `addRemoteCommand()`| リモートコマンドマネージャーにリモートコマンドを追加します |
| `addRemoteCommandForInstance()`| 特定のTealiumインスタンスのために、リモートコマンドマネージャーにリモートコマンドを追加します |
| `getPersistentData()` | 永続データを取得します |
| `getPersistentDataForInstance()` | 特定のTealiumインスタンスの永続データを取得します|
| `getVolatileData()` | 揮発性データを取得します |
| `getVolatileDataForInstance()` | 特定のTealiumインスタンスの揮発性データを取得します |
| `initialize()` | Tealiumインスタンスを初期化します |
| `initializeCustom()` | カスタムオプションでTealiumインスタンスを初期化します |
| `initializeWithConsentManager()` | Tealiumインスタンスを初期化し、同意管理を有効にします |
| `removePersistentData()` | 永続データを削除します |
| `removePersistentDataForInstance()` | 特定のTealiumインスタンスの永続データを削除します  |
| `removeRemoteCommand()` | リモートコマンドマネージャーからリモートコマンドを削除します |
| `removeRemoteCommandForInstance()` | 特定のTealiumインスタンスのリモートコマンドマネージャーからリモートコマンドを削除します |
| `removeVolatileData()` | 揮発性データを削除します |
| `removeVolatileDataForInstance()` | 特定のTealiumインスタンスの揮発性データを削除します  |
| `setPersistentData()` | 永続データを構成します |
| `setPersistentDataForInstance()` | 特定のTealiumインスタンスの永続データを構成します  |
| `setVolatileData()` | 揮発性データを構成します |
| `setVolatileDataForInstance()` | 特定のTealiumインスタンスの揮発性データを構成します  |
| `trackEvent()` | 非ビューイベントを追跡します |
| `trackEventForInstance()` | 特定のTealiumインスタンスの非ビューイベントを追跡します |
| `trackView()` | 画面ビューを追跡します |
| `trackViewForInstance()` | 特定のTealiumインスタンスの画面ビューを追跡します  |

### `addRemoteCommand()`

リモートコマンドマネージャーにリモートコマンドを追加します。

```dart
Tealium.addRemoteCommand(commandID, description, callback);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `commandID` | `String` | タグ構成からのコマンドIDの名前 | `"test_command"` |
| `description` | `String ` | リモートコマンドの説明 | `"Firebase remote command"` |
| `callback` | `Function ` | リモートコマンドからの応答を受け取った後に実行するコールバック関数。コールバックはタグマッピングからのキー値ペアのペイロードを返します。 | (例を参照) |

例:

```dart
Tealium.addRemoteCommand("firebase", "Firebase Remote Command", (payload) {

  final eventName = payload["firebase_event_name"];
  final eventProperties = payload["firebase_event_properties"];

  analytics.logEvent(name: eventName, parameters: eventProperties);
});
```

### `addRemoteCommandForInstance()`

特定のTealiumインスタンスのために、リモートコマンドマネージャーにリモートコマンドを追加します。

```dart
Tealium.addRemoteCommandForInstance(instanceName, commandID, description, callback);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `instanceName` | `String` | Tealiumインスタンスの名前 | `"instance-2"` |
| `commandID` | `String` | タグ構成からのコマンドIDの名前 | `"test_command"` |
| `description` | `String ` | リモートコマンドの説明 | `"Firebase remote command"` |
| `callback` | `Function ` | リモートコマンドからの応答を受け取った後に実行するコールバック関数。コールバックはタグマッピングからのキー値ペアのペイロードを返します。 | (例を参照) |

例:

```dart
Tealium.addRemoteCommandForInstance("instance-2", "verify_email", "Verify User Email", (user) {

	print('Howdy, ${user.name}!');
	print('We sent the verification link to ${user.email}.');

	// Send data to email service to send email to user
	// ...
});
```

### `getPersistentData()`

永続データを取得します。

```dart
Tealium.getPersistentData(key)
```

| パラメータ | 型 | 説明 | 例 |
|-----------|-------------| ---- | ------- |
| `key` | `String` | キー名 | `"key1"` |

### `getPersistentDataForInstance()`

特定のTealiumインスタンスの永続データを取得します。

```dart
Tealium.getPersistentDataForInstance(instance, key)
```

| パラメータ | 型 | 説明 | 例 |
|-----------|-------------| ---- | ------- |
| `instance`  | `String` | 特定のTealiumインスタンス名 | `"instance123"` |
| `key` | `String` | キー名 | `"key1"` |

### `getVolatileData()`

揮発性データを取得します。

```dart
Tealium.getVolatileData(key)
```

| パラメータ | 型 | 説明 | 例 |
|-----------|-------------| ---- | ------- |
| `key` | `String` | キー名 | `"key1"` |

### `getVolatileDataForInstance()`

特定のTealiumインスタンスの揮発性データを取得します。

```dart
Tealium.getVolatileDataForInstance(instance, key)
```

| パラメータ | 型 | 説明 | 例 |
|-----------|-------------| ---- | ------- |
| `instance`  | `String` | 特定のTealiumインスタンス名 | `"instance123"` |
| `key` | `String` | キー名 | `"key1"` |

### `initialize()`

Tealiumインスタンスを初期化します。

```dart
Tealium.initialize(account, profile, environment,
               iosDataSource, androidDataSource,
               instance, isLifecycleEnabled)
```

| パラメータ | 型 | 説明 |  例 |
|-----------|-------------| ---- | ------- |
| `account` | `String` | Tealiumアカウント名 |  `"companyXYZ"` |
| `profile` | `String` | Tealiumプロファイル名 |  `"main"` |
| `environment` | `String` | Tealium環境名 |  [`"dev"`, `"qa"`, `"prod"`] |
| `iosDataSource` | `String` | (オプション) データソースキー  (ない場合は`null`を構成) |  `"abc123"` |
| `androidDataSource` | `String` | (オプション) Androidデータソースキー (ない場合は`null`を構成) |  `null` |
| `instance` | `String` | (オプション) Tealiumインスタンス名 (デフォルト: `"main"`) |  `"main"` |
| `isLifecycleEnabled` | `bool` | (オプション) ライフサイクル追跡イベントを有効にする (デフォルト: `true`)|  [`true`, `false`] |
### `initializeCustom()`

Tealiumインスタンスをすべてのオプションで初期化します。

```dart
Tealium.initializeCustom(account, profile, environment,
               iosDataSource, androidDataSource,
               instance, isLifecycleEnabled,
               overridePublishSettingsUrl,
               overrideTagManagementUrl,
               enableVdataCollectEndpointUrl,
               enableConsentManager)
```

このメソッド呼び出しには以下の追加パラメータが含まれます：

| パラメータ | 型 | 説明 |  例 |
|-----------|-------------| ---- | ------- |
| `account` | `String` | Tealiumのアカウント名 |  `"companyXYZ"` |
| `profile` | `String` | Tealiumのプロファイル名 |  `"main"` |
| `environment` | `String` | Tealiumの環境名 |  [`"dev"`, `"qa"`, `"prod"`] |
| `iosDataSource` | `String` | (オプション) データソースキー (ない場合は `null`) |  `"abc123"` |
| `androidDataSource` | `String` | (オプション) Androidのデータソースキー (ない場合は `null`) |  `null` |
| `instance` | `String` | (オプション) Tealiumインスタンス名 (デフォルト: `"main"`) |  `"main"` |
| `isLifecycleEnabled` | `bool` | (オプション) ライフサイクル追跡イベントを有効にする (デフォルト: `true`)|  [`true`, `false`] |
| `overridePublishSettingsUrl` | `String` | (オプション) カスタム公開構成URLをオーバーライドする場合の文字列 (ない場合は `null`)| |
| `overrideTagManagementUrl` | `String` | (オプション) カスタムタグ管理URLをオーバーライドする場合の文字列 (ない場合は `null`)| |
| `enableVdataCollectEndpointUrl`| `String` | データエンドポイント間で切り替え (`true` はデフォルトで、ネイティブのAndroidおよびiOSライブラリがデータをCollectエンドポイントURLに送信します。`false` は古い `vdata` エンドポイントにデータを送信します (ない場合は `null`)) | |
| `enableConsentManager` | `bool` | 同意管理を有効にする (有効: `true`, 無効: `false`) | [`true`, `false`]  |

### `initializeWithConsentManager()`

Tealiumインスタンスを初期化し、同意管理を有効にします。

```dart
Tealium.initializeWithConsentManager(account, profile, environment,
               iosDataSource, androidDataSource,
               instance, isLifecycleEnabled)
```

| パラメータ | 型 | 説明 |  例 |
|-----------|-------------| ---- | ------- |
| `account` | `String` | Tealiumのアカウント名 |  `"companyXYZ"` |
| `profile` | `String` | Tealiumのプロファイル名 |  `"main"` |
| `environment` | `String` | Tealiumの環境名 |  [`"dev"`, `"qa"`, `"prod"`] |
| `iosDataSource` | `String` | (オプション) データソースキー (ない場合は `null`) |  `"abc123"` |
| `androidDataSource` | `String` | (オプション) Androidのデータソースキー (ない場合は `null`) |  `null` |
| `instance` | `String` | (オプション) Tealiumインスタンス名 (デフォルト: `"main"`) |  `"main"` |
| `isLifecycleEnabled` | `bool` | (オプション) ライフサイクル追跡イベントを有効にする (デフォルト: `true`)|  [`true`, `false`] |

### `removePersistentData()`

永続データを削除します。

```dart
Tealium.removePersistentData(keys)
```

| パラメータ | 型 | 説明 | 例 |
|-----------|-------------| ---- | ------- |
| `keys` | `List<String>` | 文字列キー名のリスト | `["persistent_var", "persistent_var2"]` |

### `removePersistentDataForInstance()`

特定のTealiumインスタンスの永続データを削除します。

```dart
Tealium.removePersistentDataForInstance(instance, keys)
```

| パラメータ | 型 | 説明 | 例 |
|-----------|-------------| ---- | ------- |
| `instance`  | `String` | 特定のTealiumインスタンス名 | `"instance123"` |
| `keys` | `List<String>` | 文字列キー名のリスト | `["persistent_var", "persistent_var2"]` |

### `removeRemoteCommand()`

リモートコマンドマネージャーからリモートコマンドを削除します。

```dart
Tealium.removeRemoteCommand(commandID);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `commandID ` | `String` | 削除するコマンドIDの名前  | `"test_command"` |

例：

```dart
Tealium.removeRemoteCommand("firebase");
```


### `removeRemoteCommandForInstance()`

特定のTealiumインスタンスのリモートコマンドマネージャーからリモートコマンドを削除します。

```dart
Tealium.removeRemoteCommandForInstance(instanceName, commandID);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `instanceName` | `String` | Tealiumインスタンスの名前 | `"instance-2"` |
| `commandID ` | `String` | 削除するコマンドIDの名前  | `"test_command"` |

```dart
Tealium.removeRemoteCommandForInstance("instance-2", "firebase");
```

### `removeVolatileData()`

揮発性データを削除します。

```dart
Tealium.removeVolatileData(keys)
```

| パラメータ | 型 | 説明 | 例 |
|-----------|-------------| ---- | ------- |
| `keys` | `List<String>` | 文字列キー名のリスト | `["volatile_var1", "volatile_var2"]` |

### `removeVolatileDataForInstance()`

特定のTealiumインスタンスの揮発性データを削除します。

```dart
Tealium.removeVolatileDataForInstance(instance, keys)
```

| パラメータ | 型 | 説明 | 例 |
|-----------|-------------| ---- | ------- |
| `instance`  | `String` | 特定のTealiumインスタンス名 | `"instance123"` |
| `keys` | `List<String>` | 文字列キー名のリスト | `["volatile_var1", "volatile_var2"]` |

### `setPersistentData()`

永続データを構成します。

```dart
Tealium.setPersistentData(data)
```

| パラメータ | 型 | 説明 | 例 |
|-----------|-------------| ---- | ------- |
| `data` | `Map<String, dynamic>` | キーと値のペアとしての永続データ | `{"key1": "value1"}` |

### `setPersistentDataForInstance()`

特定のTealiumインスタンスの永続データを構成します。

```dart
Tealium.setPersistentDataForInstance(instance, data)
```

| パラメータ | 型 | 説明 | 例 |
|-----------|-------------| ---- | ------- |
| `instance`  | `String` | 特定のTealiumインスタンス名 | `"instance123"` |
| `data` | `Map<String, dynamic>` | キーと値のペアとしての永続データ | `{"key1": "value1"}` |

### `setVolatileData()`

揮発性データを構成します。

```dart
Tealium.setVolatileData(data)
```

| パラメータ | 型 | 説明 | 例 |
|-----------|-------------| ---- | ------- |
| `data` | `Map<String, dynamic>` | キーと値のペアとしての揮発性データ | `{"key1": "value1"}` |

### `setVolatileDataForInstance()`

特定のTealiumインスタンスの揮発性データを構成します。

```dart
Tealium.setVolatileDataForInstance(instance, data)
```

| パラメータ | 型 | 説明 | 例 |
|-----------|-------------| ---- | ------- |
| `instance`  | `String` | 特定のTealiumインスタンス名 | `"instance123"` |
| `data` | `Map<String, dynamic>` | キーと値のペアとしての揮癲性データ | `{"key1": "value1"}` |

### `trackEvent()`

ビュー以外のイベントを追跡します。

```dart
Tealium.trackEvent(eventName, data)
```

| パラメータ | 型 | 説明 | 例 |
|-----------|-------------| ---- | ------- |
| `eventName` | `String` | イベントを識別する名前 |  `"Event button click"` |
| `data` | `Map<String, dynamic>` | (オプション) キーと値のペアとしてのイベントデータ |  `{"key1": "value1"}` |

### `trackEventForInstance()`

特定のTealiumインスタンスのビュー以外のイベントを追跡します。

```dart
Tealium.trackEventForInstance(instance, eventName, data)
```
| パラメータ | 型 | 説明 | 例 |
|-----------|-------------| ---- | ------- |
| `instance` | `String` | Tealiumインスタンス名 | `"instance123"` |
| `eventName` | `String` | イベントを識別する名前 | `"Event button click"` |
| `data` | `Map<String, dynamic>` | (オプション) キーと値のペアとしてのイベントデータ |  `{"key1": "value1"}` |

### `trackView()`

画面ビューを追跡します。

```dart
Tealium.trackView(viewName, data)
```

| パラメータ | 型 | 説明 |  例 |
|-----------|-------------| ---- | ------- |
| `viewName` | `String` | 画面ビューを識別する名前 | `"View screen"` |
| `data` | `Map<String, dynamic>` | (オプション) キーと値のペアとしてのイベントデータ|  `{"key1": "value1"}` |
### `trackViewForInstance()`

特定のTealiumインスタンスのための画面ビューを追跡します。

```dart
Tealium.trackViewForInstance(instance, viewName, data)
```
| パラメータ | 型 | 説明 | 例 |
|-----------|-------------| ---- | ------- |
| `instance` | `String` | Tealiumインスタンス名 | `"instance123"` |
| `viewName` | `String` | ビューを識別する名前 | `"View screen"` |
| `data` | `Map<String, dynamic>` | (オプション) キーと値のペアとしてのイベントデータ |  `{"key1": "value1"}` |