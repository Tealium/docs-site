---
title: Array of numbers
description: This article describes how to use the data types array of strings, array of numbers, and array of booleans.
url: https://docs.tealium.com/server-side/attributes/data-types/arrays/array-of-numbers/
---
The array of numbers attribute stores a list of numeric values for browsing metrics such as visits, page views, and purchase events.

Numeric values are stored as decimals or integers. Choose the type that matches your needs:

* **Decimal (default)**
  * Decimal values can have zero or more decimal digits.
  * Example: `12`, `12.0`, `12.345`
  * Recommended for attributes that represent monetary values.

* **Integer**  
  * Only whole number values are stored.
  * Example: `12`, `-4`, `3214`
  * Useful for number attributes that represent quantities, counters, or scores.

The array of numbers is available in the following scopes: Event, Visit, Visitor.

![](https://docs.tealium.com/images/server-side/screenshot-2019-11-11-at-1.24.29-pm.png)


<blockquote>
String representations of numbers (`0`, `123`, `12.95`) are converted to their numeric values. All other non-numeric values are ignored.
</blockquote>


## Enrichments

### Add a number

This enrichment adds a number value to the array. The added attribute can only be a number, iQ variable, or omnichannel attribute. For example, you may want to add the last purchase value to the rolling `purchase_total_history` value array.

**Attribute Name**: `purchase_total_history`

* **Starting value**: `[12.95]`
* **Enriched With**: `5.99`
* **Resulting value**: `[12.95, 5.99]`

### Add an array of numbers

This enrichment adds all the values from another array to the array. The added attribute type can only be an array of numbers or iQ variable. For example, you may want to add the array of purchased product prices to an array of all purchased product prices.

**Attribute Name**: `purchased_products_history`

* **Starting value**: `[24.99, 12.95]`
* **Enriched With**: `[5.99, 10.00]`
* **Resulting value**: `[24.99, 12.95, 5.99, 10.00]`

### Reset

This enrichment removes all values from the array. For example, you may want to remove the last purchase items from the array of last purchases.

**Attribute Name**: `purchase_total_history`

* **Starting value**: `[12.95, 5.99]`
* **Resulting value**: (Removed)

### Set array of numbers to be the difference of two arrays

This enrichment takes two arrays as input, looks for values that occur in one and not the other, and inserts them into the array. In this example, values from `Gift Card Amounts` that do not also occur in `Gift Cards Purchased` are added to the resulting array.

**Attribute Name**: `gift_card_not_purchased`

* **Starting value**: `[]`
* **Enriched With**:  Difference between: `Gift Card Amounts` `[5.00, 10.00, 25.00, 50.00, 100.00, 250.00]` and `Gift Cards Purchased` `[25.00, 50.00]` 
* **Resulting value**: `[5.00, 10.00, 100.00, 250.00]`
