---
title: API リファレンス
description: TealiumのCordova用クラスとメソッドのリファレンスガイドです。
url: https://docs.tealium.com/ja/platforms/cordova-v1/api/
---

<blockquote>
これはTealiumのCordova用の以前のバージョン（1.x）です。  
現在のバージョンについては、[TealiumのCordova 2.x](https://docs.tealium.com/ja/platforms/cordova/)を参照してください。
</blockquote>


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
| `track()`            | 最初の引数タイプとして`"view"`を渡すことでビューを追跡、または`"link"`を渡すことでイベントを追跡します                     |
| `trackEvent()`       | ビュー以外のすべてのアクティビティを追跡します                                                                             |
| `trackView()`        | アプリ内でユーザーが画面を開いたり変更したりするたびに追跡します                                                           |


### `addPersistent()`

Tealiumの永続データストアに永続データを追加します。

```javascript
tealium.addPersistent(key, data, instance);
```

| パラメータ  | タイプ                   | 説明                                                                     | 例                           |
|:-----------|:-----------------------|:--------------------------------------------------------------------------------|:----------------------------------|
| `key`      | `String`               | 永続化される値のキー名                                               | `"user_hashed_email"`             |
| `data`     | `String` or `[String]` | このキーに対して永続化される値                                          | `["testpersist", "testpersist2"]` |
| `instance` | `String`               | 特定のトラッキングインスタンスを参照するために使用される任意のインスタンス名 | `"tealium_main"`                  |

### `addVolatile()`

Tealiumの揮発性データストアにデータを追加します。

```javascript
tealium.addVolatile(key, data, instance);
```

| パラメータ  | タイプ                   | 説明                                                                     | 例                              |
|:-----------|:-----------------------|:--------------------------------------------------------------------------------|:-------------------------------------|
| `key`      | `String`               | 永続化される値のキー名                                               | `"user_hashed_email"`                |
| `data`     | `String` or `[String]` | このキーに対して永続化される値                                          | `["testvolatile1", "testvolatile2"]` |
| `instance` | `String`               | 特定のトラッキングインスタンスを参照するために使用される任意のインスタンス名 | `"tealium_main"`                     |
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
| `account`                | `String` | Tealiumのアカウント名                                                                       | `"companyXYZ"`                                                                                                                                                            |
| `profile`                | `String` | Tealiumのプロファイル名                                                                       | `"main"`                                                                                                                                                                  |
| `environment`            | `String` | Tealiumの環境名                                                                   | [`"dev"`, `"qa"`, `"prod"`]                                                                                                                                               |
| `instance`               | `String` | Tealiumのインスタンス名（複数インスタンス対応）                                       | `"tealium_main"`                                                                                                                                                           |
| `isLifecycleEnabled`     | `String` | （オプション）ライフサイクル追跡を有効にするための文字列値 "true" または "false"（デフォルト："true"） | [`"true"`, `"false"`]                                                                                                                                                     |
| `collectDispatchURL`     | `String` | Tealium CollectエンドポイントのURLをオーバーライド                                             | `"https: //collect. tealiumiq.com/ vdata/i.gif ?tealium_account =companyXYZ &tealium_profile =main"`                                                                      |
| `collectDispatchProfile` | `String` | Tealium Collectエンドポイントで使用するプロファイルを構成                                     | `"cordova-demo"`                                                                                                                                                          |
| `isCrashReporterEnabled` | `String` | （オプション、Androidのみ）クラッシュレポート（未捕捉例外ハンドラー）を有効にする        | [`"true"`, `"false"`]                                                                                                                                                     |
| `logLevel`               | `String` | （オプション）ログレベルを構成（デフォルトは環境に依存）                                | `tealium.logLevels.DEV`（情報、警告、エラー）、`tealium.logLevels.QA`（警告、エラー）、`tealium.logLevels.PROD`（エラーのみ）、`tealium.logLevels.SILENT`（ログなし） |
| `dataSourceId`           | `String` | （オプション）データソースキー                                                             | "abc123"                                                                                                                                                                  |

### `getPersistent()`

Tealiumの永続データから値を返します。JavaScript側で要求されたデータが見つからない場合は`null`を返します。

```javascript
tealium.getPersistent(key, instance, callback);
```

| パラメータ  | タイプ       | 説明                                                                     | 例               |
|:-----------|:-----------|:--------------------------------------------------------------------------------|:----------------------|
| `key`      | `String`   | 永続保存から取得する値のキー名                       | `"user_hashed_email"` |
| `instance` | `String`   | 特定のトラッキングインスタンスを参照するための任意のインスタンス名 | `"tealium_main"`      |
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
| `key`      | `String`   | 揮発性保存から取得する値のキー名                         | `"user_hashed_email"` |
| `instance` | `String`   | 特定のトラッキングインスタンスを参照するための任意のインスタンス名 | `"tealium_main"`      |
| `callback` | `Function` | 永続保存から要求された値を返すコールバックオブジェクト       | `null`                |

### `removePersistent()`

Tealiumの永続データストアから永続データを削除します。

```javascript
tealium.removePersistent(key, instance);
```

| パラメータ  | タイプ     | 説明                                                                     | 例               |
|:-----------|:---------|:--------------------------------------------------------------------------------|:----------------------|
| `key`      | `String` | 永続保存から削除する値のキー名                         | `"user_hashed_email"` |
| `instance` | `String` | 特定のトラッキングインスタンスを参照するための任意のインスタンス名 | `"tealium_main"`      |

### `removeVolatile()`

Tealiumの揮発性データストアから揮発性データを削除します。

```javascript
tealium.removeVolatile(key, instance);
```

| パラメータ  | タイプ     | 説明                                                                     | 例               |
|:-----------|:---------|:--------------------------------------------------------------------------------|:----------------------|
| `key`      | `String` | 揮発性メモリから削除する値のキー名                            | `"user_hashed_email"` |
| `instance` | `String` | 特定のトラッキングインスタンスを参照するための任意のインスタンス名 | `"tealium_main"`      |
### `track()`

ビューを追跡するには、最初の引数タイプとして `"view"` を渡し、イベントを追跡するには `"link"` を渡します。

```js
tealium.track(type, data, instance);
```

| パラメータ  | タイプ                   | 説明                                                                        | 例                               |
|:-----------|:-----------------------|:----------------------------------------------------------------------------|:--------------------------------|
| `type`     | `String`               | Tealium イベントタイプ名 - `"link"` (イベント) または `"view"` (画面ビュー) | [`"link"`, `"view"`]            |
| `data`     | JavaScript/JSON オブジェクト | このトラッキングコールのデータレイヤーを指定されたキーバリューペアで構成します | `{"tealium_event" : "page_view"}` |
| `instance` | `String`               | Tealium インスタンス名 - 特定のトラッキングインスタンスを指します           | `"tealium_main"`                |

### `trackEvent()`

ビュー以外のすべてのアクティビティを追跡します。

```js
tealium.trackEvent(data, instance);
```

| パラメータ  | タイプ                   | 説明                                                   | 例                             |
|:-----------|:-----------------------|:------------------------------------------------------|:--------------------------------|
| `data`     | JavaScript/JSON オブジェクト | イベントデータをキーバリューペアで指定します           | `{"tealium_event": "cart_add"}` |
| `instance` | `String`               | Tealium インスタンス名 - 特定のトラッキングインスタンスを指します | `"tealium_main"`                |

### `trackView()`

アプリでユーザーが画面を開いたり変更したりするたびに追跡します。

```js
tealium.trackView(data, instance);
```

| パラメータ  | タイプ                   | 説明                   | 例                                                         |
|:-----------|:-----------------------|:----------------------|:------------------------------------------------------------|
| `data`     | JavaScript/JSON オブジェクト | ビューデータをキーバリューペアで指定します | `{tealium_event:"screen_view", "screen_name":"Homescreen"}` |
| `instance` | `String`               | Tealium インスタンス名         | `"tealium_main"`                                            |