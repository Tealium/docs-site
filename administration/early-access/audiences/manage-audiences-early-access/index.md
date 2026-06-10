---
title: Manage audiences
description: This article provides information about creating, editing, and deleting audiences, as well as activating audiences and creating segments.
url: https://docs.tealium.com/administration/early-access/audiences/manage-audiences-early-access/
---
The new fill audience feature is in Early Access and is only available to select customers. If you are interested in trying this feature, contact your Tealium Support representative. 

An audience is a combination of one or more attribute conditions. The more filters you add, the more specific your audience.

 When you create or edit an audience, the **Audience size** value reflects the count of visitors in the audience through the previous full day.

## Create an audience  

Use the following steps to create an audience:

1. Go to **Activate &gt; Audiences**.
1. Click **&#43; New Audience**.
1. Enter a **Name** for the audience. If you use a [DataAccess]() product (EventStore, AudienceStore, EventDB, or AudienceDB), the audience name must be fewer than 128 characters in length. Otherwise, DataAccess may trim the audience name and errors may occur.
1. To add a condition for the audience, select an attribute, an operator, and a value.  
    * The estimated potential size for the audience is displayed. For more information, see [potential size](#potential-size).
    * Click **Calculate** to update the potential size as you edit or add conditions.
    * When you hover over an attribute, the enrichment for the attribute is displayed.  
    * If you select a badge for the attribute, select **is assigned** or **is not assigned**.  
    * For operators that specify a time frame, select a value and the time frame.
1. To add another condition, click **&#43; Add Condition**.
1. To save this segment, click the **Save** icon. ![](/images/guides/server-side/int-aud-save-segment-icon.png)
Enter a **Name** for the segment, then click **Done**.If you use a [DataAccess]() product (EventStore, AudienceStore, EventDB, or AudienceDB), the segment name must be fewer than 128 characters in length. Otherwise, DataAccess may trim the segment name and errors may occur.
1. To add a segment, click **&#43; Add Segment**, then add conditions for the segment.
    * Click **Calculate** to update the potential size as you edit or add conditions.
1. To add a previously saved segment, click the down-arrow next to **&#43; Add Segment** and select a segment.
    * When you hover over a segment, the conditions for the segment are displayed.
1. To exclude a segment, click **&#43; Add Segment to Exclude**, then add conditions for the segment.
1. To exclude a previously saved segment, click the down-arrow next to **&#43; Add Segment to Exclude** and select a segment.
1. To perform a one-time backfill of the audience, select **Fill Audience**. For more information, see [Fill an audience]().
1. To add a label or notes, or change the retention time, click **More Options**.
    1. To add a label, click **Add Label** and select a label.
    1. Enter notes, if needed.
    1. To modify the audience retention time, select a value from the list. The time of a visitor&#39;s last visit determines the start of the retention time for that visitor.
1. To immediately activate the audience, click **Connect &amp; Activate**, then select and configure a connector.
    * For more information, refer to the setup guide for the selected connector.
1. To save the audience without activating it, click **Done**.
1. Save and publish.

## Create an audience from an existing audience

You can duplicate an audience from the list of audiences, or from the audience detail view, then modify the duplicate to create a new audience.

To duplicate an audience from the list of audiences, follow these steps:

1. Go to **Activate &gt; Audiences**.
1. In the audience menu, select **Duplicate**.
    * The copy of the audience is displayed.
1. Click **Edit** to modify the **Name** and conditions as needed for the new audience.
1. Click **Done** or **Connect &amp; Activate**.
1. Save and publish.

To duplicate an audience from audience details, follow these steps:

1. Go to **Activate &gt; Audiences**.
1. Click an audience in the list, then click **Duplicate**.
    * The copy of the audience is displayed.
1. Click **Edit** to modify the **Name** and conditions as needed for the new audience.
1. Click **Done** or **Connect &amp; Activate**.
1. Save and publish.

## Edit an audience

To edit an audience, follow these steps:

1. Go to **Activate &gt; Audiences**.
1. Click an audience in the list, then click **Edit**.
1. Modify the audience as needed.
    * Click **Calculate** to update the potential size as you edit or add conditions.
1. To perform a one-time backfill of the audience, select **Fill Audience**. For more information, see [Fill an audience]().
1. To add an activation or view activations for this audience, click **Activations**.
    * For information on adding an activation, see [Activate an audience](#activate-an-audience).
1. To view information about visitors and activity for this audience, click **Insights**.
1. To view the functions triggered by this audience, click **Functions**.
1. When you are finished editing the audience, click **Done** or **Connect &amp; Activate**.
1. Save and publish.

## Activate an audience

To activate an audience, select and configure a connector, as follows:

1. Go to **Activate &gt; Audiences**.
1. Click an audience in the list, then click **Edit**.
1. Click the **Activations** tab, then click **&#43; Add Activation**.
1. Select and configure a connector.
    * For more information, refer to the setup guide for the selected connector.
1. Click **X** to close the audience.
1. Save and publish.

## Deactivate an audience

To deactivate an audience, follow these steps:

1. Go to **Activate &gt; Audiences**.
1. Click an audience in the list, then click **Activations**.
1. Click the connector, then toggle the connector to **Off**.
1. Save and publish.

## Delete an audience

You can delete an audience from the list of audiences or from the audience details view.

To delete an audience from the list of audiences, follow these steps:

1. Go to **Activate &gt; Audiences**.
1. Click the audience menu, and select **Delete**.
1. In the confirmation dialog, click **Delete**.
1. Save and publish.

To delete an audience from audience details, follow these steps:

1. Go to **Activate &gt; Audiences**.
1. In the list of audiences, click the audience.
1. Click **Delete**.
1. In the confirmation dialog, click **Delete**.
1. Save and publish.