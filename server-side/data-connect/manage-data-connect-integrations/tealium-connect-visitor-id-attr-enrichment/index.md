---
title: Visitor ID attribute enrichment for Tealium Connect
description: This article describes how to map and enrich a visitor ID attribute in AudienceStream for use in Data Connect.
url: https://docs.tealium.com/server-side/data-connect/manage-data-connect-integrations/tealium-connect-visitor-id-attr-enrichment/
---
To enrich a visitor ID attribute for use with Tealium Connect, complete the following steps:

1. In the Tealium event specification you created for use with Data Connect, look for an event sent to your Tealium Connect data source. 
  1. Note the name of the event attribute that you will use with the visitor ID attribute in your Workato recipe, for example, `customer_id`.
  1. Create a string event attribute of type Universal Data Object with the event attribute name, if it does not already exist.
1. Create a rule that identifies events from your Tealium Connect data source based on the built-in event attribute `tealium_datasource={{tealium_data_source_key}}` if this rule does not already exist. Your Data Source Key can be found in your [Tealium Connect data source]().
1. Navigate to **AudienceStream &gt; Visitor/Visit Attributes**. 
1. Select the visitor ID you want to use with Tealium Connect data. If a visitor ID does not already exist, complete the following steps:
  1. Click **&#43; Add Attribute**.
  1. For the attribute scope, select **Visitor** and click **Continue**.
  1. In the **Choose a Data Type** screen, select **Visitor ID** and click **Continue**.
  1. In the attribute screen, enter a name for the visitor ID attribute.
1. Select your visitor ID and click **Add Enrichment**.
1. In the **Set Visitor ID to** drop down, select the event attribute you selected above.
1. For the **When** condition, ensure this enrichment occurs when the data source is the Tealium Connect data source by choosing the Tealium Connect data source rule.
1. Click **Finish**. 

 To ensure visitors from Tealium Connect persist in AudienceStream, assign a badge whenever a Data Connect event occurs, using the same rule, if such a badge does not already exist.

