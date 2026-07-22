---
title: Array of strings
description: This article describes how to use the data types array of strings, array of numbers, and array of booleans.
url: https://docs.tealium.com/server-side/attributes/data-types/arrays/arrays/
---
## Enrichments

The array of strings attribute stores a list of text values.

The array of strings is available in the following scopes: Event, Visit, Visitor.

![](https://docs.tealium.com/images/server-side/screenshot-2019-11-11-at-1.24.29-pm.png)

### Add a string

This enrichment adds the value of a string attribute to the array. The added attribute can only be a string, iQ variable, or omnichannel attribute.

**Attribute Name**: `product_name`

* **Starting value**: `["Pants"]`
* **Enriched With**: `"Shirts"` 
* **Resulting value**: `["Pants", "Shirts"]` 

### Add an array of strings

This enrichment adds all the values from another array to the array. The added attribute can only be an array of strings or an iQ variable.

**Attribute Name**: `product_name`

* **Starting value**: `["Pants"]`
* **Enriched With**: `["Shirts", "Shoes"]`
* **Resulting value**: `["Pants", "Shirts", "Shoes"]`

### Difference between two arrays

This enrichment takes two arrays as input, and returns a new array containing all values found in the first array but not the second. In this example, values from `Wishlist Products` that do not also occur in `Purchased Products` are added to the resulting array.

**Attribute Name**: ` Unpurchased Products`

* **Starting value**: `[]`
* **Enriched With**:  
Difference between: Wishlist Products  `["Pants", "Shirt", "Shoes", "Belt"]` and Purchased Products `["Pants", "Shirt"]` 
* **Resulting value**: `["Shoes", "Belt"]`

This example shows that the resulting attribute value is replaced, not appended to and that repeated values in the first array are removed.

* **Starting value**: `[7, 8, 9]`
* **Enriched With**:  Difference between: Some Numbers `[1, 3, 1, 2, 3]` and Some Other Numbers `[3]` 
* **Resulting value**: `[1, 1, 2]`

### Reset

This enrichment removes all values from the array.

**Attribute Name**: `product_name`

* **Starting value**: `["Shoes", "Belt"]`
* **Enriched With**:
* **Resulting value**: (Removed)

### Lowercase

This enrichment lowercases every value in the array.

**Attribute Name**: `product_name`

* **Starting value**: `["Shoes", "BELT"]`
* **Enriched With**:
* **Resulting value**: `["shoes", "belt"]`

### Set to set of strings

Sets an array of strings to a set of strings. This enrichment replaces all values in the array.

**Attribute Name**: `Active Browser Types`

* **Starting value**: `["IE"]`
* **Enriched With**: `["Chrome" "FireFox", "Opera"]`
* **Resulting value**: `["Chrome" "FireFox", "Opera"]`

### Add a set of strings

Adds a set of strings to a string array. This enrichment preserves the existing values in the array, therefore there can be duplicate items in the resulting value.

**Attribute Name**: `product_name`

* **Starting value**: `["Pants"]`
* **Enriched With**: `["Pants", "Shoes", "Ties"]`
* **Resulting value**: `["Pants", "Pants", "Shoes", "Ties"]`

### Remove a string from the array

Specify a first, last, or all instances of a string to remove. This enrichment removes from an array every instance of the item selected for removal.

**Attribute Name**: `product_name`

* **Starting value**: `["Pants", "Pants", "Shoes", "Ties"]`
* **Enriched With**: `"Pants"`
* **Resulting value**: `["Shoes", "Ties"]`
