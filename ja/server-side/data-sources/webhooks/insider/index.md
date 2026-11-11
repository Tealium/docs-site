---
title: Insiderデータソース構成ガイド
description: この記事では、Insiderをデータソースとして使用し、実用的なイベントをTealiumに送信する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/webhooks/insider/
---
## 前提条件

* Event Streaming API HubおよびCustomer Data Platform（CDP）のいずれか、または両方
* Insiderアカウント


## 仕組み

InsiderをEvent StreamingまたはCustomer Data Platform（CDP）に接続するには、[Insider Webhook API](https://academy.useinsider.com/docs/webhooks-vs-apis)を使用して、Tealiumアカウント内のカスタムInsiderデータソースエンドポイントに送信リクエストを送ります。

Webhookを構成すると、チャネルインタラクションおよびリード収集イベントに関するイベント更新を自動的に受信できます。

## Insiderデータソース

InsiderデータソースをTealium Customer Data Hubプロファイルに追加すると、Webhook構成で使用する次の形式の一意のURLが生成されます。

```
https://collect.tealiumiq.com/integration/event/ACCOUNT/PROFILE/DATA_SOURCE_KEY
```

InsiderデータソースをTealium Customer Data Hubプロファイルに追加する方法については、[データソース](https://docs.tealium.com/about-data-sources/)を参照してください。データソースを追加して接続した後、プロファイルを保存してパブリッシュします。

## Insiderの構成

InsiderをTealium Customer Data Hubプロファイルに接続した後、次の手順でWebhookを構成します。

1. Insiderチャネルイベントを収集するために[Tealium Collect API](https://docs.tealium.com/ja/platforms/http-api/endpoint/)を構成したい旨を、Insiderのアカウントマネージャーに伝えます。
1. Insiderチームが、Insider内でTealiumデータソースを構成します。
1. Tealiumで、InsiderデータソースをTealiumプロファイルに追加したときに作成されたカスタムエンドポイントURLを入力します。例：

```
https://collect-us-east-1.tealiumiq.com/integration/event/{account}/{profile}/{data_source_key}
```

## イベントと属性

Insiderのイベントパラメータは、エンゲージメント行動または顧客行動イベントに基づいて事前定義されています。受信するすべてのInsiderイベント属性には、接頭辞`insider_`がエンリッチメントされます。たとえば、InsiderからTealiumに送信された`campaign_id`属性は、`insider_campaign_id`（すべて小文字）に変換されます。

### チャネルイベント

次の表は、一般的なInsiderイベント属性と、特定のチャネル固有イベントについてTealiumが受信するデータの例を示しています。このリストはすべてを網羅するものではありません。Insiderのデフォルトイベントの完全なリストについては、Insiderのドキュメントの[デフォルトイベント](https://academy.useinsider.com/docs/default-events#mobile-app-%20events)を参照してください。

| イベント属性 | 型 | 例 |
|---|---|---|
| `insider_event_group_id` | 文字列 | `ORDER123` |
| `insider_product_id` | 文字列 | `AGH210070 `|
| `insider_name` | 文字列 | `iPhone 11+` |
| `insider_taxonomy` | 文字列 | `["Electronic","Phone"]` |
| `insider_currency` | 文字列 | `USD` |
| `insider_unit_price` | 数値 | `990.9` |
| `insider_unit_sale_price` | 数値 | `890.8` |
| `insider_color` | 文字列 | `black` |
| `insider_size` | 文字列 | `one-size` |
| `insider_shipping_cost` | 数値 | `52.09` |
| `insider_promotion_name` | 文字列 | `Test20` |
| `insider_promotion_discount` | 数値 | `18.8` |
| `insider_qu `| 数値 | `1` |
| `insider_piu` | 文字列 | `https://test.com/producturl` |
| `insider_sid `| 文字列 |  |
| `insider_sc` | 数値 | `52.09` |
| `insider_vn` | 文字列 | `VoucherPromotion` |
| `insider_vd` | 数値 | `12.01` |
| `insider_si` | 文字列 | `one-size` |
| `insider_co` | 文字列 | `black` |
| `insider_url` | 文字列 | `https://test.com/producturl` |
| `insider_referrer` | 文字列 | `https://google.com` |
| `insider_device_type` | 文字列 | `web` |
| `insider_ip_address` | 文字列 | `192.158.1.38 `|
| `insider_campaign_id` | 数値 | `105901959` |
| `insider_user_agent` | 文字列 | `Mozilla/5.0 (iPad; U; CPU OS 3_2_1 like Mac OS X; en-us)` |
| `insider_url_offset_index `| 数値 | `0` |
| `insider_url_offset_type` | 文字列 | `html` |
| `insider_type` | 文字列 | `html` |
| `insider_reason` | 文字列 | `Unsubscribed Address` |
| `insider_deep_links` | 文字列 | `value1 `|
| `insider_dry_run` | 文字列 |  |
| `insider_image_url` | 文字列 | `https://your_image_url.jpg `|
| `insider_message` | 文字列 | `Your push content goes here `|
| `insider_title` | 文字列 | `Your push notification title goes here `|
| `insider_attr_email` | 文字列 | `test@test.com `|
| `insider_attr_phone` | 文字列 | `+14401231234` |
| `insider_hook_id` | 文字列 | `442811` |
| `insider_insider_id` | 文字列 | `a00d8092-0ba7-41f5-b07d-7ae64231dac3d` |


## ベンダーのドキュメント

* [WebhookとAPIの比較](https://academy.useinsider.com/docs/webhooks-vs-apis)
* [メールイベント用Webhook](https://academy.useinsider.com/docs/api-reference-email-webhooks-for-email-events)
* [トランザクションSMS用Webhook](https://academy.useinsider.com/docs/webhooks-for-transactional-sms)