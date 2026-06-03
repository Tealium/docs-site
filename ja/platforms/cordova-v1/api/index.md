---
title: API リファレンス
description: TealiumのCordova用クラスとメソッドのリファレンスガイドです。
url: https://docs.tealium.com/ja/platforms/cordova-v1/api/
---
これはTealiumのCordova用の以前のバージョン（1.x）です。  
現在のバージョンについては、[TealiumのCordova 2.x](/ja/platforms/cordova/)を参照してください。

## クラス: `Tealium`

以下は、Cordovaの`Tealium`クラスでよく使用されるメソッドをまとめたものです。

| メソッド               | 説明                                                                                                                |
|:---------------------|:---------------------------------------------------------------------------------------------------------------------------|
| `addPersistent()`    | Tealiumの永続データストアにデータを追加します                                                                             |
| `addVolatile()`      | Tealiumの揮発性データストアにデータを追加します                                                                           |
| `init()`             | TealiumのCordovaプラグインを初期化します                                                                                 |
| `getPersistent()`    | Tealiumの永続データから値を返します                                                                                       |
| `getVisitorID()`     | 現在のユーザーのTealium訪問IDを返します                                                                                 |
| `getVolatile()`      | Tealiumの揮発性データストアから値を返します                                                                               |
| `removePersistent()` | Tealiumの永続データストアからデータを削除します                                                                           |
| `removeVolatile()`   | Tealiumの揮発性データストアから揮発性データを削除します                                                                   |
| `track()`            | 最初の引数タイプとして`&#34;view&#34;`を渡すことでビューを追跡、または`&#34;link&#34;`を渡すことでイベントを追跡します                     |
| `trackEvent()`       | ビュー以外のすべてのアクティビティを追跡します                                                                             |
| `trackView()`        | アプリ内でユーザーが画面を開いたり変更したりするたびに追跡します                                                           |


### `addPersistent()`

Tealiumの永続データストアに永続データを追加します。

```javascript
tealium.addPersistent(key, data, instance);
```

| パラメータ  | タイプ                   | 説明                                                                     | 例                           |
|:-----------|:-----------------------|:--------------------------------------------------------------------------------|:----------------------------------|
| `key`      | `String`               | 永続化される値のキー名                                               | `&#34;user_hashed_email&#34;`             |
| `data`     | `String` or `[String]` | このキーに対して永続化される値                                          | `[&#34;testpersist&#34;, &#34;testpersist2&#34;]` |
| `instance` | `String`               | 特定のトラッキングインスタンスを参照するために使用される任意のインスタンス名 | `&#34;tealium_main&#34;`                  |

### `addVolatile()`

Tealiumの揮発性データストアにデータを追加します。

```javascript
tealium.addVolatile(key, data, instance);
```

| パラメータ  | タイプ                   | 説明                                                                     | 例                              |
|:-----------|:-----------------------|:--------------------------------------------------------------------------------|:-------------------------------------|
| `key`      | `String`               | 永続化される値のキー名                                               | `&#34;user_hashed_email&#34;`                |
| `data`     | `String` or `[String]` | このキーに対して永続化される値                                          | `[&#34;testvolatile1&#34;, &#34;testvolatile2&#34;]` |
| `instance` | `String`               | 特定のトラッキングインスタンスを参照するために使用される任意のインスタンス名 | `&#34;tealium_main&#34;`                     |
### `init()`

Tealium Cordovaプラグインを初期化します。

```java
tealium.init(config, successCallBack, errorCallback);
```

| パラメータ           | タイプ                   | 説明                                                             |
|:------------------|:-----------------------|:------------------------------------------------------------------------|
| `config`          | JavaScript/JSON オブジェクト | 構成オブジェクト（下記の表を参照）                                     |
| `successCallback` | 関数               | デフォルトの成功コールバックをオーバーライドしてカスタム成功処理を可能にする |
| `errorCallback`   | 関数               | デフォルトの成功コールバックをオーバーライドしてカスタム成功処理を可能にする |

