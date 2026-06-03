---
title: Example code
description: This article provides code examples for data transformation functions.
url: https://docs.tealium.com/server-side/functions/data-transformation-functions/functions-transforms-example-code/
---
## Delete a variable

In this example, the function deletes a variable containing sensitive data (email address).

```js
transform((event) =&gt; {
    delete event.data.udo.user.email;
});
```


## Populate a variable

The following example populates the `page_name` variable with the title.

```js
transform((event) =&gt; {
    if (!event.data.udo.page_name) {
        event.data.udo.page_name = event.data.dom.title;
    }
});
```


## Create a variable

This example create a `page_hierarchy` variable from multiple variables.

```js
transform((event) =&gt; {
    const { site_region, site_section, category_name } = event.data.udo;
    event.data.udo.page_hierarchy = &#39;${site_region}:${site_section}:${category_name}&#39;;
});
```


The following example creates `site_section`, `site_category`, and `site_subcategory` variables based on the `pathname`.

```js
transform((event) =&gt; {
    const [,site_section, site_category, site_subcategory] = event.data.dom.pathname.split(&#34;/&#34;);
    Object.assign(event.data.udo, {
        site_section,
        site_category,
        site_subcategory
    })
});
```


## Map a value to a variable

The following example maps a value to `category_name` based on the value of `category_id` :

```js
const categoryNameById = {
    38: &#34;Mobile&#34;,
    39: &#34;Engagement&#34;,
    40: &#34;Monitoring&#34;
};

transform((event) =&gt; {
    event.data.udo.products = event.data.udo.products
        .map(product =&gt; ({
            ...product,
            category_name: categoryNameById[product.category_id]
        }));
});
```


## Modify an existing variable

The following example changes a variable to all lowercase.

```js
transform((event) =&gt; {
    const searchKeyword = event.data.udo.search_keyword;
    if (searchKeyword) {
        event.data.udo.search_keyword = searchKeyword.toLowerCase();
    }
});
```


This example renames a variable by setting its value to a new variable and deleting the existing variable.

```js
transform((event) =&gt; {
    event.data.udo.page_title = event.data.udo.page_name;
    delete event.data.udo.page_name;
});
```


## Concatenate values and create a new variable

This example concatenates two values and deletes one of the values. It also creates a new variable.

```js
import flatten from &#39;tealium/util/flatten&#39;;

// &#34;transform&#34; function lets you access event and apply changes
transform((event) =&gt; {
    // concatenate test1 and test2 properties
    const { test1, test2 } = event.data.udo;
    event.data.udo.test_concatenated = `${test1}:${test2}`;

    // delete test1 property
    delete event.data.udo.test1;

    // add a new test3 property
    event.data.udo.test3 = &#39;TEST3&#39;;

    console.log(JSON.stringify(event, null, 2));
})
```