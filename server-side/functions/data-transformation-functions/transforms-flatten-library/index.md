---
title: Flatten nested objects
description: This article provides information on the `flatten` library, which is used to convert a nested object into an object that is not nested.
url: https://docs.tealium.com/server-side/functions/data-transformation-functions/transforms-flatten-library/
---
## How it works

The `flatten` library is a standard library that is imported in the default code for a data transformation function. This library provides the `flatten()` utility, which converts a nested object into an object that is not nested. `flatten()` returns an object that contains strings and arrays of strings.

`flatten()` accepts two parameters, as follows:

`flatten(target[, options])`

* `target` is the event object passed to the data transformation function.
* `options` is an object that specifies how nested keys are handled during the conversion.

The `options` parameter contains the following properties:

|**Property**| **Data Type**| **Description**|
|---| ---| ---|
|`delimiter`| `String` | The character used to combine parent and child property names. The default is `.`.|
|`prefix`| `String` |  The string concatenated at the beginning of the new key name followed by the `delimiter`. |
|`ignoreKeys`| `String[]` | An array of keys to omit from the output.|
|`replaceKeys`| `Object{string:string}` | Specifies new names for keys, where the key is the existing key in the object and the value is the new key. &lt;br&gt;Example: `{ &#34;uid&#34; : &#34;user_id&#34; }` |

## Parameters

The following examples show how the `options` properties are used. These examples use the following nested object as the target to be flattened:

```js
const object = {
  page: {
    id: 1
  },
  user: {
    id: 1
  },
  util: [&#34;1&#34;, &#34;2&#34;, &#34;3&#34;]
};
```

### `delimiter`

If `delimiter` is `_`, the following object is returned:

```json
{
  &#34;page_id&#34;: 1,
  &#34;user_id&#34;: 1,
  &#34;util&#34;: [&#34;1&#34;, &#34;2&#34;, &#34;3&#34;]
}
```

### `prefix`

If `prefix` is `fl`, the following object is returned:

```json
{
  &#34;fl.user.id&#34;: 1,
  &#34;fl.page.id&#34;: 1,
  &#34;fl.util&#34;: [&#34;1&#34;, &#34;2&#34;, &#34;3&#34;]
}
```

### `ignoreKeys`

If `ignoreKeys` is `[&#34;page&#34;, &#34;util&#34;]`, the following object is returned:

```json
{
  &#34;user.id&#34;: 1
}
```

### `replaceKeys`

If `replaceKeys` is defined as follows:

```js
const replaceKeys = {
  &#34;user&#34;: &#34;&#34;,
  &#34;page&#34;: &#34;p&#34;
}
```

The following object is returned:

```json
{
  &#34;id&#34;: 1,
  &#34;p.id&#34;: 1,
  &#34;util&#34;: [&#34;1&#34;, &#34;2&#34;, &#34;3&#34;]
}
```

## Full example

The following example shows a complex object to be flattened:

```js
import flatten from &#39;tealium/util/flatten&#39;;
const options = {
  delimiter: &#34;_&#34;,
  ignoreKeys: [&#34;array_of_strings&#34;],
  replaceKeys: {
    &#34;number&#34;: &#34;float&#34;,
    &#34;array_of_objects&#34;: &#34;modified_array_of_strings&#34;,
    &#34;ordinal&#34;: &#34;&#34;
  },
  prefix: &#34;t&#34;
}

const output = flatten({
  &#34;boolean&#34;: true,
  &#34;number&#34;: 12.34,
  &#34;string&#34;: &#34;value&#34;,
  &#34;date&#34;: new Date(1631009413904),
  &#34;array_of_strings&#34;: [&#34;first&#34;, &#34;second&#34;],
  &#34;array_of_arrays&#34;: [
    [1, 2],
    [3, 4]
  ],
  &#34;array_of_objects&#34;: [{
    &#34;ordinal&#34;: &#34;first&#34;
  }, {
    &#34;ordinal&#34;: &#34;second&#34;
  }],
  &#34;object&#34;: {
    &#34;child_boolean&#34;: true,
    &#34;child_number&#34;: 12.34,
    &#34;child_string&#34;: &#34;value&#34;,
    &#34;child_array_of_strings&#34;: [&#34;first&#34;, &#34;second&#34;],
    &#34;child_array_of_arrays&#34;: [
      [1, 2],
      [3, 4]
    ],
    &#34;child_object&#34;: {
      &#34;gchild_boolean&#34;: true,
      &#34;gchild_number&#34;: 12.34,
      &#34;gchild_string&#34;: &#34;value&#34;,
      &#34;gchild_array_of_strings&#34;: [&#34;first&#34;, &#34;second&#34;],
      &#34;gchild_array_of_arrays&#34;: [
        [1, 2],
        [3, 4]
      ]
    }
  }
}, options);
```

The following object is returned by `flatten()`:

```js
{
  &#34;t_boolean&#34;: &#34;true&#34;,
  &#34;t_float&#34;: &#34;12.34&#34;,
  &#34;t_string&#34;: &#34;value&#34;,
  &#34;t_date&#34;: &#34;2021-09-07T10:10:13.904Z&#34;,
  &#34;t_array_of_arrays&#34;: [&#34;1&#34;,&#34;2&#34;,&#34;3&#34;,&#34;4&#34;],
  &#34;t_modified_array_of_strings&#34;: [&#34;first&#34;,&#34;second&#34;],
  &#34;t_object_child_boolean&#34;: &#34;true&#34;,
  &#34;t_object_child_number&#34;: &#34;12.34&#34;,
  &#34;t_object_child_string&#34;: &#34;value&#34;,
  &#34;t_object_child_array_of_strings&#34;: [&#34;first&#34;,&#34;second&#34;],
  &#34;t_object_child_array_of_arrays&#34;: [&#34;1&#34;,&#34;2&#34;,&#34;3&#34;,&#34;4&#34;],
  &#34;t_object_child_object_gchild_boolean&#34;: &#34;true&#34;,
  &#34;t_object_child_object_gchild_number&#34;: &#34;12.34&#34;,
  &#34;t_object_child_object_gchild_string&#34;: &#34;value&#34;,
  &#34;t_object_child_object_gchild_array_of_strings&#34;: [&#34;first&#34;,&#34;second&#34;],
  &#34;t_object_child_object_gchild_array_of_arrays&#34;: [&#34;1&#34;,&#34;2&#34;,&#34;3&#34;,&#34;4&#34;]
}
```