`config` オブジェクトは最初の引数として渡され、以下のデータを含んでいます：

```java
tealium.init({account, profile, environment, instance,
                isLifecycleEnabled,
                collectDispatchURL,
                collectDispatchProfile,
                isCrashReporterEnabled,
                logLevel,
                dataSourceId});
```

| パラメータ                    | タイプ     | 説明                                                                                | 例                                                                                                                                                                   |
|:-------------------------|:---------|:-------------------------------------------------------------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `account`                | `String` | Tealiumのアカウント名                                                                       | `&#34;companyXYZ&#34;`                                                                                                                                                            |
| `profile`                | `String` | Tealiumのプロファイル名                                                                       | `&#34;main&#34;`                                                                                                                                                                  |
| `environment`            | `String` | Tealiumの環境名                                                                   | [`&#34;dev&#34;`, `&#34;qa&#34;`, `&#34;prod&#34;`]                                                                                                                                               |
| `instance`               | `String` | Tealiumのインスタンス名（複数インスタンス対応）                                       | `&#34;tealium_main&#34;`                                                                                                                                                           |
| `isLifecycleEnabled`     | `String` | （オプション）ライフサイクル追跡を有効にするための文字列値 &#34;true&#34; または &#34;false&#34;（デフォルト：&#34;true&#34;） | [`&#34;true&#34;`, `&#34;false&#34;`]                                                                                                                                                     |
| `collectDispatchURL`     | `String` | Tealium CollectエンドポイントのURLをオーバーライド                                             | `&#34;https: //collect. tealiumiq.com/ vdata/i.gif ?tealium_account =companyXYZ &amp;tealium_profile =main&#34;`                                                                      |
| `collectDispatchProfile` | `String` | Tealium Collectエンドポイントで使用するプロファイルを構成                                     | `&#34;cordova-demo&#34;`                                                                                                                                                          |
| `isCrashReporterEnabled` | `String` | （オプション、Androidのみ）クラッシュレポート（未捕捉例外ハンドラー）を有効にする        | [`&#34;true&#34;`, `&#34;false&#34;`]                                                                                                                                                     |
| `logLevel`               | `String` | （オプション）ログレベルを構成（デフォルトは環境に依存）                                | `tealium.logLevels.DEV`（情報、警告、エラー）、`tealium.logLevels.QA`（警告、エラー）、`tealium.logLevels.PROD`（エラーのみ）、`tealium.logLevels.SILENT`（ログなし） |
| `dataSourceId`           | `String` | （オプション）データソースキー                                                             | &#34;abc123&#34;                                                                                                                                                                  |

### `getPersistent()`

Tealiumの永続データから値を返します。JavaScript側で要求されたデータが見つからない場合は`null`を返します。

```javascript
tealium.getPersistent(key, instance, callback);
```

| パラメータ  | タイプ       | 説明                                                                     | 例               |
|:-----------|:-----------|:--------------------------------------------------------------------------------|:----------------------|
| `key`      | `String`   | 永続保存から取得する値のキー名                       | `&#34;user_hashed_email&#34;` |
| `instance` | `String`   | 特定のトラッキングインスタンスを参照するための任意のインスタンス名 | `&#34;tealium_main&#34;`      |
| `callback` | `Function` | 永続保存から要求された値を返すコールバックオブジェクト       | `null`                |

### `getVisitorID()`

現在のユーザーのTealium訪問IDを返します。

| 戻り値            | 戻り値のタイプ |
|:-------------------|:------------|
| 現在の訪問ID | `String`    |

### `getVolatile()`

Tealiumの揮発性データストアから値を返します。JavaScript側で要求されたデータが見つからない場合は`null`を返します。

```javascript
tealium.getVolatile(key, instance, callback);
```

