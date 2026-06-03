---
title: ユーティリティ関数
description: TealiumがJavaScript用に提供するユーティリティ関数のリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/javascript/api/utility-functions/
---
以下の `utag.ut` 関数が利用可能です：

| 関数 | 説明 |
| --- | --- |
| `decode()` | エンコードされたURIコンポーネントまたは `String` のデコード値を返します |
| `encode()` | デコードされたURIコンポーネントまたは `String` のエンコード値を返します |
| `flatten()` | オブジェクト引数のフラット化された値を返します |
| `hasOwn()` | オブジェクトが指定されたプロパティを自身のプロパティとして持っているかどうかを示すブール値を返します |
| `isEmpty()` | 引数が空であることを示すブール値 `true` を返すか、空でない場合はブール値 `false` を返します |
| `isEmptyObject()` | オブジェクト引数が空であることを示すブール値 `true` を返すか、空でない場合はブール値 `false` を返します |
| `loader()` | タグテンプレートはこの関数を使用して、タグをiframe、画像、またはスクリプトとしてロードし、タグがロードされたときにコールバックをトリガーします。 |
| `merge()` | 一つのオブジェクトから別のオブジェクトへプロパティをマージします |
| `typeOf()` | 変数の型を文字列として返します |


## `utag.ut.decode()`

エンコードされたURIコンポーネントまたは `String` のデコード値を返します。この関数は標準的なJavaScript関数 [`decodeURIComponent()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/decodeURIComponent) と [`unescape()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/unescape) をラップしています。

```js
utag.ut.decode(encodedStr)
```

| パラメータ | タイプ | 説明 |
| --- | --- | --- |
| `encodedStr` | `String` | デコードするためのエンコードされた文字列 |

例：

```js
utag.ut.decode(&#34;Tealium%20Developer%20Docs!&#34;);     // &#34;Tealium Developer Docs!&#34;
utag.ut.decode(&#34;https%3A%2F%2Fdocs.tealium.com&#34;);  // &#34;https://docs.tealium.com&#34;
```

## `utag.ut.encode()`

デコードされたURIコンポーネントまたは文字列のエンコード値を返します。この関数は標準的なJavaScript関数 [`encodeURIComponent()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/encodeURIComponent) と [`escape()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/escape) をラップしています。

```js
utag.ut.encode(decodedStr)
```

| パラメータ | タイプ | 説明 |
| --- | --- | --- |
| `decodedStr` | `String` | エンコードするためのデコードされた文字列 |

例：

```js
utag.ut.encode(&#34;Tealium Developer Docs!&#34;);   // &#34;Tealium%20Developer%20Docs!&#34;
utag.ut.encode(&#34;https://docs.tealium.com&#34;);  // &#34;https%3A%2F%2Fdocs.tealium.com&#34;
```

## `utag.ut.flatten()`

オブジェクト引数のフラット化された値を返します。この関数は、渡されるオブジェクトが1レベル深さであることを前提としています。文字列、配列、ブール値、または数値（浮動小数点数または整数）に到達すると、関数は停止します。多階層のオブジェクトやオブジェクトの配列に対してこの関数を使用しないでください。

```js
utag.ut.flatten(obj)
```

| パラメータ | タイプ | 説明 |
| --- | --- | --- |
| `obj` | `Object` | フラット化するオブジェクト |

例：

```js
utag.ut.flatten({&#34;order_id&#34;: &#34;0123567&#34;, &#34;cart&#34;: {&#34;total_items&#34;: 3, &#34;total_amount&#34;: 123.45},&#34;order_tax&#34;: 9.97});
// {order_id: &#34;0123567&#34;, cart.total_items: 3, cart.total_amount: 123.45, order_tax: 9.97}
```


## `utag.ut.hasOwn()`

