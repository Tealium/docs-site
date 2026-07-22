---
title: Example code
description: This article provides code examples for data transformation functions.
url: https://docs.tealium.com/server-side/functions/data-transformation-functions/functions-transforms-example-code/
---
## Delete a variable

In this example, the function deletes a variable containing sensitive data (email address).

```js
transform((event) => {
    delete event.data.udo.user.email;
});
```


## Populate a variable

The following example populates the `page_name` variable with the title.

```js
transform((event) => {
    if (!event.data.udo.page_name) {
        event.data.udo.page_name = event.data.dom.title;
    }
});
```


## Create a variable

This example create a `page_hierarchy` variable from multiple variables.

```js
transform((event) => {
    const { site_region, site_section, category_name } = event.data.udo;
    event.data.udo.page_hierarchy = '${site_region}:${site_section}:${category_name}';
});
```


The following example creates `site_section`, `site_category`, and `site_subcategory` variables based on the `pathname`.

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


## Map a value to a variable

The following example maps a value to `category_name` based on the value of `category_id` :

```js
const categoryNameById = {
    38: "Mobile",
    39: "Engagement",
    40: "Monitoring"
};

transform((event) => {
    event.data.udo.products = event.data.udo.products
        .map(product => ({
            ...product,
            category_name: categoryNameById[product.category_id]
        }));
});
```


## Modify an existing variable

The following example changes a variable to all lowercase.

```js
transform((event) => {
    const searchKeyword = event.data.udo.search_keyword;
    if (searchKeyword) {
        event.data.udo.search_keyword = searchKeyword.toLowerCase();
    }
});
```


This example renames a variable by setting its value to a new variable and deleting the existing variable.

```js
transform((event) => {
    event.data.udo.page_title = event.data.udo.page_name;
    delete event.data.udo.page_name;
});
```


## Concatenate values and create a new variable

This example concatenates two values and deletes one of the values. It also creates a new variable.

```js
import flatten from 'tealium/util/flatten';

// "transform" function lets you access event and apply changes
transform((event) => {
    // concatenate test1 and test2 properties
    const { test1, test2 } = event.data.udo;
    event.data.udo.test_concatenated = `${test1}:${test2}`;

    // delete test1 property
    delete event.data.udo.test1;

    // add a new test3 property
    event.data.udo.test3 = 'TEST3';

    console.log(JSON.stringify(event, null, 2));
})
```