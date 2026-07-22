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
|Product Categories Viewed| "Home Improvement", "Electronics", "Apparel", "Kitchen"|
|Browsers Used| "Chrome", "Safari"|
|Cart Items| "iPad", "Screen Protector", "Headphones"|

The set of strings attribute is available in the following scopes: Visit and Visitor.

![](https://docs.tealium.com/images/server-side/screenshot-2019-11-11-at-1.26.28-pm.png)

### Size limits

Sets of strings are limited to 30,000 strings. The size of a each string is not limited, but these attributes are still limited by the maximum size of the profile after encryption and compression (400 KB).

## Enrichments

### Add to Set of Strings

Add a string value to a set of strings. Adds only unique strings.

**Attribute Name**: `product_category`

* **Starting Value**:  `"Home Improvement", "Electronics", "Kitchen"`
* **Enriched With**: `"Apparel", "Electronics"`
* **Resulting Value**: `"Home Improvement", "Electronics", "Kitchen", "Apparel"`

The result ignores the "Electronics" item because it exists already in the set of strings.

### Store Array as Set of Strings

This enrichment is used to save the values from an array of strings attribute into a set of strings attribute. All duplicate elements in the array are ignored in the new set, which permits only unique strings.

**Attribute Name**: `Product Categories Viewed`

* **Starting Value**:  `"Kitchen"`
* **Enriched With**: `["Home Improvement", "Electronics", "Kitchen"]`
* **Resulting Value**: `"Home Improvement", "Electronics", "Kitchen"`

### Update Set of Strings By Set of Strings

This enrichment appends the values from another set of strings attribute into the set of strings. For example, to track the product categories that a visitor purchases from you might have two set of strings attributes named "Categories Purchased", with one scoped to visit to capture when the purchase occurs and one scoped to visitor to store the master set.

|**Visit: Categories Purchased**| **Visitor: Categories Purchased**|
|---|---|
|`"Electronics"`| `"Electronics"`|
|`"Kitchen", "Apparel"`| `"Electronics", "Kitchen", "Apparel"`|
|`"Kitchen", "Electronics"`| `"Electronics", "Kitchen", "Apparel"`|

While the set of strings scoped to visit is overwritten with new values each time, the enrichment copies those values into the set of strings scoped to visitor where the master list expands, storing each unique value encountered.

**Attribute Name**: `Product Category Purchased`

* **Starting Value**:  `"Electronics"`
* **Enriched With**: `"Home Improvement", "Electronics", "Kitchen"`
* **Resulting Value**: `"Electronics", "Home Improvement", "Kitchen"`

### Difference Between Two Sets of Strings

Create a new set of strings attribute that contains the items from one set of strings that do not appear in another set of strings. For example, to find the categories that a customer browsed, but did not purchase from, use this enrichment to find the difference between "Categories Browsed" and "Categories Purchased".

Example:

Find values present in: `Categories Browsed` and that are not in: `Categories Purchased`.

**Attribute Name**: `Browsed Categories Not Purchased`

* **Starting Value**:  
* **Enriched With**:  "Categories Browsed": `"Home Improvement", "Kitchen", "Windows"` "Categories Purchased": `"Home Improvement"` 
* **Resulting Value**: `"Kitchen", "Windows"`

### Remove Set of Strings

Remove a set of strings based on a set of conditions. This is the equivalent of deleting the set.

**Attribute Name**: `product_category`

* **Starting Value**:  `"Home Improvement", "Kitchen", "Windows"`
* **Resulting Value**: (Removed)

### Lowercase Set of Strings

Lowercase a set of strings based on a set of conditions.

**Attribute Name**: `product_category`

* **Starting Value**:  `"Home Improvement", "Electronics", "Kitchen"`
* **Resulting Value**: `"home improvement", "electronics", "kitchen"`

### Set to Top Tally Items

Create a set of strings using the highest valued items from a tally. For example, to track the three most viewed products, create a set of strings to capture the top three entries from a tally attribute that tracks the occurrences of viewed products.

**Attribute Name**: `Top 3 Products Viewed`

* **Starting Value**:  -- 
* **Enriched With**: Top 3 Items in "Viewed Products": <br> `{ "AirPods Pro" : 3 "iPhone 10" : 6 "iPhone Case" : 10 "MacBook Pro" : 1 "iMac" : 2 }`
* **Resulting Value**: `"iPhone Case", "iPhone 10", "AirPods Pro"`

### Set to Tally Items Above Target Value

Create a set of strings using the items from a tally whose values are above a set threshold. For example, to track products that have been viewed more than 20 times, create a set of strings to capture the entries from a tally attribute that tracks the occurrences of viewed products.

**Attribute Name**: `Products Viewed 20+ Times`

* **Starting Value**: --
* **Enriched With**:  Items in "Products Viewed" that are greater than 20: <br>`{  "AirPods Pro" : 21,  "iPhone 10" : 35, "iPhone Case" : 12, "MacBook Pro" : 1 "iMac" : 2 }` 
* **Resulting Value**:  `"iPhone 10", "AirPods Pro"` 

### Remove Entry from Set of Strings

Remove an entry from a set of strings based on a set of conditions. For example, remove the entry "iPhone Case" from a set of strings that tracks a product wish list because it has been purchased.

**Attribute Name**: `Product Wish List`

* **Starting Value**:  `"iPhone 10", "AirPods Pro", "iPhone Case"`
* **Enriched With**:  Remove `purchased_product` (value "iPhone Case") 
* **Resulting Value**: `"iPhone 10", "AirPods Pro"`
