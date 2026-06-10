---
title: Manage connectors
description: This article explains how to manage connectors, including activating or deactivating connectors, duplicating and deleting connectors, and getting a connector or action UID.
url: https://docs.tealium.com/server-side/connectors/manage/
---
For information about adding a connector, see [Add a connector]().

## Activate or deactivate a connector

When you deactivate a connector, none of the actions for the connector will fire. To deactivate a specific action for a connector, deactivate the action. For more information, see [Activate or deactivate a connector action](). 

To activate or deactivate a connector, use the following steps:

1. Go to **Connect &gt; Connectors &gt; Overview**.
1. Click the checkbox next to the connector to be activated or deactivated.  
You can select multiple connectors that have the same status. A toolbar is displayed showing the number of connectors selected and actions that can be taken. For example:  
![](/images/server-side/connectors/activate-deactivate.png)
1. Click **Activate** or **Deactivate**.
1. Save and publish.

After activating a connector, you can activate the connector actions.

## Activate or deactivate an action

To activate or deactivate an action, use the following steps:

1. Go to **Connect &gt; Connectors &gt; Overview**.
1. Click the connector, then click the **Actions** tab.
1. Click the checkbox next to the actions to be activated or deactivated.  
You can select multiple actions that have the same status. A toolbar is displayed showing the number of actions selected and actions that can be taken. For example:
![](/images/server-side/connectors/activate-actions.png)
1. Click **Activate** or **Deactivate**.
1. Save and publish.

## Change the action type

To change the action type of an action, use the following steps:

1. Go to **Connect &gt; Connectors &gt; Overview**.
1. Click the connector, then click the **Actions** tab.
1. Click the action. The **Action Details** screen is displayed.
1. In the upper-right corner of the screen, click the more actions button and click **Change Action Type**.
    ![](/images/server-side/connectors/change-action-type.png)
1. Select the action type you want to use and click **Done**. A warning message is displayed.
1. Click **Change Action Type** to confirm the change or **Cancel** to cancel.
1. Update the data mappings as needed. For more information, see [Data Mappings]().
1. Click **Done**.
1. Save and publish.

## Duplicate a connector

To duplicate a connector and the associated actions, use the following steps:

1. Go to **Connect &gt; Connectors &gt; Overview**.
1. Click the connector menu, then click **Duplicate**.  
    ![](/images/server-side/connectors/duplicate-connector.png)  
    A new, identical connector, including the associated actions, is shown in the list of connectors. The connector name is appended with **- copy**.  
    ![](/images/server-side/connectors/duplicate-copy.png)
1. (Recommended) Click the duplicate connector and change the connector name.
1. (Optional) To add or edit actions associated with the new connector, click **&#43; New Action**, then follow the usual steps to add an action.
1. Click **Done**.
1. Save and publish.

## Delete a connector

To delete a connector, use the following steps: 

1. Go to **Connect &gt; Connectors &gt; Overview**.  
1. Click the connector menu, then click **Delete**.  
If there are actions associated with the connector, a prompt is displayed to verify that you want to delete all actions for the connector.
1. To delete the connector and all actions, click **Delete**.
1. To keep the connector and all actions, click **Cancel**.
1. Save and publish.

## Delete a connector action

To delete a connector action, use the following steps: 

1. Go to **Connect &gt; Connectors &gt; Overview**.
1. Select a connector by clicking that row. The **Connector Details** screen is displayed.
1. Click the **Actions** tab.
1. Click the action menu for the action you want to delete, then select **Delete**.
1. In the confirmation dialog, click **Delete**.
1. Save and publish.


## Add to favorites

Mark a connector as a favorite to make it easy to find using the **Favorite** filter menu.

There several ways to mark a connector as a favorite:

On the **Connectors Overview** screen, click the star next to the connector name.  
![](/images/server-side/connectors/connectors-favorites-star.png)

On the connectors details screen, in the top action bar, click **Favorite**.  
![](/images/server-side/connectors/connectors-details-favorite.png)

## Perform bulk actions on connector actions

The following actions can be done for multiple actions at the same time:

* Activate
* Deactivate
* Edit Labels
* Delete

Use the following steps to perform bulk actions for a connector action:

1. Go to **Connect &gt; Connectors &gt; Overview**.
1. Select a connector by clicking that row. The **Connector Details** screen is displayed.
1. Click the **Actions** tab.
1. Click the box next to each action you want to change or delete.  
Or, to select all actions, click the box next to **Name** in the table heading.  
The actions toolbar is displayed, as follows:  
![](/images/server-side/connectors/bulk-actions-toolbar.png)
1. Click the appropriate action: **Edit Labels** or **Delete**.  
If you selected **Delete**, click **Delete** in the confirmation dialog. If you selected **Edit Labels**, select a label to add or remove.

## Get a connector ID

To get the connector ID for a connector, use the following steps:

1. Go to **Connect &gt; Connectors &gt; Overview**.
1. Select a connector by clicking that row.  
The **Connector Details** screen is displayed, which shows the UID for the connector below the connector name. For example:  
![](/images/server-side/connectors/get-uid.png)
1. To copy the connector UID, select the UID text, right-click, and select **Copy**.

## Get an action ID

To get the action ID for a connector action, use the following steps:

1. Go to **Connect &gt; Connectors &gt; Overview**.
1. Select a connector by clicking that row. 
1. On the **Connector Details** screen, click the **Actions** tab.
1. Select an action by clicking that row.  
The **Action Details** screen is displayed, which shows the UID for the action below the action name. For example:  
![](/images/server-side/connectors/get-action-uid.png)
1. To copy the action UID, select the UID text, right-click, and select **Copy**.

## Revert to a previous connector version

You can revert to a previous connector version using **Version History**. For more information, see [Server-side version history]().
