---
title: Tally Attribute
description: This article explains how to use the tally attribute.
url: https://docs.tealium.com/server-side/attributes/data-types/tally/
---
## How it works

The tally attribute stores a collection of key-value pairs that count the occurrences of named items across many events.

For example, to keep track of the product categories that a visitor purchases from, use a tally named &#34;Product Category Purchases&#34; and enrich it with the names of product categories found in the event attribute `product_category` when purchase events occur. Over time the tally will provide valuable information about the visitor&#39;s buying habits.

|Tally Key| Tally Value|
| --- | --- |
|&#34;Shoes&#34;| 1|
|&#34;Pants&#34;| 3|
|&#34;Shirts&#34;| 7|
|&#34;Shorts&#34;| 2|

* The key represents the name of the item that occurred, for example the value of the `product_category` attribute &#34;Shoes&#34;.
* The value represents the number of times it occurred.

### Size limits

Tallies are limited to 30,000 key-value pairs. Tally attributes are also limited by the maximum size of the profile after encryption and compression (400 KB).

### Scope

The tally attribute is available in the following scopes: Visit, Visitor.

![](/images/server-side/screenshot-2019-11-11-at-1.26.28-pm.png)

### Tally favorite

By default, each tally attribute generates a corresponding string attribute that automatically captures the name of the tally entry with the highest value. This string attribute has the same name as the tally, but with the word &#34;(favorite)&#34; appended. For example, a tally named &#34;Product Categories Purchased&#34; would also have a string attribute named &#34;Product Categories Purchased (Favorite)&#34;.

### Tally tie breaker logic

A tally tie occurs when multiple keys have the same value. When this happens, the favorite is chosen based on the following logic:

* If a tie occurs, the most recently incremented key becomes the favorite.
* If more than one key was incremented simultaneously using an array of values, the last entry processed becomes the favorite.
* If the order in which multiple keys were incremented is unclear, the favorite is chosen using an alphabetical sort.

### Examples

The events below describes some possible tally tie scenarios and the chosen favorite in each scenario.

**Event 1**

There is only one key `Apparel` in this `page_category` event, so it becomes the favorite.

```
// Recieved Event
&#34;page_category&#34;: { [&#34;Apparel&#34;] }

// Result
&#34;page_category&#34;:{
    &#34;Apparel&#34;: 1
},
&#34;page_category_favorite&#34;: &#34;Apparel&#34;
```

**Event 2**

In this event, two keys `Apparel` and `Accessories` are received, causing a 3-way tie. Since `Accessories` is the last entry processed, it becomes the favorite.

```
// Received Event
&#34;page_category&#34;: { [&#34;Apparel&#34;, &#34;Accessories&#34;] }

// Result
&#34;page_category&#34;: {
    &#34;Books&#34;: 1,
    &#34;Apparel&#34;: 1,
    &#34;Accessories&#34;: 1
},
&#34;page_category&#34;: &#34;Accessories&#34;
```

**Event 3**

In this event, one key `Apparel` is received making it the key with the highest value, therefore, it becomes favorite.

```js
// Recieved Event
&#34;page_category&#34;: { [&#34;Apparel&#34;] }

// Result
&#34;page_category&#34;: {
    &#34;Accessories&#34;: 1,
    &#34;Apparel&#34;: 2,
    &#34;Books&#34;: 1
},
&#34;page_category_favorite&#34;: &#34;Apparel&#34;
```

## Example

The following table illustrates the example of a tally named &#34;Product Category Purchased&#34;, which counts the number of times each product category was purchased from. This tally automatically populates a string attribute with the name of the entry containing the highest value.

**Tally Attribute: &#34;Product Category Purchased&#34;**

|Tally Key| Tally Value|
| --- | --- |
|&#34;Shoes&#34;| 1|
|&#34;Pants&#34;| 3|
|&#34;Shirts&#34;| 7|
|&#34;Shorts&#34;| 2|
|**String Attribute: &#34;Product Category Purchased (Favorite)&#34;**| **&#34;Shirts&#34;**|

## Enrichments

### Increment Tally

Increment a number within a tally based on the value of another attribute. For example, to track the number of times each product category is viewed, use a tally named Product Category Viewed and enrich it with the `product_category` attribute. The values of `product_category` become entries in the tally.

