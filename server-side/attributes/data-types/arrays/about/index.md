---
title: About arrays
description: This article describes how to use the data types array of strings, array of numbers, and array of booleans.
url: https://docs.tealium.com/server-side/attributes/data-types/arrays/about/
---
## How it works

Arrays are used to store a list of values. Whereas a string or number attribute can only contain a single value, such as `"Home Page"` or `12.95`, an array can contain multiple values, such as `["Pants", "Shirts"]` or `[5.99, 12.95]`. Arrays are available for the [number](), [string](), and [boolean]() attribute data types.

Arrays are represented in JSON format in all examples.

```json
["Pants", "Shirts", "Shoes"]
[2, 4, 6]
[true, false, false]
[]
```


<blockquote>
Arrays can contain duplicate values.
</blockquote>


### Size limits

Arrays are limited to 30,000 entries. The size of each boolean and number entry is not limited, but string entries are limited as follows:

* EventStream string attributes have a maximum length of 1,500 characters. Strings are truncated to 1,500 characters if they exceed this limit.
* AudienceStream string attributes values have a maximum length of 1,000 characters. If an enrichment results in a string larger than 1,000 characters, the value is not saved.

These attributes are limited by the maximum size of the profile after encryption and compression (400 KB).