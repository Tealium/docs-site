---
title: API リファレンス
description: TealiumのReact Native用クラスとメソッドのリファレンスガイドです。
url: https://docs.tealium.com/ja/platforms/react-native-v1/api/
---
これはTealiumのReact Native用の以前のバージョン（1.x）です。  
現在のバージョンについては、[Tealium for React Native 2.x](/ja/platforms/react-native/)をご覧ください。

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
| `commandID` | `String` | タグ構成からのコマンドIDの名前 | `&#34;test_command&#34;` |
| `description` | `String ` | リモートコマンドの説明 | `&#34;Firebase remote command&#34;` |
| `callback` | `Function ` | リモートコマンドからの応答を受け取った後に実行するコールバック関数。コールバックはタグマッピングからのキー値ペアのペイロードを返します。 | (例を参照) |

例:

```javascript
Tealium.addRemoteCommand(&#34;firebase&#34;, &#34;Firebase remote command&#34;, function(payload) {

  var eventName = payload[&#34;firebase_event_name&#34;];
  var eventProperties = payload[&#34;firebase_event_properties&#34;];

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
| `instanceName` | `String` | Tealiumインスタンスの名前 | `&#34;instance-2&#34;` |
| `commandID` | `String` | タグ構成からのコマンドIDの名前 | `&#34;test_command&#34;` |
| `description` | `String ` | リモートコマンドの説明 | `&#34;Firebase remote command&#34;` |
| `callback` | `Function ` |  リモートコマンドからの応答を受け取った後に実行するコールバック関数。コールバックはタグマッピングからのキー値ペアのペイロードを返します。 | (例を参照) |

例:

```javascript
Tealium.addRemoteCommand(&#34;instance-2&#34;, &#34;survey&#34;, &#34;Display feedback survey&#34;, function(payload) {

	var title = payload[&#34;survey_title&#34;];
	var question = payload[&#34;survey_question&#34;];

	Alert.alert(title, question, [{text: &#39;Yes&#39;, onPress: () =&gt; surveyHandler()},
								  {text: &#39;No&#39;, onPress: () =&gt; surveyHandler()}]);

});
```

### `getPersistentData()`
特定のキーの値を取得します。

```javascript
Tealium.getPersistentData(key, value);
```

| パラメータ | タイプ | 説明 | 例 |
| --- | --- | --- | --- |
| `key` | `String` | 値のキー名  | `&#34;foo&#34;` |
| `value` | `Object` | キー値ペアのJSONオブジェクト | `function(value) {console.log(&#34;get persistent: &#34; &#43; value);}` |


### `getPersistentDataForInstanceName()`
特定のTealiumインスタンスとキーの永続データ値を取得します。アプリに複数のTealiumインスタンスがある場合に使用します。

```javascript
Tealium.getPersistentDataForInstanceName(instanceName, key, value);
```
| パラメータ | タイプ | 説明 | 例 |
| --- | --- | --- | --- |
| `name` | `String` | インスタンス名  | `&#34;instance-2&#34;` |
| `key` | `String` | 値のキー名  | `&#34;foo&#34;` |
| `data` | `Object` | キー値ペアのJSONオブジェクト | `function(value) {console.log(&#34;get volatile: &#34; &#43; value);}` |

### `getUserConsentCategories()`
ユーザーの同意カテゴリを取得します。ユーザー同意カテゴリを使用するためのコールバックを渡します。

```javascript
Tealium.getUserConsentCategories(userConsentCategories);
```

| パラメータ | タイプ | 説明 | 例 |
| --- | --- | --- | --- |
| `userConsentCategories` | `Callback` | ユーザー同意カテゴリを使用するコールバック関数 | `function (consentCategories) {console.log(&#34;categories &#39;main&#39;: &#34; &#43; consentCategories);}` |
### `getUserConsentCatgoriesForInstanceName()`
特定のTealiumインスタンスに対してユーザーの同意カテゴリを取得します。ユーザーの同意カテゴリを使用するためにコールバックを渡します。アプリにTealiumの複数のインスタンスがある場合に使用します。