The number attribute stores a number for browsing metrics such as visits, page views, and events. Common examples include Lifetime Value, Order Total Transaction, or Days Since Last Purchase.

To specify the number type, select **Decimal** or **Integer** from the **Type** drop-down list.

* **Decimal**
    * Default value.
    * Decimal values can have zero (0) or more decimal digits.
    * Example: `12`, `12.0`, `12.345`
    * Required for attributes that represent monetary values.
* **Integer**  
    * Only whole number values are stored.
    * Example: `12`, `-4`, `3214`
    * Useful for whole number attributes that represent quantities, counters, or scores.

**Attribute Name**: &#34;Product Category Viewed&#34;

* **Starting Value**: `{&#34;Shoes&#34;: 7, &#34;Pants&#34;: 1, &#34;Shirts&#34;: 3}`
* **Enriched With**: `product_category:&#34;Shoes&#34;`
* **Resulting Value**: `{&#34;Shoes&#34;: 8, &#34;Pants&#34;: 1, &#34;Shirts&#34;: 3}`

### Increment Tally Value

Increment a tally entry based on a custom name with a custom value or another attribute value. For example, use a tally named &#34;Product Category Searched&#34; and enrich it with a hard-coded value of &#34;Did Not Search&#34; when a search has not occurred (a condition likely based on a boolean attribute that keeps track of searches). Since the name &#34;Did Not Search&#34; would not naturally occur in a `product_category` attribute, this enrichment is used to add the custom entry.

**Attribute Name**: &#34;Product Category Searched&#34;

* **Starting Value**: `{&#34;Shoes&#34;: 7, &#34;Pants&#34;: 1, &#34;Shirts&#34;: 3}`
* **Enriched With**: Custom Key: `&#34;Did Not Search&#34;`&lt;br&gt; Custom Increment: `1`
* **Resulting Value**: `{&#34;Did Not Search&#34;: 1, &#34;Shoes&#34;: 7, &#34;Pants&#34;: 1, &#34;Shirts&#34;: 3}`

### Increment Tally by Tally

Increment the values in a tally by the values found in another tally.

**Attribute Name**: &#34;Product Category Purchased (Lifetime)&#34;

* **Starting Value**: `{&#34;Shoes&#34;: 7, &#34;Pants&#34;: 1, &#34;Shirts&#34;: 3}`
* **Enriched With**: `{&#34;Shoes&#34;: 1, &#34;Shirts&#34;: 2, &#34;Dresses&#34;: 1}`
* **Resulting Value**: `{&#34;Shoes&#34;: 8, &#34;Pants&#34;: 1, &#34;Shirts&#34;: 5, &#34;Dresses&#34;: 1}`

### Increment Tally by Set of Strings

Increment the entries in a tally based on the entries in a set of strings. For example, use a tally named &#34;Product Category Searched (Lifetime)&#34; to track the product categories searched per visit, and enrich it with a set of strings named &#34;Product Categories Searched (Visit)&#34; at the end of each visit.

**Attribute Name**: &#34;Product Category Searched (Lifetime)&#34;

* **Starting Value**: `{&#34;Shoes&#34;: 7, &#34;Pants&#34;: 1, &#34;Shirts&#34;: 3}`
* **Enriched With**: Product Categories Search (Visit):`{&#34;Shoes&#34;, &#34;Pants&#34;, &#34;Hats&#34;}`
* **Resulting Value**: `[&#34;Shoes&#34;: 8, &#34;Pants&#34;: 2, &#34;Shirts&#34;: 3, &#34;Hats&#34;: 1}`

### Set Rolling Average Based on Timeline

The rolling average is the arithmetic mean of numerical values captured over time. These values come from [number]() and [tally]() attributes that are all collected as entries in a [Timeline](). The timeline&#39;s expiration determines which entries can be factored into the final average. If there is no expiration date, it is a simple average solution.

**Attribute Name**: &#34;Average Product Category Purchase Amounts&#34;

