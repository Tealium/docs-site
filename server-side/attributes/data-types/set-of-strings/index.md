---
title: Set of Strings Attribute
description: The set of strings attribute stores a set of unique text values.
url: https://docs.tealium.com/server-side/attributes/data-types/set-of-strings/
---
## How it works

Values in a set are only stored once, regardless of the number of times they occur for the visitor or visit. The set of strings attribute is most commonly used for product categories viewed, pages viewed, and products purchased.

Examples:

|Attribute name| Values|
|---| ---|
|Product Categories Viewed| &#34;Home Improvement&#34;, &#34;Electronics&#34;, &#34;Apparel&#34;, &#34;Kitchen&#34;|
|Browsers Used| &#34;Chrome&#34;, &#34;Safari&#34;|
|Cart Items| &#34;iPad&#34;, &#34;Screen Protector&#34;, &#34;Headphones&#34;|

The set of strings attribute is available in the following scopes: Visit and Visitor.

![](/images/server-side/screenshot-2019-11-11-at-1.26.28-pm.png)

### Size limits

Sets of strings are limited to 30,000 strings. The size of a each string is not limited, but these attributes are still limited by the maximum size of the profile after encryption and compression (400 KB).

## Enrichments

### Add to Set of Strings

Add a string value to a set of strings. Adds only unique strings.

**Attribute Name**: `product_category`

* **Starting Value**:  `&#34;Home Improvement&#34;, &#34;Electronics&#34;, &#34;Kitchen&#34;`
* **Enriched With**: `&#34;Apparel&#34;, &#34;Electronics&#34;`
* **Resulting Value**: `&#34;Home Improvement&#34;, &#34;Electronics&#34;, &#34;Kitchen&#34;, &#34;Apparel&#34;`

The result ignores the &#34;Electronics&#34; item because it exists already in the set of strings.

### Store Array as Set of Strings

This enrichment is used to save the values from an array of strings attribute into a set of strings attribute. All duplicate elements in the array are ignored in the new set, which permits only unique strings.

**Attribute Name**: `Product Categories Viewed`

* **Starting Value**:  `&#34;Kitchen&#34;`
* **Enriched With**: `[&#34;Home Improvement&#34;, &#34;Electronics&#34;, &#34;Kitchen&#34;]`
* **Resulting Value**: `&#34;Home Improvement&#34;, &#34;Electronics&#34;, &#34;Kitchen&#34;`

### Update Set of Strings By Set of Strings

This enrichment appends the values from another set of strings attribute into the set of strings. For example, to track the product categories that a visitor purchases from you might have two set of strings attributes named &#34;Categories Purchased&#34;, with one scoped to visit to capture when the purchase occurs and one scoped to visitor to store the master set.

|**Visit: Categories Purchased**| **Visitor: Categories Purchased**|
|---|---|
|`&#34;Electronics&#34;`| `&#34;Electronics&#34;`|
|`&#34;Kitchen&#34;, &#34;Apparel&#34;`| `&#34;Electronics&#34;, &#34;Kitchen&#34;, &#34;Apparel&#34;`|
|`&#34;Kitchen&#34;, &#34;Electronics&#34;`| `&#34;Electronics&#34;, &#34;Kitchen&#34;, &#34;Apparel&#34;`|

While the set of strings scoped to visit is overwritten with new values each time, the enrichment copies those values into the set of strings scoped to visitor where the master list expands, storing each unique value encountered.

**Attribute Name**: `Product Category Purchased`

* **Starting Value**:  `&#34;Electronics&#34;`
* **Enriched With**: `&#34;Home Improvement&#34;, &#34;Electronics&#34;, &#34;Kitchen&#34;`
* **Resulting Value**: `&#34;Electronics&#34;, &#34;Home Improvement&#34;, &#34;Kitchen&#34;`

### Difference Between Two Sets of Strings

Create a new set of strings attribute that contains the items from one set of strings that do not appear in another set of strings. For example, to find the categories that a customer browsed, but did not purchase from, use this enrichment to find the difference between &#34;Categories Browsed&#34; and &#34;Categories Purchased&#34;.

Example:

Find values present in: `Categories Browsed` and that are not in: `Categories Purchased`.

**Attribute Name**: `Browsed Categories Not Purchased`

* **Starting Value**:  
* **Enriched With**:  &#34;Categories Browsed&#34;: `&#34;Home Improvement&#34;, &#34;Kitchen&#34;, &#34;Windows&#34;` &#34;Categories Purchased&#34;: `&#34;Home Improvement&#34;` 
* **Resulting Value**: `&#34;Kitchen&#34;, &#34;Windows&#34;`

### Remove Set of Strings

Remove a set of strings based on a set of conditions. This is the equivalent of deleting the set.

**Attribute Name**: `product_category`

* **Starting Value**:  `&#34;Home Improvement&#34;, &#34;Kitchen&#34;, &#34;Windows&#34;`
* **Resulting Value**: (Removed)

### Lowercase Set of Strings

Lowercase a set of strings based on a set of conditions.

**Attribute Name**: `product_category`

* **Starting Value**:  `&#34;Home Improvement&#34;, &#34;Electronics&#34;, &#34;Kitchen&#34;`
* **Resulting Value**: `&#34;home improvement&#34;, &#34;electronics&#34;, &#34;kitchen&#34;`

### Set to Top Tally Items

Create a set of strings using the highest valued items from a tally. For example, to track the three most viewed products, create a set of strings to capture the top three entries from a tally attribute that tracks the occurrences of viewed products.

**Attribute Name**: `Top 3 Products Viewed`

* **Starting Value**:  -- 
* **Enriched With**: Top 3 Items in &#34;Viewed Products&#34;: &lt;br&gt; `{ &#34;AirPods Pro&#34; : 3 &#34;iPhone 10&#34; : 6 &#34;iPhone Case&#34; : 10 &#34;MacBook Pro&#34; : 1 &#34;iMac&#34; : 2 }`
* **Resulting Value**: `&#34;iPhone Case&#34;, &#34;iPhone 10&#34;, &#34;AirPods Pro&#34;`

### Set to Tally Items Above Target Value

Create a set of strings using the items from a tally whose values are above a set threshold. For example, to track products that have been viewed more than 20 times, create a set of strings to capture the entries from a tally attribute that tracks the occurrences of viewed products.

**Attribute Name**: `Products Viewed 20&#43; Times`

* **Starting Value**: --
* **Enriched With**:  Items in &#34;Products Viewed&#34; that are greater than 20: &lt;br&gt;`{  &#34;AirPods Pro&#34; : 21,  &#34;iPhone 10&#34; : 35, &#34;iPhone Case&#34; : 12, &#34;MacBook Pro&#34; : 1 &#34;iMac&#34; : 2 }` 
* **Resulting Value**:  `&#34;iPhone 10&#34;, &#34;AirPods Pro&#34;` 

### Remove Entry from Set of Strings

Remove an entry from a set of strings based on a set of conditions. For example, remove the entry &#34;iPhone Case&#34; from a set of strings that tracks a product wish list because it has been purchased.

**Attribute Name**: `Product Wish List`

* **Starting Value**:  `&#34;iPhone 10&#34;, &#34;AirPods Pro&#34;, &#34;iPhone Case&#34;`
* **Enriched With**:  Remove `purchased_product` (value &#34;iPhone Case&#34;) 
* **Resulting Value**: `&#34;iPhone 10&#34;, &#34;AirPods Pro&#34;`
