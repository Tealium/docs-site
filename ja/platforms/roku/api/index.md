---
title: APIリファレンス
description: Roku向けにTealiumが提供するクラスとメソッドのリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/roku/api/
---
以下に、Tealium for Rokuライブラリで使用できる関数を示します。Roku向けアプリは、強力なスクリプト言語であるBrightScriptで記述されます。BrightScriptの詳細については、[こちら](https://sdkdocs.roku.com/display/sdkdoc/BrightScript+Language+Reference)を参照してください。

## クラス：`TealiumBuilder`

以下に、Rokuライブラリの`TealiumBuilder`クラスで一般的に使用されるメソッドの概要を示します。

| メソッド | 説明 |
| ----- | ------ |
| `SetDatasource()` | `Tealium`オブジェクトのデータソースキーを構成します。 |
| `SetEnvironment()` | `Tealium`オブジェクトの環境を構成します。|
| `SetLogLevel()` | `Tealium`オブジェクトのログレベルを構成します。|
| `TealiumBuilder()` | `Tealium`オブジェクトの初期化を支援するビルダーコンストラクター関数です。 |

### `SetDatasource()`

`Tealium`オブジェクトのデータソースキーを構成します。

```javascript
SetDatasource(datasource)
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `datasource` | String | データソースキー | `"def456"` |

### `SetEnvironment()`

`Tealium`オブジェクトの環境を構成します。

```javascript
SetEnvironment(environment)
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `environment` | String | Tealium環境名 | [`"dev"`, `"qa"`, `"prod"`] |

### `SetLogLevel()`

`Tealium`オブジェクトのログレベルを構成します。

```javascript
SetLogLevel(logLevel)
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `logLevel`  | Integer | Tealiumのログレベル | `1` |

### `TealiumBuilder()`

`Tealium`オブジェクトの初期化を支援するビルダー関数です。ユーティリティ関数を使用して、任意のパラメータを構成します。`Build()`を呼び出してTealiumオブジェクトを作成します。

```javascript
TealiumBuilder(account, profile, logLevel)
```

| パラメータ | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| `account` | String | Tealiumアカウント名 | `"account123"` |
| `profile` | String | Tealiumプロファイル名（デフォルト：`"main"`） | `"main"` |
| `logLevel` | String | ログレベル | `1` |

## クラス：`TealiumCore`

以下に、Rokuライブラリの`TealiumCore`クラスで一般的に使用されるメソッドの概要を示します。

| メソッド | 説明 |
| ----- | ------ |
| `ToStr()` | 現在のTealiumインスタンスの構成詳細を含む読み取り可能な文字列を返します。 |
| `TrackEvent()` | 関連データを伴うイベントをトラッキングし、必要に応じてコールバック関数をトリガーします。 |
| `ResetSessionId()` | セッションIDをリセットし、新しいセッションIDを返します。 |

### `ToStr()`

現在のTealiumインスタンスの構成詳細を含む、人間が読み取り可能な文字列を返します。

```javascript
ToStr()
```

| 戻り値 | 戻り値の型 | 例 |
| --- | --- | --- |
| 現在のTealiumインスタンスの構成詳細を含む、人間が読み取り可能な文字列。 | String | `"Tealium instance for account: ACCOUNT profile: PROFILE environment: ENV"` |

### `TrackEvent()`

関連データを伴うイベントをトラッキングし、必要に応じてコールバック関数をトリガーします。

```javascript
trackEvent(eventType, title, data)
```

| パラメータ | 型 | 説明 |
| --- | --- | --- |
| `eventType` | String | Tealiumイベントタイプ（`activity`、`conversion`、`derived`、`interaction`、または`view`）。 |
| `eventName` | String | イベント名（Tealium Customer Data Hubでは`event_name`属性になります）。 |
| `data` | Object | コンテキストイベントデータ。キーと値のペアを含む`roAssociativeArray`オブジェクトです。|

### `ResetSessionId()`

セッションIDをリセットし、新しいセッションIDを返します。セッションIDは、Webサイトのセッションと同様に現在のユーザーセッションを識別しますが、有効期限はありません。`createTealium()`が呼び出されるたびに、新しいセッションIDが作成されます。

```javascript
resetSessionId() as Integer
```
| 戻り値 | 戻り値の型 |
| --- | --- |
| 新しいセッションID | Integer |