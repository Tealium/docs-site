---
title: Usage examples
url: https://docs.tealium.com/server-side/attributes/enrichments/usage-examples/
---
## Increment or decrement number – "Lifetime Order Total (LTV)"

This enrichment can modify a number with a positive value (increment) or a negative value (decrement). This value can come from another attribute or be set as a static number.

* **Attribute:** Lifetime Value (LTV)
* **Scope:** Visitor
* **Data Type:** Number

Knowing the amount spent across all orders from a visitor is a valuable piece of information. This data can be used for many purposes, such as to offer promotional deals or to assign a badge to visitors whose spending exceeds a certain threshold. Since the value of this attribute will persist for the lifetime of the visitor, it will be visitor-scoped.

This enrichment has the following requirements:

* An event attribute to identify when a purchase is made, for example: `"tealium_event": "purchase"`.
* An event attribute for the dollar amount of the purchase, for example: `"order_total": "123.45"`.

To configure this enrichment:

1. Create a visitor attribute with the number data type, titled "Lifetime Order Total (LTV)"
1. Add the "Increment or Decrement Number" enrichment
1. Select **order_total** from the drop-down list.
1. Select **Any Event** from the WHEN drop-down list.
1. Create a new rule titled "Order Thank You Page" with the following condition:

[
  [
    {
      "input": "tealium_event",
      "operator": "equals",
      "filter": "purchase"
    }
  ]  
]


## Set difference between two dates – "Days Since Last Purchase"

This enrichment calculates the elapsed time between two events and stores the numeric value in one of the following units: minutes, hours, days, weeks, or months.

* **Attribute:** Days Since Last Purchase
* **Scope:** Visitor
* **Data Type:** Number

This enrichment will calculate the number of days since a visitor made a purchase. The resulting value is always a positive number.

This enrichment has the following requirements:

* An event attribute to identify when a purchase is made, for example: `tealium_event="purchase"`.
* A visitor attribute to capture the date of a purchase event.

To configure this enrichment:

1. Create a visitor attribute with the number data type titled "Last Purchase Date".
1. Select **Any Event** from the WHEN drop-down list.
1. Create a new rule (if it doesn't already exist) titled "Order Thank You Page" with the following condition:

[
  [
    {
      "input": "tealium_event",
      "operator": "equals",
      "filter": "purchase"
    }
  ]  
]

1. Create a visitor attribute with the number data type titled `Days Since Last Purchase`.
1. Add the Set Difference Between Two Dates enrichment.
1. Set the two dates to: "Visit start" (built-in attribute) and "Last Purchase Date".
1. Set the units to "Days".
1. Select **New Visit** from the WHEN drop-down list.

## Split string (A/B Testing – "Split Test Group"

This enrichment defines visitor group names and assigns them to an attribute based on a percentage distribution. The names (or values) of your segments can come from another string attribute or from a custom value. This enrichment is helpful in running A/B tests or targeting groups of users.

The group distributions are calculated based on a random number generator. The enrichment does not monitor the current ratio of segments prior to assigning a value, so for smaller samples you may see ratios that do not exactly match the percentages you set. However, as the number of assignments increases, the ratio of assignments will gradually match the percentages you set.

For example, if you set up three segments with distributions of 50%, 30%, and 20%, within a small sample set you might see ratios of 48%, 34%, and 18%. However, as more visitors get assigned into the segments, the ratio values will approach the expected values.

* **Attribute:** Split Test Group
* **Scope:** Visit/Visitor
* **Data Type:** String

To test a new campaign on a small segment of your visitors, presumably before rolling it out for all visitors, you use the split string enrichments to assign a small percentage of your visitors into the "Action" group. This identified segment of visitors can then be built into an audience for which you can take actions.

For this example we will create the following distribution of segments:

* 85% – "Control": The control group that will not be part of the test.
* 15% – "Variation1": The group to be included in the test.

To configure this enrichment:

1. Create a string visit attribute named `Split Test Group`.
1. Add the **Split String** enrichment.
1. For each group, set a name and a percent.
1. Select **New Visit** from the WHEN drop-down list.

Now you can use this attribute in a rule to include the relevant visitors in an audience. The rule logic might be:

[
  [
    {
      "input": "Split Test Group",
      "operator": "equals",
      "filter": "Variation1"
    }
  ]  
]


## Store array as set of strings – "Purchase Categories"

The **Store Array as Set of String** enrichment saves the values from an array of strings attribute into a set of strings attribute. This enrichment will not create a perpetual set. Meaning, you cannot append to a set of string using this enrichment, it will always overwrite the value. To preserve a set of strings and append new values you must use the **Update Set of String By Set of Strings** enrichment.

* **Attribute:** Purchase Categories
* **Scope:** Visit
* **Data Type:** Set of Strings

Starting with an event attribute of the data type array of strings called `product_category`, populated on purchase events to contain the category names of the products purchased. To store this as a Visitor/Visit attribute called "Purchase Categories", it must be converted to a set of strings. Then, on each purchase event, the `product_category` values get appended to the `Product Categories Purchased` attribute through enrichments.

| array of strings (product_category) | Set of Strings (Product Category Purchased) |
| --- | --- |
|`["Pants", "Shirts"]`| `"Pants", "Shirts"`|
|`["Boots", "Belts", "Belts"]`| `"Boots", "Belts"`|

## Update set of strings by set of strings – "Lifetime Purchase Categories"

This enrichment appends the values from one set of strings attribute into another set of strings attribute. This lets you store the values that occur in one set (and that change from event to event) into a second set that persists for the life of the visitor.

In this table `Set A` is overwritten with new values for each event and the enrichment is copying those values into `Set B` where the master list grows.

We recommend pairing this enrichment with **Store Array as Set of Strings** enrichment so that the resulting set can be preserved before it is overwritten by incoming values.

| Set A (Event) | Set B (Visitor) |
| --- | --- |
|`"Pants", "Shirts"`| `"Pants", "Shirts"`|
|`"Shoes", "Pants"`| `"Pants", "Shirts", "Shoes"`|
|`"Shirts", "Shirts", "Watches"`| `"Pants", "Shirts", "Shoes", "Watches"`|

* **Attribute:** Lifetime Purchase Categories
* **Scope:** Visitor
* **Data Type:** Set of Strings

To maintain an accumulated set of product categories purchased from you will have one event array of strings attribute and two visit and visitor set of strings attributes: one to capture the views as they happen and one to capture all historical views.

This enrichment has the following requirements:

* An event attribute to identify when a purchase is made. For example, `tealium_event="purchase"`
* An array of strings event attribute to identify product categories during a purchase, for example: `"product_category": ["Boots", "Belts"]`.
* A set of strings visit attribute to capture product categories purchased for the visit.
* A set of strings visitor attribute to capture all product categories purchased.

To configure this enrichment:

1. Create an event attribute with the array of strings data type named `product_category`.
1. Create a set of strings visit attribute named `Product Category Purchased`.
      * Add the **Store Array as Set of Strings** enrichment.
      * Select the attribute `product_category`.
      * Set the **WHEN** to `Any Event`.
      * Set the rule to the `Purchase Event`.

1. Create a set of strings visitor attribute named `Lifetime Product Category Purchased`.
      * Add the **Update Set of Strings by Set of Strings** enrichment.
      * Select the attribute `Product Category Purchased`.
      * Set the *WHEN* to `Visit Ended`.

## Set rolling average based on timeline – "90-Day Order Average"

This enrichment calculates the rolling average (arithmetic mean) of numeric values captured in a timeline attribute.

This example uses a "90-Day Orders" timeline to capture order total values over the last 90 days. As the timeline progresses, entries falling outside the expiration window are discarded and the final rolling average is recalculated with the set of valid entries.


<blockquote>
This example also applies to the **Set Rolling Sum Based on Timeline** enrichment.
</blockquote>


The table below illustrates a timeline of entries (assume today is March 25). All entries, including the entry on Jan 1, are included in the arithmetic mean.

**timeline Attribute: "90-Day Orders"**

|**Valid Entries**| **Order Total ($)**|
| --- | --- |
|Jan 1| 10.00|
|Feb 15| 20.00|
|Mar 25| 30.00|

**Rolling Average** is (10.00 + 20.00 + 30.00) ÷ 3 = 20.00

A few weeks later, the Jan 1 entry is discarded because it falls outside the 90 day expiration and the rolling average is recalculated for the valid entries. Notice how the resulting average changes when an expired entry is excluded from the aggregate.

**timeline Attribute: "90-Day Orders"**

|**Expired Entries**| **Order Total (in $)**|
| --- | --- |
|Jan 1| 10.00|

|**Valid Entries**| **Order Total (in $)**|
| --- | --- |
|Feb 15| 20.00|
|Mar 25| 30.00|
|Apr 10| 40.00|

**Rolling Average** is (20.00 + 30.00 + 40.00) ÷ 3 = 30.00 

* **Attribute:** 90-Day Order Average
* **Scope:** Visitor
* **Data Type:** Number

Starting with a timeline attribute to capture order totals from the **last 90 days**, you will create a new visitor attribute using the **Rolling Average** enrichment to store average the order totals.

This enrichment has the following requirements:

* An event string attribute to identify when a purchase is made, for example: `tealium_event: "purchase"`.
* An event number attribute for the dollar amount of the purchase, for example: `order_total: "123.45"`.
* A visitor timeline attribute to capture order totals for 90 days.
* An visitor number attribute to capture the average of order totals.

To configure this enrichment:

1. Create a visitor timeline attribute named `90-Day Order timeline`.
1. Click **Create An Entry > Set Expiration** and set it to "90 days".
1. Click **Create An Entry > Update timeline** and set the following:
      * **Record**: Time of event received
      * **Capture data**: `order_total`
      * **WHEN**: Any Event
      * **Rule**: tealium_event EQUALS "purchase"

1. Create a visitor number attribute named `90-Day Order Average`
1. Add the **Set Rolling Average Based On timeline** enrichment with `order_total` and **90-Day Order timeline** selected.
