---
title: Flatten JSON Objects Extension
description: Use the Flatten JSON Objects extension to convert a nested data layer object into a new object with only one layer of key-value pairs.
url: https://docs.tealium.com/iq-tag-management/extensions/extensions-list/flatten-json-objects-extension/
---

For more advanced options in converting a data layer, see the [Data Layer Converter]().

### Prerequisites

* See [About Extensions]()

### Requirements

* utag v4.38 or later. For more information about updating the `utag.js` template, see our knowledge base article [Best Practices for Updating to the Latest Version of utag.js](https://support.tealiumiq.com/en/support/solutions/articles/36000363470).

### How it works

The following are a few examples that demonstrate how the Flatten JSON Objects extension works:

* Objects such as `parent -&gt; child` are flattened as `parent.child`.
* Array objects such as `parent -&gt; array -&gt; [obj1,objN]` are flattened as `parent.array0.obj1key `and `parent.arrayN.objNkey`.
* For arrays an additional `parent.array.array-size` value are set automatically.

## Using the extension

Once the extension is added, the following configuration options are available:

* **JSON Object**: The JSON object variable to flatten.
* **Output Object**: Output object variable to contain the results.

## Example

Here is an example of a JSON object including a parent to child relationship and an array:

![](/images/iq-tag-management/no-title-1265i9f0146e131a9389e.png)

```
var person_object = {
  &#34;firstName&#34; : &#34;John&#34;,
  &#34;lastName&#34; : &#34;Doe&#34;,
  &#34;age&#34; : 25,
  &#34;address&#34; : {
    &#34;streetAddress&#34; : &#34;1234 Main St&#34;,
    &#34;city&#34; : &#34;Los Angeles&#34;,
    &#34;state&#34; : &#34;CA&#34;,
    &#34;postalCode&#34; : &#34;90010&#34;
  },
  &#34;phoneNumber&#34; : [
    {
      &#34;type&#34; : &#34;home&#34;,
      &#34;number&#34; : &#34;310-555-1234&#34;
    },
    {
      &#34;type&#34; : &#34;fax&#34;,
      &#34;number&#34; : &#34;310-555-5678&#34;
    }
  ]
};

```

When flattened, the object becomes:

```
var person_flatobject = {
    &#34;address.city&#34; : &#34;Los Angeles&#34;,
    &#34;address.postalCode&#34; : &#34;90010&#34;
    &#34;address.state&#34; : &#34;CA&#34;,
    &#34;address.streetAddress&#34;: &#34;1234 Main St&#34;,
    &#34;age&#34; : 25,
    &#34;firstName&#34; : &#34;John&#34;,
    &#34;lastName&#34; : &#34;Doe&#34;,
    &#34;phoneNumber.array-size&#34; : 2
    &#34;phoneNumber0.number&#34; : &#34;310-555-1234&#34;
    &#34;phoneNumber0.type&#34;  : &#34;home&#34;,
    &#34;phoneNumber1.number&#34; : &#34;310-555-5678&#34;
    &#34;phoneNumber1.type&#34;  : &#34;fax&#34;
};

```

If items from the new object need to be referenced as data layer variables, use the notation as stated in `person_flatobject`. For example, access the `state` data in the address as `person_flatobject.address.state`.

![](/images/iq-tag-management/no-title-1266i4a38c24e66920d3e.png)
