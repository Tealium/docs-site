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
| [`getBooleanArray()`](#getbooleanarray) | 指定されたキーの`Array&lt;Boolean&gt;`を取得します |
| [`getDouble()`](#getdouble)             | 指定されたキーの`Double`を取得します     |
| [`getDoubleArray()`](#getdoublearray)   | 指定されたキーの`Array&lt;Double&gt;`を取得します |
| [`getInt()`](#getint)                   | 指定されたキーの`Int`を取得します        |
| [`getIntArray()`](#getintarray)         | 指定されたキーの`Array&lt;Int&gt;`を取得します |
| [`getJsonArray()`](#getjsonarray)       | 指定されたキーの`org.json.JSONArray`を取得します |
| [`getJsonObject()`](#getjsonobject)     | 指定されたキーの`org.json.JSONObject`を取得します |
| [`getLong()`](#getlong)                 | 指定されたキーの`Long`を取得します       |
| [`getLongArray()`](#getlongarray)       | 指定されたキーの`Array&lt;Long&gt;`を取得します |
| [`getString()`](#getstring)             | 指定されたキーの`String`を取得します     |
| [`getStringArray()`](#getstringarray)   | 指定されたキーの`Array&lt;String&gt;`を取得します |
| [`keys()`](#keys)                       | データレイヤーに現在存在するすべてのキーの`List&lt;String&gt;`を返します |
| [`putBoolean()`](#putboolean)           | 指定されたキーに`Boolean`を格納します         |
| [`putBooleanArray()`](#putbooleanarray) | 指定されたキーに`Array&lt;Boolean&gt;`を格納します  |
| [`putDouble()`](#putdouble)             | 指定されたキーに`Double`を格納します          |
| [`putDoubleArray()`](#putdoublearray)   | 指定されたキーに`Array&lt;Double&gt;`を格納します   |
| [`putInt()`](#putint)                   | 指定されたキーに`Int`を格納します            |
| [`putIntArray()`](#putintarray)         | 指定されたキーに`Array&lt;Int&gt;`を格納します     |
| [`putJsonArray()`](#putjsonarray)       | 指定されたキーに`org.json.JSONArray`を格納します |
| [`putJsonObject()`](#putjsonobject)     | 指定されたキーに`org.json.JSONObject`を格納します |
| [`putLong()`](#putlong)                 | 指定されたキーに`Long`を格納します            |
| [`putLongArray()`](#putlongarray)       | 指定されたキーに`Array&lt;Long&gt;`を格納します     |
| [`putString()`](#putstring)             | 指定されたキーに`String`を格納します          |
| [`putStringArray()`](#putstringarray)   | 指定されたキーに`Array&lt;String&gt;`を格納します   |
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
tealium.dataLayer.contains(&#34;KEY&#34;)
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
val any = tealium.dataLayer.get(&#34;KEY&#34;)
```

### `getBoolean`

指定されたキーで`Boolean`値を取得します。このキーの値が`Boolean`でない場合は`null`が返されます。

| パラメータ | タイプ     | 説明                              |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | 取得する変数の名前 |

```java
val bool = tealium.dataLayer.getBoolean(&#34;KEY&#34;)
```

### `getBooleanArray`

指定されたキーで`Array&lt;Boolean&gt;`値を取得します。このキーの値が`Array&lt;Boolean&gt;`でない場合は`null`が返されます。

| パラメータ | タイプ     | 説明                              |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | 取得する変数の名前 |

```java
val booleanArray = tealium.dataLayer.getBooleanArray(&#34;KEY&#34;)
```

### `getDouble`

指定されたキーで`Double`値を取得します。このキーの値が`Double`でない場合は`null`が返されます。

| パラメータ | タイプ     | 説明                              |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | 取得する変数の名前 |

```java
val double = tealium.dataLayer.getDouble(&#34;KEY&#34;)
```

### `getDoubleArray`

指定されたキーで`Array&lt;Double&gt;`値を取得します。このキーの値が`Array&lt;Double&gt;`でない場合は`null`が返されます。

| パラメータ | タイプ     | 説明                              |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | 取得する変数の名前 |

```java
val doubleArray = tealium.dataLayer.getDoubleArray(&#34;KEY&#34;)
```

### `getInt`

指定されたキーで`Int`値を取得します。このキーの値が`Int`でない場合は`null`が返されます。

| パラメータ | `タイプ`   | 説明                              |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | 取得する変数の名前 |

```java
val int = tealium.dataLayer.getInt(&#34;KEY&#34;)
```

### `getIntArray`

指定されたキーで`Array&lt;Int&gt;`値を取得します。このキーの値が`Array&lt;Int&gt;`でない場合は`null`が返されます。

| パラメータ | タイプ     | 説明                              |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | 取得する変数の名前 |

```java
val intArray = tealium.dataLayer.getIntArray(&#34;KEY&#34;)
```

### `getJsonArray`

指定されたキーで`org.json.JSONArray`値を取得します。このキーの値がJSONArrayでない場合は`null`が返されます。

| パラメータ | タイプ     | 説明                              |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | 取得する変数の名前 |

```java
val jsonArray = tealium.dataLayer.getJsonArray(&#34;KEY&#34;)
```
### `getJsonObject`

指定されたキーで `org.json.JSONObject` の値を取得します。このキーの値が JSONObject でない場合は、`null` が返されます。

| パラメータ | タイプ     | 説明                                      |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | 取得する変数の名前                         |

```java
val jsonObject = tealium.dataLayer.getJsonObject(&#34;KEY&#34;)
```

### `getLong`

指定されたキーで `Long` の値を取得します。このキーの値が `Long` でない場合は、`null` が返されます。

| パラメータ | タイプ     | 説明                                      |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | 取得する変数の名前                         |

```java
val long = tealium.dataLayer.getLong(&#34;KEY&#34;)
```

### `getLongArray`

指定されたキーで `Array&lt;Long&gt;` の値を取得します。このキーの値が `Array&lt;Long&gt;` でない場合は、`null` が返されます。

| パラメータ | タイプ     | 説明                                      |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | 取得する変数の名前                         |

```java
val longArray = tealium.dataLayer.getLongArray(&#34;KEY&#34;)
```

### `getString`

指定されたキーで `String` の値を取得します。このキーの値が `String` でない場合は、`null` が返されます。

| パラメータ | タイプ     | 説明                                      |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | 取得する変数の名前                         |

```java
val string = tealium.dataLayer.getString(&#34;KEY&#34;)
```

### `getStringArray`

指定されたキーで `Array&lt;String&gt;` の値を取得します。このキーの値が `Array&lt;String&gt;` でない場合は、`null` が返されます。

| パラメータ | タイプ     | 説明                                      |
|:-----------|:---------|:-----------------------------------------|
| `key`      | `String` | 取得する変数の名前                         |

```java
val stringArray = tealium.dataLayer.getStringArray(&#34;KEY&#34;)
```

### `keys`

データレイヤーに現在保存されているすべてのキーの `List&lt;String&gt;` を返します

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
tealium.dataLayer.putBoolean(&#34;KEY&#34;, true, Expiry.FOREVER)
```

### `putBooleanArray`

指定されたキーに `Array&lt;Boolean&gt;` 値を保存します。

| パラメータ | タイプ             | 説明                                       |
|:-----------|:-----------------|:--------------------------------------------|
| `key`      | `String`         | 保存される変数の名前                         |
| `value`    | `Array&lt;Boolean&gt;` | 保存する `Array&lt;Boolean&gt;` 値                 |
| `expiry`   | `Expiry`         | (オプション) この変数の有効期限              |

```java
tealium.dataLayer.putBooleanArray(&#34;KEY&#34;, arrayOf(true, false, true), Expiry.FOREVER)
```

### `putDouble`

指定されたキーに `Double` 値を保存します。

| パラメータ | タイプ     | 説明                                       |
|:-----------|:---------|:--------------------------------------------|
| `key`      | `String` | 保存される変数の名前                         |
| `value`    | `Double` | 保存する `Double` 値                        |
| `expiry`   | `Expiry` | (オプション) この変数の有効期限              |

```java
tealium.dataLayer.putDouble(&#34;KEY&#34;, 10.5, Expiry.FOREVER)
```

### `putDoubleArray`

指定されたキーに `Array&lt;Double&gt;` 値を保存します。

| パラメータ | タイプ            | 説明                                       |
|:-----------|:----------------|:--------------------------------------------|
| `key`      | `String`        | 保存される変数の名前                         |
| `value`    | `Array&lt;Double&gt;` | 保存する `Array&lt;Double&gt;` 値                 |
| `expiry`   | `Expiry`        | (オプション) この変数の有効期限              |

```java
tealium.dataLayer.putDoubleArray(&#34;KEY&#34;, arrayOf(0.1, 10.5), Expiry.FOREVER)
```

### `putInt`

指定されたキーに `Int` 値を保存します。

| パラメータ | タイプ     | 説明                                       |
|:-----------|:---------|:--------------------------------------------|
| `key`      | `String` | 保存される変数の名前                         |
| `value`    | `Int`    | 保存する `Int` 値                           |
| `expiry`   | `Expiry` | (オプション) この変数の有効期限              |

```java
tealium.dataLayer.putInt(&#34;KEY&#34;, 10, Expiry.FOREVER)
```

### `putIntArray`

指定されたキーに `Array&lt;Int&gt;` 値を保存します。

| パラメータ | タイプ         | 説明                                       |
|:-----------|:-------------|:--------------------------------------------|
| `key`      | `String`     | 保存される変数の名前                         |
| `value`    | `Array&lt;Int&gt;` | 保存する `Array&lt;Int&gt;` 値                     |
| `expiry`   | `Expiry`     | (オプション) この変数の有効期限              |

```java
tealium.dataLayer.putIntArray(&#34;KEY&#34;, arrayOf(100, Int.MAX_VALUE), Expiry.FOREVER)
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
my_list.put(&#34;value_1&#34;);
my_list.put(&#34;value_2&#34;);
tealium.dataLayer.putJsonArray(&#34;KEY&#34;, my_list, Expiry.FOREVER);
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
my_obj.put(&#34;key&#34;, &#34;value&#34;);
tealium.dataLayer.putJsonObject(&#34;KEY&#34;, my_obj, Expiry.FOREVER);
```

### `putLong`

指定されたキーに `Long` 値を保存します。

| パラメータ | タイプ     | 説明                                       |
|:-----------|:---------|:--------------------------------------------|
| `key`      | `String` | 保存される変数の名前                         |
| `value`    | `Long`   | 保存する `Long` 値                          |
| `expiry`   | `Expiry` | (オプション) この変数の有効期限              |

```java
tealium.dataLayer.putLong(&#34;KEY&#34;, Long.MAX_VALUE, Expiry.FOREVER)
```

### `putLongArray`

指定されたキーに `Array&lt;Long&gt;` 値を保存します。

| パラメータ | タイプ          | 説明                                       |
|:-----------|:--------------|:--------------------------------------------|
| `key`      | `String`      | 保存される変数の名前                         |
| `value`    | `Array&lt;Long&gt;` | 保存する `Array&lt;Long&gt;` 値                    |
| `expiry`   | `Expiry`      | (オプション) この変数の有効期限              |

```java
tealium.dataLayer.putLongArray(&#34;KEY&#34;, arrayOf(1000L, Long.MAX_VALUE), Expiry.FOREVER)
```

### `putString`

指定されたキーに `String` 値を保存します。

| パラメータ | タイプ     | 説明                                       |
|:-----------|:---------|:--------------------------------------------|
| `key`      | `String` | 保存される変数の名前                         |
| `value`    | `String` | 保存する `String` 値                        |
| `expiry`   | `Expiry` | (オプション) この変数の有効期限              |

```java
tealium.dataLayer.putString(&#34;KEY&#34;, &#34;String Value&#34;, Expiry.FOREVER)
```
### `putStringArray`

指定されたキーに `Array&lt;String&gt;` 値を格納します。

| パラメータ | タイプ            | 説明                                     |
|:-----------|:----------------|:----------------------------------------|
| `key`      | `String`        | 格納される変数の名前                     |
| `value`    | `Array&lt;String&gt;` | 格納される `Array&lt;String&gt;` の値          |
| `expiry`   | `Expiry`        | (オプショナル) この変数の有効期限        |

```java
tealium.dataLayer.putStringArray(&#34;KEY&#34;,
    arrayOf(&#34;String 1&#34;, &#34;String 2&#34;), Expiry.FOREVER)
```

### `remove`

指定されたキーで格納されている値を削除します

| パラメータ | タイプ     | 説明                                 |
|:-----------|:---------|:------------------------------------|
| `key`      | `String` | 削除される変数の名前                 |

```java
tealium.dataLayer.remove(&#34;KEY&#34;)
```