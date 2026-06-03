---
title: Affirm受信Webhook構成ガイド
description: この記事では、Affirmデータソースを使用してAffirmアカウントにWebhookを作成し、Tealiumに対して実行可能なイベントを送信する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/webhooks/affirm/
---## 前提条件

* [Affirmアカウント](https://docs.affirm.com/affirm-developers/docs/dashboard)
* Tealium EventStreamまたはTealium AudienceStream

## 仕組み

Affirmは、指定したエンドポイントに対して送信リクエストを送る[Webhook API](https://docs.affirm.com/affirm-developers/docs/development-webhooks)を提供しています。これらのリクエストは、Affirmアカウントからの顧客活動についてTealium EventStreamとAudienceStreamに通知します。

* TealiumアカウントにAffirmデータソースを追加すると、ユニークなエンドポイントが生成されます。
* このエンドポイントは、Affirmアカウント内でWebhookを構成するために使用されます。
* 構成が完了すると、トピックに基づいてサブスクリプションを作成し、関連するプッシュ通知を受け取ってユースケースを自動化し、情報を得て、生産性を向上させることができます。

## Affirmデータソース

Affirmデータソースは、AffirmのWebhook構成で使用するためのユニークなURLを生成します。生成されたURLは以下の形式になります：

```
https://collect.tealiumiq.com/integration/event/ACCOUNT/PROFILE/DATA_SOURCE_KEY
```

Affirmデータソースを追加した後、生成されたエンドポイントをAffirmのクライアント成功マネージャーに提供してください。

関連：[データソースの追加方法]()

## Affirmの構成

データソースのエンドポイントを取得したら、以下の手順を使用してAffirmアカウントに移動し、Webhookを作成します。

1. Affirmアカウントにログインします。
1. Webhookを作成します。
1. Webhookを有効にし、保存します。

## イベントと属性

すべての受信Affirmイベント属性は自動的に`affirm_`でプレフィックスされます。例えば、Affirmは`smtp_id`属性をTealiumに送信し、それが`affirm_smtp_id`（すべて小文字）に変換されます。

Affirmによって生成されるWebhookイベントと属性の完全なリストについては、[Affirm Webhookドキュメンテーション](https://docs.affirm.com/affirm-developers/docs/development-webhooks)を参照してください。

|**イベント属性**| **タイプ**| **例**|
|---| ---| ---|
|`affirm_approved_amount`| 数値| 50000\.0|
|`affirm_checkout_token`| 文字列| &#34;5I97HK0EREM38YHK3&#34;|
|`affirm_created`| 日付| 2019-02-27T22:50:52.601851|
|`affirm_decision`| 文字列| &#34;approved&#34;, &#34;not\_approved&#34;|
|`affirm_email_address`| 文字列| &#34;Jeff.Testerson@affirm.com&#34;|
|`affirm_event`| 文字列| &#34;opened&#34;, &#34;prequal\_decision&#34;, &#34;approved&#34;, &#34;not\_approved&#34;, &#34;more\_information\_needed&#34;, &#34;confirmed&#34;|
|`affirm_event_timestamp`| 日付| 2020-02-27T22:51:57.941799|
|`affirm_expiration`| 日付| 2020-02-27T22:42:08.092894|
|`affirm_first_name`| 文字列| &#34;Jeff&#34;|
|`affirm_last_name`| 文字列| &#34;Testerson&#34;|
|`affirm_order_id`| 文字列| &#34;17.0&#34;|
|`affirm_term_apr`| 数値の配列| [19.55, 19.89, 20.12]|
|`affirm_term_created`| 日付の配列| [2019-02-27T22:42:08.092894, 2019-02-27T22:42:08.092894, 2019-02-27T22:42:08.092894]|
|`affirm_term_id`| 文字列の配列| [&#34;DX394TR2O0T6F3JM&#34;, &#34;D3QF1AOBN0SL6XXT&#34;, &#34;Z7XKQEWUW0FQOMJ2&#34;]|
|`affirm_term_installment_amount`| 数値の配列| [172127.0, 88236.0, 46348.0]|
|`affirm_term_installment_count`| 数値の配列| [3.0, 6.0, 12.0]|
|`affirm_term_interest_amount`| 数値の配列| [16381.0, 29415.0, 56176.0]|
|`affirm_term_prequal_amount`| 数値の配列| [500000.0, 500000.0, 500000.0]|
|`affirm_total`| 数値| 5000|
|`affirm_webhook_session_id`| 文字列| fal&#34;A1b2C3&#34;|

## ベンダードキュメンテーション

以下のドキュメンテーションを表示するには、Affirmにログインしている必要があります。そうでない場合は、Affirmのドキュメンテーションのメインページにリダイレクトされます。

* [Affirm Prequal Status Visibility Webhook Documentation](https://docs.affirm.com/Partners/Marketing_Messaging_Integration/Prequal_Status_Visibility_(Detailed))
* [Affirm Status Visibility Webhook Documentation](https://docs.affirm.com/Integrate_Affirm/Status_Visibility_(Detailed))

