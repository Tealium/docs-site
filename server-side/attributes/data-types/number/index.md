---
title: Number Attribute
description: This article describes how to use the number attribute.
url: https://docs.tealium.com/server-side/attributes/data-types/number/
---
The number attribute stores a numeric value for browsing metrics such as visits, page views, and events. Common examples include Lifetime Value, Order Total Transaction, or Days Since Last Purchase.

## How it works

Numeric values are stored as decimals or integers. Choose the type that matches your needs:

* **Decimal (default)**
    * Decimal values can have zero or more decimal digits.
    * For example: `12`, `12.0`, `12.345`
    * Decimal values use the Java Double class. For more information, see [Class Double](https://docs.oracle.com/javase/8/docs/api/java/lang/Double.html).
    * Recommended for attributes that represent monetary values.
* **Integer**  
    * Only whole number values are stored.
    * For example: `12`, `-4`, `3214`
    * Useful for number attributes that represent quantities, counters, or scores.

The number attribute is available in the following scopes: Event, Visit, Visitor.

![](/images/server-side/scope-3checks.png)

### Size Limits

Decimal values of number attributes must be in the range of `-1.7976931348623157×10^308` to `1.7976931348623157×10^308`. Integer values of number attributes must be in the range of `-2147483647` to `2147483647`.

Number attributes are also limited by the maximum size of the profile after encryption and compression (400 KB).

## Enrichments

### Increment or decrement number enrichment

This enrichment modifies a number with a positive value (increment) or a negative value (decrement). The modifying value can be a separate number attribute or a constant value.

For example, to calculate the Lifetime Total Value (LTV) of a visitor&#39;s orders use this enrichment to increment the attribute with the value of the `order_total` attribute each time the `purchase` event occurs.

**Attribute Name**: Lifetime Total Value

* **Initial**: `121.78` 
* **Enriched With**:  order_total `220.00`
* **Result**: `341.78`

### Set ratio

Set the quotient of two numbers as a new ratio number.

For example, to calculate the Average Cart Items Per Order use this enrichment to set the ratio of the Total Cart Items Purchased attribute to the Total Orders Completed attribute.

**Attribute Name**: Average Cart Items Per Order

* **Initial**: ---
* **Enriched With**:  
Total Cart Items Purchased: `48.00`  
Total Orders Completed: `3.00` 
* **Result**: `16.00`

### Set product

Set the product of two numbers as a new number.

For example, to calculate the `coupon_discount_amount`, use this enrichment to multiply the `order_subtotal` by the `coupon_discount_percent`.

**Attribute Name**: `coupon_discount_amount`

* **Initial**:---
* **Enriched With**:  
order_subtotal: `42.00`  
coupon_discount_percent: `0.05`
* **Result**: `2.10`

### Set difference

Set the difference of two numbers as a new number.

**Attribute Name**: `order_subtotal`

* **Initial**: `42.00 `
* **Enriched With**:  
order_subtotal: `42.00`  
coupon_discount_amount: `2.10`
* **Result**: `39.90`

### Set sum

Set to the sum of two numbers.

For example, set `order_total` to the sum of `order_subtotal` and `order_tax_amount`.

**Attribute Name**: `order_total`

* **Initial**: ---
* **Enriched With**:  
order_subtotal: `39.90`  
order_tax_amount: `3.29`
* **Result**: `43.19`

### Set number

Set the number to a specific number.

For example, set Last Purchase Amount to the value of `order_total` whenever the `purchase` event occurs.

**Attribute Name**: Last Purchase Amount

* **Initial**: ---
* **Enriched With**: order_total:`43.19`
* **Result**: `43.19`

### Set difference between two dates
(AudienceStream only)

Calculates the elapsed time between two events. Elapsed time can be expressed as one of the following:

* Minutes
* Hours
* Days
* Weeks
* Months

The difference is always stored as a positive value, so the dates can be set in any order.

For example, to calculate Days Since Last Purchase as the difference in days between Last Purchase Date and Current Visit Date.

While date attributes are stored as Unix timestamps, these examples use formatted dates for readability.

**Attribute Name**: Days Since Last Purchase

* **Initial**: ---
* **Enriched With**:  
Last Purchase Date: `&#34;2018/10/30&#34;`  
Current Visit Date: `&#34;2019/11/01&#34;`
* **Result**: `367`

### Set rolling average based on timeline
(AudienceStream only)

The rolling average is the arithmetic mean of numerical values captured over time. These values come from number and [tally]() attributes that are collected as entries in a [timeline](). The timeline&#39;s expiration determines which entries can be factored into the final average. If there is not an expiration date, it is a simple average solution.

**Attribute Name**: Average Order Value

* **Initial**: ---
* **Enriched With**: `[20.00, 30.00, 40.00, 50.00]`
* **Result**: `35.00`

### Set rolling sum based on timeline
(AudienceStream only)

A rolling sum is the aggregate of numerical values in a number or [tally]() attribute that are captured as entries in a [timeline](). The timeline&#39;s expiration determines which entries can be factored in during the aggregation.

**Attribute Name**: Total Order Value

* **Initial**: ---
* **Enriched With**: `[10.00, 20.00, 30.00, 40.00, 50.00]`
* **Result**: `150.00`

### Set number to the number of entries in timeline

Set the number to the number of entries in a timeline.

**Attribute Name**: Total Order Count

* **Initial**: ---
* **Enriched With**: `[10.00, 20.00, 30.00, 40.00, 50.00]`
* **Result**: `5.00`

### Set number to tally value
(AudienceStream only)

Set the number to a specific value within the tally. Specify the tally attribute and the name of the entry in the tally. For example, a tally for Site Category Views might have an entry for &#34;Shoes&#34;.

**Attribute Name**: Shoe Category View Count

* **Initial**: ---
* **Enriched With**: Site Category Views: `{&#34;Shoes&#34;: 42}`
* **Result**: `42`

### Set number to the count of items in tally
(AudienceStream only)

Set the attribute to the number of entries in a tally. For example, a tally for Site Category Views might have three entries in it.

**Attribute Name**: Number of Categories Viewed

* **Initial**: ---
* **Enriched With**:  
``` 
{  
  &#34;Shoes&#34;: 42,  
  &#34;Shirts&#34;: 11,  
  &#34;Pants&#34;: 8
} 
``` 
* **Result**: `3.00`

### Set number to the count of items in set of strings
(AudienceStream only)

Set the number to the count of items in a set of strings. For example, a set of strings Active Browser Types might have three entries.

**Attribute Name**: Number of Active Browser Types

* **Initial**: ---
* **Enriched With**: `[&#34;Firefox&#34;, &#34;Safari&#34;, &#34;Chrome&#34;]`
* **Result**: `3.00`

### Set number to tally&#39;s rolling max based on a timeline
(AudienceStream only)

Set the number to the rolling maximum of another number in a tally captured within a timeline.

**Attribute Name**: Highest Order Value

* **Initial**: ---
* **Enriched With**: `[10.00, 20.00, 30.00, 40.00, 50.00]`
* **Result**: `50.00`

### Set number to change in number
(AudienceStream only)

Set this attribute to the difference between it and another attribute since the last event. For example, use this enrichment to capture the difference between a previous order amount and the current order amount. To set an attribute named Change in Order Value, set it to the change in `order_subtotal` since the previous order.

**Attribute Name**: Change in Order Value

* **Initial**: `30.00 `
* **Enriched With**: order_subtotal: `42.00`
* **Result**: `12.00`

### Set number to change in date
(AudienceStream only)

Set this attribute to the change in value of the selected value between this event and the last event. For example, use this enrichment to capture the change in months of the Last Purchase Date date attribute each time a purchase occurs.

The change in date can be expressed as one of the following:

* Minutes
* Hours
* Days
* Weeks
* Months

**Attribute Name**: Months Since Last Purchase

* **Initial**: 
* **Enriched With**:  
Last Purchase Date (last event): `&#34;10/31/2019&#34;`  
Last Purchase Date (this event): `&#34;12/31/2019&#34;` 
* **Result**: 2 (months)

### Set To Number Based On Average of An Array of Numbers
(EventStream only)

Set this attribute to the average of an array of numbers.

**Attribute Name**: Average Purchase Price

* **Initial**: ---
* **Enriched With**: `[20.00, 25.00, 30.00, 35.00, 40.00]`
* **Result**: `30.00`

### Set To Number Based On Max of An Array of Numbers
(EventStream only)

Set this attribute to the maximum value within an array of numbers.

**Attribute Name**: Most Expensive Product Purchased

* **Initial**: ---
* **Enriched With**: `[20.00, 25.00, 30.00, 35.00, 40.00]`
* **Result**: `40.00`

### Set To Number Based On Min of An Array of Numbers
(EventStream only)

Set this attribute to the minimum value within an array of numbers.

**Attribute Name**: Least Expensive Product Purchased

* **Initial**: ---
* **Enriched With**: `[20.00, 25.00, 30.00, 35.00, 40.00]`
* **Result**: `20.00`

### Set to the number of items in an array

Set to the number of items in an array. For example, to store the number of products in the cart, use this enrichment to capture the number of items in the `cart_product_id` array.

**Attribute Name**: `num_cart_items`

* **Initial**: ---
* **Enriched With**: product_id: `[&#34;prod123&#34;, &#34;prod456&#34;]`
* **Result**: `2.00`
