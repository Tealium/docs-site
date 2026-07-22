---
title: APIリファレンス
description: TealiumがPython向けに提供するクラスとメソッドのリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/python/api/
---

## クラス: `Tealium`

以下は、Pythonライブラリの`Tealium`クラスの一般的に使用されるメソッドをまとめたものです。

| メソッド | 説明 |
| ----- | ------ |
| `Tealium()` | イベントを追跡するために使用される`Tealium`オブジェクトを作成するコンストラクタ |
| `trackEvent()` | データとコールバックのオプションパラメータを持つイベントを追跡します |

### `Tealium()`

イベントを追跡するために使用される`Tealium`オブジェクトを作成します。

```python
Tealium(account, profile, environment, path, datasource)
```

| パラメータ | タイプ | 説明 | 例 |
| --- | --- | --- | --- |
| `account` | `String` |Tealiumのアカウント名 |  `"companyXYZ"` |
| `profile` | `String` |Tealiumのプロファイル名 |  `"main"`  |
| `environment` | `String` |Tealiumの環境名 | `"prod"`|
| `datasource`  | `String` |(オプション) データソースキー（PATHが省略された場合は必須）  | `"abc123"` |

### `trackEvent()`

データとコールバックのオプションパラメータを持つイベントを追跡します。

```python
trackEvent(title, data, callback)
```

| パラメータ | タイプ | 説明 | 例 |
|-----------| ---- | -------------| --- |
| `title`   | `String` | イベントを識別する名前、例えば`user_login`変数など | `"test"` |
| `data`    | `Dictionary` | (オプション) イベントデータをキーと値のペアとして持つオブジェクト | `{"foo": "bar", "tealium_visitor_id": "1234567890"}` |
| `callback`| `Dictionary`   | (オプション) "callback"キーに関数が割り当てられたオブジェクト | `callback = self.tealiumCallback` |
