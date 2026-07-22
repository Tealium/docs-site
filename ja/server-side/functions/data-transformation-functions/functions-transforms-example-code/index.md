---
title: 例のコード
description: この記事では、データ変換関数のコード例を提供します。
url: https://docs.tealium.com/ja/server-side/functions/data-transformation-functions/functions-transforms-example-code/
---
## 変数を削除する

この例では、関数が機密データ（メールアドレス）を含む変数を削除します。

```js
transform((event) => {
    delete event.data.udo.user.email;
});
```


## 変数を埋める

次の例では、`page_name`変数にタイトルを埋め込みます。

```js
transform((event) => {
    if (!event.data.udo.page_name) {
        event.data.udo.page_name = event.data.dom.title;
    }
});
```


## 変数を作成する

この例では、複数の変数から`page_hierarchy`変数を作成します。

```js
transform((event) => {
    const { site_region, site_section, category_name } = event.data.udo;
    event.data.udo.page_hierarchy = '${site_region}:${site_section}:${category_name}';
});
```


次の例では、`pathname`に基づいて`site_section`、`site_category`、および`site_subcategory`変数を作成します。

```js
transform((event) => {
    const [,site_section, site_category, site_subcategory] = event.data.dom.pathname.split("/");
    Object.assign(event.data.udo, {
        site_section,
        site_category,
        site_subcategory
    })
});
```


## 値を変数にマッピングする

次の例では、`category_id`の値に基づいて値を`category_name`にマッピングします：

```js
const categoryNameById = {
    38: "モバイル",
    39: "エンゲージメント",
    40: "モニタリング"
};

transform((event) => {
    event.data.udo.products = event.data.udo.products
        .map(product => ({
            ...product,
            category_name: categoryNameById[product.category_id]
        }));
});
```


## 既存の変数を変更する

次の例では、変数をすべて小文字に変更します。

```js
transform((event) => {
    const searchKeyword = event.data.udo.search_keyword;
    if (searchKeyword) {
        event.data.udo.search_keyword = searchKeyword.toLowerCase();
    }
});
```


この例では、変数の値を新しい変数に構成し、既存の変数を削除することで変数の名前を変更します。

```js
transform((event) => {
    event.data.udo.page_title = event.data.udo.page_name;
    delete event.data.udo.page_name;
});
```


## 値を連結して新しい変数を作成する

この例では、2つの値を連結し、そのうちの1つの値を削除します。また、新しい変数を作成します。

```js
import flatten from 'tealium/util/flatten';

// "transform"関数を使用すると、イベントにアクセスして変更を適用できます
transform((event) => {
    // test1とtest2のプロパティを連結します
    const { test1, test2 } = event.data.udo;
    event.data.udo.test_concatenated = `${test1}:${test2}`;

    // test1プロパティを削除します
    delete event.data.udo.test1;

    // 新しいtest3プロパティを追加します
    event.data.udo.test3 = 'TEST3';

    console.log(JSON.stringify(event, null, 2));
})
```
