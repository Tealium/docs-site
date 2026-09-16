---
title: Manage segments
description: This article provides information about creating, editing, and deleting segments, as well as saving segments as favorites.
url: https://docs.tealium.com/server-side/audiences/manage-segments/
---
## Create a segment

To create an audience segment for use in multiple audiences, use the following steps:

1. Go to **Activate > Audiences**.
1. Click the **SEGMENTS** tab, then click **+ New Segment**.
1. Enter a **Name** for the segment. 
<blockquote>
If you use a [DataAccess](https://docs.tealium.com/about-dataaccess/) product (EventStore, AudienceStore, EventDB, or AudienceDB), the segment name must be fewer than 128 characters in length. Otherwise, DataAccess may trim the segment name and errors may occur.
</blockquote>

1. To add a condition, select an attribute, an operator, and a value.
    * The segment displays an estimated potential size. For more information, see [potential size](#potential-size).
    * For operators that specify a time frame, select a value and the time frame.
1. To add another condition, click **+ Add Condition**.
    * Click **Calculate** to update the potential size as you edit or add conditions.
1. Click **Done**.
You do not need to save and publish.

### Potential size

The potential size of the segment is the count of visitor profiles that match the defined segment conditions. The result displays matching visitors as a number and a percentage, alongside the total visitors in your Tealium profile within your configured retention window. The total includes both anonymous and stitched visitors.

#### Limitations

Potential segment sizing has the following limitations:

* **Visit attributes**: Visit attributes are transitory and do not persist after the visitor's session ends.
* **Unsaved and unpublished attributes**: Attribute values are only created, enriched, and saved to a visitor profile when the attribute configuration is saved and published. Until then, no values exist to query for a potential segment size calculation.
* **Rate limit**: Potential size calculations are limited to 30 requests every 6 hours for each profile. When you reach the limit, an error message appears. To request a higher limit, [contact support](https://docs.tealium.com/support/).

## Save a segment to favorites

To save a segment to favorites, use the following steps:

1. Go to **Activate > Audiences**.
1. Click the **SEGMENTS** tab.
1. Click the star next to the segment name.

## Filter the segments list

To filter the segments list by a label or by favorites, use the following steps:

1. Go to **Activate > Audiences**.
1. Click the **SEGMENTS** tab.
1. To filter by a specific label, click **Labels** and select a label.
1. To see only your favorite segments, click **Favorite** and select **Favorite**.

## Edit a segment


<blockquote>
Currently, segments that are being used in an audience cannot be edited.
</blockquote>


To edit a segment, use the following steps:

1. Go to **Activate > Audiences**.
1. Click the **SEGMENTS** tab, then select the segment to edit.
1. Click **Edit**.
    * Add or edit conditions as needed.
    * Click **Calculate** to update the potential size as you edit or add conditions.
1. Click **Done**. You do not need to save and publish.

## Delete a segment


<blockquote>
You cannot delete a segment that is in use in an audience.
</blockquote>


Use the following steps to delete a segment:

1. Go to **Activate > Audiences**, and click the **SEGMENTS** tab.
1. Click the menu for the segment, then select **Delete**.  
The segment is deleted. You do not need to save and publish.
