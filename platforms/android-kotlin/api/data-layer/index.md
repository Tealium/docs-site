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
| [`getBooleanArray()`](#getbooleanarray) | Retrieves the `Array<Boolean>` for the given key |
| [`getDouble()`](#getdouble)             | Retrieves the `Double` for the given key     |
| [`getDoubleArray()`](#getdoublearray)   | Retrieves the `Array<Double>` for the given key |
| [`getInt()`](#getint)                   | Retrieves the `Int` for the given key        |
| [`getIntArray()`](#getintarray)         | Retrieves the `Array<Int>` for the given key |
| [`getJsonArray()`](#getjsonarray)       | Retrieves the `org.json.JSONArray` for the given key |
| [`getJsonObject()`](#getjsonobject)     | Retrieves the `org.json.JSONObject` for the given key |
| [`getLong()`](#getlong)               | Retrieves the `Long` for the given key       |
| [`getLongArray()`](#getlongarray)       | Retrieves the `Array<Long>` for the given key |
| [`getString()`](#getstring)             | Retrieves the `String` for the given key     |
| [`getStringArray()`](#getstringarray)   | Retrieves the `Array<String>` for the given key |
| [`keys()`](#keys)                       | Returns a `List<String>` of all keys currently in the data layer |
| [`putBoolean()`](#putboolean)           | Stores a `Boolean` for the given key         |
| [`putBooleanArray()`](#putbooleanarray) | Stores a `Array<Boolean>` for the given key  |
| [`putDouble()`](#putdouble)             | Stores a `Double` for the given key          |
| [`putDoubleArray()`](#putdoublearray)   | Stores a `Array<Double>` for the given key   |
| [`putInt()`](#putint)                   | Stores an `Int` for the given key            |
| [`putIntArray()`](#putintarray)         | Stores an `Array<Int>` for the given key     |
| [`putJsonArray()`](#putjsonarray)       | Stores a `org.json.JSONArray` for the given key |
| [`putJsonObject()`](#putjsonobject)     | Stores a `org.json.JSONObject` for the given key |
| [`putLong()`](#putlong)                 | Stores a `Long` for the given key            |
| [`putLongArray()`](#putlongarray)       | Stores a `Array<Long>` for the given key     |
| [`putString()`](#putstring)             | Stores a `String` for the given key          |
| [`putStringArray()`](#putstringarray)   | Stores a `Array<String>` for the given key   |
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
tealium.dataLayer.contains("KEY")
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
val any = tealium.dataLayer.get("KEY")
```

### `getBoolean`

Retrieves the `Boolean` value at the given key. If the value at this key is not a `Boolean`, then `null` is returned.

| Parameters | Type     | Description                              |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | The name of the variable to be retrieved |

```java
val bool = tealium.dataLayer.getBoolean("KEY")
```

### `getBooleanArray`

Retrieves the `Array<Boolean>` value at the given key. If the value at this key is not a `Array<Boolean>`, then `null` is returned.

| Parameters | Type     | Description                              |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | The name of the variable to be retrieved |

```java
val booleanArray = tealium.dataLayer.getBooleanArray("KEY")
```

### `getDouble`

Retrieves the `Double` value at the given key. If the value at this key is not a `Double`, then `null` is returned.

| Parameters | Type     | Description                              |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | The name of the variable to be retrieved |

```java
val double = tealium.dataLayer.getDouble("KEY")
```

### `getDoubleArray`

Retrieves the `Array<Double>` value at the given key. If the value at this key is not a `Array<Double>`, then `null` is returned.

| Parameters | Type     | Description                              |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | The name of the variable to be retrieved |

```java
val doubleArray = tealium.dataLayer.getDoubleArray("KEY")
```

### `getInt`

Retrieves the `Int` value at the given key. If the value at this key is not a `Int`, then `null` is returned.

| Parameters | `Type`   | Description                              |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | The name of the variable to be retrieved |

```java
val int = tealium.dataLayer.getInt("KEY")
```

### `getIntArray`

Retrieves the `Array<Int>` value at the given key. If the value at this key is not a `Array<Int>`, then `null` is returned.

| Parameters | Type     | Description                              |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | The name of the variable to be retrieved |

```java
val intArray = tealium.dataLayer.getIntArray("KEY")
```

### `getJsonArray`

Retrieves the `org.json.JSONArray` value at the given key. If the value at this key is not a JSONArray, then `null` is returned.

| Parameters | Type     | Description                              |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | The name of the variable to be retrieved |

```java
val jsonArray = tealium.dataLayer.getJsonArray("KEY")
```

### `getJsonObject`

Retrieves the `org.json.JSONObject` value at the given key. If the value at this key is not a JSONObject, then `null` is returned.

| Parameters | Type     | Description                              |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | The name of the variable to be retrieved |

```java
val jsonObject = tealium.dataLayer.getJsonObject("KEY")
```

### `getLong`

Retrieves the `Long` value at the given key. If the value at this key is not a `Long`, then `null` is returned.

| Parameters | Type     | Description                              |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | The name of the variable to be retrieved |

```java
val long = tealium.dataLayer.getLong("KEY")
```

### `getLongArray`

Retrieves the `Array<Long>` value at the given key. If the value at this key is not a `Array<Long>`, then `null` is returned.

| Parameters | Type     | Description                              |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | The name of the variable to be retrieved |

```java
val longArray = tealium.dataLayer.getLongArray("KEY")
```

### `getString`

Retrieves the `String` value at the given key. If the value at this key is not a `String`, then `null` is returned.

| Parameters | Type     | Description                              |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | The name of the variable to be retrieved |

```java
val string = tealium.dataLayer.getString("KEY")
```

### `getStringArray`

Retrieves the `Array<String>` value at the given key. If the value at this key is not a `Array<String>`, then `null` is returned.

| Parameters | Type     | Description                              |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | The name of the variable to be retrieved |

```java
val stringArray = tealium.dataLayer.getStringArray("KEY")
```

### `keys`

Returns the `List<String>` of all keys currently stored in the data layer

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
tealium.dataLayer.putBoolean("KEY", true, Expiry.FOREVER)
```

### `putBooleanArray`

Stores a `Array<Boolean>` value at the given key.

| Parameters | Type             | Description                                 |
|:-----------|:-----------------|:--------------------------------------------|
| `key`      | `String`         | The name of the variable being stored       |
| `value`    | `Array<Boolean>` | The `Array<Boolean>` value to be store      |
| `expiry`   | `Expiry`         | (Optional) The Expiry time of this variable |

```java
tealium.dataLayer.putBooleanArray("KEY", arrayOf(true, false, true), Expiry.FOREVER)
```

### `putDouble`

Stores a `Double` value at the given key.

| Parameters | Type     | Description                                 |
|:-----------|:---------|:--------------------------------------------|
| `key`      | `String` | The name of the variable being stored       |
| `value`    | `Double` | The `Double` value to be store              |
| `expiry`   | `Expiry` | (Optional) The Expiry time of this variable |

```java
tealium.dataLayer.putDouble("KEY", 10.5, Expiry.FOREVER)
```

### `putDoubleArray`

Stores a `Array<Double>` value at the given key.

| Parameters | Type            | Description                                 |
|:-----------|:----------------|:--------------------------------------------|
| `key`      | `String`        | The name of the variable being stored       |
| `value`    | `Array<Double>` | The `Array<Double>` value to be store       |
| `expiry`   | `Expiry`        | (Optional) The Expiry time of this variable |

```java
tealium.dataLayer.putDoubleArray("KEY", arrayOf(0.1, 10.5), Expiry.FOREVER)
```


### `putInt`

Stores a `Int` value at the given key.

| Parameters | Type     | Description                                 |
|:-----------|:---------|:--------------------------------------------|
| `key`      | `String` | The name of the variable being stored       |
| `value`    | `Int`    | The `Int` value to be store                 |
| `expiry`   | `Expiry` | (Optional) The Expiry time of this variable |

```java
tealium.dataLayer.putInt("KEY", 10, Expiry.FOREVER)
```

### `putIntArray`

Stores a `Array<Int>` value at the given key.

| Parameters | Type         | Description                                 |
|:-----------|:-------------|:--------------------------------------------|
| `key`      | `String`     | The name of the variable being stored       |
| `value`    | `Array<Int>` | The `Array<Int>` value to be store          |
| `expiry`   | `Expiry`     | (Optional) The Expiry time of this variable |

```java
tealium.dataLayer.putIntArray("KEY", arrayOf(100, Int.MAX_VALUE), Expiry.FOREVER)
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
my_list.put("value_1");
my_list.put("value_2");
tealium.dataLayer.putJsonArray("KEY", my_list, Expiry.FOREVER);
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
my_obj.put("key", "value");
tealium.dataLayer.putJsonObject("KEY", my_obj, Expiry.FOREVER);
```

### `putLong`

Stores a `Long` value at the given key.

| Parameters | Type     | Description                                 |
|:-----------|:---------|:--------------------------------------------|
| `key`      | `String` | The name of the variable being stored       |
| `value`    | `Long`   | The `Long` value to be store                |
| `expiry`   | `Expiry` | (Optional) The Expiry time of this variable |

```java
tealium.dataLayer.putLong("KEY", Long.MAX_VALUE, Expiry.FOREVER)
```

### `putLongArray`

Stores a `Array<Long>` value at the given key.

| Parameters | Type          | Description                                 |
|:-----------|:--------------|:--------------------------------------------|
| `key`      | `String`      | The name of the variable being stored       |
| `value`    | `Array<Long>` | The `Array<Long>` value to be store         |
| `expiry`   | `Expiry`      | (Optional) The Expiry time of this variable |

```java
tealium.dataLayer.putLongArray("KEY", arrayOf(1000L, Long.MAX_VALUE), Expiry.FOREVER)
```

### `putString`

Stores a `String` value at the given key.

| Parameters | Type     | Description                                 |
|:-----------|:---------|:--------------------------------------------|
| `key`      | `String` | The name of the variable being stored       |
| `value`    | `String` | The `String` value to be store              |
| `expiry`   | `Expiry` | (Optional) The Expiry time of this variable |

```java
tealium.dataLayer.putString("KEY", "String Value", Expiry.FOREVER)
```

### `putStringArray`

Stores a `Array<String>` value at the given key.

| Parameters | Type            | Description                                 |
|:-----------|:----------------|:--------------------------------------------|
| `key`      | `String`        | The name of the variable being stored       |
| `value`    | `Array<String>` | The `Array<String>` value to be store       |
| `expiry`   | `Expiry`        | (Optional) The Expiry time of this variable |

```java
tealium.dataLayer.putStringArray("KEY",
    arrayOf("String 1", "String 2"), Expiry.FOREVER)
```

### `remove`

Removes the value stored at the given key

| Parameters | Type     | Description                            |
|:-----------|:---------|:---------------------------------------|
| `key`      | `String` | The name of the variable to be removed |

```java
tealium.dataLayer.remove("KEY")
```
