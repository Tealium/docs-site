---
title: Load Order Manager
url: https://docs.tealium.com/iq-tag-management/extensions/load-order-manager/
---
Improve the way you view and manage tags and extensions with the Load Order Manager. The Load Order Manager combines tags and extensions on a single screen to show a high-level overview of their execution order. This view provides a separate interface to edit the order of operations of your tags and extensions. Use this interface to view the actual order that tags and extensions are loaded and quickly change their order.

The main list view for tags and extensions can be sorted and filtered without affecting the order of execution of the viewed items.

## Panel layout

The Load Order Manager screen is displayed as two panels. The side panel shows each scope of the execution order that a tag or extension can appear and the main panel shows each tag and extension in their exact execution order.

The side panel lists each scope of the execution order and the number of items currently assigned to that scope. Click a scope to scroll the main panel directly to that section.

The main panel displays each tag and extension grouped by their execution scope. Use this view for the following actions:

* Drag and drop an item to a different position.
* Use quick links to:
    * Move an item to the top of a section.
    * Move an item to the bottom of a section.
    * Change the scope of an item.
* Search across all tags and extensions.
* Manually enter a position number of an item.
* Collapse and expand sections.
* Move items in bulk.
* Change the scope of items in bulk.
* Hide and show inactive items.

![](/images/iq-tag-management/load-order-manager-overview.png)

For more information, read about [order of operations]().

## Using load order manager

Use the following steps to start using Load Order Manager:

1. Go to **iQ Tag Management &gt; Tags** (or **Extensions**).
1. In the list view, click **Edit Load Order**.  
The Load Order Manager screen displays your tags and extensions, by scope, in execution order.
    * In the side panel, each scope displays the number of tags for that scope.  
        ![](/images/iq-tag-management/load-order-manager-number-of-tags-per-scope.png)
    * The details and order of execution number for individual tags and extensions displays in the main panel.  
![](/images/iq-tag-management/load-order-manager-order-of-execution-column.png)

### Change order within a scope

From the Load Order Manager screen, use the following steps to drag and drop a tag or extension to change the execution order within a scope:

1. In the Load Order Manager screen, click and hold the row for the tag or extension you want to move.  
    ![](/images/iq-tag-management/load-order-manager-drag-to-new-position-in-same-scope.png)
1. Drag up or down to the position you want and release (drop).  
The tag or extension you edited is now in the new position and the order number is updated.
1. Click **Apply Changes**.

### Change scope

From the Load Order Manager screen, use the following steps to drag and drop a tag or extension to change the execution order and move to a different scope:

1. In the Load Order Manager screen, click and hold the tag or extension you want to move.  
An open hand icon displays when you are holding an item to drag and drop.
1. Drag the item to the left and release (drop) in the scope you would like to move the item to.  
    ![](/images/iq-tag-management/load-order-manager-move-to-new-scope.png)  
    Invalid moves are prevented. You can only drop into a valid scope.
    The tag or extension you moved is now in the new position.
1. Click **Apply Changes**.
1. Save and Publish your changes.

### Quick links

For ease of use, use the quick links menu of each tag or extension.

Use the following steps to change the execution order of a tag or extension using the drop-down menu:

1. In the Load Order Manager screen, click the drop-down menu to the right of a tag or extension.
1. Select **Move to Section Top**, **Move to section Bottom**, or a select valid scope.  
Only valid options display in the list, all others are greyed out.  
    ![](/images/iq-tag-management/load-order-manager-quick-links-for-moves.png)
1. Click **Apply Changes**.

### Using order number

From the Load Order Manager screen, use the following steps to change the execution order within a scope by editing the order number:

1. In the Load Order Manager screen, click in the order field for the tag or extension you want to move.  
    ![](/images/iq-tag-management/load-order-manager-manually-update-order-number.png)
1. Edit the order number by typing the new execution order number in the box.
1. Click **Apply Changes**.  
The tag or extension you moved is now in the new position.

### Bulk actions

From the Load Order Manager screen, use the following steps to perform bulk reordering of one or more tags or extensions:

1. In the Load Order Manager screen, click the checkbox to the left of one or more tags or extensions.  
At the top of the screen, three (3) new drop-down lists display, **Scope To**, **Move**, and a display of the number of items selected.  
    ![](/images/iq-tag-management/load-order-manager-select-bulk.png)
1. To move all selected items to a new scope, click the **Scope To** drop-down list and select the new scope.  
Only valid scopes are for all items selected are available to move to, all others are greyed out.  
    ![](/images/iq-tag-management/load-order-manager-bulk-scope-to-dropdown.png)
1. To move all selected items to the top or bottom of a section, click the **Move** drop-down list and select **Move to Section Top** or **Move to Section Bottom**.  
    ![](/images/iq-tag-management/load-order-manager-move-section-to-top-or-bottom.png)
1. Click **Apply Changes**.  
The tags or extensions you moved are now in their new positions.
1. Save and Publish your changes.

### Find a tag or extension

You can now use text to filter your searches for tags or extensions for more refined search results. You can filter by Label, Title, Type, or UID.

The following example looks for items with the word **extension** to identify items with &#34;extension&#34; in the Type column.

Use the following steps to search for items with the GA label:

1. In the Load Order Manager interface, go to the search field and type the text you seek in the search field.  
    ![](/images/iq-tag-management/load-order-manager-search-results.png)
1. The search results display all items with the word &#34;extension&#34; anywhere in the title, type, or label columns.  
If the search results return more than one page, click the up or down arrow to the right of the search field to scroll through the results.
