---
title: データレイヤー
description: Google Tag ManagerマーケットプレイスのCollectタグについて、組み込み（自動）データレイヤー変数を学びます。
url: https://docs.tealium.com/ja/platforms/google-tag-manager/data-layer/
---
データレイヤーには、追跡されているページに関する基本情報を収集する組み込み変数が含まれています。これらの変数には、クッキー、ページの標準DOM変数、ロードされた構成に関するTealium固有の変数が含まれます。

[詳しくはこちら](https://docs.tealium.com/data-layer-variables/)で、利用可能なデータレイヤー変数の種類について学びましょう。

## 標準ページデータ
以下の変数は、Webページで利用可能な標準JavaScriptプロパティから生成されます。

示されている例の値は、次のページURLに基づいています：

`http://www.example.com/path/file.html?param1=value1#hash=fragment`

| 変数                      | 説明                                                                                              | 例                                                                   |
|:--------------------------|:-------------------------------------------------------------------------------------------------|:--------------------------------------------------------------------|
| `dom.domain`              | URLの完全なドメイン。出典: location.hostname                                                    | `www.example.com`                                                   |
| `dom.hash`                | URLのハッシュフラグメント（#文字を除く）。出典: location.hash                                    | `hash=fragment`                                                     |
| `dom.pathname`            | クエリパラメータとドメインを除いたURLのパス。出典: location.pathname                            | `"/path/file.html"`                                                 |
| `dom.query_string`        | URLの完全なクエリ文字列。出典: location.search                                                  | `param1=value1`                                                     |
| `dom.referrer`            | 前のページのURL。出典: document.referrer                                                        |                                                                     |
| `dom.title`               | &lt;title&gt;タグのテキスト。出典: document.title                                                | `"Page Title" `                                                     |
| `dom.url`                 | ページの完全なURL。出典: document.URL                                                           | `http://www.example.com/ PATH/FILE.html?param1=VALUE#hash=FRAGMENT` |
| `dom.viewport_height`     | ブラウザビューポートの高さ。出典: window.innerHeightまたはdocument.documentElement.clientHeight | `1320`                                                              |
| `dom.viewport_width`      | ブラウザビューポートの幅。出典: window.innerWidthまたはdocument.documentElement.clientWidth    | `1278`                                                              |

## クッキー

以下の変数は、`TEAL`という名前の単一のクッキーに保存および維持されます。それぞれが`TEAL`オブジェクトの変数です。

| 変数                              | 説明                                                            | 例               |
|:----------------------------------|:---------------------------------------------------------------|:----------------|
| `tealium)_session_event_number`   | 現在のセッションのイベント数。                                   | `2`             |
| `tealium_session_number`          | このユニーク訪問のセッション数。                               | `1`             |
| `tealium_session_id`              | セッションのユニーク識別子。                                     | `1628542077230` |
| `tealium_visitor_id`              | 訪問のユニーク識別子。40文字以上の場合があります。             | `016297481...`  |

以下は、TEALクッキーのdocument.cookie形式の例であり、変数値が`$`文字で区切られて表示されます。

`TEAL=v:927b2ebc092a70110329356772472215264145f9fa1$t:1628543914615$s:1628542077230%3Bexp-sess$sn:1$en:3`

## Tealiumデータ

| 変数                        | 名称                              | 例                        |
|:----------------------------|:----------------------------------|:-------------------------|
| tealium_account             | アカウント名                      | sandbox                  |
| tealium_datasource          | データソースキー                   | abc123                   |
| tealium_environment         | 公開環境                          | prod                     |
| tealium_event               | Tealiumイベント名                  | my_event                 |
| tealium_library_name        | ライブラリ名                      | tealium.js               |
| tealium_library_version     | ライブラリバージョン               | 5.0.3                    |
| tealium_profile             | アカウントプロファイル             | main                     |
| tealium_random              | ランダム数                        | 7782219645308327         |
| tealium_timestamp_epoch     | 現在のUnixタイムスタンプ（秒）     | 1522956509               |
| tealium_timestamp_local     | ローカルタイムスタンプ             | 2018-04-05T12:28:29.019  |
| tealium_timestamp_utc       | UTCタイムスタンプ                  | 2018-04-05T19:28:29.019z |
| tealium_cookie_domain       | TEALクッキーが構成されているドメイン | example.com              |
| tealium_domain              | ウェブサイトのドメイン             | example.com              |

## 例示データ

以下は、自動的に利用可能な組み込みデータレイヤーの例です。

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

Google Tag Managerのイベントは、Tealium Customer Data Hubの仕様に合わせてTealium属性名にフラット化されます。イベントデータはTealium EventStreamによって受信されます。

`tealium_event`の値は、`dataLayer.push`コールの`event`の値です。Google Tag Managerはイベント名としてデフォルトのページビュー値を`gtm.js`に構成します。デフォルトを上書きするには、イベント名を含む変数をTealiumイベント構成に構成します。


<blockquote>
属性は自動的に追加されません。これらの属性をTealium EventStreamに追加する必要があります。
</blockquote>


## Eコマース

以下の購入イベントの例は、クライアントサイドのeコマースイベントがどのようにフラット化されるかを示しています。

```js
dataLayer.push({
  'ecommerce': {
    'purchase': {
      'actionField': {
        'id': 'T12345',    // トランザクションID。購入および払い戻しに必要です。
        'affiliation': 'オンラインストア',
        'revenue': '35.43',
        'tax':'4.90',
        'shipping': '5.99',
        'coupon': 'SUMMER_SALE'
      },
      'products': [{
        'name': 'トライブレンド アンドロイド Tシャツ',     // 名前またはIDが必要です。
        'id': '12345',
        'price': '15.25',
        'brand': 'Google',
        'category': 'アパレル',
        'variant': 'グレー',
        'quantity': 1,
        'coupon': ''
       },
       {
        'name': 'ドーナツフライデー香るTシャツ',
        'id': '67890',
        'price': '33.75',
        'brand': 'Google',
        'category': 'アパレル',
        'variant': 'ブラック',
        'quantity': 1
       }]
    }
  }
});
```
フラット化後、購入イベントは以下のようになります：

```js
"ecommerce.purchase.actionField.affiliation": "オンラインストア"
"ecommerce.purchase.actionField.coupon": "SUMMER_SALE"
"ecommerce.purchase.actionField.id": "T12345"
"ecommerce.purchase.actionField.revenue": "35.43"
"ecommerce.purchase.actionField.shipping": "5.99"
"ecommerce.purchase.actionField.tax": "4.90"
"ecommerce.purchase.products.brand": [ "Google", "Google" ]
"ecommerce.purchase.products.category": [ "アパレル", "アパレル" ]
"ecommerce.purchase.products.coupon": [ "", "" ]
"ecommerce.purchase.products.id": [ "12345", "67890" ]
"ecommerce.purchase.products.name": [ "トライブレンド アンドロイド Tシャツ", "ドーナツフライデー香るTシャツ" ]
"ecommerce.purchase.products.price": [ "15.25", "33.75" ]
"ecommerce.purchase.products.variant": [ "グレー", "ブラック" ]
"ecommerce.purchase.products.quantity": [ "1", "1" ]
```

フラットナーはドット表記を使用してキーを作成し、購入イベントからのすべての値の配列を値として構成します。

## イベント

以下の`dataLayer.push`コマンドは、データレイヤーに「event」が含まれるときに発火します：

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

Tealium EventStreamに到着するデータレイヤーは以下のようになります。`type_object`のみがフラット化され、関数は削除されます。

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