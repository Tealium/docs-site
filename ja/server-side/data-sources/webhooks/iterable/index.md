---
title: Iterable 受信 Webhook 構成ガイド
description: この記事では、Iterable データソースを使用して Iterable アカウントに Webhook を作成し、対応可能なイベントを Tealium に送信する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/webhooks/iterable/
---## 前提条件

* [Iterable アカウント](https://app.iterable.com/login)
* Event Streaming または Customer Data Platform（CDP）

## 仕組み

Iterable は、指定したエンドポイントに送信リクエストを送る [Webhook API](https://support.iterable.com/hc/en-us/articles/208013936-System-Webhooks) を提供しています。これらのリクエストは、Iterable アカウント内のアクティビティを Event Streaming に通知します。Iterable データソースを追加すると、一意のエンドポイントが生成されます。このエンドポイントを使用して Iterable Webhook を構成します。

## Iterable データソース

Iterable データソースは、Iterable Webhook の構成で使用する一意の URL を生成します。URL は次の形式で生成されます。

```
https://collect.tealiumiq.com/integration/event/ACCOUNT/PROFILE/DATA_SOURCE_KEY
```

Iterable データソースを Tealium Customer Data Hub プロファイルに追加する方法については、[データソース](https://docs.tealium.com/about-data-sources/)を参照してください。データソースを追加して接続したら、プロファイルを保存してパブリッシュします。

## Iterable の構成

データソースのエンドポイントを取得したら、次の手順で Iterable アカウントに移動して Webhook を作成します。

1. Iterable アカウントにログインします。
1. **Integrations &gt; System Webhooks** に移動します。
1. **Create Webhook** をクリックします。  
システム Webhook の作成フォームが表示されます。
1. Tealium データソースから生成されたエンドポイントを Webhook URL として入力します。
1. **Edit** をクリックします。
1. **Enabled** チェックボックスをオンにします。
1. **Save** をクリックします。

## イベントと属性

受信するすべての Iterable イベント属性には、自動的に `iterable_` というプレフィックスがエンリッチメントされます。たとえば、Iterable が `eventname` 属性を Tealium に送信すると、その属性は `iterable_eventname`（すべて小文字）に変換されます。

**Iterable** によって生成される Webhook イベントと属性の完全なリストについては、[Iterable Webhook ドキュメント](https://support.iterable.com/hc/en-us/articles/208013936-System-Webhooks)を参照してください。

|**イベント属性**| **型**| **例**|
|---| ---| ---|
|`iterable_datafields_appalreadyrunning`| ブール値| false|
|`iterable_datafields_browsertoken`| 文字列| cZn\_inqLGPk:APA91bHsn5jo0-4V55RB38eCeLHj8ZXVJYciU7k6Kipbit3lrRlEe2Dt6bNzR4lSf6r2YNVdWY8l90hV0jmb\_Y7y5ufcJ68xNI7wbsH6Q2jbEghA\_Qo4kWbtu6A4NZN4gxc1xsEbyh7b|
|`iterable_datafields_campaignid`| 数値| 723636|
|`iterable_datafields_campaignname`| 文字列| キャンペーン名|
|`iterable_datafields_canonicalurlid`| 文字列| 3145668988|
|`iterable_datafields_channelids`| 数値| 例：8539|
|`iterable_datafields_city`| 文字列| San Francisco|
|`iterable_datafields_contentavailable`| ブール値| false|
|`iterable_datafields_contentid`| 数値| 3681|
|`iterable_datafields_createdat`| 文字列| 2019-08-07 23:43:48 +00:00|
|`iterable_datafields_device`| 文字列| Gmail|
|`iterable_datafields_email`| 文字列| docs@iterable.com|
|`iterable_datafields_emailids`| 文字列| 例：723636:t1020396:docs@iterable.com|
|`iterable_datafields_emailsubject`| 文字列| 件名|
|`iterable_datafields_expiresat`| 文字列| 2019-08-08 22:37:40 +00:00|
|`iterable_datafields_fromphonenumberid`| 数値| 258|
|`iterable_datafields_fromsmssenderid`| 数値| 258|
|`iterable_datafields_inappbody`| 文字列| &lt;!DOCTYPE html PUBLIC \\\\-//W3C//DTD XHTML|
|`iterable_datafields_ip`| 文字列| 162\.245.22.159|
|`iterable_datafields_isghostpush`| ブール値| false|
|`iterable_datafields_linkid`| 文字列| 3145668988|
|`iterable_datafields_linkurl`| 文字列| <https://www.iterable.com>|
|`iterable_datafields_messagecontext_savetoinbox`| ブール値| false|
|`iterable_datafields_messagecontext_trigger`| 文字列| immediate|
|`iterable_datafields_messageid`| 文字列| 4238c918b20a41dfbe9a910275b76f12|
|`iterable_datafields_messagetypeids`| 数値| 例：9106|
|`iterable_datafields_payload_path`| 文字列| "your\_folder/30"|
|`iterable_datafields_platformendpoint`| 文字列| &lt;Platform endpoint&gt;|
|`iterable_datafields_pushmessage`| 文字列| プッシュメッセージのテキスト|
|`iterable_datafields_reason`| 文字列| DuplicateMarketingMessage|
|`iterable_datafields_recipientstate`| 文字列| Complaint|
|`iterable_datafields_region`| 文字列| CA|
|`iterable_datafields_signupsource`| 文字列| ResubscribePage|
|`iterable_datafields_smsmessage`| 文字列| メッセージのテキスト|
|`iterable_datafields_smsproviderresponse_code`| 数値| 20404|
|`iterable_datafields_smsproviderresponse_message`| 文字列| リクエストされたリソース /2010-04-01/Accounts/ACCOUNT\_NUMBER/Messages.json が見つかりませんでした|
|`iterable_datafields_smsproviderresponse_more_info`| 文字列| <https://www.twilio.com/docs/errors/20404>|
|`iterable_datafields_smsproviderresponse_status`| 数値| 404|
|`iterable_datafields_templateid`| 数値| 1020396|
|`iterable_datafields_templatename`| 文字列| テンプレート名|
|`iterable_datafields_tophonenumber`| 文字列| +16503926753|
|`iterable_datafields_transactionaldata_comment`| 文字列| transactionalData のリスト...|
| `iterable_datafields_unsubsource` | 文字列| EmailLink|
| `iterable_datafields_url` | 文字列|  [https://iterable.com/?\_e=a4b8cc0358422787f5cd5525005017172432ae33](https://iterable.com/?_e=a4b8cc0358422787f5cd5525005017172432ae33) |
| `iterable_datafields_useragent` | 文字列| Mozilla/5.0 (Macintosh; Intel Mac OS X 10\_12\_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.36|
| `iterable_datafields_useragentdevice` | 文字列| Mac|
| `iterable_datafields_workflowid` | 数値| 53505|
| `iterable_datafields_workflowname` | 文字列| ワークフロー名|
| `iterable_email` | 文字列| dev@tealium.com|
| `iterable_eventname` | 文字列| pushUninstall|

## ベンダードキュメント

* [Iterable Webhook ドキュメント](https://support.iterable.com/hc/en-us/articles/208013936-System-Webhooks)