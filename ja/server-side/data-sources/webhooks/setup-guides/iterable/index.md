---
title: IterableからのWebhook構成ガイド
description: この記事では、Iterableデータソースを使用してIterableアカウントにWebhookを作成し、Tealiumにアクション可能なイベントを送信する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/webhooks/setup-guides/iterable/
---## 前提条件

* [Iterableアカウント](https://app.iterable.com/login)
* Tealium EventStreamまたはTealium AudienceStream

## 仕組み

Iterableは、指定したエンドポイントに対して送信リクエストを送る[Webhook API](https://support.iterable.com/hc/en-us/articles/208013936-System-Webhooks)を提供しています。これらのリクエストは、Tealium EventStreamにIterableアカウントのアクティビティを通知します。Iterableデータソースを追加すると、ユニークなエンドポイントが生成されます。このエンドポイントは、IterableのWebhookを構成するために使用されます。

## Iterableデータソース

Iterableデータソースは、IterableのWebhook構成で使用するためのユニークなURLを生成します。URLは以下の形式で生成されます：

```
https://collect.tealiumiq.com/integration/event/ACCOUNT/PROFILE/DATA_SOURCE_KEY
```

Tealium Customer Data HubプロファイルにIterableデータソースを追加する方法については、[Data Sources](https://docs.tealium.com/about-data-sources/)を参照してください。データソースを追加し、接続した後は、プロファイルを保存して公開します。

## Iterableの構成

データソースのエンドポイントを取得したら、以下の手順でIterableアカウントに移動し、Webhookを作成します。

1. Iterableアカウントにログインします。
1. **Integrations &gt; System Webhooks**に移動します。
1. **Create Webhook**をクリックします。  
システムWebhook作成フォームが表示されます。
1. Tealiumデータソースから生成されたエンドポイントをWebhook URLとして入力します。
1. **Edit**をクリックします。
1. **Enabled**チェックボックスをチェックします。
1. **Save**をクリックします。

## イベントと属性

すべてのIterableからのイベント属性は自動的に`iterable_`でプレフィックスされます。例えば、Iterableは`eventname`属性をTealiumに送信し、それは`iterable_eventname`（すべて小文字）に変換されます。

**Iterable**が生成するWebhookイベントと属性の完全なリストについては、[Iterable Webhook Documentation](https://support.iterable.com/hc/en-us/articles/208013936-System-Webhooks)を参照してください。

|**イベント属性**| **タイプ**| **例**|
|---| ---| ---|
|`iterable_datafields_appalreadyrunning`| Boolean| false|
|`iterable_datafields_browsertoken`| String| cZn\_inqLGPk:APA91bHsn5jo0-4V55RB38eCeLHj8ZXVJYciU7k6Kipbit3lrRlEe2Dt6bNzR4lSf6r2YNVdWY8l90hV0jmb\_Y7y5ufcJ68xNI7wbsH6Q2jbEghA\_Qo4kWbtu6A4NZN4gxc1xsEbyh7b|
|`iterable_datafields_campaignid`| Number| 723636|
|`iterable_datafields_campaignname`| String| My campaign name|
|`iterable_datafields_canonicalurlid`| String| 3145668988|
|`iterable_datafields_channelids`| Number| 例: 8539|
|`iterable_datafields_city`| String| サンフランシスコ|
|`iterable_datafields_contentavailable`| Boolean| false|
|`iterable_datafields_contentid`| Number| 3681|
|`iterable_datafields_createdat`| String| 2019-08-07 23:43:48 +00:00|
|`iterable_datafields_device`| String| Gmail|
|`iterable_datafields_email`| String| docs@iterable.com|
|`iterable_datafields_emailids`| String| 例: 723636:t1020396:docs@iterable.com|
|`iterable_datafields_emailsubject`| String| My subject|
|`iterable_datafields_expiresat`| String| 2019-08-08 22:37:40 +00:00|
|`iterable_datafields_fromphonenumberid`| Number| 258|
|`iterable_datafields_fromsmssenderid`| Number| 258|
|`iterable_datafields_inappbody`| String| &lt;!DOCTYPE html PUBLIC \\\\-//W3C//DTD XHTML|
|`iterable_datafields_ip`| String| 162\.245.22.159|
|`iterable_datafields_isghostpush`| Boolean| false|
|`iterable_datafields_linkid`| String| 3145668988|
|`iterable_datafields_linkurl`| String| <https://www.iterable.com>|
|`iterable_datafields_messagecontext_savetoinbox`| Boolean| false|
|`iterable_datafields_messagecontext_trigger`| String| immediate|
|`iterable_datafields_messageid`| String| 4238c918b20a41dfbe9a910275b76f12|
|`iterable_datafields_messagetypeids`| Number| 例: 9106|
|`iterable_datafields_payload_path`| String| "your\_folder/30"|
|`iterable_datafields_platformendpoint`| String| &lt;Platform endpoint&gt;|
|`iterable_datafields_pushmessage`| String| Push message text|
|`iterable_datafields_reason`| String| DuplicateMarketingMessage|
|`iterable_datafields_recipientstate`| String| Complaint|
|`iterable_datafields_region`| String| CA|
|`iterable_datafields_signupsource`| String| ResubscribePage|
|`iterable_datafields_smsmessage`| String| Message text|
|`iterable_datafields_smsproviderresponse_code`| Number| 20404|
|`iterable_datafields_smsproviderresponse_message`| String| The requested resource /2010-04-01/Accounts/ACCOUNT\_NUMBER/Messages.json was not found|
|`iterable_datafields_smsproviderresponse_more_info`| String| <https://www.twilio.com/docs/errors/20404>|
|`iterable_datafields_smsproviderresponse_status`| Number| 404|
|`iterable_datafields_templateid`| Number| 1020396|
|`iterable_datafields_templatename`| String| My template name|
|`iterable_datafields_tophonenumber`| String| +16503926753|
|`iterable_datafields_transactionaldata_comment`| String| transactionalData lists the...|
| `iterable_datafields_unsubsource` | String| EmailLink|
| `iterable_datafields_url` | String|  [https://iterable.com/?\_e=a4b8cc0358422787f5cd5525005017172432ae33](https://iterable.com/?_e=a4b8cc0358422787f5cd5525005017172432ae33) |
| `iterable_datafields_useragent` | String| Mozilla/5.0 (Macintosh; Intel Mac OS X 10\_12\_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.36|
| `iterable_datafields_useragentdevice` | String| Mac|
| `iterable_datafields_workflowid` | Number| 53505|
| `iterable_datafields_workflowname` | String| My workflow name|
| `iterable_email` | String| dev@tealium.com|
| `iterable_eventname` | String| pushUninstall|

## ベンダーのドキュメンテーション

* [Iterable Webhook Documentation](https://support.iterable.com/hc/en-us/articles/208013936-System-Webhooks)

