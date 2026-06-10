---
title: Facebook Lead Ads Data Connect Integration Setup Guide
description: This article describes how to set up an integration between Tealium Data Connect and Facebook Lead Ads.
url: https://docs.tealium.com/server-side/data-connect/manage-data-connect-integrations/facebook/
---
The Facebook Lead Ads Data Connect integration offers several ways to improve your marketing strategies and streamline customer data management. You can collect leads, import them into your CRM system for quick access, set up automated follow-ups, trigger real-time personalization, and automate marketing efforts to turn leads into customers.

Send conversion lead ads using the **Send Lead Event** in Data Connect. To set up conversion lead events, follow the guide below.

## Requirements

* Tealium EventStream or AudienceStream
* Tealium Data Connect
* Tealium DataAccess (for EventStore or EventDB)
* Lead ID

## Use cases

Here are some ways you can use the Tealium Data Connect integration with Facebook Lead Ads:

1. **Lead generation and enrichment**: Use Facebook Lead Ads to collect leads from potential customers. Then, integrate these leads into your CRM system and enrich them with additional data using Tealium Data Connect to create more detailed customer profiles.
1. **Seamless lead import**: Automatically import leads generated from Facebook Lead Ads into your CRM system through Tealium Data Connect. This ensures that your sales and marketing teams have immediate access to new leads.
1. **Automated follow-up**: Set up automated follow-up sequences in your CRM that are triggered by lead submissions through Facebook Lead Ads. This can include sending personalized emails, SMS messages, or scheduling follow-up calls.
1. **Real-time personalization**: When a lead interacts with your Facebook Lead Ads, Tealium Data Connect can trigger real-time personalization on your website or in your email campaigns. This ensures that leads are immediately engaged with tailored content.
1. **Lead scoring and segmentation**: Automatically score and segment leads based on data collected by Facebook Lead Ads. This lets you effectively prioritize and target leads, ensuring your sales team focuses on the most promising prospects.
1. **Marketing automation**: You can integrate Facebook Lead Ads with your marketing automation platform using Tealium Data Connect. This enables automated follow-up emails, SMS messages, or other communications to move leads through the sales process.
1. **Suppression**: Exclude individuals who have unsubscribed from email communications, opted out of specific email campaigns, or have already converted or taken a specified action. This ensures compliance with regulations like GDPR, maintains an organized email marketing list, and prevents unnecessary ad spending on audiences that have already achieved the conversion.

## Integration flow

The diagram below illustrates the Facebook Lead Ads Data Connect integration flow. Follow the detailed instructions below to successfully set up your Tealium Data Connect integration with Facebook Lead Ads.

![](/images/server-side/data-connect/fb-lead-ads-data-connect-integration-flow.png)

## Create a Facebook Lead Ads integration

These are the steps required to create a Facebook Lead Ads integration with Tealium Data Connect:

1. Set up a Tealium Connect data source.
1. Create a recipe to send new leads from Facebook to Tealium.
1. Set up an audience and audience connector to send new/updated lead records from Tealium to Salesforce.
1. Create another recipe to receive new/updated lead records from Salesforce to Tealium.
1. Set up event feed for leads.
1. Set up an event connector to send updated lead records back to Facebook.
1. Test with trace and activate the recipe.

### Step 1: Set up a Tealium Connect data source

Set up a Tealium Connect data source. For the steps, see [set up a Tealium Connect data source]().

### Step 2: Create a new recipe to send new leads from Facebook to Tealium

For details on how to create a new recipe, see [create a recipe in Data Connect]().

Complete the following steps to create and set up your recipe:

1. Go to **DataConnect &gt; Integrations** and create a new recipe that triggers from the Facebook Lead Ads app. For details on how to create a recipe that **Triggers from an App**, see the steps to create a recipe in [Create a recipe in Data Connect]().
1. To build your recipe:
    1. Under **Trigger**, select **New Lead**.
    1. Connect to your Facebook Business Manager account.
    1. Once connected, configure the connector settings to specify which Facebook Lead Ads account and forms you want to pull data from:
    1. In the **Setup** step:
        * Select the **Page** you want to pull data from.
        * In the **Form ID** field, select **Use form ID** and enter a form ID from your Meta Business Suite (formerly Facebook Business Manager).
    1. Set up an action to send new lead generations to Tealium. For details, see [Configure an action]().

        ![](/images/server-side/data-connect/new-lead-generations-to-Tealium-action.png)

### Step 3: Send new/updated lead records from Tealium to Salesforce

