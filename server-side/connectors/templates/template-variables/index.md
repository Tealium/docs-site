---
title: Connector template variables
description: Learn how to build advanced connector requests using template variables.
url: https://docs.tealium.com/server-side/connectors/templates/template-variables/
---
## Overview

Connector templates and template variables let you build custom API requests for connectors. Use them to dynamically populate payloads in the format required by a vendor&#39;s endpoint, such as JSON or XML.

Templates define the structure of your API request and template variables provide the dynamic values.

For more information, see .


## How it works

Template variables are attribute mappings that provide the dynamic data for your templates.

For example, to include a dynamic order ID value in a template, map the attribute `order_id` to a template variable named `orderID`.  Then, in the template, reference `{{orderID}}` where the order ID value should appear.

To add template variables, go to the connector action, click the **Templates** tab, and map attributes to variable names.

![](/images/server-side/connectors/connector-templates-variables-mapping.png)

## Data types

To use connector templates effectively, it&#39;s important to understand the structure of the data used to render a template.

This section describes how to use template variables of different data types in templates, including how to reference values directly, use helper methods like `.toJson`, and how to  iterate over multiple values.

These examples are based on the following template variable mappings:

![](/images/server-side/connectors/connector-template-variables-mapping-sample.png)

### Badge

A variable mapped to a badge attribute has the value `true` if it&#39;s assigned or an empty value if it&#39;s not assigned. A badge variable never has the value `false`, so to avoid blank values, use a section and inverted section to force a value of `true` or `false`.

**Template variable values:**
```js
unbadgedBadge =
didSearchBadge = true
```

**Template:**
```json
{
    &#34;badge1&#34;: &#34;{{unbadgedBadge}}&#34;,
    &#34;badge2&#34;: {{didSearchBadge}},
    &#34;badge1SectionInvert&#34;: {{#unbadgedBadge}}true{{/unbadgedBadge}}{{^unbadgedBadge}}false{{/unbadgedBadge}},
    &#34;badge2SectionInvert&#34;: {{#didSearchBadge}}true{{/didSearchBadge}}{{^didSearchBadge}}false{{/didSearchBadge}}
}
```

**Rendered template:**
```json
{
    &#34;badge1&#34;: &#34;&#34;,
    &#34;badge2&#34;: true,
    &#34;badge1SectionInvert&#34;: false,
    &#34;badge2SectionInvert&#34;: true
}
```

### Boolean

A variable mapped to a boolean is either `true`, `false`, or unassigned. Render the value directly or use it in section or inverted section logic. Boolean values are not quoted. 

**Template variable values:**
```js
returningVisitorBoolean = false
```

**Template:**
```json
{
    &#34;boolean&#34;: {{returningVisitorBoolean}},
    &#34;booleanSectionTrue&#34;: {{#returningVisitorBoolean}}true{{/returningVisitorBoolean}},
    &#34;booleanSectionInvert&#34;: {{^returningVisitorBoolean}}false{{/returningVisitorBoolean}}
}
```

**Rendered template:**
```json
{
  &#34;boolean&#34;: false, 
  &#34;booleanSectionTrue&#34;: , 
  &#34;booleanSectionInvert&#34;: false
}
```

Keep in mind that the boolean value might not be set. To handle this in a template, use section and inverted section logic to force a value to be rendered.

**Template logic:**
```json
{
    &#34;boolean&#34;: {{#returningVisitorBoolean}}true{{/returningVisitorBoolean}}{{^returningVisitorBoolean}}false{{/returningVisitorBoolean}}
}
```

### Date

A variable mapped to a date attribute is represented as a timestamp (numbers) in the template data and rendered as ISO 8601 strings in the output.

Helper functions: [formatDate](), [toTimestamp](), [toTimestampMs](), [unixTimestamp](), [unixTimestampMs]().

**Template variable values:**
```js
firstVisitDate = 1749081326718
```

**Template:**
```json
{
    &#34;date&#34;: &#34;{{firstVisitDate}}&#34;
}
```

**Rendered template:**
```json
{
    &#34;date&#34;: &#34;2025-06-04T23:55:26.718Z&#34;
}
```

### Number

A variable mapped to a number attribute can be rendered directly or converted to an integer using `.toInteger`.

**Template variable values:**
```js
lifetimeVisitCountNumber = 1.0
```

**Template:**
```json
{
    &#34;number&#34;: {{lifetimeVisitCountNumber}},
    &#34;numberToInteger&#34;: {{lifetimeVisitCountNumber.toInteger}}
}
```

**Rendered template:**
```json
{
    &#34;number&#34;: 1.0,
    &#34;numberToInteger&#34;: 1
}
```

### String

