---
title: About connector templates
description: Learn how to build advanced connector requests using templates.
url: https://docs.tealium.com/server-side/connectors/templates/about/
---
## Overview

Connector templates and template variables let you build custom API requests for connectors. Use them to dynamically populate payloads in the format required by a vendor's endpoint, such as JSON or XML.

Templates define the structure of your API request and template variables provide the dynamic values.

This is an example of attributes mapped to template variables:

These are example values for those variables:

```js
email      = "user@example.com"
orderTotal = 9.99
orderID    = "0123456789"
```

This is an example template that uses these variables:

```json
{
  "order": {
    "customerEmail": "{{email}}",
    "total": {{orderTotal}},
    "id": "{{orderID}}"
  }
}
```

This is the rendered template where the variable placeholders have been replaced with their values:

```json
{
  "order": {
    "customerEmail": "user@example.com",
    "total": 9.99,
    "id": "0123456789"
  }
}
```

## Templates

Templates are blueprints for your API requests. They specify the structure and format that the receiving endpoint expects.

Each component of a request has its own template to let you meet the exact requirements of your vendor's API:

* **Header**: Sets request headers, such as authorization tokens, media type, or custom headers required by the vendor.
* **URL**: Customizes the endpoint URL. Substitute dynamic parameters in the hostname or path using template variables. This is useful when the endpoint or resource path changes based on the data being sent.
* **URL parameters**: Dynamically add a query string to the endpoint. Use this template to add or modify the entire query string parameter of the URL. The result of this template is combined with the result of the URL template to build the final request endpoint URL.
* **Body**: Creates a custom payload body for the request.
* **Custom**: Create and name your own template, then map it to any part of the request.

A connector may require dynamic values in the URL, query parameters, headers, and body. The following examples show how each template type is used:

### URL

The URL template sets the URL endpoint for the outgoing request. The value rendered in the template should include everything from the `https://` up to the query string `?`. To set the query string, see [URL parameters](#url-parameters)

This URL template dynamically sets the account ID part of the path. This option is helpful when your vendor requires different endpoints based on the region, site, or environment of the data source. This example requires a mapping from an attribute with the account ID value to the template variable `accountID`.

```none
https://api.example.com/track/{{accountID}}/
```

### URL parameters

The URL parameters template sets the query string of the URL endpoint for the outgoing request. The value rendered in the template is joined with the URL of the request using the query string character `?`.

This URL parameters template builds a query string with a dynamic `order_id` parameter and a static `source` parameter.

```none
order_id={{orderID}}&source=tealium
```

If this template were used with the previous URL template, the final rendered URL would look something like this:

```none
https://api.example.com/track/ABC123/?order_id=0123456789&source=tealium
```

### Header

The header template is appended to the header of the outgoing request. Use this template to add custom headers for authentication or other special requirements of the vendor endpoint.

This header template specifies a custom header to keep the request secure using a dynamically created hash. This example requires a template variable `secretHash`, set either from a mapped attribute or another custom template.

```none
X-Secret: {{secretHash}}
```

### Body template

The body template sets the request payload.

This body template creates a JSON payload with dynamic values for the user email, order total, and a list of items.

```json
{
  "order": {
    "customerEmail": "{{email}}",
    "total": {{orderTotal}},
    "id": "{{orderID}}"
  }
}
```

## Template variables

Template variables are attribute mappings that provide the dynamic data for your templates.

For example, to include a dynamic order ID value in a template, map the attribute `order_id` to a template variable named `orderID`.  Then, in the template, reference `{{orderID}}` where the order ID value should appear.

For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).

## Syntax

These examples show the syntax to reference template variables and build control structures in your templates. 

### Variables

A variable represents a value that can be substituted into a template. To reference a variable's value, use double curly braces around the variable name, for example: `{{var}}`.

In the following example, the template variable `{{str}}` is substituted with its value `Hello`.


|Template| Rendered Value|
|---| ---|
|`{{str}} world` | `Hello world`|

### Arrays

The following example gets the first value in the array of numbers `{{arrn}}`, referenced by specifying the index.

|Template|Rendered Value|
|---| ---|
|`The first value is {{arrn.0}}`| `The first value is 1.0`|
|`The second value is {{arrn.1}}`| `The second value is 2.0`|
|`The third value is {{arrn.2}}`| `The third value is 3.0`|

### Sections

A section of content, surrounded by `{{#var}} {{/var}}` tags, is rendered if there is an object found for the given key. This includes a boolean of value `true`, a non-empty tally, and a non-empty array.

In the following example, since the boolean variable `bln` is `true`, the content is rendered. The content does not render if the value is `false`.

|Template|Rendered Value|
|---| ---|
|`{{#bln}}Section of content{{/bln}}`| `Section of content` |

In the following example, since the array of strings `arrs` is not empty, the content is rendered three times, once for each array element. The content does not render if the array is empty.

|Template|Rendered Value|
|---| ---|
|`{{#arrs}}Section of content.{{/arrs}}`|  `Section of content.Section of content.Section of content.` |

### Inverted sections

A section of content, surrounded by `{{^var}} {{/var}}` tags, is rendered if there is no object found in the context. This includes a boolean of value `false`, an empty tally, or an empty array.

