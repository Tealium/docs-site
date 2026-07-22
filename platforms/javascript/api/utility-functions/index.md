---
title: Utility Functions
description: Reference guide for utility functions provided by Tealium for JavaScript.
url: https://docs.tealium.com/platforms/javascript/api/utility-functions/
---
The following `utag.ut` functions are available:

| Function | Description |
| --- | --- |
| `decode()` | Returns the decoded value of an encoded URI component or `String` |
| `encode()` | Returns the encoded value of a decoded URI component or `String` |
| `flatten()` | Returns the flattened value of an object argument|
| `hasOwn()` | Returns a boolean indicating whether the object has the specified property as its own property |
| `isEmpty()` | Returns a boolean `true` indicating the argument is empty, or boolean `false` if not empty |
| `isEmptyObject()` | Returns a boolean `true` indicating the object argument is empty, or boolean `false` if not empty |
| `loader()` | Tag templates use this function to load tags as iframes, images, or scripts and to trigger a callback when the tag is loaded. |
| `merge()` | Merges the properties from one object into another object|
| `typeOf()` | Returns a variables type as a string |


## `utag.ut.decode()`

Returns the decoded value of an encoded URI component or `String`. This function wraps around the standard JavaScript functions [`decodeURIComponent()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/decodeURIComponent) and [`unescape()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/unescape).  

```js
utag.ut.decode(encodedStr)
```

| Parameter | Type | Description |
| --- | --- | --- |
| `encodedStr` | `String` | The encoded string to be decoded |

Examples:

```js
utag.ut.decode("Tealium%20Developer%20Docs!");     // "Tealium Developer Docs!"
utag.ut.decode("https%3A%2F%2Fdocs.tealium.com");  // "https://docs.tealium.com"
```

## `utag.ut.encode()`

Returns the encoded value of a decoded URI component or string. This function wraps around the standard JavaScript functions [`encodeURIComponent()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/encodeURIComponent) and [`escape()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/escape).

```js
utag.ut.encode(decodedStr)
```

| Parameter | Type | Description |
| --- | --- | --- |
| `decodedStr` | `String` | The decoded string to be encoded |

Examples:

```js
utag.ut.encode("Tealium Developer Docs!");   // "Tealium%20Developer%20Docs!"
utag.ut.encode("https://docs.tealium.com");  // "https%3A%2F%2Fdocs.tealium.com"
```

## `utag.ut.flatten()`

Returns the flattened value of an object argument, delimited by a `.` character. This function assumes that the object passed is only 1 level deep. The function stops when arriving at a string, array, boolean, or number (float or integer). Do not use this function for multilevel objects or arrays of objects.

```js
utag.ut.flatten(obj)
```

| Parameter | Type | Description |
| --- | --- | --- |
| `obj` | `Object` | The object to be flattened |

Example:

```js
utag.ut.flatten({"order_id": "0123567", "cart": {"total_items": 3, "total_amount": 123.45},"order_tax": 9.97});
// {order_id: "0123567", cart.total_items: 3, cart.total_amount: 123.45, order_tax: 9.97}
```


## `utag.ut.hasOwn()`

