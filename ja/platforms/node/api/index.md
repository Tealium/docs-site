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
| `config` | var| キーと値のペアとしてのTealium構成オブジェクトデータ| `{&#34;account&#34;:&#34;ACCOUNT&#34;, &#34;profile&#34;:&#34;PROFILE&#34;, &#34;datasource&#34;:&#34;DATASOURCE&#34;};` |

`config`オブジェクトパラメータには次のキーと値のペアがあります

| パラメータ | 型| 説明| 例
|-----------|------| --- | --- |
| `account` |  `String` |  Tealiumプロファイルの名前| `&#34;companyXYZ&#34;` |
| `profile` | `String`| Tealiumプロファイルの名前| `&#34;main&#34;` |
| `datasource` | `String` | （オプション）データソースキー| `&#34;abc123&#34;` |
### `track()`

ビューとイベントをトラッキングします。

```javascript
tealium.track(event, data); 
```

| パラメータ | 型| 説明| 例|
| --- |  ---| --- | --- |
| `event` | `String` | イベントの名前（`tealium_event`の値を構成）| `&#34;event&#34;` |
| `data` | `Dictionary` | キーと値のペアとしてのイベントデータを持つオブジェクト| `{&#34;some_key&#34;: &#34;some_value&#34;}` |
