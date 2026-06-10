---
title: Manage data mappings
description: This article explains how to manage data mappings.
url: https://docs.tealium.com/iq-tag-management/data-mappings/manage/
---
## Add a variable mapping

Vendor tag parameters (also called destinations) are built into the **Data Mappings** configuration screen for the tag. This is where you add and manage data mappings.

Follow these steps create a variable mapping:

1. Expand a tag to view the details for that tag.
1. Click the **Mapped Variables** tab.
1. Select the variable to map.
1. Click **&#43; Add Mapping**.
1. Select a destination from the list, or click **&#43; Add Custom Destination** and enter a new custom destination.
1. Click **Done**. The new data mapping is displayed.
1. Repeat steps 2 through 6 to map additional variables.

When done, click **Apply**.

## Add an event mapping

Use an event mapping to associate your event names with the vendor&#39;s event names and corresponding tracking. First, select your event variable (typically `tealium_event`), then enter the event name from your data layer, then select the corresponding vendor event to trigger.

![](/images/iq-tag-management/data-mappings-event-triggers.png)

Use the following steps to map an event:

1. Expand a tag to view the details for that tag.
1. Click the **Mapped Variables** tab.
1. Select the event variable to map.
1. Click **&#43; Add Mapping**.
1. Under **Category**, find the **Events** section.
1. In the **Trigger** field, enter the event name from your data layer.
1. In the **Event** drop-down, select the vendor&#39;s event to trigger.
1. Click **&#43; Add**. Repeat these steps to map multiple events.
1. Click **Apply**.

Event mappings appear in the data mappings list in the format of `EVENT_NAME:VENDOR_EVENT`. For example, if you mapped the `cart_add` event to the vendor&#39;s event `addToCart`, the mapping appears as `cart_add:addToCart`.

![](/images/iq-tag-management/mapped-event-triggers.png)

## Add an event parameter mapping

Use an event mapping to associate your event parameter names with settings parameter names.

![](/images/iq-tag-management/data-mappings-event-parameters.png)

Use the following steps to map an event parameter:

1. Expand a tag to view the details for that tag.
1. Under **Mapped Variables**, click **Edit**.
1. Select the event variable to map.
1. Click **&#43; Select Destination**.
1. Under **Category**, find the **Event Parameters** section.
1. In the **Event** drop-down, select the vendor&#39;s event parameter from your data layer.
1. In the **Parameters** drop-down, select the settings parameter to map to.
1. Click **&#43; Add**. Repeat these steps to map multiple event parameters.
1. Click **Apply**.

Event parameters mappings appear in the data mappings list in the format of `EVENT_NAME:SETTINGS_PARAMETER`. For example, if you mapped the `sendscreenview` event parameter to the settings parameter `dynamic_var`, the mapping appears as `sendscreenview:dynamic_var`.

![](/images/iq-tag-management/mapped-event-parameters.png)

## Add a custom value mapping

Use the following steps to create a data mapping that uses a custom (static) value instead of a data layer variable:

1. Expand a tag to view the details for that tag.
1. Click the **Mapped Variables** tab.
1. Expand the **Variables** drop-down list or click **Use Custom Value**.  
1. Click **Select Destination**.  
The mapping dialog displays the supported vendor parameters.
1. Select the type of value to set and enter a value.
    * **Text:** a simple text value.
    * **JS Code:** a native JavaScript value, such as a number, boolean, array, object, or an inline function.  
1. Click **Close**.

The mapped variable is displayed. Repeat these steps to map additional custom values.

When done, click **Apply**.

## Add a custom data mapping

While the built-in destinations cover most of your mapping needs, you can optionally define a custom data mapping to send data to a vendor parameter that you name.

Use the following steps to create a custom data mapping:

1. Expand a tag to view the details for that tag.
1. Click the **Mapped Variables** tab.
1. Select a data layer variable from the **Variables** drop-down or click **&#43; Add Variable** to use a new one.
1. Click **&#43; Add Custom** **Destination** in the top panel or in the lower left panel.
1. Enter a name for the custom variable.
1. Click **OK** in the top panel or **&#43; Add** if you used the bottom panel option.  
    ![](/images/iq-tag-management/whiteui-tiq-datamappings-two-options-to-add-custom-destination.png)

Repeat the steps to add more custom mappings. When complete, click **Done**. The custom mapping is displayed in the **Data Mappings** tab.

## Mapping an AudienceStream attribute

AudienceStream attributes are enriched attributes about your visitors that are sent back to your website for use with personalization.

Your profile must be populated by attributes from the matching AudienceStream profile. Those attributes are made available as data mappings in the variables drop-down menu. They are organized by attribute types and are labeled as AudienceStream variables.

For more information, see [About Data Layer Enrichment]().

## View data mapping change history

To view the change history of a data mapping, go to **Tag Management &gt; Tags** and click **View Tag History**.

## Edit a mapping

Use the following steps to edit a destination for a mapped variable:

1. Expand a tag to view the details for that tag.
1. Click the **Mapped Variables** tab.
1. In a data layer variable row, click the pencil icon.
1. Edit any of the following:  
    * Change the destination name
    * Map to another destination
    * Remove the destination
1. Click **Done**.
1. Repeat to edit more mappings.
1. When complete, click **Apply**.

## Edit a custom data mapping

Use the following steps to edit the destination variable:

1. Expand a tag to view the details for that tag.
1. Click the **Mapped Variables** tab.
1. In a data layer variable row, click the edit icon.
1. Click **&#43;Add Custom Destination**.
1. Enter the new name.  
1. Click **OK** to apply the changes.
1. When complete, click **Done**.

&lt;!-- ## Reorder mappings

You can drag and drop data mappings in your preferred order. This is helpful if you want to order your mappings alphabetically for better organization.

Order of mapping is important when two or more data layer variables are mapped to the same vendor destination. In this case, the last mapping takes precedence. --&gt;

## Delete a mapping

Use the following steps to delete a mapping:

1. Expand a tag to view the details for that tag.
1. Click the **Mapped Variables** tab.
1. Click the trash icon next to the mapping you want to remove.  
1. Click **Apply** to confirm.  
No warning or confirmation message appears. The deleted mapping cannot be restored.