Returns a boolean indicating whether the object has the specified property as its own property (as opposed to inheriting it). The function performs a `null` check and wraps the JavaScript function [`hasOwnProperty()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwnProperty).

```js
utag.ut.hasOwn(obj, key)
```

| Parameter | Type | Description |
| --- | --- | --- |
| `obj` | `Object` | The object to test |
| `key` | `String` | The property to test |

Examples:

```js
var obj = new Object();     // Create an object
obj.x = 3.14;               // Define a non-inherited local property

utag.ut.hasOwn(obj, 'x');          // true - x is a local property of obj
utag.ut.hasOwn(obj, 'y');          // false - obj doesn't have a property y
```

## `utag.ut.isEmpty()`

Returns a boolean `true` indicating the argument is empty, or boolean `false` if not empty.  It first determines the data type by using the `utag.ut.typeOf()` function, and returns the following based on the type:

| Type | Return value description |
| --- | --- |
| `number` | Returns the value of the JavaScript function `isNaN()` |
| `boolean` | Returns `false` |
| `String` | Returns `true` if the string object's `.length` field is 0 |
| `Object` | returns the value of the `utag.ut.isEmptyObject()` function |

```js
utag.ut.isEmpty(arg)
```

| Parameter | Type | Description |
| --- | --- | --- |
| `arg` | [`number`, `boolean`, `String`, `Object`] | The argument to test if empty |

Examples:

```js
utag.ut.isEmpty(5);         // false
utag.ut.isEmpty(NaN);       // true
utag.ut.isEmpty(undefined); // true
utag.ut.isEmpty(true);      // false
utag.ut.isEmpty(false);     // false
utag.ut.isEmpty("Tealium"); // false
utag.ut.isEmpty("");        // true

```


## `utag.ut.isEmptyObject()`

Returns a boolean `true` indicating the object argument is empty, or boolean `false` if not empty.

```js
utag.ut.isEmptyObject(obj)
```

| Parameter | Type | Description |
| --- | --- | --- |
| `obj` | `Object` | The object to test if empty|

Examples:

```js
utag.ut.isEmptyObject({});              // true
utag.ut.isEmptyObject({ foo: "bar" });  // false
```

## `utag.ut.loader()`

Tealium’s tag templates uses this function to load tags. It loads iframes, images, scripts and allows for callbacks when a script is loaded. The function only accepts one object argument.

If a file is loaded as an iframe with the same ID as an existing iframe, the function removes the existing element before adding it to avoid impacting browser history and to maintain a cleaner DOM.

```js
utag.ut.loader(object)
```

The `object` has the following parameters:

| Parameter  | Description |
| --- | --- |
| `src` | URL of the file to load |
| `type` | The type of tag to load: "iframe", "img", or "script" (default)|
| `id` | (Optional) The element ID |
| `cb` | (Optional) A callback function |
| `attrs`| (Optional) An object of additional HTML element attributes |

Example:

```js
utag.ut.loader({
  type: "iframe",
  src: "https://example.com/path/file.js",
  id: "teal-tag1",
  cb: function() {},
  attrs: {"async":"true"}})
// Results in the following HTML element:
// <iframe id="teal-tag1"  async="true" height="1" width="1" style="display:none"
//   src="https://example.com/path/file.js"> </iframe>
```

## `utag.ut.merge()`

Merges the properties from one object into another object. This function does not handle multilevel objects. First flatten the objects before attempting to merge them. This function creates references if used on an array.

```js
utag.ut.merge(obj1, obj2, flag)
```

| Parameter | Type | Description |
| --- | --- | --- |
| `obj1` | Object | The first key-value pair object to merge |
| `obj2` | Object | The second key-value pair object to merge |
| `overwrite` | number | A flag, `0` (no) or `1` (yes), to overwrite the property value in `obj1` from the property value of `obj2` |

Examples:

```js
foo = { "key1":"value1", "key2":"value2" }
bar = { "key1":"value4", "key3":"value3" }
utag.ut.merge(foo, bar, 0)
// foo: {key1: "value1", key2: "value2", key3: "value3"}
// bar: {key1: "value4", key3: "value3"}

foo = { "key1":"value1", "key2":"value2" }
bar = { "key1":"value4", "key3":"value3" }
utag.ut.merge(foo, bar, 1)
// foo: {key1: "value4", key2: "value2", key3: "value3"}
// bar: {key1: "value4", key3: "value3"}
```

## `utag.ut.typeOf()`

Returns an argument's variable type as a `String`.

```js
utag.ut.typeOf(arg)
```

| Parameter | Type | Description |
| --- | --- | --- |
| `arg` | Any type | The argument to determine the type of |

Examples:
```js
utag.ut.typeOf(5);         // "number"
utag.ut.typeOf("Tealium"); // "string"
utag.ut.typeOf(imgObj);    // "htmlimagelement"
utag.ut.typeOf(obj);       // "object"
utag.ut.typeOf(null);      // "null"
utag.ut.typeOf(undefined); // "undefined"
utag.ut.typeOf(obj.cb);    // "function"
```
