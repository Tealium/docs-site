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
|`replaceKeys`| `Object{string:string}` | Specifies new names for keys, where the key is the existing key in the object and the value is the new key. <br>Example: `{ "uid" : "user_id" }` |

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
  util: ["1", "2", "3"]
};
```

### `delimiter`

If `delimiter` is `_`, the following object is returned:

```json
{
  "page_id": 1,
  "user_id": 1,
  "util": ["1", "2", "3"]
}
```

### `prefix`

If `prefix` is `fl`, the following object is returned:

```json
{
  "fl.user.id": 1,
  "fl.page.id": 1,
  "fl.util": ["1", "2", "3"]
}
```

### `ignoreKeys`

If `ignoreKeys` is `["page", "util"]`, the following object is returned:

```json
{
  "user.id": 1
}
```

### `replaceKeys`

If `replaceKeys` is defined as follows:

```js
const replaceKeys = {
  "user": "",
  "page": "p"
}
```

The following object is returned:

```json
{
  "id": 1,
  "p.id": 1,
  "util": ["1", "2", "3"]
}
```

## Full example

The following example shows a complex object to be flattened:

```js
import flatten from 'tealium/util/flatten';
const options = {
  delimiter: "_",
  ignoreKeys: ["array_of_strings"],
  replaceKeys: {
    "number": "float",
    "array_of_objects": "modified_array_of_strings",
    "ordinal": ""
  },
  prefix: "t"
}

const output = flatten({
  "boolean": true,
  "number": 12.34,
  "string": "value",
  "date": new Date(1631009413904),
  "array_of_strings": ["first", "second"],
  "array_of_arrays": [
    [1, 2],
    [3, 4]
  ],
  "array_of_objects": [{
    "ordinal": "first"
  }, {
    "ordinal": "second"
  }],
  "object": {
    "child_boolean": true,
    "child_number": 12.34,
    "child_string": "value",
    "child_array_of_strings": ["first", "second"],
    "child_array_of_arrays": [
      [1, 2],
      [3, 4]
    ],
    "child_object": {
      "gchild_boolean": true,
      "gchild_number": 12.34,
      "gchild_string": "value",
      "gchild_array_of_strings": ["first", "second"],
      "gchild_array_of_arrays": [
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
  "t_boolean": "true",
  "t_float": "12.34",
  "t_string": "value",
  "t_date": "2021-09-07T10:10:13.904Z",
  "t_array_of_arrays": ["1","2","3","4"],
  "t_modified_array_of_strings": ["first","second"],
  "t_object_child_boolean": "true",
  "t_object_child_number": "12.34",
  "t_object_child_string": "value",
  "t_object_child_array_of_strings": ["first","second"],
  "t_object_child_array_of_arrays": ["1","2","3","4"],
  "t_object_child_object_gchild_boolean": "true",
  "t_object_child_object_gchild_number": "12.34",
  "t_object_child_object_gchild_string": "value",
  "t_object_child_object_gchild_array_of_strings": ["first","second"],
  "t_object_child_object_gchild_array_of_arrays": ["1","2","3","4"]
}
```
