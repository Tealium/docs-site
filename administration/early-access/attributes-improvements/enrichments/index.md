---
title: Manage enrichments
description: This article describes enrichments and how to add them.
url: https://docs.tealium.com/administration/early-access/attributes-improvements/enrichments/
---

<blockquote>
The new attributes interface is in Early Access and is only available to select customers. If you are interested in trying this feature, contact your Tealium Support representative.
</blockquote>


## How it works

An enrichment is the use of custom logic to transform an attribute from a static value to a dynamic one. This is used to create new data values or modify incoming data. Available enrichments are dependent on the data type of the attribute. For example, the ability to increment or decrement a numeric value is available to number attributes.

## View enrichments

To view enrichments:

1. From the left navigation bar, go to **Transform > Visitor / Visit Attributes** to view your attributes. ![](https://docs.tealium.com/images/server-side/attributes/visit-visitor-attributes-table.png)
1. Click any attribute in the table to view that attribute's details. ![](https://docs.tealium.com/images/server-side/attributes/attribute-details-slideout.png)

## Add an enrichment

To add an enrichment:

1. In the **Add Attribute** dialog, click **Add Enrichment** and select the  enrichment you want.
1. The settings vary depending on the data type of enrichment. For details about enrichments for each data type, see [Data Types](https://docs.tealium.com/data-types/).
1. Select **WHEN** to trigger the enrichment. This controls the timing of the enrichment.
    * **New Visitor** – Occurs the first time a visitor comes to your site.
    * **New Visit** – Occurs on a new visit by a visitor.
    * **Any Event** – Occurs on any event.
    * **Visit Ended** – Occurs when a visit ends, based on the following time of inactivity:
        * Web sessions: 30 minutes (10 minutes [if only one event is received](https://support.tealiumiq.com/en/support/solutions/articles/36000363388-how-are-single-page-visits-processed-in-audiencestream-))
        * Mobile App sessions: 2 minutes
        * Omnichannel sessions: 1 minute

1. Select an existing **Rule** condition or [create a new rule]().
1. Click **Finish**.
1. Save and publish your profile to apply the changes.

## Size limits 

Some enrichments, such as the Join Attributes enrichment, can increase the size of an attribute. Most attributes for EventStream and AudienceStream have storage capacity limits and specific behaviors for when those limits are exceeded. Also, the entire visit or visitor profile has a limit of 400 KB compressed and encrypted.

For more information, see [About attributes](https://docs.tealium.com/about-attributes/#size-limits).