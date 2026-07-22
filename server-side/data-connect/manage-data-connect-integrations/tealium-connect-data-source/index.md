---
title: Set up a Tealium Connect data source
description: This article describes how to set up a Tealium Connect data source.
url: https://docs.tealium.com/server-side/data-connect/manage-data-connect-integrations/tealium-connect-data-source/
---
To send events to Tealium Collect and identify Data Connect events, use a Tealium Connect data source for each integration. Having a dedicated data source for each Data Connect integration makes it easy to see the related events in [Live Events](https://docs.tealium.com/about-live-events/). You can also configure connectors in Tealium EventStream or AudienceStream that process only Data Connect events.

For more information about data sources in Tealium, see [About Data Sources](https://docs.tealium.com/about-data-sources/).


<blockquote>
We recommend setting one Tealium Connect data source per originating data source. For example, a Tealium Connect data source for Salesforce data and a separate one for Snowflake data, etc.
</blockquote>


Complete the following steps to add a Tealium Connect data source:

1. Navigate to **Connect > Data Sources**.
1. Click **+ Add Data Source**.
1. From the **Select a Platform** screen, select **Tealium Connect**.
1. In the **Name** field under **Summary**, enter a name and click **Continue**. 
1. In the **Choose Event Specifications** step, click **Continue**. 
1. Select your event specifications and click **Continue** or click **Skip** to skip this step.
1. The **Get Code** screen shows the Tealium Connect endpoint URL in the following format:  
```
https://collect-us-east-1.tealiumiq.com/dataconnect/event/{{account}}/{{profile}}/{{data source key}}
```
You will need this key to set up your Tealium Events app in Workato.
<blockquote>
The Tealium API Domain will be custom for clients using [Tealium Private Cloud](https://tealium.com/resource/fundamentals/tealium-private-cloud/).
</blockquote>

8. (Optional) To download installation instructions, click **Download as PDF**.
9. Click **Save & Continue**.
10. A summary of the data source appears.
11. Click **Close**.  
The new data source is visible in the **Data Sources** dashboard.
12. To activate the data source endpoint, **Save/Publish** your profile.


<blockquote>
To find your data source key after setting up Tealium Connect, navigate to the **Data Sources** dashboard, click the data source you want to use, and copy the key from the **Data Source Key** field.
</blockquote>

