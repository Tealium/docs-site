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
utag.ut.decode(&#34;Tealium%20Developer%20Docs!&#34;);     // &#34;Tealium Developer Docs!&#34;
utag.ut.decode(&#34;https%3A%2F%2Fdocs.tealium.com&#34;);  // &#34;https://docs.tealium.com&#34;
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
utag.ut.encode(&#34;Tealium Developer Docs!&#34;);   // &#34;Tealium%20Developer%20Docs!&#34;
utag.ut.encode(&#34;https://docs.tealium.com&#34;);  // &#34;https%3A%2F%2Fdocs.tealium.com&#34;
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
utag.ut.flatten({&#34;order_id&#34;: &#34;0123567&#34;, &#34;cart&#34;: {&#34;total_items&#34;: 3, &#34;total_amount&#34;: 123.45},&#34;order_tax&#34;: 9.97});
// {order_id: &#34;0123567&#34;, cart.total_items: 3, cart.total_amount: 123.45, order_tax: 9.97}
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

utag.ut.hasOwn(obj, &#39;x&#39;);          // true - x is a local property of obj
utag.ut.hasOwn(obj, &#39;y&#39;);          // false - obj doesn&#39;t have a property y
```

## `utag.ut.isEmpty()`

Returns a boolean `true` indicating the argument is empty, or boolean `false` if not empty.  It first determines the data type by using the `utag.ut.typeOf()` function, and returns the following based on the type:

| Type | Return value description |
| --- | --- |
| `number` | Returns the value of the JavaScript function `isNaN()` |
| `boolean` | Returns `false` |
| `String` | Returns `true` if the string object&#39;s `.length` field is 0 |
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
utag.ut.isEmpty(&#34;Tealium&#34;); // false
utag.ut.isEmpty(&#34;&#34;);        // true

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
utag.ut.isEmptyObject({ foo: &#34;bar&#34; });  // false
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
| `type` | The type of tag to load: &#34;iframe&#34;, &#34;img&#34;, or &#34;script&#34; (default)|
| `id` | (Optional) The element ID |
| `cb` | (Optional) A callback function |
| `attrs`| (Optional) An object of additional HTML element attributes |

Example:

```js
utag.ut.loader({
  type: &#34;iframe&#34;,
  src: &#34;https://example.com/path/file.js&#34;,
  id: &#34;teal-tag1&#34;,
  cb: function() {},
  attrs: {&#34;async&#34;:&#34;true&#34;}})
// Results in the following HTML element:
// &lt;iframe id=&#34;teal-tag1&#34;  async=&#34;true&#34; height=&#34;1&#34; width=&#34;1&#34; style=&#34;display:none&#34;
//   src=&#34;https://example.com/path/file.js&#34;&gt; &lt;/iframe&gt;
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
foo = { &#34;key1&#34;:&#34;value1&#34;, &#34;key2&#34;:&#34;value2&#34; }
bar = { &#34;key1&#34;:&#34;value4&#34;, &#34;key3&#34;:&#34;value3&#34; }
utag.ut.merge(foo, bar, 0)
// foo: {key1: &#34;value1&#34;, key2: &#34;value2&#34;, key3: &#34;value3&#34;}
// bar: {key1: &#34;value4&#34;, key3: &#34;value3&#34;}

foo = { &#34;key1&#34;:&#34;value1&#34;, &#34;key2&#34;:&#34;value2&#34; }
bar = { &#34;key1&#34;:&#34;value4&#34;, &#34;key3&#34;:&#34;value3&#34; }
utag.ut.merge(foo, bar, 1)
// foo: {key1: &#34;value4&#34;, key2: &#34;value2&#34;, key3: &#34;value3&#34;}
// bar: {key1: &#34;value4&#34;, key3: &#34;value3&#34;}
```

## `utag.ut.typeOf()`

Returns an argument&#39;s variable type as a `String`.

```js
utag.ut.typeOf(arg)
```

| Parameter | Type | Description |
| --- | --- | --- |
| `arg` | Any type | The argument to determine the type of |

Examples:
```js
utag.ut.typeOf(5);         // &#34;number&#34;
utag.ut.typeOf(&#34;Tealium&#34;); // &#34;string&#34;
utag.ut.typeOf(imgObj);    // &#34;htmlimagelement&#34;
utag.ut.typeOf(obj);       // &#34;object&#34;
utag.ut.typeOf(null);      // &#34;null&#34;
utag.ut.typeOf(undefined); // &#34;undefined&#34;
utag.ut.typeOf(obj.cb);    // &#34;function&#34;
```
