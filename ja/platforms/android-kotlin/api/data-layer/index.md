---
title: DataLayer
description: TealiumのAndroid（Kotlin）用DataLayerクラスとメソッドのリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/android-kotlin/api/data-layer/
---
## クラス: `DataLayer`

このクラスは、追跡されるすべてのイベントに含まれるキーと値のデータのための永続的および揮発性のデータ保存を提供します。

`DataLayer` クラスには以下のメソッドが用意されています。

| メソッド                                  | 説明                                  |
|:----------------------------------------|:---------------------------------------------|
| [`all()`](#all)                         | データレイヤーに現在存在するすべてのキーと値のペアを取得します |
| [`clear()`](#clear)                     | データレイヤーからすべてのデータを削除します         |
| [`contains()`](#contains)               | キーがデータレイヤーに存在する場合はtrueを返します |
| [`count()`](#count)                     | データレイヤーに現在存在するすべての値の数を返します |
| [`get()`](#get)                         | 指定されたキーの値を取得します        |
| [`getBoolean()`](#getboolean)           | 指定されたキーの`Boolean`を取得します    |
| [`getBooleanArray()`](#getbooleanarray) | 指定されたキーの`Array<Boolean>`を取得します |
| [`getDouble()`](#getdouble)             | 指定されたキーの`Double`を取得します     |
| [`getDoubleArray()`](#getdoublearray)   | 指定されたキーの`Array<Double>`を取得します |
| [`getInt()`](#getint)                   | 指定されたキーの`Int`を取得します        |
| [`getIntArray()`](#getintarray)         | 指定されたキーの`Array<Int>`を取得します |
| [`getJsonArray()`](#getjsonarray)       | 指定されたキーの`org.json.JSONArray`を取得します |
| [`getJsonObject()`](#getjsonobject)     | 指定されたキーの`org.json.JSONObject`を取得します |
| [`getLong()`](#getlong)                 | 指定されたキーの`Long`を取得します       |
| [`getLongArray()`](#getlongarray)       | 指定されたキーの`Array<Long>`を取得します |
| [`getString()`](#getstring)             | 指定されたキーの`String`を取得します     |
| [`getStringArray()`](#getstringarray)   | 指定されたキーの`Array<String>`を取得します |
| [`keys()`](#keys)                       | データレイヤーに現在存在するすべてのキーの`List<String>`を返します |
| [`putBoolean()`](#putboolean)           | 指定されたキーに`Boolean`を格納します         |
| [`putBooleanArray()`](#putbooleanarray) | 指定されたキーに`Array<Boolean>`を格納します  |
| [`putDouble()`](#putdouble)             | 指定されたキーに`Double`を格納します          |
| [`putDoubleArray()`](#putdoublearray)   | 指定されたキーに`Array<Double>`を格納します   |
| [`putInt()`](#putint)                   | 指定されたキーに`Int`を格納します            |
| [`putIntArray()`](#putintarray)         | 指定されたキーに`Array<Int>`を格納します     |
| [`putJsonArray()`](#putjsonarray)       | 指定されたキーに`org.json.JSONArray`を格納します |
| [`putJsonObject()`](#putjsonobject)     | 指定されたキーに`org.json.JSONObject`を格納します |
| [`putLong()`](#putlong)                 | 指定されたキーに`Long`を格納します            |
| [`putLongArray()`](#putlongarray)       | 指定されたキーに`Array<Long>`を格納します     |
| [`putString()`](#putstring)             | 指定されたキーに`String`を格納します          |
| [`putStringArray()`](#putstringarray)   | 指定されたキーに`Array<String>`を格納します   |
| [`remove()`](#remove)                   | 指定されたキーの値を削除します          |

### `all`

データレイヤーに現在格納されているすべてのキーと値のペアのマップを返します。

```java
val dataLayer = tealium.dataLayer.all()
```

### `clear`

データレイヤーに現在格納されているすべてのアイテムをクリアします。

```java
tealium.dataLayer.clear()
```

### `contains`

指定されたキーがデータレイヤーに存在する場合は`true`を返し、そうでない場合は`false`を返します。

| パラメータ | タイプ     | 説明                            |
|:-----------|:---------|:---------------------------------------|
| `key`      | `String` | 削除する変数の名前 |

```java
tealium.dataLayer.contains("KEY")
```

### `count`

データレイヤーに現在格納されているアイテムの数を返します。

```java
tealium.dataLayer.count()
```

### `get`

指定されたキーで値を取得します。返される型は許可されている型のいずれかに一致しますが、そうでない場合は`null`が返されます。

このメソッドは`Any`タイプ（Javaの`Object`に相当）の変数を取得します。データタイプを適切に使用するために型キャスティングまたは`instanceof`を使用して型を検査します。

| パラメータ | タイプ     | 説明                              |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | 取得する変数の名前 |

```java
val any = tealium.dataLayer.get("KEY")
```

### `getBoolean`

指定されたキーで`Boolean`値を取得します。このキーの値が`Boolean`でない場合は`null`が返されます。

| パラメータ | タイプ     | 説明                              |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | 取得する変数の名前 |

```java
val bool = tealium.dataLayer.getBoolean("KEY")
```

### `getBooleanArray`

指定されたキーで`Array<Boolean>`値を取得します。このキーの値が`Array<Boolean>`でない場合は`null`が返されます。

| パラメータ | タイプ     | 説明                              |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | 取得する変数の名前 |

```java
val booleanArray = tealium.dataLayer.getBooleanArray("KEY")
```

### `getDouble`

指定されたキーで`Double`値を取得します。このキーの値が`Double`でない場合は`null`が返されます。

| パラメータ | タイプ     | 説明                              |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | 取得する変数の名前 |

```java
val double = tealium.dataLayer.getDouble("KEY")
```

### `getDoubleArray`

指定されたキーで`Array<Double>`値を取得します。このキーの値が`Array<Double>`でない場合は`null`が返されます。

| パラメータ | タイプ     | 説明                              |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | 取得する変数の名前 |

```java
val doubleArray = tealium.dataLayer.getDoubleArray("KEY")
```

### `getInt`

指定されたキーで`Int`値を取得します。このキーの値が`Int`でない場合は`null`が返されます。

| パラメータ | `タイプ`   | 説明                              |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | 取得する変数の名前 |

```java
val int = tealium.dataLayer.getInt("KEY")
```

### `getIntArray`

指定されたキーで`Array<Int>`値を取得します。このキーの値が`Array<Int>`でない場合は`null`が返されます。

| パラメータ | タイプ     | 説明                              |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | 取得する変数の名前 |

```java
val intArray = tealium.dataLayer.getIntArray("KEY")
```

### `getJsonArray`

指定されたキーで`org.json.JSONArray`値を取得します。このキーの値がJSONArrayでない場合は`null`が返されます。

| パラメータ | タイプ     | 説明                              |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | 取得する変数の名前 |

```java
val jsonArray = tealium.dataLayer.getJsonArray("KEY")
```
### `getJsonObject`

指定されたキーで `org.json.JSONObject` の値を取得します。このキーの値が JSONObject でない場合は、`null` が返されます。

| パラメータ | タイプ     | 説明                                      |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | 取得する変数の名前                         |

```java
val jsonObject = tealium.dataLayer.getJsonObject("KEY")
```

### `getLong`

指定されたキーで `Long` の値を取得します。このキーの値が `Long` でない場合は、`null` が返されます。

| パラメータ | タイプ     | 説明                                      |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | 取得する変数の名前                         |

```java
val long = tealium.dataLayer.getLong("KEY")
```

### `getLongArray`

指定されたキーで `Array<Long>` の値を取得します。このキーの値が `Array<Long>` でない場合は、`null` が返されます。

| パラメータ | タイプ     | 説明                                      |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | 取得する変数の名前                         |

```java
val longArray = tealium.dataLayer.getLongArray("KEY")
```

### `getString`

指定されたキーで `String` の値を取得します。このキーの値が `String` でない場合は、`null` が返されます。

| パラメータ | タイプ     | 説明                                      |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | 取得する変数の名前                         |

```java
val string = tealium.dataLayer.getString("KEY")
```

### `getStringArray`

指定されたキーで `Array<String>` の値を取得します。このキーの値が `Array<String>` でない場合は、`null` が返されます。

| パラメータ | タイプ     | 説明                                      |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | 取得する変数の名前                         |

```java
val stringArray = tealium.dataLayer.getStringArray("KEY")
```

### `keys`

データレイヤーに現在保存されているすべてのキーの `List<String>` を返します

```java
tealium.dataLayer.keys()
```

### `putBoolean`

指定されたキーに `Boolean` 値を保存します。

| パラメータ | タイプ      | 説明                                       |
|:-----------|:----------|:--------------------------------------------|
| `key`      | `String`  | 保存される変数の名前                         |
| `value`    | `Boolean` | 保存する `Boolean` 値                        |
| `expiry`   | `Expiry`  | (オプション) この変数の有効期限              |

```java
tealium.dataLayer.putBoolean("KEY", true, Expiry.FOREVER)
```

### `putBooleanArray`

指定されたキーに `Array<Boolean>` 値を保存します。

| パラメータ | タイプ             | 説明                                       |
|:-----------|:-----------------|:--------------------------------------------|
| `key`      | `String`         | 保存される変数の名前                         |
| `value`    | `Array<Boolean>` | 保存する `Array<Boolean>` 値                 |
| `expiry`   | `Expiry`         | (オプション) この変数の有効期限              |

```java
tealium.dataLayer.putBooleanArray("KEY", arrayOf(true, false, true), Expiry.FOREVER)
```

### `putDouble`

指定されたキーに `Double` 値を保存します。

| パラメータ | タイプ     | 説明                                       |
|:-----------|:---------|:--------------------------------------------|
| `key`      | `String` | 保存される変数の名前                         |
| `value`    | `Double` | 保存する `Double` 値                        |
| `expiry`   | `Expiry` | (オプション) この変数の有効期限              |

```java
tealium.dataLayer.putDouble("KEY", 10.5, Expiry.FOREVER)
```

### `putDoubleArray`

指定されたキーに `Array<Double>` 値を保存します。

| パラメータ | タイプ            | 説明                                       |
|:-----------|:----------------|:--------------------------------------------|
| `key`      | `String`        | 保存される変数の名前                         |
| `value`    | `Array<Double>` | 保存する `Array<Double>` 値                 |
| `expiry`   | `Expiry`        | (オプション) この変数の有効期限              |

```java
tealium.dataLayer.putDoubleArray("KEY", arrayOf(0.1, 10.5), Expiry.FOREVER)
```

### `putInt`

指定されたキーに `Int` 値を保存します。

| パラメータ | タイプ     | 説明                                       |
|:-----------|:---------|:--------------------------------------------|
| `key`      | `String` | 保存される変数の名前                         |
| `value`    | `Int`    | 保存する `Int` 値                           |
| `expiry`   | `Expiry` | (オプション) この変数の有効期限              |

```java
tealium.dataLayer.putInt("KEY", 10, Expiry.FOREVER)
```

### `putIntArray`

指定されたキーに `Array<Int>` 値を保存します。

| パラメータ | タイプ         | 説明                                       |
|:-----------|:-------------|:--------------------------------------------|
| `key`      | `String`     | 保存される変数の名前                         |
| `value`    | `Array<Int>` | 保存する `Array<Int>` 値                     |
| `expiry`   | `Expiry`     | (オプション) この変数の有効期限              |

```java
tealium.dataLayer.putIntArray("KEY", arrayOf(100, Int.MAX_VALUE), Expiry.FOREVER)
```

### `putJsonArray`

指定されたキーに `org.json.JSONArray` 値を保存します。

| パラメータ | タイプ        | 説明                                       |
|:-----------|:------------|:--------------------------------------------|
| `key`      | `String`    | 保存される変数の名前                         |
| `value`    | `JSONArray` | 保存する `org.json.JSONArray` 値             |
| `expiry`   | `Expiry`    | (オプション) この変数の有効期限              |

```java
val my_list = new JSONArray();
my_list.put("value_1");
my_list.put("value_2");
tealium.dataLayer.putJsonArray("KEY", my_list, Expiry.FOREVER);
```

### `putJsonObject`

指定されたキーに `org.json.JSONObject` 値を保存します。

| パラメータ | タイプ         | 説明                                       |
|:-----------|:-------------|:--------------------------------------------|
| `key`      | `String`     | 保存される変数の名前                         |
| `value`    | `JSONObject` | 保存する `org.json.JSONObject` 値           |
| `expiry`   | `Expiry`     | (オプション) この変数の有効期限              |

```java
val my_obj = new JSONObject();
my_obj.put("key", "value");
tealium.dataLayer.putJsonObject("KEY", my_obj, Expiry.FOREVER);
```

### `putLong`

指定されたキーに `Long` 値を保存します。

| パラメータ | タイプ     | 説明                                       |
|:-----------|:---------|:--------------------------------------------|
| `key`      | `String` | 保存される変数の名前                         |
| `value`    | `Long`   | 保存する `Long` 値                          |
| `expiry`   | `Expiry` | (オプション) この変数の有効期限              |

```java
tealium.dataLayer.putLong("KEY", Long.MAX_VALUE, Expiry.FOREVER)
```

### `putLongArray`

指定されたキーに `Array<Long>` 値を保存します。

| パラメータ | タイプ          | 説明                                       |
|:-----------|:--------------|:--------------------------------------------|
| `key`      | `String`      | 保存される変数の名前                         |
| `value`    | `Array<Long>` | 保存する `Array<Long>` 値                    |
| `expiry`   | `Expiry`      | (オプション) この変数の有効期限              |

```java
tealium.dataLayer.putLongArray("KEY", arrayOf(1000L, Long.MAX_VALUE), Expiry.FOREVER)
```

### `putString`

指定されたキーに `String` 値を保存します。

| パラメータ | タイプ     | 説明                                       |
|:-----------|:---------|:--------------------------------------------|
| `key`      | `String` | 保存される変数の名前                         |
| `value`    | `String` | 保存する `String` 値                        |
| `expiry`   | `Expiry` | (オプション) この変数の有効期限              |

```java
tealium.dataLayer.putString("KEY", "String Value", Expiry.FOREVER)
```
### `putStringArray`

指定されたキーに `Array<String>` 値を格納します。

| パラメータ | タイプ            | 説明                                     |
|:-----------|:----------------|:----------------------------------------|
| `key`      | `String`        | 格納される変数の名前                     |
| `value`    | `Array<String>` | 格納される `Array<String>` の値          |
| `expiry`   | `Expiry`        | (オプショナル) この変数の有効期限        |

```java
tealium.dataLayer.putStringArray("KEY",
    arrayOf("String 1", "String 2"), Expiry.FOREVER)
```

### `remove`

指定されたキーで格納されている値を削除します

| パラメータ | タイプ     | 説明                                 |
|:-----------|:---------|:------------------------------------|
| `key`      | `String` | 削除される変数の名前                 |

```java
tealium.dataLayer.remove("KEY")
```