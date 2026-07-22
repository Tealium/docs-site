---
title: Flatten JSON Objects Extension
description: Use the Flatten JSON Objects extension to convert a nested data layer object into a new object with only one layer of key-value pairs.
url: https://docs.tealium.com/iq-tag-management/extensions/extensions-list/flatten-json-objects-extension/
---


<blockquote>
For more advanced options in converting a data layer, see the [Data Layer Converter](https://docs.tealium.com/set-up-data-layer-converter/).
</blockquote>


### Prerequisites

* See [About Extensions]()

### Requirements

* utag v4.38 or later. For more information about updating the `utag.js` template, see our knowledge base article [Best Practices for Updating to the Latest Version of utag.js](https://support.tealiumiq.com/en/support/solutions/articles/36000363470).

### How it works

The following are a few examples that demonstrate how the Flatten JSON Objects extension works:

* Objects such as `parent -> child` are flattened as `parent.child`.
* Array objects such as `parent -> array -> [obj1,objN]` are flattened as `parent.array0.obj1key `and `parent.arrayN.objNkey`.
* For arrays an additional `parent.array.array-size` value are set automatically.

## Using the extension

Once the extension is added, the following configuration options are available:

* **JSON Object**: The JSON object variable to flatten.
* **Output Object**: Output object variable to contain the results.

## Example

Here is an example of a JSON object including a parent to child relationship and an array:

![](https://docs.tealium.com/images/iq-tag-management/no-title-1265i9f0146e131a9389e.png)

```
var person_object = {
  "firstName" : "John",
  "lastName" : "Doe",
  "age" : 25,
  "address" : {
    "streetAddress" : "1234 Main St",
    "city" : "Los Angeles",
    "state" : "CA",
    "postalCode" : "90010"
  },
  "phoneNumber" : [
    {
      "type" : "home",
      "number" : "310-555-1234"
    },
    {
      "type" : "fax",
      "number" : "310-555-5678"
    }
  ]
};

```

When flattened, the object becomes:

```
var person_flatobject = {
    "address.city" : "Los Angeles",
    "address.postalCode" : "90010"
    "address.state" : "CA",
    "address.streetAddress": "1234 Main St",
    "age" : 25,
    "firstName" : "John",
    "lastName" : "Doe",
    "phoneNumber.array-size" : 2
    "phoneNumber0.number" : "310-555-1234"
    "phoneNumber0.type"  : "home",
    "phoneNumber1.number" : "310-555-5678"
    "phoneNumber1.type"  : "fax"
};

```

If items from the new object need to be referenced as data layer variables, use the notation as stated in `person_flatobject`. For example, access the `state` data in the address as `person_flatobject.address.state`.

![](https://docs.tealium.com/images/iq-tag-management/no-title-1266i4a38c24e66920d3e.png)
