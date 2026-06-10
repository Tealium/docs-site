---
title: Google Ads Leads構成ガイド
description: この記事では、Google Ads Leadsデータソースの追加と、このデータソースのWebhookの追加について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/webhooks/setup-guides/google-ads-leads/
---

Google Adsのリードフォーム拡張機能は、訪問があなたの広告内のフォームに情報を直接提出することでリードを生成するのに役立ちます。リアルタイムでリードデータをTealiumに送信するには、TealiumのGoogle Ads LeadsデータソースとGoogle Ads Lead Form webhook統合を使用します。

## Google Ads Leadsデータソースの追加

Tealium Customer Data HubプロファイルにGoogle Ads Leadsデータソースを追加するには、[Data Sources]()を参照してください。データソースを追加し、接続した後、プロファイルを保存して公開します。

Tealium Customer Data HubプロファイルにGoogle Ads Leadsデータソースを追加すると、webhook構成で使用するためのユニークなURLとデータソースキーが生成されます。URLの形式は次のとおりです：

```
https://collect.tealiumiq.com/integration/event/ACCOUNT/PROFILE/DATA_SOURCE_KEY
```

## Google Ads Leadフォームwebhookの構成

Google Ads Lead Form webhook統合の構成についての詳細は、[リードフォーム拡張機能のwebhook統合の構成](https://support.google.com/google-ads/answer/10089407 &#34;https://support.google.com/google-ads/answer/10089407&#34;)を参照してください。

### 新しいキャンペーンのwebhookを構成する

新しいキャンペーンのwebhookを構成するには、以下の手順を実行します：

1. Google Adsでキャンペーンの構成を行う際に、**Extensions &amp;gt; More Extensions &amp;gt; Lead Form Extensions**に移動します。
1. フォームに情報を入力した後、**Export Leads from Google Ads &amp;gt; Other Data Integration Options**をクリックします。
1. Webhook Integrationフォームに以下のデータソース情報を入力します：
    * Webhook URL – 生成されたデータソースURL。
    * Key – 生成されたデータソースキー。

1. キャンペーンの構成を続けます。

### 既存のキャンペーンのwebhookを構成する

リードフォームを持つ既存のキャンペーンのwebhookを構成するには、以下の手順を実行します：

1. Google Adsアカウントで、**Ads &amp;amp; Extensions &amp;gt; Extensions**に移動します。
1. **Lead Form**をクリックします。
1. 鉛筆アイコンをクリックしてリードフォームの名前を編集します。
1. **Export Leads from Google Ads &amp;gt; Other Data Integration Options**をクリックします。
1. Webhook Integrationフォームに以下のデータソース詳細を入力します：
    * Webhook URL – 生成されたデータソースURL。
    * Key – 生成されたデータソースキー。

1. **Save**をクリックします。

## イベントと属性

すべての受信Google Ads Leadsイベント属性は`google_ads_lead_`で始まります。属性はリードフォームフィールドの構成により異なります。

このデータソースからのイベントには、以下のイベント属性が含まれる可能性があります：

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

## ベンダーのドキュメンテーション

* [リードフォーム拡張機能について](https://support.google.com/google-ads/answer/9423234?hl=en&amp;amp;ref_topic=9716366)
* [Discoveryキャンペーンでのリードフォームの使用](https://support.google.com/google-ads/answer/10014398?hl=en#zippy=%2Cadd-a-lead-form-to-an-existing-campaign)
* [リードフォーム拡張機能のwebhook統合の構成](https://support.google.com/google-ads/answer/10089407 &#34;https://support.google.com/google-ads/answer/10089407&#34;)
