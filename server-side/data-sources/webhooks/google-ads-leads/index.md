---
title: Google Ads Leads setup guide
description: This article provides information on adding a Google Ads Leads data source and adding a webhook for this data source.
url: https://docs.tealium.com/server-side/data-sources/webhooks/google-ads-leads/
---

The Lead Form extensions in Google Ads help you generate leads by letting visitors submit their information in a form directly in your ad. To send leads data to Tealium in real time, use Tealium&#39;s Google Ads Leads data source and a Google Ads Lead Form webhook integration.

## Add a Google Ads Leads data source

To add the Google Ads Leads data source to your Tealium Customer Data Hub profile, see [Data Sources](). After adding and connecting the data source, save and publish your profile.

Adding the Google Ads Leads data source to your Tealium Customer Data Hub profile generates a unique URL and a data source key to use in your webhook configuration. The format of the URL is as follows:

```
https://collect.tealiumiq.com/integration/event/ACCOUNT/PROFILE/DATA_SOURCE_KEY
```

## Configure a Google Ads Lead form webhook

For more information on configuring a Google Ads Lead Form webhook integration, see [Set up a webhook integration for a lead form extension](https://support.google.com/google-ads/answer/10089407 &#34;https://support.google.com/google-ads/answer/10089407&#34;).

### Configure a webhook for a new campaign

Follow these steps to configure a webhook for a new campaign:

1. During campaign setup in Google Ads, go to **Extensions &amp;gt; More Extensions &amp;gt; Lead Form Extensions**.
1. After entering information in the form, click **Export Leads from Google Ads &amp;gt; Other Data Integration Options**.
1. Enter the following data source information in the Webhook Integration form:
    * Webhook URL – the generated data source URL.
    * Key – the generated data source key.

1. Continue with campaign setup.

### Configure a webhook for an existing campaign

Follow these steps to configure a webhook for an existing campaign with a lead form:

1. In your Google Ads account, navigate to **Ads &amp;amp; Extensions &amp;gt; Extensions**.
1. Click **Lead Form**.
1. Click the pencil icon to edit the lead form name.
1. Click **Export Leads from Google Ads &amp;gt; Other Data Integration Options**.
1. Enter the following data source details in the Webhook Integration form:
    * Webhook URL – the generated data source URL.
    * Key – the generated data source key.

1. Click **Save**.

## Events and attributes

All incoming Google Ads Leads event attributes are prefixed with `google_ads_lead_`. The attributes vary depending on the configuration of the lead form fields.

Events from this data source may have the following event attributes:

|Key| Type| Example|
|---| ---| ---|
|`google_ads_lead_lead_id`| String| &#34;ID-123-abcDEFghiJKLmno456PQRstuVWXyz-7890&#34;|
|`google_ads_lead_api_version`| String| &#34;1.0&#34;|
|`google_ads_lead_form_id`| String| &#34;2&#34;|
|`google_ads_lead_campaign_id`| String| &#34;281492475085606&#34;|
|`google_ads_lead_google_key`| String| &#34;231ji3&#34;|
|`google_ads_lead_is_test`| String| &#34;true&#34;|
|`google_ads_lead_gcl_id`| String| &#34;ID-123-abcDEFghiJKLmno456PQRstuVWXyz-7890&#34;|
|`google_ads_lead_adgroup_id`| String| &#34;20000000000&#34;|
|`google_ads_lead_creative_id`| String| &#34;30000000000&#34;|
|`google_ads_lead_full_name`| String| &#34;Test Tester&#34;|
|`google_ads_lead_first_name`| String| &#34;Test&#34;|
|`google_ads_lead_last_name`| String| &#34;Tester&#34;|
|`google_ads_lead_phone_number`| String| &#34;888-555-1212&#34;|
|`google_ads_lead_email`| String| &#34;tester@googleads.com&#34;|
|`google_ads_lead_city`| String| &#34;San Diego&#34;|
|`google_ads_lead_postal_code`| String| &#34;92121&#34;|
|`google_ads_lead_region`| String| &#34;California&#34;|
|`google_ads_lead_country`| String| &#34;United States&#34;|
|`google_ads_lead_company_name`| String| &#34;XYZ Corp&#34;|
|`google_ads_lead_job_title`| String| &#34;Leads Tester&#34;|

## Vendor documentation

* [About lead form extensions](https://support.google.com/google-ads/answer/9423234?hl=en&amp;amp;ref_topic=9716366)
* [Using lead forms in Discovery campaigns](https://support.google.com/google-ads/answer/10014398?hl=en#zippy=%2Cadd-a-lead-form-to-an-existing-campaign)
* [Set up a webhook integration for a lead form extension](https://support.google.com/google-ads/answer/10089407 &#34;https://support.google.com/google-ads/answer/10089407&#34;)
