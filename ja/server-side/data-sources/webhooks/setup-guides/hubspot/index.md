---
title: HubspotワークフローのインカミングWebhook構成ガイド
description: この記事では、Hubspotデータソースを使用してHubspotアカウントにWebhookを作成し、Tealiumにアクション可能なイベントを送信する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/webhooks/setup-guides/hubspot/
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
    * HubSpotマーケティングプロフェッショナルまたはエンタープライズアカウントでは、**Contacts &gt; Workflows**に移動します。
    * HubSpotセールスプロフェッショナルアカウントでは、**Sales Tools &gt; Workflows**に移動します。

1. 編集したいワークフローの名前をクリックします。
1. アクションを追加するためにプラス（**+**）アイコンをクリックし、右ペインで**Trigger a webhook**を選択します。
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
|`hubspot_wf_vid`| 文字列| "3234574"|
|`hubspot_wf_canonical_vid`| 文字列| "3234574"|
|`hubspot_wf_portal_id`| 文字列| "62515"|
|`hubspot_wf_is_contact`| ブール値| "true"|
|`hubspot_wf_profile_token`| 文字列| "AO_T-mOFUify..."|
|`hubspot_wf_profile_url`| 文字列| "https://app.hubspot.com/..."|
|`hubspot_wf_properties_lead_source`| 文字列| "DiscoverOrg"|
|`hubspot_wf_properties_num_unique_conversion_events`| 文字列| "0"|
|`hubspot_wf_properties_hs_analytics_revenue`| 文字列| "0.0"|
|`hubspot_wf_properties_createdate`| 文字列| "1484026585538"|
|`hubspot_wf_properties_hs_email_optout`| 文字列| "true"|
|`hubspot_wf_properties_hs_predictivecontactscore`| 文字列| "50"|
|`hubspot_wf_properties_annualrevenue`| 文字列| "181900000"|
|`hubspot_wf_properties_hs_analytics_num_page_views`| 文字列| "0"|
|`hubspot_wf_properties_state`| 文字列| "MA"|
|`hubspot_wf_properties_zip`| 文字列| "02139"|
|`hubspot_wf_properties_hs_predictability`| 文字列| "bucket_3"|
|`hubspot_wf_properties_hubspotscore`| 文字列| "0"|
|`hubspot_wf_properties_linkedinconnections`| 文字列| "0"|
|`hubspot_wf_properties_hs_lifecyclestage_subscriber_date`| 文字列| "1484026585538"|
|`hubspot_wf_properties_hs_analytics_average_page_views`| 文字列| "0"|
|`hubspot_wf_properties_lastname`| 文字列| "Huang"|
|`hubspot_wf_properties_twitterhandle`| 文字列| "ghidinelli"|
|`hubspot_wf_properties_phone`| 文字列| "555-122-2323"|
|`hubspot_wf_properties_num_conversion_events`| 文字列| "0"|
|`hubspot_wf_properties_currentlyinworkflow`| 文字列| "false"|
|`hubspot_wf_properties_hs_analytics_num_event_completions`| 文字列| "2"|
|`hubspot_wf_properties_followercount`| 文字列| "582"|
|`hubspot_wf_properties_associatedcompanyid`| 文字列| "184896670"|
|`hubspot_wf_properties_firstname`| 文字列| "Codey"|
|`hubspot_wf_properties_city`| 文字列| "Cambridge"|
|`hubspot_wf_properties_hs_social_num_broadcast_clicks`| 文字列| "0"|
|`hubspot_wf_properties_hs_analytics_num_visits`| 文字列| "0"|
|`hubspot_wf_properties_twitterbio`| 文字列| "Racer, entrepreneur, world traveler..."|
|`hubspot_wf_properties_hs_social_linkedin_clicks`| 文字列| "0"|
|`hubspot_wf_properties_hs_twitterid`| 文字列| "49019793"|
|`hubspot_wf_properties_associatedcompanylastupdated`| 文字列| "13365279006997343"|
|`hubspot_wf_properties_hs_analytics_source`| 文字列| "OFFLINE"|
|`hubspot_wf_properties_company`| 文字列| "HubSpot"|
|`hubspot_wf_properties_email`| 文字列| "testingapis@hubspot.com"|
|`hubspot_wf_properties_linkedinbio`| 文字列| "Racecar driver, entrepreneur, world traveler..."|
|`hubspot_wf_properties_website`| 文字列| "http://hubspot.com"|
|`hubspot_wf_properties_address`| 文字列| "25 First Street"|
|`hubspot_wf_properties_hs_analytics_first_timestamp`| 文字列| "1484026585538"|
|`hubspot_wf_properties_lastmodifieddate`| 文字列| "1484858431084"|
|`hubspot_wf_properties_photo`| 文字列| "<https://d2ojpxxtu63wzl.cloudfront.net/st>..."|
|`hubspot_wf_properties_hs_social_google_plus_clicks`| 文字列| "0"|
|`hubspot_wf_properties_kloutscoregeneral`| 文字列| "48"|
|`hubspot_wf_properties_hs_social_facebook_clicks`| 文字列| "0"|
|`hubspot_wf_properties_twitterprofilephoto`| 文字列| "https://pbs.twimg.com/profile_images..."|
|`hubspot_wf_properties_hs_social_twitter_clicks`| 文字列| "0"|
|`hubspot_wf_properties_hs_analytics_source_data_1`| 文字列| "API"|
|`hubspot_wf_properties_lifecyclestage`| 文字列| "subscriber"|
|`hubspot_wf_associated_company_company_id`| 文字列| "184896670"|
|`hubspot_wf_associated_company_portal_id`| 文字列| "62515"|
|`hubspot_wf_associated_company_properties_country`| 文字列| "United States"|
|`hubspot_wf_associated_company_properties_city`| 文字列| "Cambridge"|
|`hubspot_wf_associated_company_properties_num_associated_contacts`| 文字列| "102"|
|`hubspot_wf_associated_company_properties_timezone`| 文字列| "America/New_York"|
|`hubspot_wf_associated_company_properties_facebook_company_page`| 文字列| "https://www.facebook.com/hubspot"|
|`hubspot_wf_associated_company_properties_createdate`| 文字列| "1457708103847"|
|`hubspot_wf_associated_company_properties_description`| 文字列| "HubSpot is the world’s leading..."|
|`hubspot_wf_associated_company_properties_industry`| 文字列| "COMPUTER_SOFTWARE"|
|`hubspot_wf_associated_company_properties_total_money_raised`| 文字列| "$100.5M"|
|`hubspot_wf_associated_company_properties_days_to_close`| 文字列| "220"|
|`hubspot_wf_associated_company_properties_hs_analytics_num_visits`| 文字列| "0"|
|`hubspot_wf_associated_company_properties_linkedin_company_page`| 文字列| "http://www.linkedin.com/company/68529"|
|`hubspot_wf_associated_company_properties_recent_conversion_event_name`| 文字列| "Contact Us: excedalogic form"|
|`hubspot_wf_associated_company_properties_hs_analytics_source`| 文字列| "OFFLINE"|
|`hubspot_wf_associated_company_properties_num_contacted_notes`| 文字列| "12"|
|`hubspot_wf_associated_company_properties_annualrevenue`| 文字列| "250000000"|
|`hubspot_wf_associated_company_properties_founded_year`| 文字列| "2006"|
|`hubspot_wf_associated_company_properties_hs_analytics_num_page_views`| 文字列| "0"|
|`hubspot_wf_associated_company_properties_state`| 文字列| "MA"|
|`hubspot_wf_associated_company_properties_linkedinbio`| 文字列| "HubSpot is the world’s leading..."|
|`hubspot_wf_associated_company_properties_zip`| 文字列| "02141"|
|`hubspot_wf_associated_company_properties_notes_last_updated`| 文字列| "1480625888696"|
|`hubspot_wf_associated_company_properties_website`| 文字列| "hubspot.com"|
|`hubspot_wf_associated_company_properties_closedate`| 文字列| "1476768116137"|
|`hubspot_wf_associated_company_properties_hs_analytics_first_timestamp`| 文字列| "1390574181854"|
|`hubspot_wf_associated_company_properties_first_conversion_date`| 文字列| "1477892839033"|
|`hubspot_wf_associated_company_properties_engagements_last_meeting_booked`| 文字列| ""|
|`hubspot_wf_associated_company_properties_first_contact_createdate`| 文字列| "1390574181854"|
|`hubspot_wf_associated_company_properties_twitterhandle`| 文字列| "HubSpot"|
|`hubspot_wf_associated_company_properties_hs_lastmodifieddate`| 文字列| "1484854497180"|
|`hubspot_wf_associated_company_properties_notes_last_contacted`| 文字列| "1479030015191"|
|`hubspot_wf_associated_company_properties_phone`| 文字列| "+1 888-482-7768"|
|`hubspot_wf_associated_company_properties_num_conversion_events`| 文字列| "40"|
|`hubspot_wf_associated_company_properties_domain`| 文字列| "hubspot.com"|
|`hubspot_wf_associated_company_properties_is_public`| 文字列| "true"|
|`hubspot_wf_associated_company_properties_name`| 文字列| "Hubspot, Inc."|
|`hubspot_wf_associated_company_properties_recent_conversion_date`| 文字列| "1484844458500"|
|`hubspot_wf_associated_company_properties_first_conversion_event_name`| 文字列| "excedalogic form"|
|`hubspot_wf_associated_company_properties_num_notes`| 文字列| "12"|

## ベンダーのドキュメンテーション

* [ワークフローでのWebhooksの使用](https://developers.hubspot.com/docs/methods/workflows/webhook_information)
