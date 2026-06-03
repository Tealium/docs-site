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
| `data` | JSONオブジェクト | キーと値のペアとしてのページビューデータ | `{&#34;tealium_event&#34; : &#34;user_login&#34;, &#34;customer_id&#34; : &#34;0123456789&#34;}` |

### `setConfig()`

`utag.js` ファイルへのパスを構築するために使用される構成。

```javascript
setConfig(config : {account, profile, environment})
```

| パラメータ | タイプ | 説明 | 例 |
| --- | --- | --- | --- |
| `account` | `string` | Tealiumのアカウント名 | `&#34;companyXYZ&#34;` |
| `profile` | `string` | Tealiumのプロファイル名 | `&#34;main&#34; ` |
| `environment` | `string` | Tealiumの環境名 | [`&#34;dev&#34;`, `&#34;qa&#34;`, `&#34;prod&#34;`] |

### `view()`

ページビューを追跡します。

```javascript
view(data? : any)
```

| パラメータ | タイプ | 説明 | 例 |
| --- | --- | --- | --- |
| `data` | JSONオブジェクト | キーと値のペアとしてのイベントデータ | `{&#34;tealium_event&#34; : &#34;product_view&#34;, &#34;page_type&#34; : &#34;product&#34;, &#34;product_id&#34; : [&#34;PROD123&#34;]}` |
