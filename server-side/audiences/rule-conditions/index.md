---
title: Rule Condition Definitions
description: This article lists the operators available when building conditions for audiences and rules.
url: https://docs.tealium.com/server-side/audiences/rule-conditions/
---

## Condition Operators

Some operators apply only to certain attribute types, which is indicated in the **Applies to** column.

|Operators| Description| Applies to|
|---| ---| ---|
|array contains|  An item in the array is an exact match to the value you specify.&lt;br&gt;&lt;br&gt;**True**&lt;br&gt; `[&#34;iOS&#34;, &#34;Android&#34;]` array contains &#34;Android&#34; &lt;br&gt;&lt;br&gt;**False**&lt;br&gt; `[&#34;Women&#39;s Clothing&#34;, &#34;Shoes&#34;]` array contains &#34;Women&#34; |  Array |
|array does not contain|  No item in the array is an exact match to the value you specify. &lt;br&gt;&lt;br&gt;**True**&lt;br&gt; `[&#34;iOS&#34;, &#34;Android&#34;]` array does not contain &#34;Samsung&#34; &lt;br&gt;&lt;br&gt;**False**&lt;br&gt; `[&#34;Women&#39;s Clothing&#34;, &#34;Shoes&#34;]` array does not contain &#34;Shoes&#34; |  Array |
|contains|  Attribute value includes the value you specify. &lt;br&gt;&lt;br&gt;**True**&lt;br&gt; `&#34;user@tealium.com&#34;` contains &#34;tealium&#34;&lt;br&gt; `[&#34;iOS&#34;, &#34;Android&#34;]` array contains &#34;Android&#34; &lt;br&gt;&lt;br&gt;**False**&lt;br&gt; `[&#34;Women&#39;s Clothing&#34;, &#34;Shoes&#34;]` array contains &#34;Women&#34; |  Array&lt;br&gt; String&lt;br&gt; Tally&lt;br&gt; Visitor ID |
| contains&lt;br&gt; (ignore case) | Attribute value includes the value you specify.|  String&lt;br&gt; Visitor ID |
|does not contain| Attribute value excludes the value you specify.|  Array&lt;br&gt; String&lt;br&gt; Visitor ID&lt;br&gt; Tally |
| does not contain&lt;br&gt; (ignore case) | Attribute value excludes the value you specify.|  Array&lt;br&gt; String&lt;br&gt; Visitor ID&lt;br&gt; Tally |
|contains partial string|  Attribute value partially matches the value you specify. &lt;br&gt;&lt;br&gt;**True**&lt;br&gt; `[&#34;Women&#39;s Clothing&#34;, &#34;Shoes&#34;]` array contains &#34;Women&#34; &lt;br&gt;&lt;br&gt;**False**&lt;br&gt; `[&#34;Women&#39;s Clothing&#34;, &#34;Shoes&#34;]` array contains &#34;Tops&#34; |  Array&lt;br&gt; Tally&lt;br&gt; Visitor ID |
| contains partial string&lt;br&gt; (ignore case) | Attribute value partially matches the value you specify, regardless of case.|  Array&lt;br&gt; Tally&lt;br&gt; Visitor ID |
|equals|  Attribute value matches the whole value you specify. &lt;br&gt;&lt;br&gt;**True**&lt;br&gt; `&#34;purchase&#34;` equals &#34;purchase&#34;&lt;br&gt;  equals 0 &lt;br&gt;&lt;br&gt;**False**&lt;br&gt; `&#34;Luggage&#34;` equals &#34;luggage&#34;&lt;br&gt;  equals 1 |  Number&lt;br&gt; String&lt;br&gt; Visitor ID |
| equals (ignore case) | Attribute value matches the whole value you specify.|  String&lt;br&gt; Visitor ID |
|does not equal| Attribute value does not match the whole value you specify.|  Number&lt;br&gt; String&lt;br&gt; Visitor ID |
| does not equal (ignore case) | Attribute value does not match the whole value you specify.|  String&lt;br&gt; Visitor ID |
|less than| Attribute value is less than the value you specify.|  Number&lt;br&gt; Date |
|less than or equal to| Attribute value is either less than or equal to the value you specify.|  Number&lt;br&gt; Date |
|greater than| Attribute value exceeds the value you specify.|  Number&lt;br&gt; Date |
|greater than or equal to| Attribute value either exceeds or equals the value you specify.|  Number&lt;br&gt; Date |
|is assigned|  Attribute exists, but may or may not have a value. &lt;br&gt;&lt;br&gt;**True**&lt;br&gt; `&#34;Shirts&#34;` is assigned &lt;br&gt;`[&#34;iOS&#34;, &#34;Android&#34;]` is assigned&lt;br&gt; `[]` is assigned &lt;br&gt;`&#34;&#34;` is assigned is assigned &lt;br&gt;`Is VIP` is assigned |  Number&lt;br&gt; Timeline&lt;br&gt; List&lt;br&gt; Badge&lt;br&gt; String&lt;br&gt; Tally&lt;br&gt; Visitor ID&lt;br&gt; Date |
|is not assigned| Attribute does not exist.|  Number&lt;br&gt; Timeline&lt;br&gt; List&lt;br&gt; Badge&lt;br&gt; String&lt;br&gt; Tally&lt;br&gt; Date&lt;br&gt; Visitor ID |
|is empty|  Tealium iQ variable does not contain any value (for example, value is undefined, null, or blank string). &lt;br&gt;&lt;br&gt;**True**&lt;br&gt; `{ page_name : undefined }`&lt;br&gt; `{ page_name : null }`&lt;br&gt; `{ page_name : &#34;&#34; }`&lt;br&gt; `{ product_id : [] }` |  Imported from Tealium iQ Tag Management |
|is not empty|  Tealium iQ variable contains any value. For example, a string containing one or more characters, a number with a value (including `0`), or an array with one or more items. &lt;br&gt;&lt;br&gt;**True**&lt;br&gt; `{ page_name : &#34;Title&#34; }`&lt;br&gt; `{ page_num : 1 }`&lt;br&gt; `{ product_id : [&#34;WidgetXYZ&#34;] }` |  Imported from Tealium iQ Tag Management |
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

This extended rule condition is available only when using the `contains` operator.

Follow these steps to include a Tally attribute key and its value in a rule:

1. Navigate to **Server-Side Tools &gt; Manage Rules**.
1. Add a new rule or select an existing rule to edit.
1. Under **Conditions**, select the Tally attribute you want to check from the first drop-down list.
1. Select the **contains** operator in the next drop-down list.
1. In the third drop-down list, select **Custom Value**.
1. Enter the key-value that you expect in the Tally attribute.  
      ![](/images/server-side/tally-rule.png)

1. Click **Perform rule on value** and select the operator you want to use to evaluate the key you specified.
1. Specify the value you want to evaluate against the key. You can use an attribute or type in a custom value.
1. Click **Save**.

## Regular expressions

The `matches regex` operator is available only for string attributes. The condition returns `true` if any part of the string matches the regular expression (regex). 

Enter a regular expression into the rule condition without slashes (`/`).For example, for the value `abc1234567890`, enter `^[a-z0-9]{13}$` to match the entire string.


![](/images/server-side/audiences/regex_example_ui.png)

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





