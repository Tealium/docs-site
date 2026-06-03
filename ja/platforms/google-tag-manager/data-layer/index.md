---
title: データレイヤー
description: Google Tag ManagerマーケットプレイスのCollectタグについて、組み込み（自動）データレイヤー変数を学びます。
url: https://docs.tealium.com/ja/platforms/google-tag-manager/data-layer/
---
データレイヤーには、追跡されているページに関する基本情報を収集する組み込み変数が含まれています。これらの変数には、クッキー、ページの標準DOM変数、ロードされた構成に関するTealium固有の変数が含まれます。

[詳しくはこちら]()で、利用可能なデータレイヤー変数の種類について学びましょう。

## 標準ページデータ
以下の変数は、Webページで利用可能な標準JavaScriptプロパティから生成されます。

示されている例の値は、次のページURLに基づいています：

`http://www.example.com/path/file.html?param1=value1#hash=fragment`

| 変数                      | 説明                                                                                              | 例                                                                   |
|:--------------------------|:-------------------------------------------------------------------------------------------------|:--------------------------------------------------------------------|
| `dom.domain`              | URLの完全なドメイン。出典: location.hostname                                                    | `www.example.com`                                                   |
| `dom.hash`                | URLのハッシュフラグメント（#文字を除く）。出典: location.hash                                    | `hash=fragment`                                                     |
| `dom.pathname`            | クエリパラメータとドメインを除いたURLのパス。出典: location.pathname                            | `&#34;/path/file.html&#34;`                                                 |
| `dom.query_string`        | URLの完全なクエリ文字列。出典: location.search                                                  | `param1=value1`                                                     |
| `dom.referrer`            | 前のページのURL。出典: document.referrer                                                        |                                                                     |
| `dom.title`               | &amp;lt;title&amp;gt;タグのテキスト。出典: document.title                                                | `&#34;Page Title&#34; `                                                     |
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
        &#34;cp._ga&#34;: &#34;GA1.2.1370368844.1628542067&#34;,
        &#34;cp._gid&#34;: &#34;GA1.2.73283117.1628542067&#34;,
        &#34;tealium_session_number&#34;: 1,
        &#34;tealium_session_event_number&#34;: 3,
        &#34;tealium_session_id&#34;: &#34;1628542077230&#34;,
        &#34;tealium_visitor_id&#34;: &#34;927b2ebc092a70110329356772472215264145f9fa1&#34;,
        &#34;dom.referrer&#34;: &#34;&#34;,
        &#34;dom.title&#34;: &#34;Example dot com&#34;,
        &#34;dom.domain&#34;: &#34;example.com&#34;,
        &#34;dom.query_string&#34;: &#34;&#34;,
        &#34;dom.hash&#34;: &#34;&#34;,
        &#34;dom.url&#34;: &#34;https://example.com/&#34;,
        &#34;dom.pathname&#34;: &#34;/&#34;,
        &#34;dom.viewport_height&#34;: 936,
        &#34;dom.viewport_width&#34;: 1517,
        &#34;meta.description&#34;: &#34;View&#34;,
        &#34;meta.viewport&#34;: &#34;width=device-width, initial-scale=1&#34;,
        &#34;meta.theme-color&#34;: &#34;#13B0E9&#34;,
        &#34;tealium_cookie_domain&#34;: &#34;example.com&#34;,
        &#34;tealium_domain&#34;: &#34;example.com&#34;,
        &#34;tealium_event&#34;: &#34;test event&#34;,
        &#34;tealium_account&#34;: &#34;xxxxxxxxxxxx&#34;,
        &#34;tealium_profile&#34;: &#34;main&#34;,
        &#34;tealium_environment&#34;: &#34;prod&#34;,
        &#34;tealium_datasource&#34;: &#34;test1234&#34;,
        &#34;tealium_random&#34;: &#34;9870188345895229&#34;,
        &#34;tealium_library_name&#34;: &#34;tealium.js&#34;,
        &#34;tealium_library_version&#34;: &#34;5.0.3&#34;,
        &#34;tealium_timestamp_epoch&#34;: 1628542114,
        &#34;tealium_timestamp_utc&#34;: &#34;2021-08-09T20:48:34.616Z&#34;,
        &#34;tealium_timestamp_local&#34;: &#34;2021-08-09T13:48:34.616&#34;,
        &#34;timing.domain&#34;: &#34;example.com&#34;,
        &#34;timing.pathname&#34;: &#34;/&#34;,
        &#34;timing.query_string&#34;: &#34;&#34;,
        &#34;timing.timestamp&#34;: 1628542085435,
        &#34;timing.dns&#34;: 1,
        &#34;timing.connect&#34;: 99,
        &#34;timing.response&#34;: 0,
        &#34;timing.dom_loading_to_interactive&#34;: 7,
        &#34;timing.dom_interactive_to_complete&#34;: 129,
        &#34;timing.load&#34;: 0,
        &#34;timing.time_to_first_byte&#34;: 95,
        &#34;timing.front_end&#34;: 163,
        &#34;timing.fetch_to_response&#34;: 210,
        &#34;timing.fetch_to_complete&#34;: 373,
        &#34;timing.fetch_to_interactive&#34;: 244
}

