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
|`replaceKeys`| `Object{string:string}` | キーの新しい名前を指定します。キーはオブジェクト内の既存のキーで、値は新しいキーです。 &lt;br&gt;例： `{ &#34;uid&#34; : &#34;user_id&#34; }` |

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
  util: [&#34;1&#34;, &#34;2&#34;, &#34;3&#34;]
};
```

### `delimiter`

`delimiter` が `_` の場合、以下のオブジェクトが返されます：

```json
{
  &#34;page_id&#34;: 1,
  &#34;user_id&#34;: 1,
  &#34;util&#34;: [&#34;1&#34;, &#34;2&#34;, &#34;3&#34;]
}
```

### `prefix`

`prefix` が `fl` の場合、以下のオブジェクトが返されます：

```json
{
  &#34;fl.user.id&#34;: 1,
  &#34;fl.page.id&#34;: 1,
  &#34;fl.util&#34;: [&#34;1&#34;, &#34;2&#34;, &#34;3&#34;]
}
```

### `ignoreKeys`

`ignoreKeys` が `[&#34;page&#34;, &#34;util&#34;]` の場合、以下のオブジェクトが返されます：

```json
{
  &#34;user.id&#34;: 1
}
```

### `replaceKeys`

`replaceKeys` が以下のように定義されている場合：

```js
const replaceKeys = {
  &#34;user&#34;: &#34;&#34;,
  &#34;page&#34;: &#34;p&#34;
}
```

以下のオブジェクトが返されます：

```json
{
  &#34;id&#34;: 1,
  &#34;p.id&#34;: 1,
  &#34;util&#34;: [&#34;1&#34;, &#34;2&#34;, &#34;3&#34;]
}
```

## 完全な例

以下の例は、フラット化する複雑なオブジェクトを示しています：

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

以下のオブジェクトが `flatten()` によって返されます：

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
