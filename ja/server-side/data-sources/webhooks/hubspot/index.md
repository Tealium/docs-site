---
title: HubspotワークフローのインカミングWebhook構成ガイド
description: この記事では、Hubspotデータソースを使用してHubspotアカウントにWebhookを作成し、Tealiumにアクション可能なイベントを送信する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/webhooks/hubspot/
---
## 前提条件

* HubSpotマーケティングプロフェッショナル、セールスプロフェッショナル、またはエンタープライズアカウント
* Tealium EventStreamおよび/またはTealium AudienceStreamアカウント

## 仕組み

HubSpotは、指定したエンドポイントに対して送信リクエストを送るWebhook APIを提供しています。これらのリクエストは、EventStreamに対するプッシュ通知のように機能し、HubSpotアカウントで何が起こったかを通知します。UDHでHubSpotデータソースを追加すると、HubSpotのWebhookを構成するために使用するユニークなエンドポイントが生成されます。

## HubSpotデータソースの追加

進行する前にHubSpotデータソースを追加します。HubSpotデータソースは、HubSpotの構成でHTTP POST URLとして使用するためのユニークなURLを生成します。生成されるURLの形式は次のとおりです：

```
https://collect.tealiumiq.com/integration/event/ACCOUNT/PROFILE/DATA_SOURCE_KEY
```

## HubSpotの構成

データソースのエンドポイントを取得したら、HubSpotアカウントに移動してWebhookを作成します。

