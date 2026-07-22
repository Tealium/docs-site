---
title: Cookie 機能
description: Tealium for JavaScript で提供されている Cookie 機能に関するリファレンス ガイド。
url: https://docs.tealium.com/ja/platforms/javascript/api/cookie-functions/
---
## `utag.loader.SC()`

この関数は、名前空間`utag_`内の複数値のCookieを構成および削除します。余分なCookieが追加されないように`utag_main`サブCookieを構成するために一般的に使用されます。

ドメイン上のCookieの数を最小限に抑えるため、複数値のCookieオブジェクトを構成することをお勧めします。複数値のCookieは、複数の値をキーと値のペアとして1つのCookie名前空間に格納します。この関数 は `utag_main`を構成するために一般的に使用されます



<blockquote>
これは、["データ値を保持"拡張機能](https://community.tealiumiq.com/t5/iQ-Tag-Management/Persist-Data-Value-Extension/ta-p/13623)によって使用されるのと同じ関数です。
</blockquote>


次の形式は、Cookieの名前空間、名前、値、オプションの有効期限、および追加機能を指定するためのオプションのフラグを識別することによってCookieを構成する方法を示しています。
```js
utag.loader.SC(namespace, {"name": "value;exp-expiry"}, flag);
```

| パラメータ | 型| 説明| 例|
| ---       | ---| ---         | ---     |
| `namespace`    | `String` | Cookieの名前空間。`utag_`で始まる必要があります。| `"utag_multi"` |
| `name:value`   | `Object` | 複数値のCookieを表すキーと値のペアからなるオブジェクト。| `{"uid": "012345689", "aff": "SiteAff1;exp-7d"}` |
| `expiry`  | `String` | （オプション）Cookieの有効期限。`exp-`で始まる必要があります。| `exp-12h` |
| `flag`    | `String` | （オプション）1つ以上のCookieを削除するためのフラグ。| `"d"` |


**有効期限オプション**
使用可能なCookie有効期限オプションは次のとおりです。

| Expiry unit| 説明| 例|
| --- | ---| --- |
| `#d` | 日数で表す有効期限（何も指定されていない場合はデフォルトの単位）| `exp-7d`または`exp-7`（7日間）|
| `#h` | 時間数で表す有効期限| `"exp-8h"`（8時間）|
| `#u` | [Unixタイムスタンプ](https://www.epochconverter.com/)で表す有効期限| `"exp-1549271521u"`（2022年12月22日午前0時（GMT））|
| `session` | セッション終了時間で表す有効期限（デフォルトは[セッションタイムアウト](https://docs.tealium.com/ja/platforms/javascript/settings/#session-timeout)：30分）| `"exp-session"` |


<blockquote>
タイムスタンプベースの有効期限（`"exp-1549271521u"`など）には、Unixタイムスタンプであることを示す`u`が末尾に付きます。Cookie自体で構成されている値（`"exp-1549271521"`
</blockquote>
など）と混同しないでください。

有効期限オプションが構成されていない場合、デフォルトの動作は`utag.js`のバージョンに基づきます。

- **4.27+** - デフォルトはCookieの作成日から1年後です。
- **4.26以前** - デフォルトの有効期限は2099年です。

**Cookieの構成**
複数値のCookieを構成するには、キーと値のペアからなるオブジェクトを`value`パラメータに渡します。

次の例では、`utag_multi`という名前の複数値のCookieが作成されます。
```js
utag.loader.SC("utag_multi", {
    "uid"      : "012345689",      // default expiry
    "test_seg" : "groupA;exp-12h", // 12 hour expiry
    "aff"      : "SiteAff1;exp-7d" // 7 day expiry
});
```

**Cookieの削除**
1. 以上のCookie値を削除するには、オプションの`flag`パラメータを使用します。

複数値のCookieから1つ以上の値を削除します。指定したキーと値の各ペアが削除されます。
```js
utag.loader.SC("utag_multicookie", {"test_seg":"", "aff":""}, "d");
```

複数値のCookieからすべての値を削除します。
```js
utag.loader.SC("utag_multicookie", {}, "da");
```

