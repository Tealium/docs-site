---
title: APIリファレンス
description: Tealium for Rokuで提供されているクラスとメソッドに関するリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/roku/api/
---以下では、Tealium for Rokuライブラリで提供されている関数を示します。Roku用アプリは、強力なスクリプト言語であるBrightScriptで作成されています。BrightScriptの詳細については、[こちら](https://sdkdocs.roku.com/display/sdkdoc/BrightScript+Language+Reference)を参照してください。

## クラス：`TealiumBuilder`

以下は、Rokuライブラリで一般的に使用される`TealiumBuilder`クラスのメソッドをまとめたものです。

| メソッド | 説明|
| ----- | ------|
| `SetDatasource()` | `Tealium`オブジェクトのデータソースキーを構成します|
| `SetEnvironment()` | `Tealium`オブジェクトの環境を構成します|
| `SetLogLevel()` | `Tealium`オブジェクトのログレベルを構成します|
| `TealiumBuilder()` | `Tealium`オブジェクトの初期化に役立つビルダーコンストラクタ関数|

### `SetDatasource()`

`Tealium`オブジェクトのデータソースキーを構成します。

```javascript
SetDatasource(datasource)
```

| パラメータ | 型| 説明| 例|
| --- | ---| --- | --- |
| `datasource` | `String` | データソースキー| "def456"|


### `SetEnvironment()`

`Tealium`オブジェクトの環境を構成します。

```javascript
SetEnvironment(environment)
```

| パラメータ | 型| 説明| 例|
| --- | ---| --- | --- |
| `environment` | `String` | Tealium環境の名前| [`"dev"`, `"qa"`, `"prod"`]|

### `SetLogLevel()`

`Tealium`オブジェクトのログレベルを構成します。

```javascript
SetLogLevel(logLevel)
```

| パラメータ | 型| 説明| 例|
| --- | ---| --- | --- |
| `logLevel`  | 整数| Tealiumログレベル| `1` |


### `TealiumBuilder()`

`Tealium`オブジェクトの初期化に役立つビルダー関数。ユーティリティ関数を使って任意のパラメータを構成します。Build()を呼び出してTealiumオブジェクトを作成します。

```javascript
TealiumBuilder(account, profile, logLevel)
```

| パラメータ | 型| 説明| 例|
| --- | ---| --- | --- |
| `account` | `String` | Tealiumアカウントの名前| `"account123"` |
| `profile` | `String` | Tealiumプロファイルの名前（デフォルト：`"main"`）| `"main"` |
| `logLevel` | `String` | ログレベル| `1` |


## クラス：`TealiumCore`

以下は、Rokuライブラリで一般的に使用される`TealiumCore`クラスのメソッドをまとめたものです。

| メソッド | 説明|
| ----- | ------|
| `ToStr()` | 現在のTealiumインスタンスの構成の詳細を含む判読可能な文字列を返します|
| `TrackEvent()` | 関連付けられたデータを含むイベントをトラッキングし、任意でコールバック関数をトリガーします|
| `ResetSessionId()` | リセットして新しいセッションIDを返します|

### `ToStr()`
現在のTealiumインスタンスの構成の詳細を含む判読可能な文字列を返します。

```javascript
ToStr()
```

| 戻り値 | 戻り値の型| 例|
| --- | ---| --- |
| Readable String containing the configuration details of the current Tealium instance | `String` | `"Tealium instance for account: ACCOUNT profile: PROFILE environment: ENV"` |


### `TrackEvent()`

関連付けられたデータを含むイベントをトラッキングし、任意でコールバック関数をトリガーします。

```javascript
trackEvent(eventType, eventName, data, callback)
```

| パラメータ | 型| 説明|
| --- | ---| --- |
| `eventType` | `String` | Tealiumのイベントの種類（アクティビティ、コンバージョン、インタラクション、ビュー）|
| `eventName` | `String` | イベントの名前（Tealium Customer Data Hubの`event_name`属性になります）|
| `data` | `Object` | コンテクスチュアルイベントデータである、キーと値のペアを含む`roAssociativeArray`オブジェクト|
| `callback` | `Object` | `roEvent`引数を受け取る"callback"という名前の関数プロパティを持つオブジェクト。このコールバック関数は、TrackEventコールの完了時にトリガーされます。|

コールバック関数は、以下を含む複数の目的で使用されます。

*   コール失敗時のリトライまたはフォールバックシステムの構築
*   キューイングまたはスロットリングシステムの管理
*   Loggerのカスタマイズ
*   アプリケーションロジックのチェーン

### `ResetSessionId()`

リセットして新しいセッションIDを返します。このセッションIDは、ウェブサイトセッションと同様に、現在のユーザーセッションを識別しますが、有効期限がありません。`createTealium()`が呼び出されるたびに、新しいセッションIDが作成されます。 

```javascript
resetSessionId() as Integer
```
| 戻り値 | 戻り値の型|
| --- | ---|
| A new session ID | `Integer` |
