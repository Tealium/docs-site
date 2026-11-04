---
title: データレイヤー
description: Google タグマネージャーのマーケットプレイスにある Collect タグで使用できる、組み込み（自動）データレイヤー変数について説明します。
url: https://docs.tealium.com/ja/platforms/google-tag-manager/data-layer/
---
データレイヤーには、トラッキング対象のページに関する基本情報を収集する組み込み変数が含まれています。これらの変数には、Cookie、ページの標準 DOM 変数、読み込まれた構成に関する Tealium 固有の変数が含まれます。

利用可能なデータレイヤー変数の種類については、[詳細](https://docs.tealium.com/data-layer-variables/)を参照してください。


## 標準ページデータ

以下の変数は、Web ページで使用可能な標準 JavaScript プロパティから生成されます。

以下に示す値の例は、次のページ URL に基づいています。

`http://www.example.com/path/file.html?param1=value1#hash=fragment`

| 変数                  | 説明                                                                                                           | 例                                                                  |
|:----------------------|:---------------------------------------------------------------------------------------------------------------|:--------------------------------------------------------------------|
| `dom.domain`          | URL の完全なドメイン。ソース: location.hostname                                                                | `www.example.com`                                                   |
| `dom.hash`            | URL のハッシュフラグメント（# 文字を除く）。ソース: location.hash                                               | `hash=fragment`                                                     |
| `dom.pathname`        | クエリパラメータとドメインを除いた URL のパス。ソース: location.pathname                                        | `"/path/file.html"`                                                 |
| `dom.query_string`    | URL の完全なクエリ文字列。ソース: location.search                                                              | `param1=value1`                                                     |
| `dom.referrer`        | 前のページの URL。ソース: document.referrer                                                                    |                                                                     |
| `dom.title`           | &lt;title&gt; タグ内のテキスト。ソース: document.title                                                         | `"Page Title" `                                                     |
| `dom.url`             | ページの完全な URL。ソース: document.URL                                                                       | `http://www.example.com/ PATH/FILE.html?param1=VALUE#hash=FRAGMENT` |
| `dom.viewport_height` | ブラウザーのビューポートの高さ。ソース: window.innerHeight または document.documentElement.clientHeight         | `1320`                                                              |
| `dom.viewport_width`  | ブラウザーのビューポートの幅。ソース: window.innerWidth または document.documentElement.clientWidth             | `1278`                                                              |

## Cookie

以下の変数は、`TEAL` という名前の単一の Cookie に保存され、管理されます。それぞれが `TEAL` オブジェクト内の変数です。

| 変数                            | 説明                                                               | 例              |
|:--------------------------------|:-------------------------------------------------------------------|:----------------|
| `tealium)_session_event_number` | 現在のセッションにおけるイベント数。                               | `2`             |
| `tealium_session_number`        | この一意の訪問のセッション数。                                   | `1`             |
| `tealium_session_id`            | セッションの一意の識別子。                                         | `1628542077230` |
| `tealium_visitor_id`            | 訪問の一意の識別子。40 文字以上になる場合があります。             | `016297481...`  |

以下は、TEAL Cookie の document.cookie 形式の例です。変数値が `$` 文字で区切られています。

`TEAL=v:927b2ebc092a70110329356772472215264145f9fa1$t:1628543914615$s:1628542077230%3Bexp-sess$sn:1$en:3`

## Tealium データ

| 変数                    | 名前                              | 例                       |
|:------------------------|:----------------------------------|:-------------------------|
| tealium_account         | アカウント名                      | sandbox                  |
| tealium_datasource      | データソースキー                  | abc123                   |
| tealium_environment     | パブリッシュ環境                  | prod                     |
| tealium_event           | Tealium イベント名                | my_event                 |
| tealium_library_name    | ライブラリ名                      | tealium.js               |
| tealium_library_version | ライブラリバージョン              | 5.0.3                    |
| tealium_profile         | アカウントプロファイル            | main                     |
| tealium_random          | 乱数                              | 7782219645308327         |
| tealium_timestamp_epoch | 現在の Unix タイムスタンプ（秒）   | 1522956509               |
| tealium_timestamp_local | ローカルタイムスタンプ            | 2018-04-05T12:28:29.019  |
| tealium_timestamp_utc   | UTC タイムスタンプ                 | 2018-04-05T19:28:29.019z |
| tealium_cookie_domain   | TEAL Cookie が構成されるドメイン   | example.com              |
| tealium_domain          | Web サイトのドメイン              | example.com              |

## データの例

以下は、自動的に利用可能になる組み込みデータレイヤーの例です。

```
{
        "cp._ga": "GA1.2.1370368844.1628542067",
        "cp._gid": "GA1.2.73283117.1628542067",
        "tealium_session_number": 1,
        "tealium_session_event_number": 3,
        "tealium_session_id": "1628542077230",
        "tealium_visitor_id": "927b2ebc092a70110329356772472215264145f9fa1",
        "dom.referrer": "",
        "dom.title": "Example dot com",
        "dom.domain": "example.com",
        "dom.query_string": "",
        "dom.hash": "",
        "dom.url": "https://example.com/",
        "dom.pathname": "/",
        "dom.viewport_height": 936,
        "dom.viewport_width": 1517,
        "meta.description": "View",
        "meta.viewport": "width=device-width, initial-scale=1",
        "meta.theme-color": "#13B0E9",
        "tealium_cookie_domain": "example.com",
        "tealium_domain": "example.com",
        "tealium_event": "test event",
        "tealium_account": "xxxxxxxxxxxx",
        "tealium_profile": "main",
        "tealium_environment": "prod",
        "tealium_datasource": "test1234",
        "tealium_random": "9870188345895229",
        "tealium_library_name": "tealium.js",
        "tealium_library_version": "5.0.3",
        "tealium_timestamp_epoch": 1628542114,
        "tealium_timestamp_utc": "2021-08-09T20:48:34.616Z",
        "tealium_timestamp_local": "2021-08-09T13:48:34.616",
        "timing.domain": "example.com",
        "timing.pathname": "/",
        "timing.query_string": "",
        "timing.timestamp": 1628542085435,
        "timing.dns": 1,
        "timing.connect": 99,
        "timing.response": 0,
        "timing.dom_loading_to_interactive": 7,
        "timing.dom_interactive_to_complete": 129,
        "timing.load": 0,
        "timing.time_to_first_byte": 95,
        "timing.front_end": 163,
        "timing.fetch_to_response": 210,
        "timing.fetch_to_complete": 373,
        "timing.fetch_to_interactive": 244
}

```
## データレイヤー変数のフラット化

Google Tag Manager のイベントは、Tealium Customer Data Hub の仕様を満たすために、Tealium の属性名にフラット化されます。イベントデータは Event Streaming によって受信されます。

`tealium_event` の値は、`dataLayer.push` 呼び出し内の `event` の値です。Google Tag Manager は、デフォルトのページビュー値として、イベント名に `gtm.js` を構成します。このデフォルト値を上書きするには、Tealium Event 構成構成にイベント名を含む変数を構成します。


<blockquote>
属性は自動的には追加されません。Event Streaming でこれらの属性を追加する必要があります。
</blockquote>


## E コマース

次の購入イベントの例は、クライアント側の E コマースイベントがどのようにフラット化されるかを示しています。

```js
dataLayer.push({
  'ecommerce': {
    'purchase': {
      'actionField': {
        'id': 'T12345',    // Transaction ID. Required for purchases and refunds.
        'affiliation': 'Online Store',
        'revenue': '35.43',
        'tax':'4.90',
        'shipping': '5.99',
        'coupon': 'SUMMER_SALE'
      },
      'products': [{
        'name': 'Triblend Android T-Shirt',     // Name or ID is required.
        'id': '12345',
        'price': '15.25',
        'brand': 'Google',
        'category': 'Apparel',
        'variant': 'Gray',
        'quantity': 1,
        'coupon': ''
       },
       {
        'name': 'Donut Friday Scented T-Shirt',
        'id': '67890',
        'price': '33.75',
        'brand': 'Google',
        'category': 'Apparel',
        'variant': 'Black',
        'quantity': 1
       }]
    }
  }
});
```

フラット化後、購入イベントは次のようになります。

```js
"ecommerce.purchase.actionField.affiliation": "Online Store"
"ecommerce.purchase.actionField.coupon": "SUMMER_SALE"
"ecommerce.purchase.actionField.id": "T12345"
"ecommerce.purchase.actionField.revenue": "35.43"
"ecommerce.purchase.actionField.shipping": "5.99"
"ecommerce.purchase.actionField.tax": "4.90"
"ecommerce.purchase.products.brand": [ "Google", "Google" ]
"ecommerce.purchase.products.category": [ "Apparel", "Apparel" ]
"ecommerce.purchase.products.coupon": [ "", "" ]
"ecommerce.purchase.products.id": [ "12345", "67890" ]
"ecommerce.purchase.products.name": [ "Triblend Android T-Shirt", "Donut Friday Scented T-Shirt" ]
"ecommerce.purchase.products.price": [ "15.25", "33.75" ]
"ecommerce.purchase.products.variant": [ "Gray", "Black" ]
"ecommerce.purchase.products.quantity": [ "1", "1" ]
```

フラット化処理ではドット表記を使用してキーが作成され、値には購入イベントのすべての値を含む配列が構成されます。

## イベント

次の `dataLayer.push` コマンドは、データレイヤーに「event」が含まれている場合に実行されます。

```js
window.dataLayer.push({
  event: "test_number",
  type_number: 5,
  type_string: 'hello',
  type_object: { someKey: 'someValue' },
  type_array: [1,2,3,4],
  type_function: function() { return 'hello'; },
  type_boolean: true
});
```

Event Streaming に到達するデータレイヤーは次のようになります。`type_object` のみがフラット化され、関数は削除されます。

```
{
    "event": "test_number",
    "type_number": 5,
    "type_string": "hello",
    "type_object.someKey": "someValue",
    "type_array": [1, 2, 3, 4],
    "type_boolean": true
}
```