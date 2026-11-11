---
title: HubSpot Workflow受信Webhook構成ガイド
description: この記事では、HubSpotデータソースを使用してHubSpotアカウントにWebhookを作成し、処理可能なイベントをTealiumに送信する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/webhooks/hubspot/
---
## 前提条件

* HubSpot Marketing Professional、Sales Professional、またはEnterpriseアカウント
* Event Streamingおよび／またはCustomer Data Platform（CDP）アカウント

## 仕組み

HubSpotは、指定したエンドポイントに送信リクエストを送るWebhook APIを提供しています。これらのリクエストはEvent Streamingへのプッシュ通知として機能し、HubSpotアカウントで発生した事象を通知します。UDHにHubSpotデータソースを追加すると、一意のエンドポイントが生成されます。このエンドポイントを使用してHubSpot Webhookを構成します。

## HubSpotデータソースの追加

続行する前に、HubSpotデータソースを追加します。HubSpotデータソースによって、HubSpotの構成でHTTP POST URLとして使用する一意のURLが生成されます。生成されるURLの形式は次のとおりです。

```
https://collect.tealiumiq.com/integration/event/ACCOUNT/PROFILE/DATA_SOURCE_KEY
```

## HubSpotの構成

データソースのエンドポイントを取得したら、HubSpotアカウントに移動してWebhookを作成します。

