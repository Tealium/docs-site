---
title: Connectors: Add a connector
description: This step shows how to add a connector, configure an action, and use data mappings.
url: https://docs.tealium.com/server-side/getting-started/eventstream-api-hub/add-connector/
---
This example uses the Google Sheets connector to show how to log events to a spreadsheet, but you may use your own vendor. To prepare for this step, create a Google Sheets spreadsheet named `EventStream Test` and name the first three columns: `Timestamp`, `Search Term`, and `Search Results`.

The spreadsheet looks like this:

![](/images/server-side/es-getting-started-connector-google-sheet-spreadsheet.jpg)

## Add the Google Sheets connector

Use the following steps to configure the Google Sheets connector:

1. Go to **EventStream &gt; Event Connectors**
1. Click **&#43; Add Connector**.
1. Under **Categories** in the side navigation panel, click **Big Data** to filter the list.
1. Select **Google Sheets** then click **Continue**.
    ![](/images/server-side/connectors-select-source.png)
1. On the **Source** tab, select the data source and event feed that correspond to the data that you want to send, and enter a name for this action.
1. On the **Configuration** tab, click **Add Connector**, enter the name of the connection, and then click **Establish Connection**. The authorization dialog for your Google account appears.
1. Confirm your user account name and click **Allow**. The configuration window for the connector now displays a `Connected` message. Click **Done**.
1. On the **Action** tab, select the default action **Add or Update Row** and configure the following parameters:
    * **Row Operation**  
  Select **Add Only** to add new a row without lookup, **Update Only** to lookup an existing row and update it, or **Add or Update** to look up an existing row update it if found or add a new row if not found.
    * **Spreadsheet Name**  
  Identifies the name of the spreadsheet file to use.  
  Select the spreadsheet name from the drop-down, or enter the name of the spreadsheet file to use (such as `EventStream Test`).
    * **Worksheet Name**  
  Identifies the name of the worksheet within the spreadsheet to use.  
  Select the worksheet name from the drop-down, or enter the name of the worksheet to use (such as `Sheet1`).
    * **Row ID**  
  Identifies the column that contains the unique row ID for each event. This column is usually the event timestamp attribute. We named the column `Timestamp` to be used in the mapping.  
        ![](/images/server-side/screen-shot-2020-05-27-at-2.52.47-pm.png)  
        Select your attribute from the **Map** list and enter the corresponding spreadsheet column name (Custom Value) in the **To** field. When the action fires, it searches for the attribute value in the specified column, then:  
        * If the value exists, the matching row is updated as specified by the **Row Data** mappings (see next).
        * If the value does not exist, a new row is created with a **Row ID** value and attributes specified in **Row Data**.
    * **Row Data**  
    Map additional attributes that you want to add to the spreadsheet. Each attribute must have an assigned column name in the spreadsheet. In this case, we are logging the value of the `search_keyword` attribute into the spreadsheet column named `Search Term`.  
        ![](/images/server-side/screen-shot-2020-05-27-at-2.53.25-pm.png)
    * **Exclude empty values when updating**  
    Check this box if you want to exclude empty attributes from updating or overriding existing data in your spreadsheet.

1. Click **Continue** to go to the **Summary** tab, and then click **Finish** to save.

Now save and publish your account, and go the next step to start testing with the Trace tool.
