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
| `account` | `String` |Tealiumのアカウント名 |  `&#34;companyXYZ&#34;` |
| `profile` | `String` |Tealiumのプロファイル名 |  `&#34;main&#34;`  |
| `environment` | `String` |Tealiumの環境名 | `&#34;prod&#34;`|
| `datasource`  | `String` |(オプション) データソースキー（PATHが省略された場合は必須）  | `&#34;abc123&#34;` |

### `trackEvent()`

データとコールバックのオプションパラメータを持つイベントを追跡します。

```python
trackEvent(title, data, callback)
```

| パラメータ | タイプ | 説明 | 例 |
|-----------| ---- | -------------| --- |
| `title`   | `String` | イベントを識別する名前、例えば`user_login`変数など | `&#34;test&#34;` |
| `data`    | `Dictionary` | (オプション) イベントデータをキーと値のペアとして持つオブジェクト | `{&#34;foo&#34;: &#34;bar&#34;, &#34;tealium_visitor_id&#34;: &#34;1234567890&#34;}` |
| `callback`| `Dictionary`   | (オプション) &#34;callback&#34;キーに関数が割り当てられたオブジェクト | `callback = self.tealiumCallback` |
