---
title: Manage labels
url: https://docs.tealium.com/iq-tag-management/labels/manage/
---
Managing labels requires the **Save Existing Versions** permission. Creating, editing, and deleting labels does not require that you save the profile, but if you add or remove a label from an item you must save the profile.

## Label names

Label names can only contain unaccented letters (A–Z), numbers, and the underscore character. If you created a label with accented letters or punctuation marks prior to August 2017, you must rename the label without those characters before you can save changes or edit it.

## Create a label

There are three ways to create a label: directly on one item, directly on multiple items, or on the **Manage Labels** screen.

### Label an item

To create a label directly on an item:

1. View the details of one of the following items:
    * **Variable**
    * **Load Rule**
    * **Tag**
    * **Extension**
1. In the left panel, click **Apply Labels**.  
    ![](/images/iq-tag-management/whiteui-tiq-addnewlabel.png)
1. Click the folder to change the label color.
1. Enter the name of the label and press **Enter** or click the return arrow (**↩**).
1. Click **Save/Publish** to save your changes.

### Label multiple items

To create a label directly on multiple items:

1. Go to one of the following screens:
    * **Data Layer &gt; Variables**
    * **Load Rules**
    * **Tags**
    * **Extensions**
1. Click the box next to the items you want to label.
1. At the top of the table, click **Apply Labels**.  
    ![](/images/guides/iq/labels-apply-multiple.png)
1. Click the folder to change the label color.
1. Enter the name of the label and press **Enter** or click the return arrow (**↩**).
1. Click **Save/Publish** to save your changes.

### From Manage Labels

To create a label from the **Manage Labels** screen:

1. In the admin menu, click **Manage Labels**.  
    ![](/images/iq-tag-management/add-label.png)
1. Enter a **Name** for the label.
1. Select a **Color** for the label.
1. To restrict the ability to make changes to items with this label applied, click **Yes** under **Assign as Resource Lock**, then select users. Learn more about [resource locks]().
1. To add another label, click **Save &amp; Add Another**, otherwise click **Save Changes**.

## Filter by label

1. Navigate to **iQ Tag Management**.
1. Go to one of the following screens:
    * **Data Layer &gt; Variables**
    * **Load Rules**
    * **Tags**
    * **Extensions**

1. Click **Filter** and select **All Labels**, then enter label text to search for.  
The matching labels are displayed.
1. Select a label from the list to filter buy that label.  
You may only filter by one label at a time.  
The **Filter** list now displays **Filter On**.
1. To remove the filter, click **Clear All Filters**.

## Search with labels

Use the following steps to search Tealium iQ based on labels:

1. In the search bar at the top of the screen, enter the label you want to search by.  
    ![](/images/iq-tag-management/whiteui-tiq-lables-searchtiq.png)  
The search bar displays results for labels applied to tags, load rules, and extensions.
1. Select any label from the search results to go to that area of the interface, filtered by the label searched for.

## Delete a label

1. In the admin menu, click **Manage Labels**.
1. Select the label you want to delete to expand the details.
1. Click **Delete**.  
    ![](/images/iq-tag-management/delete-label.png)  
A message appears asking you to confirm your deletion.
1. Click **Delete Label**.  
The label is now removed.