A variable mapped to a string attribute can be referenced directly. If you are building a JSON template, use `.toJson` to ensure an escaped string that can be quoted.

Helper functions: [hash](), [md5](), [sha1](), [sha256](), [substring]().

**Template variable values:**
```json
activeBrowserTypeString = &#34;Chrome&#34;
```

**Template:**
```json
{
    &#34;string&#34;: &#34;{{activeBrowserTypeString.toJson}}&#34;
}
```

**Rendered template:**
```json
{
    &#34;string&#34;: &#34;Chrome&#34;
}
```

### Set of Strings

A variable mapped to a set of strings attribute is similar to an array but may not preserve order. To render a set of strings variable as an array, use `.toJson`. For more advanced cases, use an iteration to apply a custom format for each entry.

Helper functions: [sum]().

**Template variable values:**
```json
activeBrowserTypesSetOfStrings = [&#34;Chrome&#34;, &#34;Safari&#34;]
```

**Template:**
```json
{
    &#34;setOfStrings&#34;: {{activeBrowserTypesSetOfStrings}},
    &#34;setOfStringsToJson&#34;: {{activeBrowserTypesSetOfStrings.toJson}},
    &#34;setOfStringsIter&#34;: [
    {{#activeBrowserTypesSetOfStrings}}
        &#34;-- {{.}} --&#34;{{#iter.hasNext}},{{/iter.hasNext}}
    {{/activeBrowserTypesSetOfStrings}}
    ]
}
```

Referencing a set of strings variable directly, without `.toJson` or iterating, renders unquoted values.

**Rendered template:**
```json
{
    &#34;setOfStrings&#34;: [Chrome,Safari], 
    &#34;setOfStringsToJson&#34;: [&#34;Chrome&#34;, &#34;Safari&#34;],
    &#34;setOfStringsIter&#34;: [
        &#34;-- Chrome --&#34;,
        &#34;-- Safari --&#34;
    ]
}
```

### Arrays

A variable mapped to an array attribute should be referenced with `.toJson`. For more advanced cases, use an iteration to apply a custom format for each entry.

Helper functions: [sum]().

Referencing an array variable directly renders unquoted values.

**Template variable values:**
```json
browsersArray = [&#34;Chrome&#34;, &#34;Safari&#34;]
```

**Template:**
```json
{
    &#34;array&#34;: {{browsersArray}},
    &#34;arrayToJson&#34;: {{browsersArray.toJson}},
    &#34;arrayIter&#34;: [
    {{#browsersArray}}
        &#34;-- ({{iter.index}}) {{.}} --&#34;{{#iter.hasNext}},{{/iter.hasNext}}
    {{/browsersArray}}
    ],
}
```

**Rendered template:**
```json
{
    &#34;array&#34;: [Chrome,Safari], 
    &#34;arrayToJson&#34;: [&#34;Chrome&#34;, &#34;Safari&#34;], 
    &#34;arrayIter&#34;: [
        &#34;-- (1) Chrome --&#34;,
        &#34;-- (2) Safari --&#34;
    ] 
}
```

### Tally

A variable mapped to a tally attribute is a map of keys to numeric values. Use `.toJson` to render the full tally with quoted keys. Use `.entrySet` to iterate the tally, then `key` and `value` to reference the key-value pairs.

Referencing a tally directly renders unquoted values.

**Template variable values:**
```js
categoriesTally = { 
    &#34;Shirts&#34; : 1, 
    &#34;Blazers&#34; : 2,  
    &#34;Electronics&#34; : 4, 
    &#34;Eyewear&#34; : 1 
}
```

**Template:**
```json
{
    &#34;tally&#34;: {{categoriesTally}},
    &#34;tallyToJson&#34;: {{categoriesTally.toJson}},
    &#34;tallyIter&#34;: {
        {{#each categoriesTally.entrySet}}
        &#34;{{key}}&#34;: &#34;{{value.toInteger}}&#34;{{#iter.hasNext}},{{/iter.hasNext}}
        {{/each}}
    }
}
```

**Rendered template:**
```json
{
    &#34;tally&#34;: {Shirts=1, Blazers=2, Electronics=4, Eyewear=1},
    &#34;tallyToJson&#34;: {
        &#34;Shirts&#34;:1,
        &#34;Blazers&#34;:2,
        &#34;Electronics&#34;:4,
        &#34;Eyewear&#34;:1
    }, 
    &#34;tallyIter&#34;: { 
        &#34;Shirts&#34;: &#34;1&#34;,  
        &#34;Blazers&#34;: &#34;2&#34;, 
        &#34;Electronics&#34;: &#34;4&#34;,
        &#34;Eyewear&#34;: &#34;1&#34; 
  }
}
```
