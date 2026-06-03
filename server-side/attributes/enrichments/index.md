---
title: About enrichments
url: https://docs.tealium.com/server-side/attributes/enrichments/
---

An enrichment is the use of custom logic to transform an attribute from a static value to a dynamic one. This is used to create new data values or modify incoming data. Pre-built enrichments are available for each data type. For example, the ability to increment or decrement a numeric value is available to number attributes.

## Linked enrichments

When two or more enrichments have a dependency on the same attribute, they become _linked enrichments_. The following example shows the enrichments applied to the start and end of a visit. The enrichment in the `Visit Start` attribute uses the `Visit End` attribute and vice-versa. Because each enrichment is linked to the other by an attribute, they are considered linked enrichments.

![](/images/server-side/whiteui-usingenrichments-visitstart-and-visitend-linked-enrichments-combined-screens.png)

## Size limits 

Some enrichments, such as the Join Attributes enrichment, can increase the size of an attribute. Most attributes for EventStream and AudienceStream have storage capacity limits and specific behaviors for when those limits are exceeded. Also, the entire visit or visitor profile has a limit of 400 KB compressed and encrypted.

For more information, see[About attributes]().