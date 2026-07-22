---
title: Rule Condition Definitions
description: This article lists the operators available when building conditions for audiences and rules.
url: https://docs.tealium.com/server-side/audiences/rule-conditions/
---

## Condition Operators


<blockquote>
Some operators apply only to certain attribute types, which is indicated in the **Applies to** column.
</blockquote>


|Operators| Description| Applies to|
|---| ---| ---|
|array contains|  An item in the array is an exact match to the value you specify.<br><br>**True**<br> `["iOS", "Android"]` array contains "Android" <br><br>**False**<br> `["Women's Clothing", "Shoes"]` array contains "Women" |  Array |
|array does not contain|  No item in the array is an exact match to the value you specify. <br><br>**True**<br> `["iOS", "Android"]` array does not contain "Samsung" <br><br>**False**<br> `["Women's Clothing", "Shoes"]` array does not contain "Shoes" |  Array |
|contains|  Attribute value includes the value you specify. <br><br>**True**<br> `"user@tealium.com"` contains "tealium"<br> `["iOS", "Android"]` array contains "Android" <br><br>**False**<br> `["Women's Clothing", "Shoes"]` array contains "Women" |  Array<br> String<br> Tally<br> Visitor ID |
| contains<br> (ignore case) | Attribute value includes the value you specify.|  String<br> Visitor ID |
|does not contain| Attribute value excludes the value you specify.|  Array<br> String<br> Visitor ID<br> Tally |
| does not contain<br> (ignore case) | Attribute value excludes the value you specify.|  Array<br> String<br> Visitor ID<br> Tally |
|contains partial string|  Attribute value partially matches the value you specify. <br><br>**True**<br> `["Women's Clothing", "Shoes"]` array contains "Women" <br><br>**False**<br> `["Women's Clothing", "Shoes"]` array contains "Tops" |  Array<br> Tally<br> Visitor ID |
| contains partial string<br> (ignore case) | Attribute value partially matches the value you specify, regardless of case.|  Array<br> Tally<br> Visitor ID |
|equals|  Attribute value matches the whole value you specify. <br><br>**True**<br> `"purchase"` equals "purchase"<br>  equals 0 <br><br>**False**<br> `"Luggage"` equals "luggage"<br>  equals 1 |  Number<br> String<br> Visitor ID |
| equals (ignore case) | Attribute value matches the whole value you specify.|  String<br> Visitor ID |
|does not equal| Attribute value does not match the whole value you specify.|  Number<br> String<br> Visitor ID |
| does not equal (ignore case) | Attribute value does not match the whole value you specify.|  String<br> Visitor ID |
|less than| Attribute value is less than the value you specify.|  Number<br> Date |
|less than or equal to| Attribute value is either less than or equal to the value you specify.|  Number<br> Date |
|greater than| Attribute value exceeds the value you specify.|  Number<br> Date |
|greater than or equal to| Attribute value either exceeds or equals the value you specify.|  Number<br> Date |
|is assigned|  Attribute exists, but may or may not have a value. <br><br>**True**<br> `"Shirts"` is assigned <br>`["iOS", "Android"]` is assigned<br> `[]` is assigned <br>`""` is assigned is assigned <br>`Is VIP` is assigned |  Number<br> Timeline<br> List<br> Badge<br> String<br> Tally<br> Visitor ID<br> Date |
|is not assigned| Attribute does not exist.|  Number<br> Timeline<br> List<br> Badge<br> String<br> Tally<br> Date<br> Visitor ID |
|is empty|  Tealium iQ variable does not contain any value (for example, value is undefined, null, or blank string). <br><br>**True**<br> `{ page_name : undefined }`<br> `{ page_name : null }`<br> `{ page_name : "" }`<br> `{ product_id : [] }` |  Imported from Tealium iQ Tag Management |
|is not empty|  Tealium iQ variable contains any value. For example, a string containing one or more characters, a number with a value (including `0`), or an array with one or more items. <br><br>**True**<br> `{ page_name : "Title" }`<br> `{ page_num : 1 }`<br> `{ product_id : ["WidgetXYZ"] }` |  Imported from Tealium iQ Tag Management |
|is true| Boolean value equals **True**.|  Boolean |
|is false| Boolean value equals **False**.|  Boolean |
|occurred less than| Date value is not yet past the number of minutes/hours/days/weeks/months you specify.|  Date |
|occurred more than|  Date value is past the number of minutes/hours/days/weeks/months you specify. |  Date |
|is started| Funnel is initiated for the visitor/visit.|  Funnel |
|is completed| Funnel has ended for the visitor/visit.|  Funnel |
|step completed| Step is successfully completed for the visitor/visit.|  Funnel |
|step not completed| Step is not completed for the visitor/visit.|  Funnel |
|is executed| Tag has successfully fired on the page.| Tags in your Tealium iQ Tag Management profile|
|matches regex|  Lets you use regular expressions (regex) in rules, enrichments, and audiences. For more information, see [Regular expressions](#regular-expressions)  |  String |

## Using the Extended Rule Condition for the Tally Attribute

You can create a rule condition to check if the key for a [Tally]() attribute contains a specific value using the `contains` operator.


<blockquote>
This extended rule condition is available only when using the `contains` operator.
</blockquote>


Follow these steps to include a Tally attribute key and its value in a rule:

1. Navigate to **Transform > Rules**.
1. Add a new rule or select an existing rule to edit.
1. Under **Conditions**, select the Tally attribute you want to check from the first drop-down list.
1. Select the **contains** operator in the next drop-down list.
1. In the third drop-down list, select **Custom Value**.
1. Enter the key-value that you expect in the Tally attribute.  
      ![](https://docs.tealium.com/images/server-side/tally-rule.png)

1. Click **Perform rule on value** and select the operator you want to use to evaluate the key you specified.
1. Specify the value you want to evaluate against the key. You can use an attribute or type in a custom value.
1. Click **Save**.

## Regular expressions

The `matches regex` operator is available only for string attributes. The condition returns `true` if any part of the string matches the regular expression (regex). 


<blockquote>
Enter a regular expression into the rule condition without slashes (`/`).For example, for the value `abc1234567890`, enter `^[a-z0-9]{13}$` to match the entire string.
</blockquote>


![](https://docs.tealium.com/images/server-side/audiences/regex_example_ui.png)

The `matches regex` operator has two options:

* **Multiline Mode**:  
Instead of matching `^` and `$` at only the beginning or end of the entire string, matches `^` and `$` at the beginning and end of any line within the string in the attribute value.
* **Case Insensitive**:  
Ignores letter case when comparing the string to the attribute value.

The following regular expressions illustrate return values for various common string qualifiers for the example value `abc1234567890`:

|Regex|Return Value|Description|
|-----|------------|-----------|
|`\d{3}`|`true`|No boundary qualifiers, matches anywhere within the string.|
|`^abc`|`true`|Start of string qualifier (`^`) matches at the start of the string.|
|`\d{3}$`|`true`|End of string qualifier (`$`) matches at the end of the string.|
|`^[a-z0-9]{13}$`|`true`|Start and end qualifier matches the entire string.|
|`^[a-zA-Z]{4}`|`false`|Start of string qualifier: does not match four consecutive uppercase or lowercase letters.|
|`[a-zA-Z]{4}$`|`false`|End of string qualifier: no letters at the end of the string.|
|`^[a-z0-9]{15}$`|`false`|Start and end qualifier: requires a value 15 characters long, which is not present.|





