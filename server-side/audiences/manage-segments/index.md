---
title: Manage segments
description: This article provides information about creating, editing, and deleting segments, as well as saving segments as favorites.
url: https://docs.tealium.com/server-side/audiences/manage-segments/
---
## Create a segment

To create an audience segment that can be used in multiple audiences, use the following steps:

1. Go to **AudienceStream &gt; Audiences**.
1. Click the **SEGMENTS** tab, then click **&#43; New Segment**.
1. Enter a **Name** for the segment. If you use a [DataAccess]() product (EventStore, AudienceStore, EventDB, or AudienceDB), the segment name must be fewer than 128 characters in length. Otherwise, DataAccess may trim the segment name and errors may occur.
1. To add a condition, select an attribute, an operator, and a value.
    * The estimated potential size for the segment is displayed. For more information, see [potential size](#potential-size).
    * For operators that specify a time frame, select a value and the time frame.
1. To add another condition, click **&#43; Add Condition**.
    * Click **Calculate** to update the potential size as you edit or add conditions.
1. Click **Done**.
Save and publish is not required.

### Potential size

The potential size of the segment is the count of visitor profiles that match the defined segment conditions. The calculation result displays the number of visitors meeting the conditions as both a number and a percentage, alongside the total number of visitors. The total visitors count is the number of visitors in your Tealium profile within your configured retention window, which includes both anonymous and stitched visitors.

#### Limitations

Potential segment sizing is not available when a segment is built with the following attributes:

* **Visit attributes**: Visit attributes are transitory and do not persist after the visitor’s session ends.
* **Unsaved and unpublished attributes**: Attribute values are only created, enriched, and saved to a visitor profile when the attribute configuration is saved and published. Until the save and publish process occurs, no values exist that can be queried to calculate a potential segment size.

## Save a segment to favorites

To save a segment to favorites, use the following steps:

1. Go to **AudienceStream &gt; Audiences**.
1. Click the **SEGMENTS** tab.
1. Click the star next to the segment name.

## Filter the segments list

To filter the segments list by a label or by favorites, use the following steps:

1. Go to **AudienceStream &gt; Audiences**.
1. Click the **SEGMENTS** tab.
1. To filter by a specific label, click **Labels** and select a label.
1. To see only your favorite segments, click **Favorite** and select **Favorite**.

## Edit a segment

Currently, segments that are being used in an audience cannot be edited.

To edit a segment, use the following steps:

1. Go to **AudienceStream &gt; Audiences**.
1. Click the **SEGMENTS** tab, then select the segment to edit.
1. Click **Edit**.
    * Add or edit conditions as needed.
    * Click **Calculate** to update the potential size as you edit or add conditions.
1. Click **Done**. Save and publish is not required.

## Delete a segment

You cannot delete a segment that is in use in an audience.

Use the following steps to delete a segment:

1. Go to **AudienceStream &gt; Audiences**, and click the **SEGMENTS** tab.
1. Click the menu for the segment, then select **Delete**.  
The segment is deleted. Save and Publish is not required.