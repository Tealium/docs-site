---
title: ネストされたオブジェクトのフラット化
description: この記事では、ネストされたオブジェクトをネストされていないオブジェクトに変換するために使用される `flatten` ライブラリについて説明します。
url: https://docs.tealium.com/ja/server-side/functions/data-transformation-functions/transforms-flatten-library/
---
## 仕組み

`flatten` ライブラリは、データ変換関数のデフォルトコードでインポートされる標準ライブラリです。このライブラリは `flatten()` ユーティリティを提供し、ネストされたオブジェクトをネストされていないオブジェクトに変換します。`flatten()` は、文字列と文字列の配列を含むオブジェクトを返します。

`flatten()` は以下の2つのパラメータを受け取ります：

`flatten(target[, options])`

* `target` は、データ変換関数に渡されるイベントオブジェクトです。
* `options` は、変換中にネストされたキーがどのように処理されるかを指定するオブジェクトです。

`options` パラメータには以下のプロパティが含まれます：

|**プロパティ**| **データ型**| **説明**|
|---| ---| ---|
|`delimiter`| `String` | 親と子のプロパティ名を結合するために使用される文字。デフォルトは `.`。|
|`prefix`| `String` |  新しいキー名の先頭に連結される文字列、その後に `delimiter` が続きます。 |
|`ignoreKeys`| `String[]` | 出力から省略するキーの配列。|
|`replaceKeys`| `Object{string:string}` | キーの新しい名前を指定します。キーはオブジェクト内の既存のキーで、値は新しいキーです。 <br>例： `{ "uid" : "user_id" }` |

## パラメータ

以下の例は、`options` プロパティがどのように使用されるかを示しています。これらの例では、以下のネストされたオブジェクトをフラット化する対象として使用します：

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

`delimiter` が `_` の場合、以下のオブジェクトが返されます：

```json
{
  "page_id": 1,
  "user_id": 1,
  "util": ["1", "2", "3"]
}
```

### `prefix`

`prefix` が `fl` の場合、以下のオブジェクトが返されます：

```json
{
  "fl.user.id": 1,
  "fl.page.id": 1,
  "fl.util": ["1", "2", "3"]
}
```

### `ignoreKeys`

`ignoreKeys` が `["page", "util"]` の場合、以下のオブジェクトが返されます：

```json
{
  "user.id": 1
}
```

### `replaceKeys`

`replaceKeys` が以下のように定義されている場合：

```js
const replaceKeys = {
  "user": "",
  "page": "p"
}
```

以下のオブジェクトが返されます：

```json
{
  "id": 1,
  "p.id": 1,
  "util": ["1", "2", "3"]
}
```

## 完全な例

以下の例は、フラット化する複雑なオブジェクトを示しています：

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

以下のオブジェクトが `flatten()` によって返されます：

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
