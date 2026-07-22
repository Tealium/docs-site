---
title: String Attribute
description: Use string attributes to store text values.
url: https://docs.tealium.com/server-side/attributes/data-types/string/
---
## How it works

Strings are used for customer information such as First Name and Postal Code, order information such as Order ID and Shipping Method, or site information such as Site Section or Site Language.

The string attribute is available in the following scopes: Event, Visit, Visitor.

![](https://docs.tealium.com/images/server-side/attribute-scopes-table-all.png)

### Size limits

EventStream string attributes have a maximum length of 1,500 characters. Strings are truncated to 1,500 characters if they exceed this limit.

AudienceStream string attributes values have a maximum length of 1,000 characters. If an enrichment results in a string larger than 1,000 characters, the value is not saved.

String attributes are also limited by the maximum size of the profile after encryption and compression (400 KB).

## Enrichments

The following enrichments are available to string attributes.

### Set string

This enrichment sets the value of a string attribute, either from a constant value you provide or from the value of another string attribute. The source values can only be a string, iQ variable, or Omnichannel attribute.

**Attribute Name**: `customer_type`

* **Starting Value**: `""`
* **Enriched With**: `"unknown"`
* **Resulting Value**: `"unknown"`

### Split string

This enrichment lets you set multiple values based on a distribution percentage. Each value you set also has a percentage setting. There can be multiple value/percentage entries, but the distribution must total 100%. The distribution is based on a random number generator, so smaller samples might not match the distribution, but as more values are assigned the distribution ratio will become more accurate. The source values can only be a string, iQ variable, or Omnichannel attribute.

In this example an attribute named `test_group` is used to segment users into two equal groups (50/50), one named "GroupA" and the other "GroupB". This attribute can then be used to identify activity associated with each group.

**Attribute Name**: `test_group`

* **Starting Value**: `""`
* **Resulting Value**: Set string's value to `"GroupA"` for `50%` of string population<br> Set string's value to `"GroupB"` for `50%` of string populartion

See also: [Enrichment Example: Split String](https://support.tealiumiq.com/en/support/solutions/articles/36000363487-enrichment-example-split-string)

### Remove string

This enrichment removes the entire value from the attribute.

* **Starting Value**: `"Jane Smith"`
* **Resulting Value**: (Removed)

### Lowercase string

This enrichment will lowercase the current value of the string attribute.

**Attribute Name**: `email_address`

* **Starting Value**: `"First.Last@Example.com"`
* **Resulting Value**: `"first.last@example.com"`

### Join attributes

This enrichment joins multiple values with a delimiter to form a single text value. The delimiter can be one or more characters. For example, you could create a page hierarchy value by combining `site_section`, `page_category`, and other page level attributes.

**Attribute Name**: `page_path`

* **Starting Value**: `""`
* **Enriched With**:  
Attribute 1: `site_region="en-us"`  
Attribute 2: `site_section="Electronics"`  
Attribute 3: `category_name="Tablets"`  
Delimiter: `":"`
* **Resulting Value**: `"en-us:Electronics:Tablets"`

### Set string to date

This enrichment converts a date value to a string and allows for custom formatting. The source values can be a date, string, iQ variable, or file import attribute. For more information about the date formatter, see [Date attribute](https://docs.tealium.com/date-attribute/#date-formatter))

**Attribute Name**: `last_purchase_date`

* **Starting Value**: `""`
* **Enriched With**: Last Login Date with format `"yyy-MM-dd"`
* **Resulting Value**: `"2019-12-31"`
