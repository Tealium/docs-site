---
title: Manage events
description: This article describes how to manage event listeners.
url: https://docs.tealium.com/iq-tag-management/events/manage/
---
Manage events either from the **Events** screen or from the expanded **Tag Details** screen.

## Create an event

Create an event listener in three steps: Select an event type, configure the event, and create event rules.

### Step 1: Select an event type

1. Go to **Events** and click **&#43; New Event**.  
1. In the **Event Type** step, select the type of event that you want to track.
1. Click **Next**. 

### Step 2: Configure the event listener

1. In the **Configuration** step, enter a **Name** for the event listener.
1. (Optional) Enter **Notes** about this event listener.
1. Under **Scope**, select a scope from the list to determine when the event listener initialization code runs on the page. We recommend that you use the **DOM Ready** scope. For more information, see [Event score]().
1. Under **Tracking Event**, select the tracking event for the event listener from the list. If you plan to subscribe a tag to this event listener, be sure to select a tracking event that is supported by the tag, or the event listener will not work with that tag.  
    * **View** – Track when a visitor views a page.
    * **Link** – Track when a visitor interacts with a page, such as clicks, video scrolls, etc.
    * **Custom** – Enter a custom tracking event in the text box (for example, `video`).
1. Under **Publish Locations**, select the publish locations for the event. If you deselect the checkbox for a publish location, the event listener will not be published to that location. For example, if you deselect **Prod**, the event listener will not be pushed to your live site, even if you select **Prod** as a publish target from the **Save** dialog. For more information, see [About publishing]().
1. In the **Element Selector** box, enter the element ID, class, or selector of the item you want to target. For more information, see [Event element selector]().
1. Under **Event Triggers**, select the event triggers for this event and set the thresholds for those triggers. For more information about each event type&#39;s event triggers, read the documentation from our list of [Event Types]().
1. Under **Trigger Frequency**, select whether you want to track every time that event listener is triggered on a page (**Always**) or track only the first time an event is triggered (**Once**). For more information, see [Event triggers]().
1. Configure the trigger variables for the event listener. These are the values sent with the event listener tracking call. You can edit existing trigger variables or add new ones to collect additional data with the visitor actions. For more information about variables, see [Event Variables](). For more information about event type&#39;s event trigger variables, read the documentation from our list of [Event Types](). 
1. When you are done configuring the event listener, click **Next**. 

### Step 3: Create rules

1. In the **Rules** dialog, set the rules that determine if a page loads your new event listener. The left side of the dialog displays the logic the page uses for loading the event listener. The right side of the dialog lists all the available rules on the profile that you can reuse for this event listener. ![](/images/guides/iq/event-rules.png)
1. To create a new rule, click **&#43; Add Rule**. For information about how to create and configure a rule, see [Load Rules]().
1. Build the logical conditions for the event listener by dragging and dropping the rules from the list on the right side of the dialog to the logic boxes on the left side. For more information about logical operators and load rules with events, see [Event Rules Examples](). If you do not select any rules, the event listener loads and listens on every page. This can cause performance issues for your visitors as well as your data collection.
1. When you are done arranging the rules for your event, click **Save**.

To save your work to the profile, click **Save/Publish**.

### Tags with events

After you create an event listener, you can subscribe a tag to the event listener in the **Rules and Events** section for a tag. Precisely control when a tag fires and when the data that is sent to the tag endpoint by combining load rules for a tag and an event listener conditions.

For more about tags and event listeners, see [Subscribe a tag to an event]().

### Duplicate an event

Duplicate an event listener to create a copy of it in the profile. For example, if you have a mouseover event with a complex set of rules that you want to apply to another element on a page, duplicate that event listener and change the **Element Selector** in the duplicate to the new element.

1. From the **Events** screen, click the event you want to duplicate.
1. In the **Event Details** slideout, click **Duplicate**. 
1. Click the duplicate event in the **Events** dashboard. 
1. In the **Configuration** tab, click **Edit**. 
1. Enter a unique name and customize settings for the event listener. 

## View event details

Go to **Events** and click an event to see and edit the event listener details.

* The **Configuration** tab displays the title, scope, tracking event, triggers, occurrence, conditions, and trigger variables for the event listener.
* The **Rules** tab displays the logical conditions of the event listener.
* The **Tags** tab displays a list of the tags and their relationship to to the event listener:
  * **All Pages and Events** - The tag is not subscribed to the event listener. The tag and event trigger will fire separately.
  * **Linked** - The tag is subscribed to the event listener. The tag will fire based on how the event listener appears in the tag&#39;s rules logic.

To view the change history of an event, click **Change History**.

For more information about subscribing tags to event listeners, see [Subscribing Tags to Events]().

## Edit an event

1. Navigate to the **Events** dashboard and click the event listener that you want to edit. 
1. Select the tab of the element you want to edit: **Configuration**, **Rules**, or **Tags**.  
    * To make changes to an event listener relationship with a tag, you must make those changes within the tag configuration. Click the **Tags** tab and select the tag you want to edit. You can then edit the tag from the **Tags** dashboard.
1. Click **Edit**.
1. After you complete your changes, click **Done**.

If you change the scope of an event that uses data layer values, variables, and load rules to **Pre Loader**, the interface will display a validation error and you will need to remove them from the event before you can save.

## Activate or deactivate an event

If you deactivate an event that is subscribed to a tag, it is removed from the tag. We recommend that you check the tag before and after you deactivate an event to ensure that any subscribed tags continue to load properly.

* To deactivate an event, navigate to **Events** and set the event listener toggle to **Off**. If the event is in use, confirm that you want to deactivate it.
* To reactivate an event listener, set the event listener toggle to **On**.

## Delete an event

Deleting an event listener removes all instances of it from the `utag.js` file.

If you deactivate an event listener that is subscribed to a tag, Tealium iQ Tag Management removes the deactivated event listener logic from the tag logic. We recommend that you check the tag logic before and after you deactivate an event listener to ensure that any subscribed tags function and load properly.

1. Go to **Events** and click the event listener that you want to delete. 
1. In the **Event Details** slideout, click **Delete**. 
1. In the confirmation dialog, confirm that you want to delete the event listener and click **Delete**. Otherwise, click **Cancel**.
    * If the event listener you want to delete is in use, a warning message appears.
    * To delete the event listener, click **Delete**. Otherwise, click **Cancel**.