In the following example, since `bln` is `true`, the content is not rendered. The content does render if the value is `false`.

|Template|Rendered Value|
|---| ---|
|`Section of {{^bln}}content{{/bln}}`| `Section of `|

In the following example, since the variable `missing` is not defined, the content is rendered.

|Template|Rendered Value|
|---| ---|
|`{{^missing}}Section of content{{/missing}}`| `Section of content` |

### Iteration

Templates provide several helper functions to iterate an array.

The following built-in iteration helpers are supported:

* `iter.index` (the first element is at index `1`)
* `iter.isFirst`
* `iter.isLast`
* `iter.hasNext`

#### Single array example

The following example uses the mapping of an array of booleans to the variable `arrb` and shows how to iterate over the array:

**Template**

```json
{
  "MyData": [
  {{#arrb}}
  {
    "idx": {{iter.index}},
    {{#iter.isFirst}}"first": true,{{/iter.isFirst}}
    {{#iter.isLast}}"last": true,{{/iter.isLast}}
    "val": {{.}}
  }{{#iter.hasNext}},{{/iter.hasNext}}
  {{/arrb}}
  ]
}
```

| Syntax                                      | Description                                              |
|----------------------------------------------|----------------------------------------------------------|
| `{{#arrb}} ... {{/arrb}}`                    | Iterates over the array.                                 |
| `{{iter.index}}`                             | The current iteration index, starting at 1.              |
| `{{#iter.isFirst}} "first": true, {{/iter.isFirst}}` | Renders if it is the first iteration.            |
| `{{#iter.isLast}} "last": true, {{/iter.isLast}}`     | Renders if it is the last iteration.             |
| `{{#iter.hasNext}}, {{/iter.hasNext}}`       | Renders a comma if the iteration has more elements.      |
| `{{.}}`                                     | Renders the current array value.                         |

**Rendered Value**

```json
{
  "MyData": [
    {
      "idx": 1,
      "first": true,
      "val": true,
    },
    {
      "idx": 2,
      "val": true,
    },
    {
      "idx": 3,
      "last": true,
      "val": false,
    }
  ]
}
```

The tally attribute supports iteration. The following example uses the mapping of a tally to the variable `tly` and uses `entrySet` to iterate each item of the tally. For each item in the tally, it references the `key` and `value`:

**Template**

```json
{
  "MyTally": {
    {{#each tly.entrySet}}
      "{{key}}": {{value.toInteger}}{{#iter.hasNext}},{{/iter.hasNext}}
    {{/each}}
  }
}
```

**Rendered Value**

```json
"MyTally": {
    "A": "1",
    "B": "2",
    "C": "3"
}
```

#### Aligned arrays example

Aligned arrays are groups of arrays that share the same length. You can use them to reference corresponding elements from each array at the same index position during each iteration.

Map your aligned arrays to names that begin with the same prefix, then a dot, then the name of your particular array. For example, the following screenshot shows all product arrays that map to `prods.(name)`:

![](https://docs.tealium.com/images/server-side/connectors/iteration-template-variables.png)

You can then iterate over the `prods` object as if it were also an array, and reference arrays inside of it using their names:

```json
{{#prods}}
  {
    "price": {{prices}},
    "currency": "{{currency}}",
    "quantity": {{quantities}}
  }{{#iter.hasNext}},{{/iter.hasNext}}
{{/prods}}
```

If the input values for the attributes are:

* Most Recent Cart Product Prices: `[83, 23.49]`
* Most Recent Cart Product Quantities: `[1, 2]`
* Most Recent Cart Product Currency: `["GBP", "GBP"]`

The output is:

```json
"products": [
  {
    "price": 83,
    "currency": "GBP",
    "quantity": 1
  },
  {
    "price": 23.49,
    "currency": "GBP",
    "quantity": 2
  }
]
```

You can also map an attribute more than once, as shown by the `product_quantities` example above. This is so that you can use the array independently outside of the `prods` object:

```json
"total_quantity": {{product_quantities.sum}}
```

Which results in the following output:

```json
"total_quantity": 3
```

Finally, note that the aligned array iteration method only works with CDH array types. It does not work with the "Any" data type imported from Tealium iQ available in EventStream. If you want to use those, you need to convert them to CDH array types.

If you know that the incoming data will always be an array, you can delete the existing Tealium iQ attribute from server-side CDH and re-add it as an array CDH attribute.

If you're unsure whether the data will always be an array, or there are too many CDH dependencies on the Tealium iQ attribute, you can use EventStream enrichments to make an array copy of the Tealium iQ attribute when the incoming data is an array, as follows:

![](https://docs.tealium.com/images/server-side/connectors/iteration-array-copy.png)

## Helper functions

Several helper functions are supported to provide additional functionality in your templates.

For more information, see [connector-template-helper-functions](https://docs.tealium.com/connector-template-helper-functions/).

## Reference

Connector templates are built on Trimou, a Java templating engine based on Mustache.

* [Trimou 2.3.0 Documentation](http://trimou.org/doc/2.3.0.Final/trimou-doc.html)