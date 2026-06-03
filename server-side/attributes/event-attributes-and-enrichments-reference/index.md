---
title: Event attributes and enrichments reference
description: This article lists all event attributes with their enrichments and corresponding rule conditions.
url: https://docs.tealium.com/server-side/attributes/event-attributes-and-enrichments-reference/
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
* For more information, see [String Attribute]().

#### Enrichments

|Enrichment| Source Values|
|---| ---|
|Set string|  ![](/images/server-side/untitled-drawing-(1).png) |
|Split (assign to randomly distributed values)| |
|Remove|
|Lowercase|
|Join with delimiter|  ![](/images/server-side/untitled-drawing-(1).png) |
|Set string to date|   ![](/images/server-side/untitled-drawing-(1).png)|

#### Rule Conditions

|Rule Conditions| Source Values|
|---| ---|
|Contains&lt;br&gt; Contains [ignore case]&lt;br&gt; Does not contain&lt;br&gt; Does not contain [ignore case]|    ![](/images/server-side/untitled-drawing-(1).png) |
|Equals &lt;br&gt; Equals [ignore case]&lt;br&gt; Does not equal&lt;br&gt; Does not equal [ignore case]|    ![](/images/server-side/untitled-drawing-(1).png) |
|Starts/ends with&lt;br&gt; Starts/ends with [ignore case]|    ![](/images/server-side/untitled-drawing-(1).png) |
|Is assigned&lt;br&gt; Is not assigned|
|Matches regex| |

## Array of Strings

* Event-level attribute
* Can be used in a webhook
* Example: `[&#34;Hello&#34;, &#34;&#34;, &#34;Mark&#34;]` (empty string will be stored in place)
* For more information, see [Attribute Data Type: Arrays]().

#### Enrichments

|Enrichment| Source Values|
|---| ---|
|Add String to array|  ![](/images/server-side/untitled-drawing-(1).png) |
|Add an array of strings| ![](/images/server-side/untitled-drawing-(1).png)|
|Set to difference between two other Arrays| ![](/images/server-side/untitled-drawing-(1).png)|
|Reset (remove all values)|
|Lowercase all entries|
|Remove first/last/all entries of|  ![](/images/server-side/untitled-drawing-(1).png)|

#### Rule Conditions

|Rule Conditions| Source Values|
|---| ---|
|Contains [partial string] &lt;br&gt; Contains [partial string] [ignore case]|      ![](/images/server-side/untitled-drawing-(1).png) |
|Does not contain (key) &lt;br&gt; Does not contain (key) [ignore case]|     ![](/images/server-side/untitled-drawing-(1).png) |
|Starts/ends with&lt;br&gt; Starts/ends with [ignore case]|     ![](/images/server-side/untitled-drawing-(1).png) |

## Number

* Event-level attribute
* Can be used in a webhook
* Example: `1.001`, or `1001`, but not `1,001`
* Numbers can be decimals or integers. Integers round up or down to the nearest whole number. (In experimental mode)
* For more information, see [Number Attribute]().

#### Enrichments

|Enrichment| Source Values|
|---| ---|
|Increment/Decrement| ![](/images/server-side/untitled-drawing-(1).png)|
|Ratio/Product/Difference/Sum| ![](/images/server-side/untitled-drawing-(1).png)|
|Set Number| ![](/images/server-side/untitled-drawing-(1).png)|
|Aggregate of array of numbers (Average, Minimum, Maximum)| |
|Set to number of Items in array| |

#### Rule Conditions

|Rule Conditions| Source Values|
|---| ---|
|Equals&lt;br&gt; Does not equal| ![](/images/server-side/untitled-drawing-(1).png)|
|Is assigned&lt;br&gt; Is not assigned|
|Greater than or equal to&lt;br&gt; Less than or equal to|  ![](/images/server-side/untitled-drawing-(1).png) |

## Array of Numbers