| パラメータ  | タイプ       | 説明                                                                     | 例               |
|:-----------|:-----------|:--------------------------------------------------------------------------------|:----------------------|
| `key`      | `String`   | 揮発性保存から取得する値のキー名                         | `&#34;user_hashed_email&#34;` |
| `instance` | `String`   | 特定のトラッキングインスタンスを参照するための任意のインスタンス名 | `&#34;tealium_main&#34;`      |
| `callback` | `Function` | 永続保存から要求された値を返すコールバックオブジェクト       | `null`                |

### `removePersistent()`

Tealiumの永続データストアから永続データを削除します。

```javascript
tealium.removePersistent(key, instance);
```

| パラメータ  | タイプ     | 説明                                                                     | 例               |
|:-----------|:---------|:--------------------------------------------------------------------------------|:----------------------|
| `key`      | `String` | 永続保存から削除する値のキー名                         | `&#34;user_hashed_email&#34;` |
| `instance` | `String` | 特定のトラッキングインスタンスを参照するための任意のインスタンス名 | `&#34;tealium_main&#34;`      |

### `removeVolatile()`

Tealiumの揮発性データストアから揮発性データを削除します。

```javascript
tealium.removeVolatile(key, instance);
```

| パラメータ  | タイプ     | 説明                                                                     | 例               |
|:-----------|:---------|:--------------------------------------------------------------------------------|:----------------------|
| `key`      | `String` | 揮発性メモリから削除する値のキー名                            | `&#34;user_hashed_email&#34;` |
| `instance` | `String` | 特定のトラッキングインスタンスを参照するための任意のインスタンス名 | `&#34;tealium_main&#34;`      |
### `track()`

ビューを追跡するには、最初の引数タイプとして `&#34;view&#34;` を渡し、イベントを追跡するには `&#34;link&#34;` を渡します。

```js
tealium.track(type, data, instance);
```

| パラメータ  | タイプ                   | 説明                                                                        | 例                               |
|:-----------|:-----------------------|:----------------------------------------------------------------------------|:--------------------------------|
| `type`     | `String`               | Tealium イベントタイプ名 - `&#34;link&#34;` (イベント) または `&#34;view&#34;` (画面ビュー) | [`&#34;link&#34;`, `&#34;view&#34;`]            |
| `data`     | JavaScript/JSON オブジェクト | このトラッキングコールのデータレイヤーを指定されたキーバリューペアで構成します | `{&#34;tealium_event&#34; : &#34;page_view&#34;}` |
| `instance` | `String`               | Tealium インスタンス名 - 特定のトラッキングインスタンスを指します           | `&#34;tealium_main&#34;`                |

### `trackEvent()`

ビュー以外のすべてのアクティビティを追跡します。

```js
tealium.trackEvent(data, instance);
```

| パラメータ  | タイプ                   | 説明                                                   | 例                             |
|:-----------|:-----------------------|:------------------------------------------------------|:--------------------------------|
| `data`     | JavaScript/JSON オブジェクト | イベントデータをキーバリューペアで指定します           | `{&#34;tealium_event&#34;: &#34;cart_add&#34;}` |
| `instance` | `String`               | Tealium インスタンス名 - 特定のトラッキングインスタンスを指します | `&#34;tealium_main&#34;`                |

### `trackView()`

アプリでユーザーが画面を開いたり変更したりするたびに追跡します。

```js
tealium.trackView(data, instance);
```

| パラメータ  | タイプ                   | 説明                   | 例                                                         |
|:-----------|:-----------------------|:----------------------|:------------------------------------------------------------|
| `data`     | JavaScript/JSON オブジェクト | ビューデータをキーバリューペアで指定します | `{tealium_event:&#34;screen_view&#34;, &#34;screen_name&#34;:&#34;Homescreen&#34;}` |
| `instance` | `String`               | Tealium インスタンス名         | `&#34;tealium_main&#34;`                                            |