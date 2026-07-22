---
title: Event attributes and enrichments reference
description: This article lists all event attributes with their enrichments and corresponding rule conditions.
url: https://docs.tealium.com/server-side/attributes/reference/event-attributes-and-enrichments-reference/
---
## How it works

This reference uses the following icons for attribute types:

|   |   |
| --- | --- |
|  [String](#string) |  [Array of Strings](#array-of-strings) |
|  [Number](#number) |   [Array of Numbers](#array-of-numbers)|
| [Boolean](#boolean) |   [Array of Booleans](#array-of-booleans)|
| [iQ Attribute](#iq-attribute-and-omnichannel-attribute) |  Custom Value|
| [Date](#date)|  [Omnichannel Date](#omnichannel-date)|
| In Experimental Mode|  Visitor ID|
| Omnichannel Attribute|  Event Level Attribute|

## String

* Event-level attribute
* Can be used in a webhook
* Example: `A String`
* For more information, see [String Attribute](https://docs.tealium.com/string-attribute/).

#### Enrichments

|Enrichment| Source Values|
|---| ---|
|Set string|  ![](https://docs.tealium.com/images/server-side/untitled-drawing-(1).png) |
|Split (assign to randomly distributed values)| |
|Remove|
|Lowercase|
|Join with delimiter|  ![](https://docs.tealium.com/images/server-side/untitled-drawing-(1).png) |
|Set string to date|   ![](https://docs.tealium.com/images/server-side/untitled-drawing-(1).png)|

#### Rule Conditions

|Rule Conditions| Source Values|
|---| ---|
|Contains<br> Contains [ignore case]<br> Does not contain<br> Does not contain [ignore case]|    ![](https://docs.tealium.com/images/server-side/untitled-drawing-(1).png) |
|Equals <br> Equals [ignore case]<br> Does not equal<br> Does not equal [ignore case]|    ![](https://docs.tealium.com/images/server-side/untitled-drawing-(1).png) |
|Starts/ends with<br> Starts/ends with [ignore case]|    ![](https://docs.tealium.com/images/server-side/untitled-drawing-(1).png) |
|Is assigned<br> Is not assigned|
|Matches regex| |

## Array of Strings

* Event-level attribute
* Can be used in a webhook
* Example: `["Hello", "", "Mark"]` (empty string will be stored in place)
* For more information, see [Attribute Data Type: Arrays]().

#### Enrichments

|Enrichment| Source Values|
|---| ---|
|Add String to array|  ![](https://docs.tealium.com/images/server-side/untitled-drawing-(1).png) |
|Add an array of strings| ![](https://docs.tealium.com/images/server-side/untitled-drawing-(1).png)|
|Set to difference between two other Arrays| ![](https://docs.tealium.com/images/server-side/untitled-drawing-(1).png)|
|Reset (remove all values)|
|Lowercase all entries|
|Remove first/last/all entries of|  ![](https://docs.tealium.com/images/server-side/untitled-drawing-(1).png)|

#### Rule Conditions

|Rule Conditions| Source Values|
|---| ---|
|Contains [partial string] <br> Contains [partial string] [ignore case]|      ![](https://docs.tealium.com/images/server-side/untitled-drawing-(1).png) |
|Does not contain (key) <br> Does not contain (key) [ignore case]|     ![](https://docs.tealium.com/images/server-side/untitled-drawing-(1).png) |
|Starts/ends with<br> Starts/ends with [ignore case]|     ![](https://docs.tealium.com/images/server-side/untitled-drawing-(1).png) |

## Number

* Event-level attribute
* Can be used in a webhook
* Example: `1.001`, or `1001`, but not `1,001`
* Numbers can be decimals or integers. Integers round up or down to the nearest whole number. (In experimental mode)
* For more information, see [Number Attribute]().

#### Enrichments

|Enrichment| Source Values|
|---| ---|
|Increment/Decrement| ![](https://docs.tealium.com/images/server-side/untitled-drawing-(1).png)|
|Ratio/Product/Difference/Sum| ![](https://docs.tealium.com/images/server-side/untitled-drawing-(1).png)|
|Set Number| ![](https://docs.tealium.com/images/server-side/untitled-drawing-(1).png)|
|Aggregate of array of numbers (Average, Minimum, Maximum)| |
|Set to number of Items in array| |

#### Rule Conditions

|Rule Conditions| Source Values|
|---| ---|
|Equals<br> Does not equal| ![](https://docs.tealium.com/images/server-side/untitled-drawing-(1).png)|
|Is assigned<br> Is not assigned|
|Greater than or equal to<br> Less than or equal to|  ![](https://docs.tealium.com/images/server-side/untitled-drawing-(1).png) |

## Array of Numbers

* Event-level attribute
* Can be used in a webhook
* Example: `["1", "", "3", "4"]` will output `[1, 0, 3, 4]`
* For more information, see [Attribute Data Type: Arrays]().

#### Enrichments

|Enrichment| Source Values|
|---| ---|
|Add Number to array| ![](https://docs.tealium.com/images/server-side/untitled-drawing-(1).png)|
|Add an array of numbers| ![](https://docs.tealium.com/images/server-side/untitled-drawing-(1).png)|
|Set to difference between two other arrays| ![](https://docs.tealium.com/images/server-side/untitled-drawing-(1).png)|
|Reset (remove all values)|

#### Rule Conditions

|Rule Conditions| Source Values|
|---| ---|
|Is assigned<br> Is not assigned| ![](https://docs.tealium.com/images/server-side/untitled-drawing-(1).png)|
|Contains number| ![](https://docs.tealium.com/images/server-side/untitled-drawing-(1).png)|

## Boolean

* Event-level attribute
* Can be used in a webhook
* Example: `true`
* For more information, see [Boolean Attribute]().

#### Enrichments

|Enrichment| Source Values|
|---| ---|
|Set to true/false|

#### Rule Conditions

|Rule Conditions| Source Values|
|---| ---|
|Is true/false|

## Array of Booleans

* Event-level attribute
* Can be used in a webhook
* Example: `[true, false, true]` (no quotes)
* For more information, see [Attribute Data Type: Arrays]().

#### Enrichments

|Enrichment| Source Values|
|---| ---|
|Add a boolean|  ![](https://docs.tealium.com/images/server-side/untitled-drawing-(1).png) |
|Add an array of booleans| ![](https://docs.tealium.com/images/server-side/untitled-drawing-(1).png)|
|Reset (remove all values)|

#### Rule Conditions

|Rule Conditions|
|---|
|Contains boolean<br> Contains only boolean|  |
|Is assigned<br> Is not assigned|  |

## Date

* Event-level attribute
* Can be used in a webhook
* Control the input format by using the "Convert From Date Format" enrichment. For example, if this enrichment is set to `ddMMYY`, pass `31122020` for December 31, 2020 as input.
* For more information, see [Date Attribute]().

#### Enrichments

|Enrichment| Source Values|
|---| ---|
|Convert from Date Format<br> (Set expected date format for event variable input.)|
|Set to current date|
|Set date<br> (Use "xxx" for date format.)| |
|Set date based on date format from | ![](https://docs.tealium.com/images/server-side/untitled-drawing-(1).png)|
|Set date based on epoch milliseconds.<br> (Use "xxx" for date format.)| ![](https://docs.tealium.com/images/server-side/untitled-drawing-(1).png) |

#### Rule Conditions

|Rule Conditions| Source Values|
|---| ---|
|Greater than or equal to<br> Less than or equal to<br> (You can compare with the current time either directly or with future or past timeframe in seconds, minutes, hours, days, weeks or months.)| |
|Is assigned<br> Is not assigned|

## iQ Attribute and Omnichannel Attribute

* Event-level attribute
* Can be used in a webhook
* Any data format
* For more information about omnichannel attributes, see [Attributes: Offline Data (Omnichannel)](https://docs.tealium.com/audiencestream-attributes-offline-data-omnichannel/).

#### Rule Conditions

|Rule Conditions|
|---|
|Contains<br> Contains [ignore case]<br> Does not contain<br> Does not contain [ignore case]|    ![](https://docs.tealium.com/images/server-side/untitled-drawing-(1).png) |
|Array does contain<br> Array does not contain|    ![](https://docs.tealium.com/images/server-side/untitled-drawing-(1).png) |
|Equals <br> Equals [ignore case]<br> Does not equal<br> Does not equal [ignore case]|    ![](https://docs.tealium.com/images/server-side/untitled-drawing-(1).png) |
|Starts/ends with<br> Starts/ends with [ignore case]|    ![](https://docs.tealium.com/images/server-side/untitled-drawing-(1).png) |
|Less than | Greater than or equal to|    ![](https://docs.tealium.com/images/server-side/untitled-drawing-(1).png) |
|Is assigned<br> Is not assigned|
|Is empty<br> Is not empty|

## Omnichannel Date

* Event-level attribute
* Can be used in a webhook
* Uses the Java Simple Date Format
* For more information about omnichannel attributes, see [Attributes: Offline Data (Omnichannel)](https://docs.tealium.com/audiencestream-attributes-offline-data-omnichannel/).

#### Rule Conditions

|Rule Conditions| Source Values|
|---| ---|
|Greater than or equal to<br> Less than or equal to| |
|Is assigned<br> Is not assigned|
|Occurred more/less than X minutes, hours, days, weeks, months ago| |
