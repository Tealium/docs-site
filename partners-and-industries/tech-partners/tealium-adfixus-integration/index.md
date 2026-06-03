---
title: Tealium + AdFixus Integration Guide
description: This article describes how to set up the AdFixus integration tag in your iQ Tag Management account.
url: https://docs.tealium.com/partners-and-industries/tech-partners/tealium-adfixus-integration/
---
With AdFixus, businesses own their data while individuals control consent with their privacy-focused solution. The AdFixus-patented first-party cookie platform empowers businesses to return a total view of their audience and use that data across their existing systems to improve personalisation, analysis, and media optimization. Ingestion of the AdFixus ID into Tealium allows organizations to leverage the AdFixus-patented identity platform alongside their Tealium data to unify a complete view of audiences (cross-domain and multi-domain) and offer their customers a seamless end-to-end unified experience.

## Prerequisites

* **Tealium**
    * At least one of the following:
        * iQ Tag Management
        * AudienceStream
        * EventStream (Optional)
* **AdFixus**
    * The AdFixus platform implemented on your organization’s web properties/domains.
    * An active AdFixus organization license key.

## How it works

Implement the AdFixus ID through your owned digital properties, not through the iQ Tag Management platform. This method of installation ensures complete browser coverage.

Add the AdFixus ID to your organization’s iQ Tag Management Data Layer, and then it can be mapped to related tags or sent to the Tealium server-side platform for ingestion and profile enrichment. If your organization uses only AudienceStream without iQ Tag Management, pass the AdFixus ID in to Tealium and assign it to the appropriate attribute.

## iQ Tag Management configuration

To integrate the AdFixus ID into iQ Tag Management:

1. Create an AdFixus [data layer variable]() with your iQ Tag Management instance.
    * Create this variable in every Tealium account profile that uses the AdFixus ID.
    * Your AdFixus ID will likely be stored in a cookie on your website. For more information, ask the [AdFixus Implementation Team](https://www.adfixus.com/contact).![](/images/tech-partners/adfixus-add-variable.png)
1. Identify the relevant tags that should send the AdFixus ID variable and [map the data points]().
    1. From the **Variables** drop-down list, select the data variable and click **Select Destination**.![](/images/tech-partners/adfixus-select-destination.png)
    1. Click **Add Custom Destination**, enter the expected name for the AdFixus ID in **Custom Destination** field, and click **&#43;Add**.![](/images/tech-partners/adfixus-custom-destination.png)
        * Repeat this process for every new or existing tag that will use the AdFixus ID.
1. Save and publish.

## Server-side configuration

To integrate the AdFixus ID into AudienceStream and EventStream:

1. If you are also using iQ Tag Management, configure the [Tealium Collect tag]().
  * The AdFixus ID appears as a universal variable under your [event attributes]().
1. If you are not using iQ Tag Management, [create an event attribute]() for the AdFixus ID.
    1. Go to **Event Attributes** and click **&#43; Add Attribute**.
    1. Select **Universal Variable** and click **Continue**.
    1. Select **String** and click **Continue**.
    1. Enter the attribute name and any other relevant information.![](/images/tech-partners/adfixus-add-attribute.png)
    1. Click **Finish**.
        * If you plan to send more data from AdFixus to Tealium, create attributes for that data too.
        * We recommend that you create [event specifications]() for all attributes in the dataset.
1. [Create a visitor attribute]() for the AdFixus ID.
    1. Go to **Visitor/Visit Attributes** and click **&#43; Add Attribute**.
    1. Select **Visitor** and click **Continue**.
    1. Select **String** or **Visitor ID** and click **Continue**.
        * If you select **Visitor ID**, you cannot change the data type later.
    1. Enter the attribute name and any other relevant information.
    1. Click **Add Enrichment**.
    1. Select the AdFixus ID event attribute that you created in step 1 or 2 and click **Create Rule**.
    1. Create a rule that checks if your attribute `is assigned` and `does not equal (ignore case) none`.![](/images/tech-partners/adfixus-attribute-ready.png)
1. Save and publish.

The AdFixus ID is now available as a mappable attribute for AudienceStream connectors and can be mapped in any related integrations.

## Vendor documentation

* [Integration: Tealium AudienceStream CDP and AdFixus](https://www.adfixus.com/integrations/integration-tealium-audience-stream-cdp-and-adfixus).