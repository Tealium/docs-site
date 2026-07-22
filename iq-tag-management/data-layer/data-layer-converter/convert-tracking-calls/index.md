---
title: Convert tracking calls
url: https://docs.tealium.com/iq-tag-management/data-layer/data-layer-converter/convert-tracking-calls/
---
You must convert data layer on tracking calls if you are passing your third-party data layer object to your Tealium tracking calls.

Example:

```js
utag.link({
    "event" : {
        "type": "cart",
        "name": "add to cart",
        "items" : [{
            "id": "prod123",
            "price": "123.45",
            "qty": "2"
        }]
    }
});
```

## Add the extension

Use the following steps to convert data layer tracking calls:

1. In the left sidebar, navigate to **Tag Management > Extensions**.
1. Add a [JavaScript extension]().
1. In the **Title** field, enter `Convert Tracking Calls`.
1. In the **Draft Name** field, enter a name for your draft.
1. In the **Scope** field, select **All Tags**.
1. Change the execution to **Before Load Rules**.
1. Copy and paste the following code into the JavaScript field for the extension:  
    ```js
        teal.flattenObject(b,b);
    ```
1. Click **Approve for Publish**.
1. Select one or more publish environments and click **Apply**.  
1. Save and publish your changes.

