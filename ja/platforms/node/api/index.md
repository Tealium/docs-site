---
title: APIリファレンス
description: Tealium for Nodeで提供されているクラスとメソッドに関するリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/node/api/
---

## クラス：`Tealium`

以下は、Nodeライブラリで一般的に使用される`Tealium`クラスのメソッドをまとめたものです。

| メソッド | 説明|
| ----- | ------|
| `addModule()` | モジュールを追加します|
| `Tealium()`| Tealiumインスタンスを構築するためのコンストラクタ|
| `track()` | ビューとイベントをトラッキングします|

### `addModule()`

Tealiumインスタンスにモジュールを追加します


```javascript
addModule(module)
```

| パラメータ | 型| 説明| 例
|-----------|------| --- | --- |
| `module` |  `var` |  モジュール名| `tealiumCollect` |

### `Tealium()`
Tealiumインスタンスを構築するためのコンストラクタ

```javascript
Tealium(config);
```

| パラメータ | 型| 説明| 例
|-----------|------| --- | --- |
| `config` | var| キーと値のペアとしてのTealium構成オブジェクトデータ| `{"account":"ACCOUNT", "profile":"PROFILE", "datasource":"DATASOURCE"};` |

`config`オブジェクトパラメータには次のキーと値のペアがあります

| パラメータ | 型| 説明| 例
|-----------|------| --- | --- |
| `account` |  `String` |  Tealiumプロファイルの名前| `"companyXYZ"` |
| `profile` | `String`| Tealiumプロファイルの名前| `"main"` |
| `datasource` | `String` | （オプション）データソースキー| `"abc123"` |
### `track()`

ビューとイベントをトラッキングします。

```javascript
tealium.track(event, data); 
```

| パラメータ | 型| 説明| 例|
| --- |  ---| --- | --- |
| `event` | `String` | イベントの名前（`tealium_event`の値を構成）| `"event"` |
| `data` | `Dictionary` | キーと値のペアとしてのイベントデータを持つオブジェクト| `{"some_key": "some_value"}` |