1. [HubSpotアカウント](https://login.hubspot.com/)にログインします。
    * HubSpot Marketing ProfessionalまたはEnterpriseアカウントで、**Contacts &gt; Workflows**に移動します。
    * HubSpot Sales Professionalアカウントで、**Sales Tools &gt; Workflows**に移動します。

1. 編集するワークフローの名前をクリックします。
1. プラス（**+**）アイコンをクリックしてアクションを追加し、右側のペインで**Trigger a webhook**を選択します。
1. ドロップダウンリストから**POST**を選択します。
1. WebHook URLに次のURLを入力します。  
      ```
      https://collect.tealiumiq.com/integration/event/{account}/{profile}/{unique_id}
      ```

1. **Save**をクリックします。
## イベントと属性

受信するすべてのHubSpotイベント属性には、自動的に `hubspot_wf_` というプレフィックスとアンダースコアがエンリッチメントされます。たとえば、`properties.lead_source` は `hubspot_wf_properties_lead_source` になります。

次の表は、HubSpotによって生成されるWebhookイベントと属性の一覧です。

|イベント属性|型|例|
|---|---|---|
|`hubspot_wf_vid`| String| "3234574"|
|`hubspot_wf_canonical_vid`| String| "3234574"|
|`hubspot_wf_portal_id`| String| "62515"|
|`hubspot_wf_is_contact`| Boolean| "true"|
|`hubspot_wf_profile_token`| String| "AO_T-mOFUify..."|
|`hubspot_wf_profile_url`| String| "https://app.hubspot.com/..."|
|`hubspot_wf_properties_lead_source`| String| "DiscoverOrg"|
|`hubspot_wf_properties_num_unique_conversion_events`| String| "0"|
|`hubspot_wf_properties_hs_analytics_revenue`| String| "0.0"|
|`hubspot_wf_properties_createdate`| String| "1484026585538"|
|`hubspot_wf_properties_hs_email_optout`| String| "true"|
|`hubspot_wf_properties_hs_predictivecontactscore`| String| "50"|
|`hubspot_wf_properties_annualrevenue`| String| "181900000"|
|`hubspot_wf_properties_hs_analytics_num_page_views`| String| "0"|
|`hubspot_wf_properties_state`| String| "MA"|
|`hubspot_wf_properties_zip`| String| "02139"|
|`hubspot_wf_properties_hs_predictability`| String| "bucket_3"|
|`hubspot_wf_properties_hubspotscore`| String| "0"|
|`hubspot_wf_properties_linkedinconnections`| String| "0"|
|`hubspot_wf_properties_hs_lifecyclestage_subscriber_date`| String| "1484026585538"|
|`hubspot_wf_properties_hs_analytics_average_page_views`| String| "0"|
|`hubspot_wf_properties_lastname`| String| "Huang"|
|`hubspot_wf_properties_twitterhandle`| String| "ghidinelli"|
|`hubspot_wf_properties_phone`| String| "555-122-2323"|
|`hubspot_wf_properties_num_conversion_events`| String| "0"|
|`hubspot_wf_properties_currentlyinworkflow`| String| "false"|
|`hubspot_wf_properties_hs_analytics_num_event_completions`| String| "2"|
|`hubspot_wf_properties_followercount`| String| "582"|
|`hubspot_wf_properties_associatedcompanyid`| String| "184896670"|
|`hubspot_wf_properties_firstname`| String| "Codey"|
|`hubspot_wf_properties_city`| String| "Cambridge"|
|`hubspot_wf_properties_hs_social_num_broadcast_clicks`| String| "0"|
|`hubspot_wf_properties_hs_analytics_num_visits`| String| "0"|
|`hubspot_wf_properties_twitterbio`| String| "Racer, entrepreneur, world traveler..."|
|`hubspot_wf_properties_hs_social_linkedin_clicks`| String| "0"|
|`hubspot_wf_properties_hs_twitterid`| String| "49019793"|
|`hubspot_wf_properties_associatedcompanylastupdated`| String| "13365279006997343"|
|`hubspot_wf_properties_hs_analytics_source`| String| "OFFLINE"|
|`hubspot_wf_properties_company`| String| "HubSpot"|
|`hubspot_wf_properties_email`| String| "testingapis@hubspot.com"|
|`hubspot_wf_properties_linkedinbio`| String| "Racecar driver, entrepreneur, world traveler..."|
|`hubspot_wf_properties_website`| String| "http://hubspot.com"|
|`hubspot_wf_properties_address`| String| "25 First Street"|
|`hubspot_wf_properties_hs_analytics_first_timestamp`| String| "1484026585538"|
|`hubspot_wf_properties_lastmodifieddate`| String| "1484858431084"|
|`hubspot_wf_properties_photo`| String| "<https://d2ojpxxtu63wzl.cloudfront.net/st>..."|
|`hubspot_wf_properties_hs_social_google_plus_clicks`| String| "0"|
|`hubspot_wf_properties_kloutscoregeneral`| String| "48"|
|`hubspot_wf_properties_hs_social_facebook_clicks`| String| "0"|
|`hubspot_wf_properties_twitterprofilephoto`| String| "https://pbs.twimg.com/profile_images..."|
|`hubspot_wf_properties_hs_social_twitter_clicks`| String| "0"|
|`hubspot_wf_properties_hs_analytics_source_data_1`| String| "API"|
|`hubspot_wf_properties_lifecyclestage`| String| "subscriber"|
|`hubspot_wf_associated_company_company_id`| String| "184896670"|
|`hubspot_wf_associated_company_portal_id`| String| "62515"|
|`hubspot_wf_associated_company_properties_country`| String| "United States"|
|`hubspot_wf_associated_company_properties_city`| String| "Cambridge"|
|`hubspot_wf_associated_company_properties_num_associated_contacts`| String| "102"|
|`hubspot_wf_associated_company_properties_timezone`| String| "America/New_York"|
|`hubspot_wf_associated_company_properties_facebook_company_page`| String| "https://www.facebook.com/hubspot"|
|`hubspot_wf_associated_company_properties_createdate`| String| "1457708103847"|
|`hubspot_wf_associated_company_properties_description`| String| "HubSpot is the world’s leading..."|
|`hubspot_wf_associated_company_properties_industry`| String| "COMPUTER_SOFTWARE"|
|`hubspot_wf_associated_company_properties_total_money_raised`| String| "$100.5M"|
|`hubspot_wf_associated_company_properties_days_to_close`| String| "220"|
|`hubspot_wf_associated_company_properties_hs_analytics_num_visits`| String| "0"|
|`hubspot_wf_associated_company_properties_linkedin_company_page`| String| "http://www.linkedin.com/company/68529"|
|`hubspot_wf_associated_company_properties_recent_conversion_event_name`| String| "Contact Us: excedalogic form"|
|`hubspot_wf_associated_company_properties_hs_analytics_source`| String| "OFFLINE"|
|`hubspot_wf_associated_company_properties_num_contacted_notes`| String| "12"|
|`hubspot_wf_associated_company_properties_annualrevenue`| String| "250000000"|
|`hubspot_wf_associated_company_properties_founded_year`| String| "2006"|
|`hubspot_wf_associated_company_properties_hs_analytics_num_page_views`| String| "0"|
|`hubspot_wf_associated_company_properties_state`| String| "MA"|
|`hubspot_wf_associated_company_properties_linkedinbio`| String| "HubSpot is the world’s leading..."|
|`hubspot_wf_associated_company_properties_zip`| String| "02141"|
|`hubspot_wf_associated_company_properties_notes_last_updated`| String| "1480625888696"|
|`hubspot_wf_associated_company_properties_website`| String| "hubspot.com"|
|`hubspot_wf_associated_company_properties_closedate`| String| "1476768116137"|
|`hubspot_wf_associated_company_properties_hs_analytics_first_timestamp`| String| "1390574181854"|
|`hubspot_wf_associated_company_properties_first_conversion_date`| String| "1477892839033"|
|`hubspot_wf_associated_company_properties_engagements_last_meeting_booked`| String| ""|
|`hubspot_wf_associated_company_properties_first_contact_createdate`| String| "1390574181854"|
|`hubspot_wf_associated_company_properties_twitterhandle`| String| "HubSpot"|
|`hubspot_wf_associated_company_properties_hs_lastmodifieddate`| String| "1484854497180"|
|`hubspot_wf_associated_company_properties_notes_last_contacted`| String| "1479030015191"|
|`hubspot_wf_associated_company_properties_phone`| String| "+1 888-482-7768"|
|`hubspot_wf_associated_company_properties_num_conversion_events`| String| "40"|
|`hubspot_wf_associated_company_properties_domain`| String| "hubspot.com"|
|`hubspot_wf_associated_company_properties_is_public`| String| "true"|
|`hubspot_wf_associated_company_properties_name`| String| "Hubspot, Inc."|
|`hubspot_wf_associated_company_properties_recent_conversion_date`| String| "1484844458500"|
|`hubspot_wf_associated_company_properties_first_conversion_event_name`| String| "excedalogic form"|
|`hubspot_wf_associated_company_properties_num_notes`| "12"|

## ベンダーのドキュメント

* [ワークフローでのWebhookの使用](https://developers.hubspot.com/docs/methods/workflows/webhook_information)