---
title: Google Ads Leads setup guide
description: This article provides information on adding a Google Ads Leads data source and adding a webhook for this data source.
url: https://docs.tealium.com/server-side/data-sources/webhooks/setup-guides/google-ads-leads/
---

The Lead Form extensions in Google Ads help you generate leads by letting visitors submit their information in a form directly in your ad. To send leads data to Tealium in real time, use Tealium's Google Ads Leads data source and a Google Ads Lead Form webhook integration.

## Add a Google Ads Leads data source

To add the Google Ads Leads data source to your Tealium Customer Data Hub profile, see [Data Sources](https://docs.tealium.com/about-data-sources/). After adding and connecting the data source, save and publish your profile.

Adding the Google Ads Leads data source to your Tealium Customer Data Hub profile generates a unique URL and a data source key to use in your webhook configuration. The format of the URL is as follows:

```
https://collect.tealiumiq.com/integration/event/ACCOUNT/PROFILE/DATA_SOURCE_KEY
```

## Configure a Google Ads Lead form webhook

For more information on configuring a Google Ads Lead Form webhook integration, see [Set up a webhook integration for a lead form extension](https://support.google.com/google-ads/answer/10089407 "https://support.google.com/google-ads/answer/10089407").

### Configure a webhook for a new campaign

Follow these steps to configure a webhook for a new campaign:

1. During campaign setup in Google Ads, go to **Extensions &gt; More Extensions &gt; Lead Form Extensions**.
1. After entering information in the form, click **Export Leads from Google Ads &gt; Other Data Integration Options**.
1. Enter the following data source information in the Webhook Integration form:
    * Webhook URL – the generated data source URL.
    * Key – the generated data source key.

1. Continue with campaign setup.

### Configure a webhook for an existing campaign

Follow these steps to configure a webhook for an existing campaign with a lead form:

1. In your Google Ads account, navigate to **Ads &amp; Extensions &gt; Extensions**.
1. Click **Lead Form**.
1. Click the pencil icon to edit the lead form name.
1. Click **Export Leads from Google Ads &gt; Other Data Integration Options**.
1. Enter the following data source details in the Webhook Integration form:
    * Webhook URL – the generated data source URL.
    * Key – the generated data source key.

1. Click **Save**.

## Events and attributes

All incoming Google Ads Leads event attributes are prefixed with `google_ads_lead_`. The attributes vary depending on the configuration of the lead form fields.

Events from this data source may have the following event attributes:

|Key| Type| Example|
|---| ---| ---|
|`google_ads_lead_lead_id`| String| "ID-123-abcDEFghiJKLmno456PQRstuVWXyz-7890"|
|`google_ads_lead_api_version`| String| "1.0"|
|`google_ads_lead_form_id`| String| "2"|
|`google_ads_lead_campaign_id`| String| "281492475085606"|
|`google_ads_lead_google_key`| String| "231ji3"|
|`google_ads_lead_is_test`| String| "true"|
|`google_ads_lead_gcl_id`| String| "ID-123-abcDEFghiJKLmno456PQRstuVWXyz-7890"|
|`google_ads_lead_adgroup_id`| String| "20000000000"|
|`google_ads_lead_creative_id`| String| "30000000000"|
|`google_ads_lead_full_name`| String| "Test Tester"|
|`google_ads_lead_first_name`| String| "Test"|
|`google_ads_lead_last_name`| String| "Tester"|
|`google_ads_lead_phone_number`| String| "888-555-1212"|
|`google_ads_lead_email`| String| "tester@googleads.com"|
|`google_ads_lead_city`| String| "San Diego"|
|`google_ads_lead_postal_code`| String| "92121"|
|`google_ads_lead_region`| String| "California"|
|`google_ads_lead_country`| String| "United States"|
|`google_ads_lead_company_name`| String| "XYZ Corp"|
|`google_ads_lead_job_title`| String| "Leads Tester"|

## Vendor documentation

* [About lead form extensions](https://support.google.com/google-ads/answer/9423234?hl=en&amp;ref_topic=9716366)
* [Using lead forms in Discovery campaigns](https://support.google.com/google-ads/answer/10014398?hl=en#zippy=%2Cadd-a-lead-form-to-an-existing-campaign)
* [Set up a webhook integration for a lead form extension](https://support.google.com/google-ads/answer/10089407 "https://support.google.com/google-ads/answer/10089407")