* Event-level attribute
* Can be used in a webhook
* Example: `[&#34;1&#34;, &#34;&#34;, &#34;3&#34;, &#34;4&#34;]` will output `[1, 0, 3, 4]`
* For more information, see [Attribute Data Type: Arrays]().

#### Enrichments

|Enrichment| Source Values|
|---| ---|
|Add Number to array| ![](/images/server-side/untitled-drawing-(1).png)|
|Add an array of numbers| ![](/images/server-side/untitled-drawing-(1).png)|
|Set to difference between two other arrays| ![](/images/server-side/untitled-drawing-(1).png)|
|Reset (remove all values)|

#### Rule Conditions

|Rule Conditions| Source Values|
|---| ---|
|Is assigned&lt;br&gt; Is not assigned| ![](/images/server-side/untitled-drawing-(1).png)|
|Contains number| ![](/images/server-side/untitled-drawing-(1).png)|

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
|Add a boolean|  ![](/images/server-side/untitled-drawing-(1).png) |
|Add an array of booleans| ![](/images/server-side/untitled-drawing-(1).png)|
|Reset (remove all values)|

#### Rule Conditions

|Rule Conditions|
|---|
|Contains boolean&lt;br&gt; Contains only boolean|  |
|Is assigned&lt;br&gt; Is not assigned|  |

## Date

* Event-level attribute
* Can be used in a webhook
* Control the input format by using the &#34;Convert From Date Format&#34; enrichment. For example, if this enrichment is set to `ddMMYY`, pass `31122020` for December 31, 2020 as input.
* For more information, see [Date Attribute]().

#### Enrichments

|Enrichment| Source Values|
|---| ---|
|Convert from Date Format&lt;br&gt; (Set expected date format for event variable input.)|
|Set to current date|
|Set date&lt;br&gt; (Use &#34;xxx&#34; for date format.)| |
|Set date based on date format from | ![](/images/server-side/untitled-drawing-(1).png)|
|Set date based on epoch milliseconds.&lt;br&gt; (Use &#34;xxx&#34; for date format.)| ![](/images/server-side/untitled-drawing-(1).png) |

#### Rule Conditions

|Rule Conditions| Source Values|
|---| ---|
|Greater than or equal to&lt;br&gt; Less than or equal to&lt;br&gt; (You can compare with the current time either directly or with future or past timeframe in seconds, minutes, hours, days, weeks or months.)| |
|Is assigned&lt;br&gt; Is not assigned|

## iQ Attribute and Omnichannel Attribute

* Event-level attribute
* Can be used in a webhook
* Any data format
* For more information about omnichannel attributes, see [Attributes: Offline Data (Omnichannel)]().

#### Rule Conditions

|Rule Conditions|
|---|
|Contains&lt;br&gt; Contains [ignore case]&lt;br&gt; Does not contain&lt;br&gt; Does not contain [ignore case]|    ![](/images/server-side/untitled-drawing-(1).png) |
|Array does contain&lt;br&gt; Array does not contain|    ![](/images/server-side/untitled-drawing-(1).png) |
|Equals &lt;br&gt; Equals [ignore case]&lt;br&gt; Does not equal&lt;br&gt; Does not equal [ignore case]|    ![](/images/server-side/untitled-drawing-(1).png) |
|Starts/ends with&lt;br&gt; Starts/ends with [ignore case]|    ![](/images/server-side/untitled-drawing-(1).png) |
|Less than | Greater than or equal to|    ![](/images/server-side/untitled-drawing-(1).png) |
|Is assigned&lt;br&gt; Is not assigned|
|Is empty&lt;br&gt; Is not empty|

## Omnichannel Date

* Event-level attribute
* Can be used in a webhook
* Uses the Java Simple Date Format
* For more information about omnichannel attributes, see [Attributes: Offline Data (Omnichannel)]().

#### Rule Conditions

|Rule Conditions| Source Values|
|---| ---|
|Greater than or equal to&lt;br&gt; Less than or equal to| |
|Is assigned&lt;br&gt; Is not assigned|
|Occurred more/less than X minutes, hours, days, weeks, months ago| |
