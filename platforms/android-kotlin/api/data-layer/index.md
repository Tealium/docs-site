---
title: DataLayer
description: Reference guide for DataLayer class and methods provided by Tealium for Android (Kotlin).
url: https://docs.tealium.com/platforms/android-kotlin/api/data-layer/
---
## Class: `DataLayer`

This class provides persistent and volatile data storage for key-value data to be included with every tracked event.

The following methods are available for the `DataLayer` class.

| Method                                  | Description                                  |
|:----------------------------------------|:---------------------------------------------|
| [`all()`](#all)                         | Retrieves all key-value pairs currently in the data layer |
| [`clear()`](#clear)                     | Removes all data from the data layer         |
| [`contains()`](#contains)               | Returns true if the key exists in the data layer |
| [`count()`](#count)                     | Returns a count of all values currently in the data layer |
| [`get()`](#get)                         | Retrieves the value for the given key        |
| [`getBoolean()`](#getboolean)           | Retrieves the `Boolean` for the given key    |
| [`getBooleanArray()`](#getbooleanarray) | Retrieves the `Array&lt;Boolean&gt;` for the given key |
| [`getDouble()`](#getdouble)             | Retrieves the `Double` for the given key     |
| [`getDoubleArray()`](#getdoublearray)   | Retrieves the `Array&lt;Double&gt;` for the given key |
| [`getInt()`](#getint)                   | Retrieves the `Int` for the given key        |
| [`getIntArray()`](#getintarray)         | Retrieves the `Array&lt;Int&gt;` for the given key |
| [`getJsonArray()`](#getjsonarray)       | Retrieves the `org.json.JSONArray` for the given key |
| [`getJsonObject()`](#getjsonobject)     | Retrieves the `org.json.JSONObject` for the given key |
| [`getLong()`](#getlong)               | Retrieves the `Long` for the given key       |
| [`getLongArray()`](#getlongarray)       | Retrieves the `Array&lt;Long&gt;` for the given key |
| [`getString()`](#getstring)             | Retrieves the `String` for the given key     |
| [`getStringArray()`](#getstringarray)   | Retrieves the `Array&lt;String&gt;` for the given key |
| [`keys()`](#keys)                       | Returns a `List&lt;String&gt;` of all keys currently in the data layer |
| [`putBoolean()`](#putboolean)           | Stores a `Boolean` for the given key         |
| [`putBooleanArray()`](#putbooleanarray) | Stores a `Array&lt;Boolean&gt;` for the given key  |
| [`putDouble()`](#putdouble)             | Stores a `Double` for the given key          |
| [`putDoubleArray()`](#putdoublearray)   | Stores a `Array&lt;Double&gt;` for the given key   |
| [`putInt()`](#putint)                   | Stores an `Int` for the given key            |
| [`putIntArray()`](#putintarray)         | Stores an `Array&lt;Int&gt;` for the given key     |
| [`putJsonArray()`](#putjsonarray)       | Stores a `org.json.JSONArray` for the given key |
| [`putJsonObject()`](#putjsonobject)     | Stores a `org.json.JSONObject` for the given key |
| [`putLong()`](#putlong)                 | Stores a `Long` for the given key            |
| [`putLongArray()`](#putlongarray)       | Stores a `Array&lt;Long&gt;` for the given key     |
| [`putString()`](#putstring)             | Stores a `String` for the given key          |
| [`putStringArray()`](#putstringarray)   | Stores a `Array&lt;String&gt;` for the given key   |
| [`remove()`](#remove)                   | Removes the value for the given key          |

### `all`

Returns a map of all the key-value pairs currently stored in the data layer.

```java
val dataLayer = tealium.dataLayer.all()
```

### `clear`

Clears all items currently stored in the data layer.

```java
tealium.dataLayer.clear()
```

### `contains`

Returns `true` if the given key exists in the data layer, otherwise `false`.

| Parameters | Type     | Description                            |
|:-----------|:---------|:---------------------------------------|
| `key`      | `String` | The name of the variable to be removed |

```java
tealium.dataLayer.contains(&#34;KEY&#34;)
```

### `count`

Returns a the number of items currently stored in the data layer.

```java
tealium.dataLayer.count()
```

### `get`

Retrieves the value at the given key. Return types match one of the allowed types, else `null` is returned.

The method gets a variable of type `Any` (equivalent to Java’s `Object`). Inspect the type by using type casting or `instanceof` to use the data type appropriately.

| Parameters | Type     | Description                              |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | The name of the variable to be retrieved |

```java
val any = tealium.dataLayer.get(&#34;KEY&#34;)
```

### `getBoolean`

Retrieves the `Boolean` value at the given key. If the value at this key is not a `Boolean`, then `null` is returned.

| Parameters | Type     | Description                              |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | The name of the variable to be retrieved |

```java
val bool = tealium.dataLayer.getBoolean(&#34;KEY&#34;)
```

### `getBooleanArray`

Retrieves the `Array&lt;Boolean&gt;` value at the given key. If the value at this key is not a `Array&lt;Boolean&gt;`, then `null` is returned.

| Parameters | Type     | Description                              |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | The name of the variable to be retrieved |

```java
val booleanArray = tealium.dataLayer.getBooleanArray(&#34;KEY&#34;)
```

### `getDouble`

Retrieves the `Double` value at the given key. If the value at this key is not a `Double`, then `null` is returned.

| Parameters | Type     | Description                              |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | The name of the variable to be retrieved |

```java
val double = tealium.dataLayer.getDouble(&#34;KEY&#34;)
```

### `getDoubleArray`

Retrieves the `Array&lt;Double&gt;` value at the given key. If the value at this key is not a `Array&lt;Double&gt;`, then `null` is returned.

| Parameters | Type     | Description                              |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | The name of the variable to be retrieved |

```java
val doubleArray = tealium.dataLayer.getDoubleArray(&#34;KEY&#34;)
```

### `getInt`

Retrieves the `Int` value at the given key. If the value at this key is not a `Int`, then `null` is returned.

| Parameters | `Type`   | Description                              |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | The name of the variable to be retrieved |

```java
val int = tealium.dataLayer.getInt(&#34;KEY&#34;)
```

### `getIntArray`

Retrieves the `Array&lt;Int&gt;` value at the given key. If the value at this key is not a `Array&lt;Int&gt;`, then `null` is returned.

| Parameters | Type     | Description                              |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | The name of the variable to be retrieved |

```java
val intArray = tealium.dataLayer.getIntArray(&#34;KEY&#34;)
```

### `getJsonArray`

Retrieves the `org.json.JSONArray` value at the given key. If the value at this key is not a JSONArray, then `null` is returned.

| Parameters | Type     | Description                              |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | The name of the variable to be retrieved |

```java
val jsonArray = tealium.dataLayer.getJsonArray(&#34;KEY&#34;)
```

### `getJsonObject`

Retrieves the `org.json.JSONObject` value at the given key. If the value at this key is not a JSONObject, then `null` is returned.

| Parameters | Type     | Description                              |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | The name of the variable to be retrieved |

```java
val jsonObject = tealium.dataLayer.getJsonObject(&#34;KEY&#34;)
```

### `getLong`

Retrieves the `Long` value at the given key. If the value at this key is not a `Long`, then `null` is returned.

| Parameters | Type     | Description                              |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | The name of the variable to be retrieved |

```java
val long = tealium.dataLayer.getLong(&#34;KEY&#34;)
```

### `getLongArray`

Retrieves the `Array&lt;Long&gt;` value at the given key. If the value at this key is not a `Array&lt;Long&gt;`, then `null` is returned.

| Parameters | Type     | Description                              |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | The name of the variable to be retrieved |

```java
val longArray = tealium.dataLayer.getLongArray(&#34;KEY&#34;)
```

### `getString`

Retrieves the `String` value at the given key. If the value at this key is not a `String`, then `null` is returned.

| Parameters | Type     | Description                              |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | The name of the variable to be retrieved |

```java
val string = tealium.dataLayer.getString(&#34;KEY&#34;)
```

### `getStringArray`

Retrieves the `Array&lt;String&gt;` value at the given key. If the value at this key is not a `Array&lt;String&gt;`, then `null` is returned.

| Parameters | Type     | Description                              |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | The name of the variable to be retrieved |

```java
val stringArray = tealium.dataLayer.getStringArray(&#34;KEY&#34;)
```

### `keys`

Returns the `List&lt;String&gt;` of all keys currently stored in the data layer

```java
tealium.dataLayer.keys()
```

### `putBoolean`

Stores a `Boolean` value at the given key.

| Parameters | Type      | Description                                 |
|:-----------|:----------|:--------------------------------------------|
| `key`      | `String`  | The name of the variable being stored       |
| `value`    | `Boolean` | The `Boolean` value to be store             |
| `expiry`   | `Expiry`  | (Optional) The Expiry time of this variable |

```java
tealium.dataLayer.putBoolean(&#34;KEY&#34;, true, Expiry.FOREVER)
```

### `putBooleanArray`

Stores a `Array&lt;Boolean&gt;` value at the given key.

| Parameters | Type             | Description                                 |
|:-----------|:-----------------|:--------------------------------------------|
| `key`      | `String`         | The name of the variable being stored       |
| `value`    | `Array&lt;Boolean&gt;` | The `Array&lt;Boolean&gt;` value to be store      |
| `expiry`   | `Expiry`         | (Optional) The Expiry time of this variable |

```java
tealium.dataLayer.putBooleanArray(&#34;KEY&#34;, arrayOf(true, false, true), Expiry.FOREVER)
```

### `putDouble`

Stores a `Double` value at the given key.

| Parameters | Type     | Description                                 |
|:-----------|:---------|:--------------------------------------------|
| `key`      | `String` | The name of the variable being stored       |
| `value`    | `Double` | The `Double` value to be store              |
| `expiry`   | `Expiry` | (Optional) The Expiry time of this variable |

```java
tealium.dataLayer.putDouble(&#34;KEY&#34;, 10.5, Expiry.FOREVER)
```

### `putDoubleArray`

Stores a `Array&lt;Double&gt;` value at the given key.

| Parameters | Type            | Description                                 |
|:-----------|:----------------|:--------------------------------------------|
| `key`      | `String`        | The name of the variable being stored       |
| `value`    | `Array&lt;Double&gt;` | The `Array&lt;Double&gt;` value to be store       |
| `expiry`   | `Expiry`        | (Optional) The Expiry time of this variable |

```java
tealium.dataLayer.putDoubleArray(&#34;KEY&#34;, arrayOf(0.1, 10.5), Expiry.FOREVER)
```


### `putInt`

Stores a `Int` value at the given key.

| Parameters | Type     | Description                                 |
|:-----------|:---------|:--------------------------------------------|
| `key`      | `String` | The name of the variable being stored       |
| `value`    | `Int`    | The `Int` value to be store                 |
| `expiry`   | `Expiry` | (Optional) The Expiry time of this variable |

```java
tealium.dataLayer.putInt(&#34;KEY&#34;, 10, Expiry.FOREVER)
```

### `putIntArray`

Stores a `Array&lt;Int&gt;` value at the given key.

| Parameters | Type         | Description                                 |
|:-----------|:-------------|:--------------------------------------------|
| `key`      | `String`     | The name of the variable being stored       |
| `value`    | `Array&lt;Int&gt;` | The `Array&lt;Int&gt;` value to be store          |
| `expiry`   | `Expiry`     | (Optional) The Expiry time of this variable |

```java
tealium.dataLayer.putIntArray(&#34;KEY&#34;, arrayOf(100, Int.MAX_VALUE), Expiry.FOREVER)
```

### `putJsonArray`

Stores an `org.json.JSONArray` value at the given key.

| Parameters | Type        | Description                                 |
|:-----------|:------------|:--------------------------------------------|
| `key`      | `String`    | The name of the variable being stored       |
| `value`    | `JSONArray` | The `org.json.JSONArray` value to be store  |
| `expiry`   | `Expiry`    | (Optional) The Expiry time of this variable |

```java
val my_list = new JSONArray();
my_list.put(&#34;value_1&#34;);
my_list.put(&#34;value_2&#34;);
tealium.dataLayer.putJsonArray(&#34;KEY&#34;, my_list, Expiry.FOREVER);
```

### `putJsonObject`

Stores an `org.json.JSONObject` value at the given key.

| Parameters | Type         | Description                                 |
|:-----------|:-------------|:--------------------------------------------|
| `key`      | `String`     | The name of the variable being stored       |
| `value`    | `JSONObject` | The `org.json.JSONObject` value to be store |
| `expiry`   | `Expiry`     | (Optional) The Expiry time of this variable |

```java
val my_obj = new JSONObject();
my_obj.put(&#34;key&#34;, &#34;value&#34;);
tealium.dataLayer.putJsonObject(&#34;KEY&#34;, my_obj, Expiry.FOREVER);
```

### `putLong`

Stores a `Long` value at the given key.

| Parameters | Type     | Description                                 |
|:-----------|:---------|:--------------------------------------------|
| `key`      | `String` | The name of the variable being stored       |
| `value`    | `Long`   | The `Long` value to be store                |
| `expiry`   | `Expiry` | (Optional) The Expiry time of this variable |

```java
tealium.dataLayer.putLong(&#34;KEY&#34;, Long.MAX_VALUE, Expiry.FOREVER)
```

### `putLongArray`

Stores a `Array&lt;Long&gt;` value at the given key.

| Parameters | Type          | Description                                 |
|:-----------|:--------------|:--------------------------------------------|
| `key`      | `String`      | The name of the variable being stored       |
| `value`    | `Array&lt;Long&gt;` | The `Array&lt;Long&gt;` value to be store         |
| `expiry`   | `Expiry`      | (Optional) The Expiry time of this variable |

```java
tealium.dataLayer.putLongArray(&#34;KEY&#34;, arrayOf(1000L, Long.MAX_VALUE), Expiry.FOREVER)
```

### `putString`

Stores a `String` value at the given key.

| Parameters | Type     | Description                                 |
|:-----------|:---------|:--------------------------------------------|
| `key`      | `String` | The name of the variable being stored       |
| `value`    | `String` | The `String` value to be store              |
| `expiry`   | `Expiry` | (Optional) The Expiry time of this variable |

```java
tealium.dataLayer.putString(&#34;KEY&#34;, &#34;String Value&#34;, Expiry.FOREVER)
```

### `putStringArray`

Stores a `Array&lt;String&gt;` value at the given key.

| Parameters | Type            | Description                                 |
|:-----------|:----------------|:--------------------------------------------|
| `key`      | `String`        | The name of the variable being stored       |
| `value`    | `Array&lt;String&gt;` | The `Array&lt;String&gt;` value to be store       |
| `expiry`   | `Expiry`        | (Optional) The Expiry time of this variable |

```java
tealium.dataLayer.putStringArray(&#34;KEY&#34;,
    arrayOf(&#34;String 1&#34;, &#34;String 2&#34;), Expiry.FOREVER)
```

### `remove`

Removes the value stored at the given key

| Parameters | Type     | Description                            |
|:-----------|:---------|:---------------------------------------|
| `key`      | `String` | The name of the variable to be removed |

```java
tealium.dataLayer.remove(&#34;KEY&#34;)
```
