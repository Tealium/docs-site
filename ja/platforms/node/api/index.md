---
title: APIリファレンス
description: Node向けにTealiumが提供するクラスとメソッドのリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/node/api/
---

## クラス：`Tealium`

以下に、Nodeライブラリの`Tealium`クラスでよく使用されるメソッドの概要を示します。

| メソッド | 説明 |
| ----- | ------ |
| `addModule()` | モジュールを追加します |
| `Tealium()` | Tealiumインスタンスを作成するコンストラクターです |
| `track()` | ビューとイベントをトラッキングします |

### `addModule()`

Tealiumインスタンスにモジュールを追加します。


```javascript
addModule(module)
```

| パラメーター | 型 | 説明 | 例
|-----------|------| --- | --- |
| `module` | `var` | モジュール名 | `tealiumCollect` |

### `Tealium()`

Tealiumインスタンスを作成するコンストラクターです。

```javascript
Tealium(config);
```

| パラメーター | 型 | 説明 | 例
|-----------|------| --- | --- |
| `config` | var | キーと値のペアで構成されたTealium構成オブジェクトのデータ | `{"account":"ACCOUNT", "profile":"PROFILE", "datasource":"DATASOURCE"};` |

`config`オブジェクトのパラメーターには、以下のキーと値のペアがあります。

| パラメーター | 型 | 説明 | 例
|-----------|------| --- | --- |
| `account` | `String` | Tealiumプロファイル名 | `"companyXYZ"` |
| `profile` | `String` | Tealiumプロファイル名 | `"main"` |
| `datasource` | `String` | （任意）データソースキー | `"abc123"` |

### `track()`

ビューとイベントをトラッキングします。

```javascript
tealium.track(event, data); 
```

| パラメーター | 型 | 説明 | 例 |
| --- |  --- | --- | --- |
| `event` | `String` | イベント名（`tealium_event`の値を構成） | `"event"` |
| `data` | `Dictionary` | キーと値のペアで構成されたイベントデータを含むオブジェクト | `{"some_key": "some_value"}` |