```javascript
Tealium.getUserConsentCategoriesForInstanceName(name, userConsentCategories);
```
| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `name` | `String` | インスタンス名 | `&#34;instance-2&#34;` |
| `userConsentCategories` | `Callback` | ユーザーの同意カテゴリを使用するコールバック関数 | `function (consentCategories) {console.log(&#34;categories &#39;main&#39;: &#34; &#43; consentCategories);}` |

### `getUserConsentStatus()`
ユーザーの同意状態を取得します。ユーザーの同意状態を使用するためにコールバックを渡します。

```javascript
Tealium.getUserConsentStatus(userConsentStatus);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `userConsentStatus` | `Callback` | ユーザーの同意状態を使用するコールバック関数 | `function(userConsentStatus) {console.log(&#34;consent status &#39;instance-2&#39;: &#34; &#43; userConsentStatus);}` |

### `getUserConsentStatusForInstanceName()`
特定のTealiumインスタンスに対してユーザーの同意状態を取得します。ユーザーの同意状態を使用するためにコールバックを渡します。アプリにTealiumの複数のインスタンスがある場合に使用します。

```javascript
Tealium.getUserConsentStatusForInstanceName(name, userConsentStatus);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `name` | `String` | インスタンス名 | `&#34;instance-2&#34;` |
| `userConsentStatus` | `Callback` | ユーザーの同意状態を使用するコールバック関数 | `function(userConsentStatus) {console.log(&#34;consent status &#39;instance-2&#39;: &#34; &#43; userConsentStatus);}` |

### `getVisitorID()`
ユーザーの訪問IDを取得します。訪問IDを使用するためにコールバックを渡します。

```javascript
Tealium.getVisitorID(visitorID);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `visitorID` | `Callback` | 訪問IDを使用するコールバック関数 | `function (visitorID) {console.log(&#34;visitorID: &#34; &#43; visitorID);}` |

### `getVisitorIDForInstanceName()`
特定のTealiumインスタンスに対してユーザーの訪問IDを取得します。訪問IDを使用するためにコールバックを渡します。アプリにTealiumの複数のインスタンスがある場合に使用します。

```javascript
Tealium.getVisitorIDForInstanceName(name, visitorID);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `name` | `String` | インスタンス名 | `&#34;instance-2&#34;` |
| `visitorID` | `Callback` | 訪問IDを使用するコールバック関数 | `function (visitorID) {console.log(&#34;visitorID: &#34; &#43; visitorID);}` |

### `getVolatileData()`
渡されたキーの値を取得します。

```javascript
Tealium.getVolatileData(key, value);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `key` | `String` | 値のキー名 | `&#34;foo&#34;` |
| `value` | `Object` | キーと値のペアのJSONオブジェクト | `function(value) {console.log(&#34;get volatile: &#34; &#43; value);}` |

### `getVolatileDataForInstanceName()`
特定のTealiumインスタンスとキーに対して揮発性データ値を取得します。アプリにTealiumの複数のインスタンスがある場合に使用します。

```javascript
Tealium.getVolatileDataForInstanceName(instanceName, key, value);
```
| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `name` | `String` | インスタンス名 | `&#34;instance-2&#34;` |
| `key` | `String` | 値のキー名 | `&#34;foo&#34;` |
| `data` | `Object` | キーと値のペアのJSONオブジェクト | `function(value) {console.log(&#34;get volatile: &#34; &#43; value);}` |

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
| `account` | `String` | Tealiumアカウント名 | `&#34;companyXYZ&#34; `|
| `profile` | `String` | Tealiumプロファイル名 | `&#34;main&#34;` |
| `environment` | `String` | Tealium環境名 |  [`&#34;dev&#34;`, `&#34;qa&#34;`, `&#34;prod&#34;`] |
| `iosDatasource` | `String` | (オプション) Tealium iOSデータソースキー | `&#34;abc123&#34;` |
| `androidDatasource` | `String` | (オプション) Tealium Androidデータソースキー | `&#34;xyz123&#34;` |
| `instance` | `String` | Tealiumインスタンス名 (デフォルト: `&#34;MAIN&#34;`) | `&#34;MAIN&#34;` |
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
| `account` | `String` | Tealiumアカウント名 | `&#34;companyXYZ&#34; `|
| `profile` | `String` | Tealiumプロファイル名 | `&#34;main&#34;` |
| `environment` | `String` | Tealium環境名 |  [`&#34;dev&#34;`, `&#34;qa&#34;`, `&#34;prod&#34;`] |
| `iosDatasource` | `String` | (オプション) Tealium iOSデータソースキー | `&#34;abc123&#34;` |
| `androidDatasource` | `String` | (オプション) Tealium Androidデータソースキー | `&#34;xyz123&#34;` |
| `instance` | `String` | Tealiumインスタンス名 (デフォルト: `&#34;MAIN&#34;`) | `&#34;MAIN&#34;` |
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
| `account` | `String` | Tealiumアカウント名 | `&#34;companyXYZ&#34; `|
| `profile` | `String` | Tealiumプロファイル名 | `&#34;main&#34;` |
| `environment` | `String` | Tealium環境名 |  [`&#34;dev&#34;`, `&#34;qa&#34;`, `&#34;prod&#34;`] |
| `iosDatasource` | `String` | (オプション) Tealium iOSデータソースキー | `&#34;abc123&#34;` |
| `androidDatasource` | `String` | (オプション) Tealium Androidデータソースキー | `&#34;xyz123&#34;` |
| `instancee` | `String` | Tealiumインスタンス名 (デフォルト: `&#34;MAIN&#34;`) | `&#34;MAIN&#34;` |
| `isLifecycleEnabled` | `Boolean` | (オプション) ライフサイクル追跡を有効にする  (デフォルト: `true`) | [`true`, `false`] |

### `isConsentLoggingEnabled()`
ユーザーの同意ログ記録が有効かどうかを確認します。同意ログの値を使用するためにコールバックを渡します。

```javascript
isConsentLoggingEnabled(enabled);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `callback` | `Callback` | ユーザーの同意ログ記録が有効かどうかを確認する | &#39;function (enabled) {console.log(&#34;consent logging enabled &#39;main&#39;: &#34; &#43; enabled);}&#39; |

### `isConsentLoggingEnabledForInstanceName()`

特定のTealiumインスタンスに対してユーザーの同意ログ記録が有効かどうかを確認します。同意ログの値を使用するためにコールバックを渡します。アプリにTealiumの複数のインスタンスがある場合に使用します。

```javascript
Tealium.isConsentLoggingEnabledForInstanceName(name, enabled);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `name` | `String` | インスタンス名 | `&#34;instance-2&#34;` |
| `callback` | `Callback` | ユーザーの同意ログ記録が有効かどうかを確認する | &#39;function (enabled) {console.log(&#34;consent logging enabled &#39;main&#39;: &#34; &#43; enabled);}&#39; |
### `removePersistentData()`
`Tealium.setPersistentData()`を使用して以前に構成された永続的なデータを削除します。

```javascript
Tealium.removePersistentData(keys);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `keys` | `[String]` | キー名の配列  | `[&#34;foo&#34;, &#34;bar&#34;]` |


### `removePersistentDataForInstanceName()`
`Tealium.setPersistentData()`を使用して以前に構成された永続的なデータを、特定のTealiumインスタンスに対して削除します。アプリにTealiumの複数のインスタンスがある場合に使用します。

```javascript
Tealium.removePersistentDataForInstanceName(instanceName, keys);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `name` | `String` | インスタンス名  | `&#34;instance-2&#34;` |
| `keys` | `[String]` | キー名の配列  | `[&#34;foo&#34;, &#34;bar&#34;]` |

### `removeRemoteCommand()`

リモートコマンドマネージャーからリモートコマンドを削除します。

```javascript
removeRemoteCommand(commandID);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `commandID ` | `String` | 削除するコマンドIDの名前  | `&#34;test_command&#34;` |

例:

```javascript
Tealium.removeRemoteCommand(&#34;firebase&#34;);
```

### `removeRemoteCommandForInstanceName()`

リモートコマンドマネージャーから、特定のTealiumインスタンスのリモートコマンドを削除します。

```javascript
removeRemoteCommandForInstanceName(instanceName, commandID);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `instanceName` | `String` | Tealiumインスタンスの名前 | `&#34;instance-2&#34;` |
| `commandID ` | `String` | 削除するコマンドIDの名前  | `&#34;test_command&#34;` |

例:

```javascript
Tealium.removeRemoteCommand(&#34;instance-2&#34;, &#34;firebase&#34;);
```

### `removeVolatileData()`
`Tealium.setVolatileData()`を使用して以前に構成された揮発性データを削除します。

```javascript
Tealium.removeVolatileData(keys);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `keys` | `[String]` | キー名の配列  | `[&#34;foo&#34;, &#34;bar&#34;]` |


### `removeVolatileDataForInstanceName()`
提供されたインスタンス名に対して揮発性データを削除します。アプリにTealiumの複数のインスタンスがある場合に使用します。

```javascript
Tealium.removeVolatileDataForInstanceName(name, keys);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `name` | `String` | インスタンス名  | `&#34;instance-2&#34;` |
| `keys` | `[String]` | キー名の配列  | `[&#34;foo&#34;, &#34;bar&#34;]` |



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
| `name` | `String` | インスタンス名 | `&#34;instance-2&#34;` |



### `setConsentLoggingEnabled()`
ユーザーの同意ログを構成します。

```javascript
Tealium.setConsentLoggingEnabled(enabled);
```
| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `enabled` | `boolean` | ユーザーの同意ログを有効にする | [`&#34;true&#34;`, `&#34;false&#34;`] |


### `setConsentLoggingEnabledForInstanceName()`
特定のTealiumインスタンスに対してユーザーの同意ログを構成します。アプリにTealiumの複数のインスタンスがある場合に使用します。

```javascript
Tealium.setConsentLoggingEnabledForInstanceName(name, enabled);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `name` | `String` | インスタンス名 | `&#34;instance-2&#34;` |
| `enabled` | `boolean` | ユーザーの同意ログを有効にする | [`&#34;true&#34;`, `&#34;false&#34;`] |

### `setPersistentData()`
アプリの再起動間でも、各後続のイベントまたはビューに送信される永続的なデータを構成します。

```javascript
Tealium.setPersistentData(data);
```
| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `data` | `Object` | キーが文字列で値が文字列または文字列の配列であるキー値ペアのJSONオブジェクト | `{&#34;persistent_key2&#34; : &#34;persistent_val2&#34;}` |


### `setPersistentDataForInstanceName()`
特定のTealiumインスタンスに対して、アプリの再起動間でも各後続のイベントまたはビューに送信される永続的なデータを構成します。アプリにTealiumの複数のインスタンスがある場合に使用します。

```javascript
Tealium.setPersistentDataForInstanceName(instanceName, data);
```
| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `name` | `String` | インスタンス名  | `&#34;instance-2&#34;` |
| `data` | `Object` | キーが文字列で値が文字列または文字列の配列であるキー値ペアのJSONオブジェクト | `{&#34;persistent_key2&#34; : &#34;persistent_val2&#34;}` |


### `setUserConsentCategories()`
ユーザーの同意カテゴリを構成します。カテゴリの文字列配列を渡して構成します。

```javascript
Tealium.setUserConsentCategories(userConsentCategories);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `userConsentCategories` | `[String]` | ユーザーの同意カテゴリの配列 | `[&#34;email&#34;, &#34;personalization&#34;]` |

### `setUserConsentCategoriesForInstanceName()`
特定のTealiumインスタンスに対してユーザーの同意カテゴリを構成します。カテゴリの文字列配列を渡して構成します。アプリにTealiumの複数のインスタンスがある場合に使用します。

```javascript
Tealium.setUserConsentCategoriesForInstanceName(name, userConsentCategories);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `name` | `String` | インスタンス名 | `&#34;instance-2&#34;` |
| `userConsentCategories` | `[String]` | ユーザーの同意カテゴリの配列 | `[&#34;analytics&#34;, &#34;big_data&#34;]` |


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
| `name` | `String` | インスタンス名 | `&#34;instance-2&#34;` |
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
| `data` | `Object` | キーが文字列で値が文字列または文字列の配列であるキー値ペアのJSONオブジェクト | `{&#34;volatile_var&#34;: &#34;volatile_val&#34;, &#34;volatile_var2&#34;: &#34;volatile_val2&#34;}` |


### `setVolatileDataForInstanceName()`
特定のTealiumインスタンスに対して、アプリが終了するまで各後続のトラッキングコールに含まれる揮癲性データを構成します。アプリにTealiumの複数のインスタンスがある場合に使用します。

```javascript
Tealium.setVolatileDataForInstanceName(name, data);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `name` | `String` | キー名 | &#34;instance-2&#34; |
| `data` | `Object` | キーが文字列で値が文字列または文字列の配列であるキー値ペアのJSONオブジェクト | `{&#34;foo&#34;: &#34;bar&#34;}` |
### `trackEvent()`

イベント名とイベントデータでイベントを追跡します。

```javascript
trackEvent(stringTitle, data);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `stringTitle` | `String` | イベント名（Tealium Customer Data Hubでの`event_name`属性になります） | `&#34;test_event&#34;` |
| `data` | `Object` | キーと値のペアのJSONオブジェクト | `{&#34;title&#34;: &#34;test_event&#34;, &#34;event_title&#34;: &#34;test_event&#34;, &#34;testkey&#34;: &#34;testval&#34;, &#34;anotherkey&#34;: &#34;anotherval&#34;}` |


### `trackEventForInstanceName()`

アプリに複数のTealiumインスタンスがある場合、特定のTealiumインスタンスのイベントを追跡します。

```javascript
trackEvent(name, stringTitle, data);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `name` | `String` | Tealiumインスタンスの名前 | `&#34;instance-2&#34;` |
| `stringTitle` | `String` | イベント名（Customer Data Hubでの`event_name`属性になります） | `&#34;test_event_2&#34;` |
| `data` | `Object` | キーと値のペアのJSONオブジェクト | |


### `trackView()`

画面名とビューデータでビューを追跡します。

```javascript
trackView(screenName, data);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `stringTitle` | `String` | イベント名（Customer Data Hubでの`screen_title`属性になります） | `&#34;test_view&#34;` |
| `data` | `Object` | キーと値のペアのJSONオブジェクト | `{&#34;title&#34;: &#34;test_view&#34;, &#34;event_title&#34;: &#34;test_view&#34;, &#34;testkey&#34;: &#34;testval&#34;, &#34;anotherkey&#34;: &#34;anotherval&#34;}` |


### `trackViewForInstanceName()`

アプリに複数のTealiumインスタンスがある場合、特定のTealiumインスタンスのビューを追跡します。

```javascript
Tealium.trackViewForInstanceName(instanceName, screenName, data);
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `name` | `String` | Tealiumインスタンスの名前 | `&#34;instance-2&#34;` |
| `stringTitle` | `String` | イベント名（Customer Data Hubでの`screen_title`属性になります） | `&#34;instance_2_view&#34;` |
| `data` | `Object` | （オプション）キーと値のペアのJSONオブジェクト | |