1. [HubSpotアカウント](https://login.hubspot.com/)にログインします。
    * HubSpotマーケティングプロフェッショナルまたはエンタープライズアカウントでは、**Contacts &amp;gt; Workflows**に移動します。
    * HubSpotセールスプロフェッショナルアカウントでは、**Sales Tools &amp;gt; Workflows**に移動します。

1. 編集したいワークフローの名前をクリックします。
1. アクションを追加するためにプラス（**&#43;**）アイコンをクリックし、右ペインで**Trigger a webhook**を選択します。
1. ドロップダウンリストから**POST**を選択します。
1. WebHook URLに以下を入力します：  
      ```
      https://collect.tealiumiq.com/integration/event/{account}/{profile}/{unique_id}
      ```

1. **Save**をクリックします。

## イベントと属性

すべての受信HubSpotイベント属性は自動的に`hubspot_wf_`でプレフィックスとアンダースコアが付けられます。例えば、`properties.lead_source` = `hubspot_wf_properties_lead_source`です。

以下の表は、HubSpotが生成するWebhookイベントと属性をリストしています：

|イベント属性| タイプ| 例|
|---| ---| ---|
|`hubspot_wf_vid`| 文字列| &#34;3234574&#34;|
|`hubspot_wf_canonical_vid`| 文字列| &#34;3234574&#34;|
|`hubspot_wf_portal_id`| 文字列| &#34;62515&#34;|
|`hubspot_wf_is_contact`| ブール値| &#34;true&#34;|
|`hubspot_wf_profile_token`| 文字列| &#34;AO_T-mOFUify...&#34;|
|`hubspot_wf_profile_url`| 文字列| &#34;https://app.hubspot.com/...&#34;|
|`hubspot_wf_properties_lead_source`| 文字列| &#34;DiscoverOrg&#34;|
|`hubspot_wf_properties_num_unique_conversion_events`| 文字列| &#34;0&#34;|
|`hubspot_wf_properties_hs_analytics_revenue`| 文字列| &#34;0.0&#34;|
|`hubspot_wf_properties_createdate`| 文字列| &#34;1484026585538&#34;|
|`hubspot_wf_properties_hs_email_optout`| 文字列| &#34;true&#34;|
|`hubspot_wf_properties_hs_predictivecontactscore`| 文字列| &#34;50&#34;|
|`hubspot_wf_properties_annualrevenue`| 文字列| &#34;181900000&#34;|
|`hubspot_wf_properties_hs_analytics_num_page_views`| 文字列| &#34;0&#34;|
|`hubspot_wf_properties_state`| 文字列| &#34;MA&#34;|
|`hubspot_wf_properties_zip`| 文字列| &#34;02139&#34;|
|`hubspot_wf_properties_hs_predictability`| 文字列| &#34;bucket_3&#34;|
|`hubspot_wf_properties_hubspotscore`| 文字列| &#34;0&#34;|
|`hubspot_wf_properties_linkedinconnections`| 文字列| &#34;0&#34;|
|`hubspot_wf_properties_hs_lifecyclestage_subscriber_date`| 文字列| &#34;1484026585538&#34;|
|`hubspot_wf_properties_hs_analytics_average_page_views`| 文字列| &#34;0&#34;|
|`hubspot_wf_properties_lastname`| 文字列| &#34;Huang&#34;|
|`hubspot_wf_properties_twitterhandle`| 文字列| &#34;ghidinelli&#34;|
|`hubspot_wf_properties_phone`| 文字列| &#34;555-122-2323&#34;|
|`hubspot_wf_properties_num_conversion_events`| 文字列| &#34;0&#34;|
|`hubspot_wf_properties_currentlyinworkflow`| 文字列| &#34;false&#34;|
|`hubspot_wf_properties_hs_analytics_num_event_completions`| 文字列| &#34;2&#34;|
|`hubspot_wf_properties_followercount`| 文字列| &#34;582&#34;|
|`hubspot_wf_properties_associatedcompanyid`| 文字列| &#34;184896670&#34;|
|`hubspot_wf_properties_firstname`| 文字列| &#34;Codey&#34;|
|`hubspot_wf_properties_city`| 文字列| &#34;Cambridge&#34;|
|`hubspot_wf_properties_hs_social_num_broadcast_clicks`| 文字列| &#34;0&#34;|
|`hubspot_wf_properties_hs_analytics_num_visits`| 文字列| &#34;0&#34;|
|`hubspot_wf_properties_twitterbio`| 文字列| &#34;Racer, entrepreneur, world traveler...&#34;|
|`hubspot_wf_properties_hs_social_linkedin_clicks`| 文字列| &#34;0&#34;|
|`hubspot_wf_properties_hs_twitterid`| 文字列| &#34;49019793&#34;|
|`hubspot_wf_properties_associatedcompanylastupdated`| 文字列| &#34;13365279006997343&#34;|
|`hubspot_wf_properties_hs_analytics_source`| 文字列| &#34;OFFLINE&#34;|
|`hubspot_wf_properties_company`| 文字列| &#34;HubSpot&#34;|
|`hubspot_wf_properties_email`| 文字列| &#34;testingapis@hubspot.com&#34;|
|`hubspot_wf_properties_linkedinbio`| 文字列| &#34;Racecar driver, entrepreneur, world traveler...&#34;|
|`hubspot_wf_properties_website`| 文字列| &#34;http://hubspot.com&#34;|
|`hubspot_wf_properties_address`| 文字列| &#34;25 First Street&#34;|
|`hubspot_wf_properties_hs_analytics_first_timestamp`| 文字列| &#34;1484026585538&#34;|
|`hubspot_wf_properties_lastmodifieddate`| 文字列| &#34;1484858431084&#34;|
|`hubspot_wf_properties_photo`| 文字列| &#34;&lt;https://d2ojpxxtu63wzl.cloudfront.net/st&gt;...&#34;|
|`hubspot_wf_properties_hs_social_google_plus_clicks`| 文字列| &#34;0&#34;|
|`hubspot_wf_properties_kloutscoregeneral`| 文字列| &#34;48&#34;|
|`hubspot_wf_properties_hs_social_facebook_clicks`| 文字列| &#34;0&#34;|
|`hubspot_wf_properties_twitterprofilephoto`| 文字列| &#34;https://pbs.twimg.com/profile_images...&#34;|
|`hubspot_wf_properties_hs_social_twitter_clicks`| 文字列| &#34;0&#34;|
|`hubspot_wf_properties_hs_analytics_source_data_1`| 文字列| &#34;API&#34;|
|`hubspot_wf_properties_lifecyclestage`| 文字列| &#34;subscriber&#34;|
|`hubspot_wf_associated_company_company_id`| 文字列| &#34;184896670&#34;|
|`hubspot_wf_associated_company_portal_id`| 文字列| &#34;62515&#34;|
|`hubspot_wf_associated_company_properties_country`| 文字列| &#34;United States&#34;|
|`hubspot_wf_associated_company_properties_city`| 文字列| &#34;Cambridge&#34;|
|`hubspot_wf_associated_company_properties_num_associated_contacts`| 文字列| &#34;102&#34;|
|`hubspot_wf_associated_company_properties_timezone`| 文字列| &#34;America/New_York&#34;|
|`hubspot_wf_associated_company_properties_facebook_company_page`| 文字列| &#34;https://www.facebook.com/hubspot&#34;|
|`hubspot_wf_associated_company_properties_createdate`| 文字列| &#34;1457708103847&#34;|
|`hubspot_wf_associated_company_properties_description`| 文字列| &#34;HubSpot is the world’s leading...&#34;|
|`hubspot_wf_associated_company_properties_industry`| 文字列| &#34;COMPUTER_SOFTWARE&#34;|
|`hubspot_wf_associated_company_properties_total_money_raised`| 文字列| &#34;$100.5M&#34;|
|`hubspot_wf_associated_company_properties_days_to_close`| 文字列| &#34;220&#34;|
|`hubspot_wf_associated_company_properties_hs_analytics_num_visits`| 文字列| &#34;0&#34;|
|`hubspot_wf_associated_company_properties_linkedin_company_page`| 文字列| &#34;http://www.linkedin.com/company/68529&#34;|
|`hubspot_wf_associated_company_properties_recent_conversion_event_name`| 文字列| &#34;Contact Us: excedalogic form&#34;|
|`hubspot_wf_associated_company_properties_hs_analytics_source`| 文字列| &#34;OFFLINE&#34;|
|`hubspot_wf_associated_company_properties_num_contacted_notes`| 文字列| &#34;12&#34;|
|`hubspot_wf_associated_company_properties_annualrevenue`| 文字列| &#34;250000000&#34;|
|`hubspot_wf_associated_company_properties_founded_year`| 文字列| &#34;2006&#34;|
|`hubspot_wf_associated_company_properties_hs_analytics_num_page_views`| 文字列| &#34;0&#34;|
|`hubspot_wf_associated_company_properties_state`| 文字列| &#34;MA&#34;|
|`hubspot_wf_associated_company_properties_linkedinbio`| 文字列| &#34;HubSpot is the world’s leading...&#34;|
|`hubspot_wf_associated_company_properties_zip`| 文字列| &#34;02141&#34;|
|`hubspot_wf_associated_company_properties_notes_last_updated`| 文字列| &#34;1480625888696&#34;|
|`hubspot_wf_associated_company_properties_website`| 文字列| &#34;hubspot.com&#34;|
|`hubspot_wf_associated_company_properties_closedate`| 文字列| &#34;1476768116137&#34;|
|`hubspot_wf_associated_company_properties_hs_analytics_first_timestamp`| 文字列| &#34;1390574181854&#34;|
|`hubspot_wf_associated_company_properties_first_conversion_date`| 文字列| &#34;1477892839033&#34;|
|`hubspot_wf_associated_company_properties_engagements_last_meeting_booked`| 文字列| &#34;&#34;|
|`hubspot_wf_associated_company_properties_first_contact_createdate`| 文字列| &#34;1390574181854&#34;|
|`hubspot_wf_associated_company_properties_twitterhandle`| 文字列| &#34;HubSpot&#34;|
|`hubspot_wf_associated_company_properties_hs_lastmodifieddate`| 文字列| &#34;1484854497180&#34;|
|`hubspot_wf_associated_company_properties_notes_last_contacted`| 文字列| &#34;1479030015191&#34;|
|`hubspot_wf_associated_company_properties_phone`| 文字列| &#34;&#43;1 888-482-7768&#34;|
|`hubspot_wf_associated_company_properties_num_conversion_events`| 文字列| &#34;40&#34;|
|`hubspot_wf_associated_company_properties_domain`| 文字列| &#34;hubspot.com&#34;|
|`hubspot_wf_associated_company_properties_is_public`| 文字列| &#34;true&#34;|
|`hubspot_wf_associated_company_properties_name`| 文字列| &#34;Hubspot, Inc.&#34;|
|`hubspot_wf_associated_company_properties_recent_conversion_date`| 文字列| &#34;1484844458500&#34;|
|`hubspot_wf_associated_company_properties_first_conversion_event_name`| 文字列| &#34;excedalogic form&#34;|
|`hubspot_wf_associated_company_properties_num_notes`| 文字列| &#34;12&#34;|

## ベンダーのドキュメンテーション

* [ワークフローでのWebhooksの使用](https://developers.hubspot.com/docs/methods/workflows/webhook_information)