```
## データレイヤー変数のフラット化

Google Tag Managerのイベントは、Tealium Customer Data Hubの仕様に合わせてTealium属性名にフラット化されます。イベントデータはTealium EventStreamによって受信されます。

`tealium_event`の値は、`dataLayer.push`コールの`event`の値です。Google Tag Managerはイベント名としてデフォルトのページビュー値を`gtm.js`に構成します。デフォルトを上書きするには、イベント名を含む変数をTealiumイベント構成に構成します。

属性は自動的に追加されません。これらの属性をTealium EventStreamに追加する必要があります。

## Eコマース

以下の購入イベントの例は、クライアントサイドのeコマースイベントがどのようにフラット化されるかを示しています。

```js
dataLayer.push({
  &#39;ecommerce&#39;: {
    &#39;purchase&#39;: {
      &#39;actionField&#39;: {
        &#39;id&#39;: &#39;T12345&#39;,    // トランザクションID。購入および払い戻しに必要です。
        &#39;affiliation&#39;: &#39;オンラインストア&#39;,
        &#39;revenue&#39;: &#39;35.43&#39;,
        &#39;tax&#39;:&#39;4.90&#39;,
        &#39;shipping&#39;: &#39;5.99&#39;,
        &#39;coupon&#39;: &#39;SUMMER_SALE&#39;
      },
      &#39;products&#39;: [{
        &#39;name&#39;: &#39;トライブレンド アンドロイド Tシャツ&#39;,     // 名前またはIDが必要です。
        &#39;id&#39;: &#39;12345&#39;,
        &#39;price&#39;: &#39;15.25&#39;,
        &#39;brand&#39;: &#39;Google&#39;,
        &#39;category&#39;: &#39;アパレル&#39;,
        &#39;variant&#39;: &#39;グレー&#39;,
        &#39;quantity&#39;: 1,
        &#39;coupon&#39;: &#39;&#39;
       },
       {
        &#39;name&#39;: &#39;ドーナツフライデー香るTシャツ&#39;,
        &#39;id&#39;: &#39;67890&#39;,
        &#39;price&#39;: &#39;33.75&#39;,
        &#39;brand&#39;: &#39;Google&#39;,
        &#39;category&#39;: &#39;アパレル&#39;,
        &#39;variant&#39;: &#39;ブラック&#39;,
        &#39;quantity&#39;: 1
       }]
    }
  }
});
```
フラット化後、購入イベントは以下のようになります：

```js
&#34;ecommerce.purchase.actionField.affiliation&#34;: &#34;オンラインストア&#34;
&#34;ecommerce.purchase.actionField.coupon&#34;: &#34;SUMMER_SALE&#34;
&#34;ecommerce.purchase.actionField.id&#34;: &#34;T12345&#34;
&#34;ecommerce.purchase.actionField.revenue&#34;: &#34;35.43&#34;
&#34;ecommerce.purchase.actionField.shipping&#34;: &#34;5.99&#34;
&#34;ecommerce.purchase.actionField.tax&#34;: &#34;4.90&#34;
&#34;ecommerce.purchase.products.brand&#34;: [ &#34;Google&#34;, &#34;Google&#34; ]
&#34;ecommerce.purchase.products.category&#34;: [ &#34;アパレル&#34;, &#34;アパレル&#34; ]
&#34;ecommerce.purchase.products.coupon&#34;: [ &#34;&#34;, &#34;&#34; ]
&#34;ecommerce.purchase.products.id&#34;: [ &#34;12345&#34;, &#34;67890&#34; ]
&#34;ecommerce.purchase.products.name&#34;: [ &#34;トライブレンド アンドロイド Tシャツ&#34;, &#34;ドーナツフライデー香るTシャツ&#34; ]
&#34;ecommerce.purchase.products.price&#34;: [ &#34;15.25&#34;, &#34;33.75&#34; ]
&#34;ecommerce.purchase.products.variant&#34;: [ &#34;グレー&#34;, &#34;ブラック&#34; ]
&#34;ecommerce.purchase.products.quantity&#34;: [ &#34;1&#34;, &#34;1&#34; ]
```

フラットナーはドット表記を使用してキーを作成し、購入イベントからのすべての値の配列を値として構成します。

## イベント

以下の`dataLayer.push`コマンドは、データレイヤーに「event」が含まれるときに発火します：

```js
window.dataLayer.push({
  event: &#34;test_number&#34;,
  type_number: 5,
  type_string: &#39;hello&#39;,
  type_object: { someKey: &#39;someValue&#39; },
  type_array: [1,2,3,4],
  type_function: function() { return &#39;hello&#39;; },
  type_boolean: true
});
```

Tealium EventStreamに到着するデータレイヤーは以下のようになります。`type_object`のみがフラット化され、関数は削除されます。

```
{
    &#34;event&#34;: &#34;test_number&#34;,
    &#34;type_number&#34;: 5,
    &#34;type_string&#34;: &#34;hello&#34;,
    &#34;type_object.someKey&#34;: &#34;someValue&#34;,
    &#34;type_array&#34;: [1, 2, 3, 4],
    &#34;type_boolean&#34;: true
}
```