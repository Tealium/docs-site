---
title: Authenticom DealerVault Data Connect Integration Setup Guide
description: This article describes how to set up an integration between Tealium Data Connect and Authenticom DealerVault.
url: https://docs.tealium.com/server-side/data-connect/manage-data-connect-integrations/authenticom/
---
The Authenticom integration with Tealium Data Connect lets you import the following vendor data feeds:

* Inventory
* Part Inventory
* Sales
* Open Repair Orders
* Special Order Parts
* Service
* Service Appointment

## Requirements

* Tealium EventStream or AudienceStream 
* Tealium Data Connect 
* Tealium DataAccess (for EventStore or EventDB)
* Authenticom API access

## Create an Authenticom integration

Use the following steps to create an Authenticom integration with Tealium Data Connect:

1. Set up a Tealium Connect data source.
1. [Contact support](https://docs.tealium.com/support/) to get the recipes imported into your Data Connect environment.
1. Establish a connection to the Authenticom API.
1. Select a data type and vendor.
1. Send events to Tealium.
1. Set up an event feed for leads.
1. Test with trace and activate the recipe.

## Step 1: Set up a Tealium Connect data source

Set up a Tealium Connect data source. For more information, see [Set up a Tealium Connect data source](https://docs.tealium.com/tealium-connect-data-source/).

## Step 2: Contact Tealium

[Contact support](https://docs.tealium.com/support/) and they will import the integration into your environment.

## Step 3: Establish a connection to the Authenticom API

To establish a connection to the Authenticom API, perform the following steps:

1. Go to **Connect > Data Connect > Integrations**.
1. Select the **Authenticom** connection.
1. Do not change **Base URL**.
1. Enter the **Subscription Key**, which is in the Authenticom Developers API portal in production.

 ![](https://docs.tealium.com/images/server-side/data-connect/authenticom-data-connect-integration-establish-connection.png)

## Step 4: Select a data type and vendor

To select the data type and vendor, perform the following steps:

1. Go to the recipe named **Authenticom - DealerVault**.
1. Select step 4 of the recipe **Retrieve dealers with updated data since a given date**.
1. Select the data type that you want to import into Tealium. The following data types are available:
    * `INV`: Inventory.
    * `PTINV`: Part Inventory.
    * `SL`: Sales.
    * `OPENRO`: Open Repair Orders.
    * `SOP`: Special Order Parts.
    * `SV`: Service.
    * `SV_APPT`: Service Appointment.
1. In the top-right of the window, click **Save**.

 ![](https://docs.tealium.com/images/server-side/data-connect/authenticom-data-connect-integration-select-data-type.png)

## Step 5: Send events to Tealium

To send events to Tealium, perform the following steps:

1. Go to **Send events in Tealium events V2**.
1. Configure the data that you want to send to Tealium.

 ![](https://docs.tealium.com/images/server-side/data-connect/authenticom-data-connect-integration-send-events.png)

For additional information, see [Create a recipe: Configure an Action](https://docs.tealium.com/create-recipe-data-connect/#step-2-configure-an-action).

## Step 6: Set up an event feed for leads

 ![](https://docs.tealium.com/images/server-side/data-connect/authenticom-data-connect-integration-set-up-event-feed.png)

Use the following steps to create an event feed:

1. Go to **Validate > Live Events** and click **+ Add Event Feed**.
1. In the **Create Event Feed** dialog, enter a **Title** and any **Notes**.
1. (Optional) Click **Add Label** to select labels to apply to this event feed.
1. Under **Event Data Storage**, enable the feed for EventStore or EventDB.
1. Set an **Attribute Condition** for the feed to capture events that match new lead events.
1. Click **Save**.
1. Save and publish your profile.

## Step 7: Test with trace and activate the recipe

Before activating the recipe, perform thorough testing. Once testing is successful, activate the recipe to start the automated data integration process.

Use the following steps to test with trace and activate the recipe:

1. Go to **Trace**.
1. Under **New Trace**, click **Start**. A dialog with a trace ID appears.
1. Copy the trace ID and click **Continue**.
1. Go to **Connect > Data Connect > Integrations**.
1. In the **Integrations** screen, perform the following steps for recipes that send new leads from Authenticom to Tealium:
    1. Select your recipe.
    1. Select the **Tealium Events V2 action** to edit it.
    1. Under **Attributes to add**, add a `tealium_trace_id` key and paste the trace ID in the **Value**.
    1. Click **Save**.
    1. From the **Start recipe** list, click **Test recipe**.
1. Return to the **Trace** interface to inspect the log details.
1. After you are done testing, click **Stop test**.
1. To activate the recipe, click **Start recipe**.