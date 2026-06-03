---
title: Array of booleans
description: This article describes how to use an array of booleans.
url: https://docs.tealium.com/server-side/attributes/data-types/arrays/array-of-booleans/
---
The array of booleans attribute stores a list of true/false values.

The array of booleans is available in the following scopes: Event, Visit, Visitor.

![](/images/server-side/screenshot-2019-11-11-at-1.24.29-pm.png)

The strings &#34;true&#34; and &#34;false&#34; (any mix of upper/lowercase) are converted to their respective boolean values. All other non-boolean values are ignored.

## Enrichments

### Add a boolean

This enrichment adds a value to the array. The added attribute can only be a boolean, iQ variable, or omnichannel attribute. For example, you may want to add a boolean to the array to represent that the customer purchased on their last visit.

**Attribute Name**: `did_purchase_on_visit`

* **Starting value**: `[true]`
* **Enriched With**: `false`
* **Resulting value**: `[true, false]`

### Add an array of booleans

This enrichment adds all the values from another array to the array. The added attribute type can only be an array of booleans or iQ variables.

**Attribute Name**: `my_booleans`

* **Starting value**: `[true]`
* **Enriched With**: `[false, true]`
* **Resulting value**: `[true, false, true]`

### Reset

This enrichment removes all values from the boolean array.

**Attribute Name**:`did_purchase_on_visit`

* **Starting value**: `[true, false, true]`
* **Resulting value**: (Removed)
