---
title: Affirm 受信 Webhook 構成ガイド
description: この記事では、Affirm データソースを使用して Affirm アカウントに Webhook を作成し、実用的なイベントを Tealium に送信する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/webhooks/affirm/
---## 前提条件

* [Affirm アカウント](https://docs.affirm.com/affirm-developers/docs/dashboard)
* Event Streaming または Customer Data Platform（CDP）

## 仕組み

Affirm は、指定したエンドポイントに送信リクエストを送る [Webhook API](https://docs.affirm.com/affirm-developers/docs/development-webhooks) を提供しています。これらのリクエストにより、Affirm アカウントでの顧客アクティビティが Event Streaming と Customer Data Platform（CDP）に通知されます。

* Tealium アカウントに Affirm データソースを追加すると、一意のエンドポイントが生成されます。
* このエンドポイントは、Affirm アカウントで Webhook を構成するために使用されます。
* 構成後は、トピックに基づいてサブスクリプションを作成し、関連するプッシュ通知を受信することで、ユースケースの自動化、最新情報の把握、生産性の向上を実現できます。

## Affirm データソース

Affirm データソースは、Affirm Webhook の構成で使用する一意の URL を生成します。生成される URL の形式は次のとおりです。

```
https://collect.tealiumiq.com/integration/event/ACCOUNT/PROFILE/DATA_SOURCE_KEY
```

続行する前に Affirm データソースを追加し、生成されたエンドポイントを Affirm Client Success Manager に提供してください。

関連項目：[データソースを追加する方法]()

## Affirm の構成

データソースのエンドポイントを取得したら、次の手順に従って Affirm アカウントに移動し、Webhook を作成します。

1. Affirm アカウントにログインします。
1. Webhook を作成します。
1. Webhook を有効にして保存します。

## イベントと属性

受信するすべての Affirm イベント属性には、自動的に `affirm_` というプレフィックスがエンリッチメントされます。たとえば、Affirm から Tealium に送信される `smtp_id` 属性は、`affirm_smtp_id`（すべて小文字）に変換されます。

Affirm が生成する Webhook イベントと属性の完全な一覧については、[Affirm Webhook ドキュメント](https://docs.affirm.com/affirm-developers/docs/development-webhooks)を参照してください。

|**イベント属性**| **型**| **例**|
|---| ---| ---|
|`affirm_approved_amount`| 数値| 50000\.0|
|`affirm_checkout_token`| 文字列| "5I97HK0EREM38YHK3"|
|`affirm_created`| 日付| 2019-02-27T22:50:52.601851|
|`affirm_decision`| 文字列| "approved", "not\_approved"|
|`affirm_email_address`| 文字列| "Jeff.Testerson@affirm.com"|
|`affirm_event`| 文字列| "opened", "prequal\_decision", "approved", "not\_approved", "more\_information\_needed", "confirmed"|
|`affirm_event_timestamp`| 日付| 2020-02-27T22:51:57.941799|
|`affirm_expiration`| 日付| 2020-02-27T22:42:08.092894|
|`affirm_first_name`| 文字列| "Jeff"|
|`affirm_last_name`| 文字列| "Testerson"|
|`affirm_order_id`| 文字列| "17.0"|
|`affirm_term_apr`| 数値の配列| [19.55, 19.89, 20.12]|
|`affirm_term_created`| 日付の配列| [2019-02-27T22:42:08.092894, 2019-02-27T22:42:08.092894, 2019-02-27T22:42:08.092894]|
|`affirm_term_id`| 文字列の配列| ["DX394TR2O0T6F3JM", "D3QF1AOBN0SL6XXT", "Z7XKQEWUW0FQOMJ2"]|
|`affirm_term_installment_amount`| 数値の配列| [172127.0, 88236.0, 46348.0]|
|`affirm_term_installment_count`| 数値の配列| [3.0, 6.0, 12.0]|
|`affirm_term_interest_amount`| 数値の配列| [16381.0, 29415.0, 56176.0]|
|`affirm_term_prequal_amount`| 数値の配列| [500000.0, 500000.0, 500000.0]|
|`affirm_total`| 数値| 5000|
|`affirm_webhook_session_id`| 文字列| fal"A1b2C3"|

## ベンダーのドキュメント

次のドキュメントを表示するには、Affirm にログインしている必要があります。ログインしていない場合は、Affirm ドキュメントのメインページにリダイレクトされます。

* [Affirm Prequal Status Visibility Webhook ドキュメント](https://docs.affirm.com/Partners/Marketing_Messaging_Integration/Prequal_Status_Visibility_(Detailed))
* [Affirm Status Visibility Webhook ドキュメント](https://docs.affirm.com/Integrate_Affirm/Status_Visibility_(Detailed))