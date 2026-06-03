---
title: Webhook Facebook App Events APIの構成方法
description: テンプレートとテンプレート変数を使用してWebhook - カスタムリクエストアクションでFacebook App Events APIを構成する方法。
url: https://docs.tealium.com/ja/server-side/connectors/webhook-connectors/vendor-examples/webhook-facebook-app-events-api/
---
## 概要

FacebookにHTTPリクエストを送信して、アプリ内の1つ以上のコンバージョンを追跡します。イベントデータはJSONエンコードされた文字列として表現されます。詳細は[Facebook App Events API](https://developers.facebook.com/docs/marketing-api/app-event-api/)を参照してください。

### API呼び出し例:

```bash
curl \
  -F &#34;event=CUSTOM_APP_EVENTS&#34; \
  -F &#34;advertiser_id=1111-1111-1111-1111&#34; \
  -F &#34;advertiser_tracking_enabled=1&#34; \
  -F &#34;application_tracking_enabled=1&#34; \
  -F &#34;custom_events=[{\&#34;_eventName\&#34;:\&#34;fb_mobile_purchase\&#34;,
                      \&#34;_valueToSum\&#34;:55.22,
                      \&#34;_logTime\&#34;:1367017882,
                      \&#34;fb_currency\&#34;:\&#34;GBP\&#34;,
                    }]&#34; \
  &#34;https://graph.facebook.com/API_VERSION/APP_ID/activities&#34;
```

提供されたcurlの例（`-F`オプション付き）は、リクエストがPOSTメソッドを使用し、そのボディが&#34;multipart/form-data&#34;コンテンツタイプであることを示しています。Webhookで構成できる個々のコンポーネントに分けて全体のリクエストを解析しましょう。

#### 1. APIエンドポイント/URL

```
https://graph.facebook.com/API_VERSION/APP_ID/activities
```

この例では、URLにはAPIバージョンと`APP_ID`のプレースホルダー値があります。これらはおそらくURLにハードコーディングできますが、デモンストレーションの目的で、動的な値を使用してこのコンポーネントを作成するURLテンプレートを使用します。

#### 2. 単純なフォームフィールドの値

```
  event = CUSTOM_APP_EVENTS
  advertiser_id = 1111-1111-1111-1111
  advertiser_tracking_enabled = 1
  application_tracking_enabled = 1
```

これらのキーと値のペアは、ボディデータセクションのカスタム値を使用してマッピングできる単純なフォームフィールドです。

#### 3. JSON値

```json
custom_events = [{ &#34;_eventName&#34;  : &#34;fb_mobile_purchase&#34;,
                   &#34;_valueToSum&#34; : 55.22,
                   &#34;_logTime&#34;    : 1367017882,
                   &#34;fb_currency&#34; : &#34;GBP&#34;,
                }]
```

この特定のフィールド`custom_events`は、より複雑な値、JSON文字列を持っています。この値をWebhookで再現するために、テンプレート変数とテンプレートを使用します。

## Webhookの構成

### メソッドフィールド

&#34;POST&#34;に構成します。

### URLフィールド

`{{url_template}}`に構成します。

URLはハードコーディング（組み込みのAPIバージョンとアプリIDとともに）またはテンプレートベースであることができます。後者のアプローチは、データレイヤー属性の柔軟性を高めるために採用されています。以下のテンプレートセクションを参照してください。

### ボディコンテンツタイプ

`multipart/form-data`オプションを選択します。

### ボディデータ

例のリクエストから各フィールドの名前/値のペアを構成します。`custom_events`の値が、作成するテンプレートの名前、`events_template`であることに注意してください。

|Facebookフィールド名| カスタム値| コメント|
|---| ---| ---|
|`event`| `CUSTOM_APP_EVENTS`|
|`advertiser_id`| `1111-1111-1111-1111`|
|`advertiser_tracking_enabled`|  `1`|
|`application_tracking_enabled`|  `1`|
|`custom_events`| `{{events_template}}`| 下で作成されたテンプレートを参照|

パラメータ値はこの例ではカスタム/静的な値ですが、動的なデータレイヤー属性として簡単に提供することができます。

### テンプレート変数

テンプレートで参照され、置換される名前/値のペアを構成します。

|テンプレート変数名| タイプ| 値|  ノート |
|---| ---| ---| ---|
| `name` |  カスタム値 |  `fb_mobile_purchase` |
| `currency` |  カスタム値 |  `USD` |
| `logTime` |  [Data Attribute]() |  現在の時間 |  `1468358987` |
| `eventSums.value` |  [Set of Strings Attribute]() |  FBイベント合計 |  ドット命名規則はテンプレート内の一致するセクションを作成します。配列値: [0.99, 4.99] |
| `apiVersion` |  カスタム値 |  `v2.6 | URLテンプレートで使用するため|
| `appId` |  カスタム値 |  `123456` | URLテンプレートで使用するため|

### テンプレート

URLと`custom_events`パラメータに割り当てるためのJSON値の2つのテンプレートを作成します。テンプレートは、波括弧の構文を使用してテンプレート変数を使用することに注意してください。

このテンプレートは、文字列属性のセットによって埋められる&#34;eventSums.value&#34;変数に基づいています。これは配列属性なので、テンプレートはテンプレート変数名のプレフィックス（この場合は&#34;eventSums&#34;）のセクションを作成します。

**url_template**:

```
https://graph.facebook.com/{{apiVersion}}/{{appId}}/activities
```

**events_template**:

```
 [ 
 {{#eventSums}} 
 {     
  &#34;_eventName&#34;  : &#34;{{name}}&#34;,     
  &#34;_valueToSum&#34; : {{value}},     
  &#34;_logTime&#34;    : {{logTime.toTimestamp}},     
  &#34;fb_currency&#34; : &#34;{{currency}}&#34;
}{{#iter.hasNext}}, {{/iter.hasNext}}
 {{/eventSums}} 
 ] 
 ```

### レンダリングされたテンプレート

テンプレートはレンダリングされ、その内容はWebhook構成のどこでも参照されます（この例では、URLとボディデータの`custom_events`フィールド）。

`_valueToSum`パラメータが文字列属性のセットから値を受け取ることに注意してください。

**url_template**:

```
https://graph.facebook.com/v2.6/12345/activities
```

**events_template**:  

```json
[     
 {         
  &#34;_eventName&#34;  : &#34;fb_mobile_purchase&#34;,         
  &#34;_valueToSum&#34; : 0.99,         
  &#34;_logTime&#34;    : 1468358987,         
  &#34;fb_currency&#34; : &#34;USD&#34;     
  },     
  {         
    &#34;_eventName&#34;  : &#34;fb_mobile_purchase&#34;,         
    &#34;_valueToSum&#34; : 4.99,         
    &#34;_logTime&#34;    : 1468358987,         
    &#34;fb_currency&#34; : &#34;USD&#34;     
  } 
] 
```