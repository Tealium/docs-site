---
title: Create a recipe in Data Connect
description: This article describes how to create a recipe in Data Connect.
url: https://docs.tealium.com/server-side/data-connect/manage-data-connect-integrations/create-recipe/
---
 To enable Data Connect and begin creating and managing recipes, contact your Tealium Customer Success Manager. 

Complete the following steps to create a recipe:

1. Navigate to **DataConnect &gt; Integrations**.
1. In the **Integrations** screen, click **Create &gt; Recipe**.
1. In the **My new recipe** slideout, enter a name for the recipe and select the profile associated with the recipe.
1. Under **Pick a starting point**, select how you want to trigger your app in Workato. 
    * Select **Run on a schedule** to build a recipe that runs on a schedule for your business case.
    * Select **Trigger from an App** to build a recipe that periodically polls the source system for new data. For more information about Workato triggers, see the [Triggers](https://docs.workato.com/recipes/triggers.html) article in the Workato Recipe Components documentation. To see which triggers are available for your app, read the app-specific document in the [Pre-built Connectors](https://docs.workato.com/connectors/prebuilt-connectors.html) documentation.
1. Click **Start building**.

## Build a recipe

Now you can start building your recipe in Workato. Generally, your recipes will follow a specific workflow: 

1. [Select a trigger](#step-1-select-a-trigger).
1. [Configure an action](#step-2-configure-an-action).
1. [Configure error handling](#step-3-configure-error-handling).

### Step 1: Select a trigger

**App-based triggers**  
Search for the **app** you want to integrate into Tealium. For schedule-based recipes, the trigger is the schedule that you configure.
   1. In the **Trigger** step, choose the trigger for your business case. Use batch processing when available to reduce the number of tasks per recipe.
   1. In the **Connection** step, connect to your app. Enter a connection name and complete the configuration. Click **Connect**. 
   1. In the **Setup** step, add any additional configurations for this app trigger. Set a trigger condition if you want to set a more specific trigger.

### Step 2: Configure an action

1. Under **Actions** click **&#43;**.
1. Under **What happens next?** select **Handle errors**.  
We recommend wrapping the Tealium Events app and related actions in an error monitoring step. Ensure you complete [Step 3]() to finish configuring error handling in your recipe. If you do not stop the recipe as described in Step 3, automatic error notifications will not work.
1. Select any apps you need to prepare the data to be imported to Tealium. For example, use the **Download file contents in Amazon S3**, **Decrypt and verify data**, and **Parse CSV** apps together to prepare encrypted CSV data stored in an Amazon S3 bucket.
1. (Optional) If your data payload size exceeds 500 records, use the **Repeat action** loop with the Tealium Events app to break your data into smaller payload sizes.   
To use this loop:
    1. Click the **&#43;** to see a list of actions. 
    1. Click **Repeat action**.
    1. Set the loop **Repeat mode** to **Batch of items**. 
    1. Set the **Batch size** to the maximum batch size for your app.
1. Under **Select an app and action**, select the **Tealium Events V2** app.
1. Enter the information from your [Tealium Connect data source]().
    * **Tealium Connect API Domain** - Enter the regional Tealium Collect API domain used in your Tealium Connect data source.
    * **Data Source Key** - Enter the data source key from your Tealium Connect data source.
    * **Tealium Account Name** and **Tealium Profile Name** - Enter your Tealium account name and profile name in the corresponding fields.A single account may have multiple corresponding profiles. Specify the Tealium profile to which you want to send events from this recipe. 
1. In the **Source Data** section, add your source data to the app.
    * **Source Data source list** - Select the [datapill(s)]() from the **Recipe data** slideout that represent data to send to Tealium. You can insert batched data from the  **Recipe data** slideout. 
    * **Visitor ID Value** - Select a datapill for the visitor ID value.
        * **If you are stitching to a known user identifier using a Visitor ID attribute**: Select the datapill in your recipe that contains the value of the user identifier. Enter the corresponding visitor attribute ID in the **Visitor Attribute ID** field. You must set up enrichments for any visitor ID attributes you want to be set for events from the recipe. For more information, see [Visitor ID attribute enrichment for Tealium Connect]().
        * **If you are importing data based on an anonymous identifier**: Select the datapill in your recipe that contains the anonymous identifier. Leave the **Visitor Attribute ID** field empty. This value directly sets the `tealium_visitor_id`.
    * **Visitor Attribute ID** - This numeric value assists in matching the `tealium_visitor_id` to an existing visitor ID attribute. For example `_{Account}_{Profile}_{Visitor Attribute ID}_{Visitor ID Value}_`. 
        * **If you are stitching to a known user identifier using a visitor ID attribute**: Enter the visitor attribute ID. Navigate to **Transform &gt; Visitor/Visit Attributes**, select the visitor attribute you want to use, and copy the attribute ID to your Tealium Events app in Workato. For more information, see [Attribute IDs](). 
        * **If you are importing data based on an anonymous identifier**: Leave this field empty. 
    * **Attributes to add** - Expand the **Attributes to add** section. Specify the key and value for each event attribute in the event Workato sends to Tealium. Ensure your **Attributes to add** contain fields with unique names, ignoring case. &lt;br&gt; Tealium processes all event field names in lowercase.
        * Any data from your recipe that you do not add here is not sent to Tealium.
        * For the key, use the **Text** input to enter the event attribute name. 
        * For the value, use the **Text** input to hardcode an event attribute value or create a value from a datapill. 
        * Use this feature to edit key names to match existing Tealium configurations to minimize additional work for new attributes, enrichments, and/or rules.
        * To create an event specification, add a `tealium_event` value in this section.
        * (Optional) Add any additional attributes you want to send to Tealium that are not necessarily from your app. For example, `tealium_event`, your `tealium_trace_id`, or `_dc_ttl_`, which describes how long the visit will last. When using `tealium_trace_id` for debug purposes, you cannot send more than five events in one batch.
1. (Optional) Select whether to enable **Hash Visitor ID**. If your use case requires visitor ID hashing, click **Show optional fields**, and enable **Hash Visitor ID**. 
    * If you defined the **Visitor Attribute ID** previously and you want to apply SHA-256 hashing to the constructed `tealium_visitor_id`, select **Yes**. For most purposes, you set this value to **No**.
    * If you want to apply SHA-256 hashing to the value of the visitor ID attribute you are stitching with, use the Workato `encode_sha256` function in the **Visitor ID Value** field.
   

### Step 3: Configure error handling

1. Click the **On Error** step.
1. Under **Retry actions in Monitor block?**, choose whether to retry actions.
1. Add a log message to the job report. 
    1. Click the **&#43;** to add an additional action to fire when an error occurs.
    1. Click **Action in an app** and select the **Logger by Workato** app.
    1. Configure the message for the logs.
1. Stop the recipe.
    1. Click the **&#43;** to add an additional action when an error occurs.
    1. Click **Action in an app** and select the **ReceipeOps by Workato** app.
    1. Select the **Stop a recipe** action.
    1. Under **Whose account are you managing?**, select **My account**. 
    1. Click **Connect**. 
    1. In the **Setup** step, select the current recipe name from the **Recipe** drop down list.
    1. Select **Yes** from the **Force stop** drop-down list.
1. Stop the current job.
    1. Click the final **&#43;** in your recipe to add an additional action when the error occurs.
    1. Click **Stop job**.
    1. Under **In job report, mark stopped job as**, select **Failed** in the drop down list.
    1. Under **Reason for failure**, type **Error**.
1. Click **Save**.
1. Click **Test** to test your recipe configuration.
 To test the error handling, temporarily change the **Tealium Connect API Domain** setting in the Tealium Events V2 app to a domain that doesn&#39;t exist. For example, temporarily change the domain to `xcollect-eu-west-1.tealiumiq.com`, test the error handling, and then change the domain back to `collect-eu-west-1.tealiumiq.com` when your testing is complete. 

