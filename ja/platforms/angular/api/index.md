---
title: APIリファレンス
description: TealiumがAngular向けに提供するクラスとメソッドのリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/angular/api/
---
## クラス: `Tealium`

以下は、Angularの `Tealium` クラスの一般的に使用されるメソッドをまとめたものです。

| メソッド | 説明 |
| ----- | ------ |
| `link()` | ページ内イベントを追跡 |
| `setConfig()` | `utag.js` ファイルへのパスを構築するために使用される構成 |
| `view()` | ページビューを追跡 |


### `link()`

ページ内イベントを追跡します。

```javascript
link(data? : any)
```

| パラメータ | タイプ | 説明 | 例 |
| --- | --- | --- | --- |
| `data` | JSONオブジェクト | キーと値のペアとしてのページビューデータ | `{"tealium_event" : "user_login", "customer_id" : "0123456789"}` |

### `setConfig()`

`utag.js` ファイルへのパスを構築するために使用される構成。

```javascript
setConfig(config : {account, profile, environment})
```

| パラメータ | タイプ | 説明 | 例 |
| --- | --- | --- | --- |
| `account` | `string` | Tealiumのアカウント名 | `"companyXYZ"` |
| `profile` | `string` | Tealiumのプロファイル名 | `"main" ` |
| `environment` | `string` | Tealiumの環境名 | [`"dev"`, `"qa"`, `"prod"`] |

### `view()`

ページビューを追跡します。

```javascript
view(data? : any)
```

| パラメータ | タイプ | 説明 | 例 |
| --- | --- | --- | --- |
| `data` | JSONオブジェクト | キーと値のペアとしてのイベントデータ | `{"tealium_event" : "product_view", "page_type" : "product", "product_id" : ["PROD123"]}` |