Complete the following steps to send new or updated lead records from Tealium to any other CRM of choice. This example uses Salesforce:

1. Set up an audience. For details, see [Create an audience]().
1. Go to **Connect &gt; Audience Connectors**.
1. Click **&#43; Add Connector** and add the [Salesforce Connector]().
1. In the **Source** step,
    1. Select the **Audience** you created above.
    1. Under **Trigger**, select **Joined Audience.**
1.  In the **Configuration** step,
    1. Enter a **Name** for this instance of the connector.
    1. Under **Authentication**, provide your login credentials to establish a connection.
1. In the **Action** step:
    1. Enter a **Name.**
    1. In **Action Type**, select **Insert Contact.**
    1. Map the enriched attributes you want to send to Salesforce when there’s a new audience with a new lead.

### Step 4: Create another recipe to receive new/updated lead records from Salesforce to Tealium

![](/images/server-side/data-connect/recipe-to-receive-lead-records.png)

1. Go to **DataConnect &gt; Integrations** and create a new recipe that triggers from the Salesforce app. For details on how to create a recipe that **Triggers from an App**, see the steps to create a recipe in [Create a recipe in Data Connect]().
1. To build your recipe:
    1. Under **Trigger**, select **New/Updated Records**. You can select either batch or real time based on your needs.  
    1. Authenticate your Tealium Data Connect account with Salesforce. This may involve entering API keys or credentials.
    1. Configure the connector settings to map the fields from Facebook Lead Ads to the corresponding fields in Salesforce. Ensure data mapping is accurate to avoid issues with data synchronization.
    1. Set up an action to send new/updated records from Salesforce to Tealium. For details, see [Configure an action]().

        ![](/images/server-side/data-connect/action-parameter-mapping.png)

### Step 5: Set up event feed for leads

Complete the following steps to create an event feed:

1. Go to **Validate &gt; Live Events** and click **&#43; Add Event Feed**.
1. In the **Create Event Feed** dialog, enter a **Title** and any **Notes**.
    The event feed title is dependent on how lead events come into Data Connect.
1. (Optional) Click **Add Label** to select labels to apply to this event feed.
1. Under **Event Data Storage**, enable the feed for EventStore or EventDB.
1. Set an **Attribute Condition** for the feed to capture events that match new lead events.
    ![](/images/server-side/data-connect/fb-lead-ads-data-connect-event-feed.png)
1. Click **Save**.
1. Save and publish your profile.

### Step 6: Set up Facebook Conversions event connector to send leads

Follow these steps to set up the [Facebook Conversions event connector](https://docs.tealium.com/server-side-connectors/facebook-conversions-connector/) to send leads to a back to Facebook:

1. Go to **Connect &gt; Event Connectors**.
1. Click **&#43; Add Connector** and add the Facebook Conversions connector.
1. In the **Source** step, 
    1. Select the **Data Source**.
    1. Select the **Event Feed** you created in the [preceding steps](#step-5-set-up-event-feed-for-leads).
1. In the **Configuration** step,
    1. Enter a **Name** for this instance of the connector.
    1. Under **Authentication**, provide your login credentials to establish a connection.
1. In the **Action** step:
    1. Enter a **Name.**
    1. In **Action Type, **select **Send Lead Event.**
    1. Map the **Lead ID** and the **Event Name** parameters.
        ![](/images/server-side/data-connect/fb-lead-ads-event-connector-action.png)
1. Click **Finish**.
1. Save and publish your profile.

### Step 7: Test with trace and activate the recipe

Before activating the recipe, perform thorough testing. Once testing is successful, activate the recipe to start the automated data integration process.

Follow these steps to test with trace and activate the recipe:

1. In the sidebar, select **Trace**.
1. Under **New Trace**, click **Start**. A dialog with a trace ID will appear.
1. Copy the trace ID and click **Continue**.
1. Go to **Data Connect** &gt; **Integrations**.
1. In the **Integrations** screen, do this for both recipes that send new leads from Facebook to Tealium and receive new/updated lead records from Salesforce to Tealium:
    1. Select your recipe.
    1. Select the **Tealium Events V2** action to edit it.
    1. Under **Attributes to add**, add a new **Key** `tealium_trace_id` and paste the trace ID in the **Value**.
    1. Click **Save**.
    1. In the **Start recipe** drop-down list, click **Test recipe**.
1. Return to the **Trace** interface to inspect the log details.
1. Once you are done testing, click **Stop test**.
1. To activate the recipe, click **Start recipe**.