* **Starting Value**: `{}`
* **Enriched With**:  Timeline entry: `{&#34;Shoes&#34;: 150.00, &#34;Pants&#34;: 75.00, &#34;Shirts&#34;: 30.00}`&lt;br&gt; Timeline entry: `{&#34;Pants&#34;: 75.00, &#34;Shirts&#34;: 42.00}`&lt;br&gt; Timeline entry: `{&#34;Shoes&#34;: 110.00, &#34;Shirts&#34;: 18.00 &#34;Hats&#34;: 25.00}` 
* **Resulting Value**: `{&#34;Shoes&#34;: 130.00, &#34;Pants&#34;: 75.00, &#34;Shirts&#34;: 30.00, &#34;Hats&#34;: 25.00}`

### Set Rolling Sum Based on Timeline

A rolling sum is the aggregate of numerical values in a number or [tally]() attribute that are captured as entries in a [timeline](). The Timeline&#39;s expiration determines which entries can be factored in during the aggregation.

**Attribute Name**: &#34;Sum Product Category Purchase Amounts&#34;

* **Starting Value**: `{}`
* **Enriched With**:  Timeline entry: `{&#34;Shoes&#34;: 150.00, &#34;Pants&#34;: 75.00, &#34;Shirts&#34;: 30.00}`&lt;br&gt; Timeline entry: `{&#34;Pants&#34;: 75.00, &#34;Shirts&#34;: 42.00}`&lt;br&gt; Timeline entry: `{&#34;Shoes&#34;: 110.00, &#34;Shirts&#34;: 18.00 &#34;Hats&#34;: 25.00}` 
* **Resulting Value**: `{&#34;Shoes&#34;: 260.00, &#34;Pants&#34;: 150.00, &#34;Shirts&#34;: 90.00, &#34;Hats&#34;: 25.00}`

### Set Tally by Corresponding Arrays

Set the tally to the values defined in two corresponding arrays. For example, use a tally named &#34;Product Category Quantity Purchased&#34; to capture the quantity of products purchased and enrich it with the two arrays `product_category` and `product_quantity` when a purchase event occurs.

**Attribute Name**: &#34;Product Category Quantity Purchased&#34;

* **Starting Value**: `{}`
* **Enriched With**:  `product_category: [&#34;Shoes&#34;, &#34;Pants&#34;, &#34;Shirts&#34;]`&lt;br&gt;`product_quantity: [1, 1, 3]` 
* **Resulting Value**: `{&#34;Shoes&#34;: 1, &#34;Pants&#34;: 1, &#34;Shirts&#34;: 3}`

### Remove Tally

Remove tally based on a set of conditions.

The remove tally enrichment can be used to reset a tally. For example, if you have been tracking visitor&#39;s product category searches, you might clear that tally once an order is placed.

**Attribute Name**: reset tally to zero

* **Starting Value**: `{&#34;Shoes&#34;: 1, &#34;Pants&#34;: 3}`
* **Enriched With**: `Purchase event occurs`
* **Resulting Value**: (Removed)

### Remove an Entry in a Tally

Remove an entry in a tally based on a set of conditions. For example, use a tally named &#34;Product Category Searched&#34; to track a visitors product searches (and potential purchases) then use this enrichment to remove the tally entries that match items in a purchase.

**Attribute Name**: &#34;Product Category Searched (Not Purchased)&#34;

* **Starting Value**: `{&#34;Shoes&#34;: 7, &#34;Pants&#34;: 1, &#34;Shirts&#34;: 3, &#34;Jeans&#34;: 10}`
* **Enriched With**: `product_catgory : &#34;Shoes&#34;`
* **Resulting Value**: `{&#34;Pants&#34;: 1, &#34;Shirts&#34;: 3, &#34;Jeans&#34;: 10}`

### Increment by 1 for Each Item in an Array

Increment by one (1) for each item in an array. For example, use a tally named &#34;Product Category Purchased&#34; and enrich it with the array attribute `product_category` when a purchase event occurs.

**Attribute Name**: &#34;Product Category Purchased&#34;

* **Starting Value**: `{&#34;Shoes&#34;: 1, &#34;Pants&#34;: 1, &#34;Shirts&#34;: 3}`
* **Enriched With**: `product_category : [&#34;Pants&#34;, &#34;Ties&#34;]`
* **Resulting Value**: `{&#34;Shoes&#34;: 1, &#34;Pants&#34;: 2, &#34;Shirts&#34;: 3, &#34;Ties&#34;: 1}`