オブジェクトが指定されたプロパティを自身のプロパティとして持っているかどうかを示すブール値を返します（継承するのではなく）。この関数は `null` チェックを行い、JavaScript関数 [`hasOwnProperty()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwnProperty) をラップします。

```js
utag.ut.hasOwn(obj, key)
```

| パラメータ | タイプ | 説明 |
| --- | --- | --- |
| `obj` | `Object` | テストするオブジェクト |
| `key` | `String` | テストするプロパティ |

例：

```js
var obj = new Object();     // オブジェクトを作成
obj.x = 3.14;               // 非継承のローカルプロパティを定義

utag.ut.hasOwn(obj, &#39;x&#39;);          // true - xはobjのローカルプロパティ
utag.ut.hasOwn(obj, &#39;y&#39;);          // false - objはプロパティyを持っていない
```

## `utag.ut.isEmpty()`

引数が空であることを示すブール値 `true` を返すか、空でない場合はブール値 `false` を返します。まず、`utag.ut.typeOf()` 関数を使用してデータタイプを決定し、そのタイプに基づいて以下の値を返します：

| タイプ | 返り値の説明 |
| --- | --- |
| `number` | JavaScript関数 `isNaN()` の値を返します |
| `boolean` | `false` を返します |
| `String` | 文字列オブジェクトの `.length` フィールドが0の場合、`true` を返します |
| `Object` | `utag.ut.isEmptyObject()` 関数の値を返します |

```js
utag.ut.isEmpty(arg)
```

| パラメータ | タイプ | 説明 |
| --- | --- | --- |
| `arg` | [`number`, `boolean`, `String`, `Object`] | 空かどうかをテストする引数 |

例：

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

オブジェクト引数が空であることを示すブール値 `true` を返すか、空でない場合はブール値 `false` を返します。

```js
utag.ut.isEmptyObject(obj)
```

| パラメータ | タイプ | 説明 |
| --- | --- | --- |
| `obj` | `Object` | 空かどうかをテストするオブジェクト |

例：

```js
utag.ut.isEmptyObject({});              // true
utag.ut.isEmptyObject({ foo: &#34;bar&#34; });  // false
```

## `utag.ut.loader()`

Tealiumのタグテンプレートはこの関数を使用してタグをロードします。iframe、画像、スクリプトをロードし、スクリプトがロードされたときにコールバックを許可します。この関数は1つのオブジェクト引数のみを受け入れます。

同じIDのiframeとしてファイルがロードされると、関数は既存の要素を削除してから追加します。これはブラウザの履歴に影響を与えず、よりクリーンなDOMを維持するためです。

```js
utag.ut.loader(object)
```

`object` には以下のパラメータがあります：

| パラメータ  | 説明 |
| --- | --- |
| `src` | ロードするファイルのURL |
| `type` | ロードするタグのタイプ：&#34;iframe&#34;, &#34;img&#34;, &#34;script&#34;（デフォルト）|
| `id` | （オプション）要素のID |
| `cb` | （オプション）コールバック関数 |
| `attrs`| （オプション）追加のHTML要素属性のオブジェクト |

例：

```js
utag.ut.loader({
  type: &#34;iframe&#34;,
  src: &#34;https://example.com/path/file.js&#34;,
  id: &#34;teal-tag1&#34;,
  cb: function() {},
  attrs: {&#34;async&#34;:&#34;true&#34;}})
// 以下のHTML要素を結果とします：
// &lt;iframe id=&#34;teal-tag1&#34;  async=&#34;true&#34; height=&#34;1&#34; width=&#34;1&#34; style=&#34;display:none&#34;
//   src=&#34;https://example.com/path/file.js&#34;&gt; &lt;/iframe&gt;
```

## `utag.ut.merge()`

一つのオブジェクトから別のオブジェクトへプロパティをマージします。この関数は多階層のオブジェクトを扱いません。マージを試みる前にオブジェクトをフラット化してください。この関数は配列に対して使用すると参照を作成します。

```js
utag.ut.merge(obj1, obj2, flag)
```

| パラメータ | タイプ | 説明 |
| --- | --- | --- |
| `obj1` | Object | マージする最初のキー-値ペアオブジェクト |
| `obj2` | Object | マージする2つ目のキー-値ペアオブジェクト |
| `overwrite` | number | `obj1` のプロパティ値を `obj2` のプロパティ値で上書きするかどうかを示すフラグ、`0`（いいえ）または `1`（はい） |

例：

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

引数の変数タイプを `String` として返します。

```js
utag.ut.typeOf(arg)
```

| パラメータ | タイプ | 説明 |
| --- | --- | --- |
| `arg` | Any type | タイプを決定する引数 |

例：
```js
utag.ut.typeOf(5);         // &#34;number&#34;
utag.ut.typeOf(&#34;Tealium&#34;); // &#34;string&#34;
utag.ut.typeOf(imgObj);    // &#34;htmlimagelement&#34;
utag.ut.typeOf(obj);       // &#34;object&#34;
utag.ut.typeOf(null);      // &#34;null&#34;
utag.ut.typeOf(undefined); // &#34;undefined&#34;
utag.ut.typeOf(obj.cb);    // &#34;function&#34;
```
