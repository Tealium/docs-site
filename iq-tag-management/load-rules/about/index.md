---
title: About load rules
description: This article provides information on adding and managing load rules. Load rules are conditions that define when and where to load a tag.
url: https://docs.tealium.com/iq-tag-management/load-rules/about/
---
A load rule determines when a tag loads on your site or app. A load rule is one or more conditions that are based on the values in the data layer. For example, a load rule condition that identifies your search page might be:


[
  [
    {
      &#34;input&#34;: &#34;page_type&#34;,
      &#34;operator&#34;: &#34;equals&#34;,
      &#34;filter&#34;: &#34;search&#34;
    }
  ]  
]


The default load rule is **All Pages**, which contains no conditions and is always true.

The following components use load rules:

* Tags
* Events
* Consent manager
* Currency converter extension
* Channels extension

## Boolean logic

Multiple conditions can be combined using boolean logic to form more complex load rules. For example, to load a tag on the search page, but only when the user is logged in, the load rule conditions might be:


[
  [
    {
      &#34;input&#34;: &#34;page_type&#34;,
      &#34;operator&#34;: &#34;equals&#34;,
      &#34;filter&#34;: &#34;search&#34;
    },
    {
      &#34;input&#34;: &#34;is_logged_in&#34;,
      &#34;operator&#34;: &#34;equals&#34;,
      &#34;filter&#34;: &#34;1&#34;
    }
  ]  
]


This complex logic can be combined into a single rule or created as two rules and then enforced using the **Match All Rules** setting. See [how to assign load rules to a tag]().

#### AND logic

Use AND logic to create a rule that is true only when all of the conditions evaluate to true. For example, a rule that combines 3 conditions using AND logic evaluates to true only if each individual condition also evaluates to true. If any of the conditions evaluate to false, then the entire rule also evaluates to false.

#### OR logic

Use OR logic to create a rule that is true when any of the conditions evaluate to true. For example, a rule that combines 3 conditions using OR logic evaluates to true if any of the individual conditions also evaluate to true. A rule that uses OR logic only evaluates to false if all of the individual conditions also evaluate to false.

## List of comparison operators

Each rule condition uses a comparison operator and a variable from the data layer. The following table lists the available comparison operators that can be used in load rule conditions. For operators that include `(ignore case)` in the name, the text value of the variable is converted to lowercase before the comparison.

|**Comparison Operator**| **When a tag loads on a page**|
|---| ---|
|`contains`&lt;br&gt; `contains (ignore case)`| The variable contains the specified sequence of characters.|
|`does not contain`&lt;br&gt; `does not contain (ignore case)`| The variable does not contain the specified sequence of characters.|
|`does not end with`&lt;br&gt; `does not end with (ignore case)`| The variable does not end with the specified sequence of characters.|
|`does not equal`&lt;br&gt; `does not equal (ignore case)`| The variable does not equal the specified value.|
|`does not start with`&lt;br&gt; `does not start with (ignore case)`| The variable does not start with the specified string of characters.|
|`ends with`&lt;br&gt; `ends with (ignore case)`| The variable does not end with the specified string of characters.|
|`equals`&lt;br&gt; `equals (ignore case)`| The variable equals the specified value.|
|`greater than`| The variable is greater than the specified value.|
|`greater than or equal to`| The variable is greater than or equal to the specified value.|
|`is badge assigned`| The badge is assigned to the visitor.&lt;br&gt; For use with [data layer enrichment]().|
|`is badge not assigned`| The badge is not assigned to the visitor.&lt;br&gt; For use with [data layer enrichment]().|
|`is defined`| The variable is defined in the data layer.|
|`is not defined`| The variable is not defined in the data layer.|
|`is populated`| The variable is defined in the data layer and is not blank or empty.|
|`is not populated`| The variable is defined in the data layer and is blank or empty.|
|`less than`| The variable is less than the specified value.|
|`less than or equal to`| The variable is less than or equal to the specified value.|
|`regular expression`| The variable matches the regular expression.|
|`starts with`&lt;br&gt; `starts with (ignore case)`| The variable begins with the specified sequence of characters. |

## Load rules and consent enforcement

While it is possible to add consent conditions into existing load rules, your use case may require you to use consent integrations for more reliable consent enforcement.

Consent integrations is a Tealium iQ Management feature that allows organizations to easily incorporate consent enforcement into their client-side data activation processes. Unlike load rules, which control when tags fire based on conditions such as page views or user interactions, consent integrations focus exclusively on ensuring user consent is respected during data collection and processing activities. For more information, see [consent integrations]().

Using load rules for consent enforcement may result in the following issues:

* Missed initial events
* Data leaks
* Difficulty completely triggering server-side tools

Additionally, you can fire tags without respecting load rules using an optional array of tag IDs (`uid_array`) in [`utag.track`]() calls. When using load rules for consent enforcement together with the `uid_array` parameter, consent conditions are ignored along with the rest of the rule.

For more information about load rules and consent integrations, see [Beyond Load Rules: Leveraging Consent Integrations for Compliance](https://tealium.com/blog/data-governance-privacy/beyond-load-rules-leveraging-consent-integrations-for-compliance/).



