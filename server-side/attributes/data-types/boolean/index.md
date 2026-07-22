---
title: Boolean Attribute
description: This article explains how to use the boolean attribute data type. Booleans are used to store true or false values.
url: https://docs.tealium.com/server-side/attributes/data-types/boolean/
---
## How it works

A boolean attribute is used to store the true or false value of a condition. For example, a boolean can store whether or not a visitor had added items to their cart or visited a specific section of site.

The boolean attribute is available in the following scopes: Event, Visit, Visitor.

![](https://docs.tealium.com/images/server-side/attribute-scopes-table-all.png)

### Size Limits

The size of a each boolean is not limited, but these attributes are still limited by the maximum size of the profile after encryption and compression (400 KB).

## Enrichments

### Set boolean

Use this enrichment to set the boolean attribute to true or false.

This example shows how to know if a visitor has added an item to his/her cart using a boolean attribute named "Did Add to Cart". Initialize the attribute by setting it to false at the beginning of each visit, then set it to true whenever the `cart_add` event occurs.

Create two enrichments to achieve this:

```
Set to: false
WHEN: New Visit
```

```
Set to: true
WHEN: Any event
Rule: tealium_event equals "cart_add"
```

**Attribute Name:** Did Add to Cart

* **Starting Value**: `""`
* **Enriched With**: `true`
* **Resulting Value** `true`
