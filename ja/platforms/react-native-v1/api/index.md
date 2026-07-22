---
title: API リファレンス
description: TealiumのReact Native用クラスとメソッドのリファレンスガイドです。
url: https://docs.tealium.com/ja/platforms/react-native-v1/api/
---

<blockquote>
これはTealiumのReact Native用の以前のバージョン（1.x）です。  
現在のバージョンについては、[Tealium for React Native 2.x](https://docs.tealium.com/ja/platforms/react-native/)をご覧ください。
</blockquote>


## クラス: `Tealium`

以下は、React Nativeライブラリ用の`Tealium`クラスで一般的に使用されるメソッドをまとめたものです。

| メソッド | 説明 |
| ----- | ------ |
| `addRemoteCommand()`| リモートコマンドマネージャーにリモートコマンドを追加します |
| `addRemoteCommandForInstance()`| 特定のTealiumインスタンス用にリモートコマンドマネージャーにリモートコマンドを追加します |
| `getPersistentData()`| 特定のキーの値を取得します |
| `getPersistentDataForInstanceName()`| 特定のTealiumインスタンスとキーの永続データ値を取得します |
| `getUserConsentCategories()` | ユーザーの同意カテゴリを取得します |
| `getUserConsentCatgoriesForInstanceName()`| 特定のTealiumインスタンスのユーザーの同意カテゴリを取得します |
| `getUserConsentStatus()`| ユーザーの同意状態を取得します |
| `getUserConsentStatusForInstanceName()`| 特定のTealiumインスタンスのユーザーの同意状態を取得します |
| `getVisitorID()`| ユーザーの訪問IDを取得します |
| `getVisitorIDForInstanceName()`| 特定のTealiumインスタンスのユーザーの訪問IDを取得します |
| `getVolatileData()`| 渡されたキーの値を取得します |
| `getVolatileDataForInstanceName()`| 特定のTealiumインスタンスとキーの揮発性データ値を取得します |
| `initialize()` |他のメソッドを呼び出す前にTealiumを初期化します |
| `initializeCustom()`|すべてのオプションでTealiumを初期化してから他のメソッドを呼び出します |
| `initializeWithConsentManager()`| 同意管理を含むTealiumを初期化します |
| `isConsentLoggingEnabled()`| ユーザーの同意ログが有効かどうかを確認します |
| `isConsentLoggingEnabledForInstanceName()`| 特定のTealiumインスタンスの同意ログが有効かどうかを確認します |
| `removePersistentData()`| `setPersistentData()`を使用して以前に構成された永続データを削除します |
| `removePersistentDataForInstanceName()`| `setPersistentData()`を使用して以前に構成された永続データを特定のTealiumインスタンス用に削除します |
| `removeRemoteCommand()` | リモートコマンドマネージャーからリモートコマンドを削除します |
| `removeRemoteCommandForInstanceName()` | 特定のTealiumインスタンス用にリモートコマンドマネージャーからリモートコマンドを削除します |
| `removeVolatileData()`| `setVolatileData()`を使用して以前に構成された揮発性データを削除します |
| `removeVolatileDataForInstanceName()`| `setVolatileData()`を使用して以前に構成された揮発性データを特定のTealiumインスタンス用に削除します |
| `resetUserConsentPreferences()`| ユーザーの同意状態とカテゴリをリセットします |
| `resetUserConsentPreferencesForInstanceName()`| 特定のTealiumインスタンスのユーザーの同意状態とカテゴリをリセットします |
| `setConsentLoggingEnabled()`| ユーザーの同意ログを構成します |
| `setConsentLoggingEnabledForInstanceName()`| 特定のTealiumインスタンスのユーザーの同意ログを構成します |
| `setPersistentData()`| 次回以降のイベントやビューに送信される永続データを構成します |
| `setPersistentDataForInstanceName()`| 特定のTealiumインスタンス用に次回以降のイベントやビューに送信される永続データを構成します |
| `setUserConsentCategories()`| ユーザーの同意カテゴリを構成します |
| `setUserConsentCategoriesForInstanceName()`| 特定のTealiumインスタンスのユーザーの同意カテゴリを構成します |
| `setUserConsentStatus()`| ユーザーの同意状態を構成します |
| `setUserConsentStatusForInstanceName()`| 特定のTealiumインスタンスのユーザーの同意状態を構成します |
| `setVolatileData()`| 次回以降のイベントやビューに送信される揮発性データを構成します |
| `setVolatileDataForInstanceName()`| 特定のTealiumインスタンス用に次回以降のトラッキングコールに含まれる揮発性データを構成します |
| `trackEvent()`| イベント名とイベントデータを使用してイベントをトラッキングします |
| `trackEventForInstanceName()`| アプリ内に複数のTealiumインスタンスがある場合、特定のTealiumインスタンスでイベントをトラッキングします |
|`trackView()` | 画面名とビューデータを使用してビューをトラッキングします |
|`trackViewForInstanceName()` | アプリ内に複数のTealiumインスタンスがある場合、特定のTealiumインスタンスでビューをトラッキングします |

### `addRemoteCommand()`

リモートコマンドマネージャーにリモートコマンドを追加します。

```javascript
addRemoteCommand(commandID, description, callback);
```

| パラメータ | タイプ | 説明 | 例 |
| --- | --- | --- | --- |
| `commandID` | `String` | タグ構成からのコマンドIDの名前 | `"test_command"` |
| `description` | `String ` | リモートコマンドの説明 | `"Firebase remote command"` |
| `callback` | `Function ` | リモートコマンドからの応答を受け取った後に実行するコールバック関数。コールバックはタグマッピングからのキー値ペアのペイロードを返します。 | (例を参照) |

例:

```javascript
Tealium.addRemoteCommand("firebase", "Firebase remote command", function(payload) {

  var eventName = payload["firebase_event_name"];
  var eventProperties = payload["firebase_event_properties"];

  analytics.logEvent(eventName, eventProperties);
});
```

### `addRemoteCommandForInstanceName()`

特定のTealiumインスタンス用にリモートコマンドマネージャーにリモートコマンドを追加します。

```javascript
addRemoteCommandForInstanceName(instanceName, commandID, description, callback);
```

| パラメータ | タイプ | 説明 | 例 |
| --- | --- | --- | --- |
| `instanceName` | `String` | Tealiumインスタンスの名前 | `"instance-2"` |
| `commandID` | `String` | タグ構成からのコマンドIDの名前 | `"test_command"` |
| `description` | `String ` | リモートコマンドの説明 | `"Firebase remote command"` |
| `callback` | `Function ` |  リモートコマンドからの応答を受け取った後に実行するコールバック関数。コールバックはタグマッピングからのキー値ペアのペイロードを返します。 | (例を参照) |

例:

```javascript
Tealium.addRemoteCommand("instance-2", "survey", "Display feedback survey", function(payload) {

	var title = payload["survey_title"];
	var question = payload["survey_question"];

	Alert.alert(title, question, [{text: 'Yes', onPress: () => surveyHandler()},
								  {text: 'No', onPress: () => surveyHandler()}]);

});
```

### `getPersistentData()`
特定のキーの値を取得します。

```javascript
Tealium.getPersistentData(key, value);
```

| パラメータ | タイプ | 説明 | 例 |
| --- | --- | --- | --- |
| `key` | `String` | 値のキー名  | `"foo"` |
| `value` | `Object` | キー値ペアのJSONオブジェクト | `function(value) {console.log("get persistent: " + value);}` |


### `getPersistentDataForInstanceName()`
特定のTealiumインスタンスとキーの永続データ値を取得します。アプリに複数のTealiumインスタンスがある場合に使用します。

```javascript
Tealium.getPersistentDataForInstanceName(instanceName, key, value);
```
| パラメータ | タイプ | 説明 | 例 |
| --- | --- | --- | --- |
| `name` | `String` | インスタンス名  | `"instance-2"` |
| `key` | `String` | 値のキー名  | `"foo"` |
| `data` | `Object` | キー値ペアのJSONオブジェクト | `function(value) {console.log("get volatile: " + value);}` |

### `getUserConsentCategories()`
ユーザーの同意カテゴリを取得します。ユーザー同意カテゴリを使用するためのコールバックを渡します。

```javascript
Tealium.getUserConsentCategories(userConsentCategories);
```

| パラメータ | タイプ | 説明 | 例 |
| --- | --- | --- | --- |
| `userConsentCategories` | `Callback` | ユーザー同意カテゴリを使用するコールバック関数 | `function (consentCategories) {console.log("categories 'main': " + consentCategories);}` |
### `getUserConsentCatgoriesForInstanceName()`
特定のTealiumインスタンスに対してユーザーの同意カテゴリを取得します。ユーザーの同意カテゴリを使用するためにコールバックを渡します。アプリにTealiumの複数のインスタンスがある場合に使用します。

```javascript
Tealium.getUserConsentCategoriesForInstanceName(name, userConsentCategories);
```
| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `name` | `String` | インスタンス名 | `"instance-2"` |
| `userConsentCategories` | `Callback` | ユーザーの同意カテゴリを使用するコールバック関数 | `function (consentCategories) {console.log("categories 'main': " + consentCategories);}` |

### `getUserConsentStatus()`
ユーザーの同意状態を取得します。ユーザーの同意状態を使用するためにコールバックを渡します。

```javascript
Tealium.getUserConsentStatus(userConsentStatus);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `userConsentStatus` | `Callback` | ユーザーの同意状態を使用するコールバック関数 | `function(userConsentStatus) {console.log("consent status 'instance-2': " + userConsentStatus);}` |

### `getUserConsentStatusForInstanceName()`
特定のTealiumインスタンスに対してユーザーの同意状態を取得します。ユーザーの同意状態を使用するためにコールバックを渡します。アプリにTealiumの複数のインスタンスがある場合に使用します。

```javascript
Tealium.getUserConsentStatusForInstanceName(name, userConsentStatus);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `name` | `String` | インスタンス名 | `"instance-2"` |
| `userConsentStatus` | `Callback` | ユーザーの同意状態を使用するコールバック関数 | `function(userConsentStatus) {console.log("consent status 'instance-2': " + userConsentStatus);}` |

### `getVisitorID()`
ユーザーの訪問IDを取得します。訪問IDを使用するためにコールバックを渡します。

```javascript
Tealium.getVisitorID(visitorID);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `visitorID` | `Callback` | 訪問IDを使用するコールバック関数 | `function (visitorID) {console.log("visitorID: " + visitorID);}` |

### `getVisitorIDForInstanceName()`
特定のTealiumインスタンスに対してユーザーの訪問IDを取得します。訪問IDを使用するためにコールバックを渡します。アプリにTealiumの複数のインスタンスがある場合に使用します。

```javascript
Tealium.getVisitorIDForInstanceName(name, visitorID);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `name` | `String` | インスタンス名 | `"instance-2"` |
| `visitorID` | `Callback` | 訪問IDを使用するコールバック関数 | `function (visitorID) {console.log("visitorID: " + visitorID);}` |

### `getVolatileData()`
渡されたキーの値を取得します。

```javascript
Tealium.getVolatileData(key, value);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `key` | `String` | 値のキー名 | `"foo"` |
| `value` | `Object` | キーと値のペアのJSONオブジェクト | `function(value) {console.log("get volatile: " + value);}` |

### `getVolatileDataForInstanceName()`
特定のTealiumインスタンスとキーに対して揮発性データ値を取得します。アプリにTealiumの複数のインスタンスがある場合に使用します。

```javascript
Tealium.getVolatileDataForInstanceName(instanceName, key, value);
```
| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `name` | `String` | インスタンス名 | `"instance-2"` |
| `key` | `String` | 値のキー名 | `"foo"` |
| `data` | `Object` | キーと値のペアのJSONオブジェクト | `function(value) {console.log("get volatile: " + value);}` |

### `initialize()`

他のメソッドを呼び出す前にTealiumを初期化します。

```javascript
initialize(account,
    profile,
    environment,
    iosDatasource,
    androidDatasource,
    instance,
    isLifecycleEnabled);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `account` | `String` | Tealiumアカウント名 | `"companyXYZ" `|
| `profile` | `String` | Tealiumプロファイル名 | `"main"` |
| `environment` | `String` | Tealium環境名 |  [`"dev"`, `"qa"`, `"prod"`] |
| `iosDatasource` | `String` | (オプション) Tealium iOSデータソースキー | `"abc123"` |
| `androidDatasource` | `String` | (オプション) Tealium Androidデータソースキー | `"xyz123"` |
| `instance` | `String` | Tealiumインスタンス名 (デフォルト: `"MAIN"`) | `"MAIN"` |
| `isLifecycleEnabled` | `Boolean` | (オプション) ライフサイクル追跡を有効にする (デフォルト: `true`) | [`true`, `false`] |

### `initializeCustom()`

他のメソッドを呼び出す前にすべてのオプションでTealiumを初期化します。

```javascript
initializeCustom(account,
        profile,
        environment,
        iosDatasource,
        androidDatasource,
        instance,
        isLifecycleEnabled,
        overridePublishSettingsURL,
        overrideTagManagementURL,
        collectURL,
        enableConsentManager,
        overrideCollectDispatchURL
    );
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `account` | `String` | Tealiumアカウント名 | `"companyXYZ" `|
| `profile` | `String` | Tealiumプロファイル名 | `"main"` |
| `environment` | `String` | Tealium環境名 |  [`"dev"`, `"qa"`, `"prod"`] |
| `iosDatasource` | `String` | (オプション) Tealium iOSデータソースキー | `"abc123"` |
| `androidDatasource` | `String` | (オプション) Tealium Androidデータソースキー | `"xyz123"` |
| `instance` | `String` | Tealiumインスタンス名 (デフォルト: `"MAIN"`) | `"MAIN"` |
| `isLifecycleEnabled` | `Boolean` | (オプション) ライフサイクル追跡を有効にする  (デフォルト: `true`) | [`true`, `false`] |
| `overridePublishSettingsURL` | `String` | パブリッシュ構成URLを上書きする場合 (デフォルト: `null`) | `null` |
| `overrideTagManagementURL` | `String` | タグ管理URLを上書きする場合 (デフォルト: `null`) | `null` |
| `collectURL` | `Boolean` | Collectエンドポイントにデータを送信する場合に有効にする (デフォルト: true) | [`true`, `false`]|
| `enableConsentManager`| `Boolean` | 同意管理を有効にする |[`true`, `false`] |
| `overrideCollectDispatchURL`| `String` | Collect URLを上書きする場合 (デフォルト: `null`) | `null` |

### `initializeWithConsentManager()`

同意管理を含めてTealiumを初期化します。

```javascript
initializeWithConsentManager(account,
  profile,
  environment,
  iosDatasource,
  androidDatasource,
  instance,
  isLifecycleEnabled);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `account` | `String` | Tealiumアカウント名 | `"companyXYZ" `|
| `profile` | `String` | Tealiumプロファイル名 | `"main"` |
| `environment` | `String` | Tealium環境名 |  [`"dev"`, `"qa"`, `"prod"`] |
| `iosDatasource` | `String` | (オプション) Tealium iOSデータソースキー | `"abc123"` |
| `androidDatasource` | `String` | (オプション) Tealium Androidデータソースキー | `"xyz123"` |
| `instancee` | `String` | Tealiumインスタンス名 (デフォルト: `"MAIN"`) | `"MAIN"` |
| `isLifecycleEnabled` | `Boolean` | (オプション) ライフサイクル追跡を有効にする  (デフォルト: `true`) | [`true`, `false`] |

### `isConsentLoggingEnabled()`
ユーザーの同意ログ記録が有効かどうかを確認します。同意ログの値を使用するためにコールバックを渡します。

```javascript
isConsentLoggingEnabled(enabled);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `callback` | `Callback` | ユーザーの同意ログ記録が有効かどうかを確認する | 'function (enabled) {console.log("consent logging enabled 'main': " + enabled);}' |

### `isConsentLoggingEnabledForInstanceName()`

特定のTealiumインスタンスに対してユーザーの同意ログ記録が有効かどうかを確認します。同意ログの値を使用するためにコールバックを渡します。アプリにTealiumの複数のインスタンスがある場合に使用します。

```javascript
Tealium.isConsentLoggingEnabledForInstanceName(name, enabled);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `name` | `String` | インスタンス名 | `"instance-2"` |
| `callback` | `Callback` | ユーザーの同意ログ記録が有効かどうかを確認する | 'function (enabled) {console.log("consent logging enabled 'main': " + enabled);}' |
### `removePersistentData()`
`Tealium.setPersistentData()`を使用して以前に構成された永続的なデータを削除します。

```javascript
Tealium.removePersistentData(keys);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `keys` | `[String]` | キー名の配列  | `["foo", "bar"]` |


### `removePersistentDataForInstanceName()`
`Tealium.setPersistentData()`を使用して以前に構成された永続的なデータを、特定のTealiumインスタンスに対して削除します。アプリにTealiumの複数のインスタンスがある場合に使用します。

```javascript
Tealium.removePersistentDataForInstanceName(instanceName, keys);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `name` | `String` | インスタンス名  | `"instance-2"` |
| `keys` | `[String]` | キー名の配列  | `["foo", "bar"]` |

### `removeRemoteCommand()`

リモートコマンドマネージャーからリモートコマンドを削除します。

```javascript
removeRemoteCommand(commandID);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `commandID ` | `String` | 削除するコマンドIDの名前  | `"test_command"` |

例:

```javascript
Tealium.removeRemoteCommand("firebase");
```

### `removeRemoteCommandForInstanceName()`

リモートコマンドマネージャーから、特定のTealiumインスタンスのリモートコマンドを削除します。

```javascript
removeRemoteCommandForInstanceName(instanceName, commandID);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `instanceName` | `String` | Tealiumインスタンスの名前 | `"instance-2"` |
| `commandID ` | `String` | 削除するコマンドIDの名前  | `"test_command"` |

例:

```javascript
Tealium.removeRemoteCommand("instance-2", "firebase");
```

### `removeVolatileData()`
`Tealium.setVolatileData()`を使用して以前に構成された揮発性データを削除します。

```javascript
Tealium.removeVolatileData(keys);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `keys` | `[String]` | キー名の配列  | `["foo", "bar"]` |


### `removeVolatileDataForInstanceName()`
提供されたインスタンス名に対して揮発性データを削除します。アプリにTealiumの複数のインスタンスがある場合に使用します。

```javascript
Tealium.removeVolatileDataForInstanceName(name, keys);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `name` | `String` | インスタンス名  | `"instance-2"` |
| `keys` | `[String]` | キー名の配列  | `["foo", "bar"]` |



### `resetUserConsentPreferences()`
ユーザーの同意状態とカテゴリをリセットします。

```javascript
Tealium.resetUserConsentPreferences();
```


### `resetUserConsentPreferencesForInstanceName()`
特定のTealiumインスタンスに対してユーザーの同意状態とカテゴリをリセットします。アプリにTealiumの複数のインスタンスがある場合に使用します。

```javascript
Tealium.resetUserConsentPreferencesForInstanceName(name);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `name` | `String` | インスタンス名 | `"instance-2"` |



### `setConsentLoggingEnabled()`
ユーザーの同意ログを構成します。

```javascript
Tealium.setConsentLoggingEnabled(enabled);
```
| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `enabled` | `boolean` | ユーザーの同意ログを有効にする | [`"true"`, `"false"`] |


### `setConsentLoggingEnabledForInstanceName()`
特定のTealiumインスタンスに対してユーザーの同意ログを構成します。アプリにTealiumの複数のインスタンスがある場合に使用します。

```javascript
Tealium.setConsentLoggingEnabledForInstanceName(name, enabled);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `name` | `String` | インスタンス名 | `"instance-2"` |
| `enabled` | `boolean` | ユーザーの同意ログを有効にする | [`"true"`, `"false"`] |

### `setPersistentData()`
アプリの再起動間でも、各後続のイベントまたはビューに送信される永続的なデータを構成します。

```javascript
Tealium.setPersistentData(data);
```
| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `data` | `Object` | キーが文字列で値が文字列または文字列の配列であるキー値ペアのJSONオブジェクト | `{"persistent_key2" : "persistent_val2"}` |


### `setPersistentDataForInstanceName()`
特定のTealiumインスタンスに対して、アプリの再起動間でも各後続のイベントまたはビューに送信される永続的なデータを構成します。アプリにTealiumの複数のインスタンスがある場合に使用します。

```javascript
Tealium.setPersistentDataForInstanceName(instanceName, data);
```
| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `name` | `String` | インスタンス名  | `"instance-2"` |
| `data` | `Object` | キーが文字列で値が文字列または文字列の配列であるキー値ペアのJSONオブジェクト | `{"persistent_key2" : "persistent_val2"}` |


### `setUserConsentCategories()`
ユーザーの同意カテゴリを構成します。カテゴリの文字列配列を渡して構成します。

```javascript
Tealium.setUserConsentCategories(userConsentCategories);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `userConsentCategories` | `[String]` | ユーザーの同意カテゴリの配列 | `["email", "personalization"]` |

### `setUserConsentCategoriesForInstanceName()`
特定のTealiumインスタンスに対してユーザーの同意カテゴリを構成します。カテゴリの文字列配列を渡して構成します。アプリにTealiumの複数のインスタンスがある場合に使用します。

```javascript
Tealium.setUserConsentCategoriesForInstanceName(name, userConsentCategories);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `name` | `String` | インスタンス名 | `"instance-2"` |
| `userConsentCategories` | `[String]` | ユーザーの同意カテゴリの配列 | `["analytics", "big_data"]` |


### `setUserConsentStatus()`

ユーザーの同意状態を構成します。

```javascript
Tealium.setUserConsentStatus(userConsentStatus);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `userConsentStatus` | `int` | ユーザーの同意状態 | [`0`, `1`, `2`, `3`] |

| 同意状態値 | 説明 |
| --- | --- |
| 0 | 不明 |
| 1 | 同意済み |
| 2 | 同意していない |
| 3 | 無効 (Objective-Cのみ) |

### `setUserConsentStatusForInstanceName()`
特定のTealiumインスタンスに対してユーザーの同意状態を構成します。アプリにTealiumの複数のインスタンスがある場合に使用します。

```javascript
Tealium.setUserConsentStatusForInstanceName(name, userConsentStatus);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `name` | `String` | インスタンス名 | `"instance-2"` |
| `userConsentStatus` | `int` | ユーザーの同意状態 | [`0`, `1`, `2`, `3`] |

| 同意状態値 | 説明 |
| --- | --- |
| 0 | 不明 |
| 1 | 同意済み |
| 2 | 同意していない |
| 3 | 無効 (Objective-Cのみ) |

### `setVolatileData()`
アプリが終了するまで、各後続のイベントまたはビューに送信される揮発性データを構成します。データはキーが文字列で値が文字列または文字列の配列であるキー値ペアのJSONオブジェクトです。

```javascript
Tealium.setVolatileData(data);
```
| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `data` | `Object` | キーが文字列で値が文字列または文字列の配列であるキー値ペアのJSONオブジェクト | `{"volatile_var": "volatile_val", "volatile_var2": "volatile_val2"}` |


### `setVolatileDataForInstanceName()`
特定のTealiumインスタンスに対して、アプリが終了するまで各後続のトラッキングコールに含まれる揮癲性データを構成します。アプリにTealiumの複数のインスタンスがある場合に使用します。

```javascript
Tealium.setVolatileDataForInstanceName(name, data);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `name` | `String` | キー名 | "instance-2" |
| `data` | `Object` | キーが文字列で値が文字列または文字列の配列であるキー値ペアのJSONオブジェクト | `{"foo": "bar"}` |
### `trackEvent()`

イベント名とイベントデータでイベントを追跡します。

```javascript
trackEvent(stringTitle, data);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `stringTitle` | `String` | イベント名（Tealium Customer Data Hubでの`event_name`属性になります） | `"test_event"` |
| `data` | `Object` | キーと値のペアのJSONオブジェクト | `{"title": "test_event", "event_title": "test_event", "testkey": "testval", "anotherkey": "anotherval"}` |


### `trackEventForInstanceName()`

アプリに複数のTealiumインスタンスがある場合、特定のTealiumインスタンスのイベントを追跡します。

```javascript
trackEvent(name, stringTitle, data);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `name` | `String` | Tealiumインスタンスの名前 | `"instance-2"` |
| `stringTitle` | `String` | イベント名（Customer Data Hubでの`event_name`属性になります） | `"test_event_2"` |
| `data` | `Object` | キーと値のペアのJSONオブジェクト | |


### `trackView()`

画面名とビューデータでビューを追跡します。

```javascript
trackView(screenName, data);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `stringTitle` | `String` | イベント名（Customer Data Hubでの`screen_title`属性になります） | `"test_view"` |
| `data` | `Object` | キーと値のペアのJSONオブジェクト | `{"title": "test_view", "event_title": "test_view", "testkey": "testval", "anotherkey": "anotherval"}` |


### `trackViewForInstanceName()`

アプリに複数のTealiumインスタンスがある場合、特定のTealiumインスタンスのビューを追跡します。

```javascript
Tealium.trackViewForInstanceName(instanceName, screenName, data);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `name` | `String` | Tealiumインスタンスの名前 | `"instance-2"` |
| `stringTitle` | `String` | イベント名（Customer Data Hubでの`screen_title`属性になります） | `"instance_2_view"` |
| `data` | `Object` | （オプション）キーと値のペアのJSONオブジェクト | |