---
title: Data Connect error handling
description: This article provides an overview of error handling and notifications in Data Connect.
url: https://docs.tealium.com/server-side/data-connect/error-handling/
---
The following types of errors can occur when running a recipe in Data Connect:

* Trigger errors 
* Recipe errors

Each type of error requires a different error notification configuration.

## Trigger errors

Errors that prevent a Workato recipe from starting. For example, if your recipe contains a connection to an application and the application server does not respond, the recipe cannot run. In this case, no data has been retrieved by Workato. The recipe will try to connect again the next time it is scheduled to run. Trigger errors occasionally happen and only require intervention if they happen repeatedly.

## Recipe errors

Errors that occur while a recipe is already running, for example, if something is misconfigured in the Tealium Events app that sends data to Tealium from your connected data source. In this case, some data has been retrieved from the data source and data will not be retrieved again the next time the recipe is scheduled to run. 

To ensure all of your data is properly processed, you must fix the error in the recipe and reprocess the Workato job(s) that failed.

 We strongly recommend wrapping your Workato actions within a **Handle errors** step for any recipe you create. This step lets you stop a recipe from running additional jobs when an error occurs. For more information about configuring a **Handle errors** step in your recipes, see [Create a recipe](). 

## Error notifications

### Account-level notifications

You can configure email notifications for trigger and recipe errors at the account level.

To set up email notifications:

1. Navigate to **Manage Platform &gt; Data Connect Workato Settings** in the server-side admin menu.
1. Under **Error notification emails**, enter any email addresses that should receive a notification when a trigger error occurs. Separate each email address with a comma. Error notifications are configured at the account level. Email addresses you supply will receive error notifications for all recipes in the account, regardless of their profile assignment.
1. Click **Save**.

### Recipe-level notifications

We strongly recommend wrapping Workato actions within a **Handle errors** step. This in-recipe error handler stops the recipe from running additional jobs and also stops the current job in an error state. You can configure this step to send an email notification with error details. Additionally, the error handler will trigger the account-level email notifications mentioned above.

For more information about configuring a **Handle errors** step in your recipes, see [Create a recipe]().