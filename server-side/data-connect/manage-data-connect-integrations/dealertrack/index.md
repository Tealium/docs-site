---
title: DealerTrack Data Connect Integration Setup Guide
description: This article describes how to set up an integration between Tealium Data Connect and DealerTrack.
url: https://docs.tealium.com/server-side/data-connect/manage-data-connect-integrations/dealertrack/
---
The DealerTrack integration with Tealium Data Connect lets you import the following data.

* Deal History
* Service Appointments
* Open Repair Orders
* Closed Repair Orders

## Requirements

* Tealium EventStream or AudienceStream 
* Tealium Data Connect 
* Tealium DataAccess (for EventStore or EventDB)
* OpenTrack access

## Create a DealerTrack integration

Use the following steps to create a DealerTrack integration with Tealium Data Connect:

1. Set up a Tealium Connect data source.
1. Establish a connection to the DealerTrack API.
1. Create a recipe to send data from DealerTrack to Tealium.
1. Send events to Tealium.
1. Set up an event feed for data.
1. Test with trace and activate the recipe.

## Step 1: Set up a Tealium Connect data source

Set up a Tealium Connect data source. For more information, see [Set up a Tealium Connect data source](https://docs.tealium.com/tealium-connect-data-source/).

## Step 2: Establish a connection to the DealerTrack API

To establish a connection to the DealerTrack API, perform the following steps:

1. Go to **Connect > Data Connect > Integrations**.
1. Click **Connections**, and then click **Create**.
1. Select the **DealerTrack** connection.
1. Under **Base URL**, enter `https://ot.dms.dealertrack.com`.
1. Enter your **Username** and **Password**.
1. Click **Connect**.

 ![](https://docs.tealium.com/images/server-side/data-connect/dealertrack-data-connect-integration-establish-connection1.png)

 ![](https://docs.tealium.com/images/server-side/data-connect/dealertrack-data-connect-integration-establish-connection2.png)

## Step 3: Create a recipe to send data from DealerTrack to Tealium

To create a recipe to send data from DealerTrack to Tealium, perform the following steps:

For more information on how to create a new recipe, see [Create a recipe in Data Connect](https://docs.tealium.com/create-recipe-data-connect/).

1. Go to **Connect > Data Connect > Integrations**.
1. In the **Integrations** screen, click **Create > Recipe**.
1. Create a new recipe that triggers from the Schedule app. For information on how to create a recipe that triggers from an app, see [Create a recipe in Data Connect](https://docs.tealium.com/create-recipe-data-connect/).

The [Actions](#actions) section below contains details on what data is possible to retrieve from DealerTrack.

## Step 4: Send events to Tealium

To send events to Tealium, perform the following steps:

1. Go to **Send Events in Tealium Events V2**.
1. Configure the data that you want to send to Tealium.

 ![](https://docs.tealium.com/images/server-side/data-connect/dealertrack-data-connect-integration-send-events.png)

For additional information, see [Create a recipe: Configure an Action](https://docs.tealium.com/create-recipe-data-connect/#step-2-configure-an-action).

## Step 5: Set up an event feed for leads

 ![](https://docs.tealium.com/images/server-side/data-connect/dealertrack-data-connect-integration-event-feed.png)

Use the following steps to create an event feed:

1. Go to **Validate > Live Events** and click **+ Add Event Feed**.
1. In the **Create Event Feed** dialog, enter a **Title** and any **Notes**.
    * The event feed title is dependent on how lead events come into Data Connect.
1. (Optional) Click **Add Label** to select labels to apply to this event feed.
1. Under **Event Data Storage**, enable the feed for EventStore or EventDB.
1. Set an **Attribute Condition** for the feed to capture events that match new lead events.
1. Click **Save**.
1. Save and publish your profile.

## Step 6: Test with trace and activate the recipe

Before activating the recipe, perform thorough testing. Once testing is successful, activate the recipe to start the automated data integration process.

Use the following steps to test with trace and activate the recipe:

1. Go to **Trace**.
1. Under **New Trace**, click **Start**. A dialog with a trace ID appears.
1. Copy the trace ID and click **Continue**.
1. Go to **Connect > Data Connect > Integrations**.
1. In the **Integrations** screen, perform the following steps for recipes that send new leads from DealerTrack to Tealium:
    1. Select your recipe.
    1. Select the **Tealium events V2 action** to edit it.
    1. Under **Attributes to add**, add a `tealium_trace_id` key and paste the trace ID in the **Value**.
    1. Click **Save**.
    1. From the **Start recipe** list, click **Test recipe**.
1. Return to the **Trace** interface to inspect the log details.
1. After you are done testing, click **Stop test**.
1. To activate the recipe, click **Start recipe**.

## Actions

The following actions can be tracked through this integration:

### Search Deal by Origination Date

| Parameter | Description |
| --------- | ----------- |
| Company Number | The company number. For example, `ZE7`. |
| Enterprise Code | The enterprise code. For example, `ZE`. |
| Server Name | The name of the server. For example, `arkonap.arkona.com`. |
| Origination Date Start | Date of the car deal, search beginning with this date. The format is `YYYY-MM-DD`. |
| Origination Date End | Date of the car deal, search ending with this date. The format is `YYYY-MM-DD`. |
| Deal Status | The status of the deal, if blank or not sent it will pull all deal statuses. Acceptable parameters are `Accepted`, `Capped`, `Closed`, `Unaccepted`, or blank. |

### Appointment Lookup

| Parameter | Description |
| --------- | ----------- |
| Company Number | The company number. For example, `ZE7`. |
| Enterprise Code | The enterprise code. For example, `ZE`. |
| Server Name | The name of the server. For example, `arkonap.arkona.com`. |
| Date From | Starting Date of Appointment Search, this is the day of the actual appointment, not when it was created. The format is `YYYY-MM-DD`. |
| Date To | Ending Date of Appointment Search, this is the day of the actual appointment, not when it was created. The format is `YYYY-MM-DD`. |
| Created Date Time Start | When to start the search of when Appointments were created. The format is `yyyy-mm-ddThh:mm:ssZ.` |
| Created Date Time End | When to end the search of when Appointments were created. The format is `yyyy-mm-ddThh:mm:ssZ`. |

### Open Repair Order Lookup

| Parameter | Description |
| --------- | ----------- |
| Company Number | The company number. For example, `ZE7`. |
| Enterprise Code | The enterprise code. For example, `ZE`. |
| Server Name | The name of the server. For example, `arkonap.arkona.com`. |
| Created Date Time Start | When to start the search of when Open Repair Orders were created. The format is `yyyy-mm-ddThh:mm:ssZ`. |
| Created Date Time End | When to end the search of when Open Repair Orders were created. The format is `yyyy-mm-ddThh:mm:ssZ`. |

### Get Closed Repair Orders

| Parameter | Description |
| --------- | ----------- |
| Company Number | The company number. For example, `ZE7`. |
| Enterprise Code | The enterprise code. For example, `ZE`. |
| Server Name | The name of the server. For example, `arkonap.arkona.com`. |
| Final Close Date Start | When to start the search for final closed repair orders. The format is `yyyy-mm-ddThh:mm:ssZ`. |
| Final Close Date End | When to end the search for final closed repair orders. The format is `yyyy-mm-ddThh:mm:ssZ`. |