---
title: About data record functions
description: This article provides an overview of data record functions in CloudStream.
url: https://docs.tealium.com/server-side/functions/data-record-functions/data-record-functions/
---

<blockquote>
To enable CloudStream functions, go to **Admin menu** > **Server-Side Settings** > **CloudStream Connectors**, set **Activate CloudStream Connectors** to `On`, and click **Save**.
</blockquote>


## How it works

Functions in CloudStream run within the CloudStream data pipeline and have access to the queried data records from your cloud data sources. Use functions within a CloudStream profile to retrieve data from other systems, augment your data, or send data to other endpoints.

Adding and managing CloudStream functions is the same as managing other functions, with the following exceptions:

* When creating a custom action function, instead of selecting an audience or an event, you select a [cloud data source](https://docs.tealium.com/about-cloud-data-sources/) and a [segment](https://docs.tealium.com/manage-cloudstream-segments/).
* Each CloudStream function can only use data from one data source. If you want to activate data from additional data sources, configure a separate function for each one.
* If a segment contains attributes mapped from multiple data sources, only the attributes from the selected data source are available in the function.

## Triggers

Data record functions execute before and after the data record is processed.

### Transformations

Transformation functions execute before the data record is processed, as shown in the following data pipeline diagram:

![](https://docs.tealium.com/images/server-side/transformations-data-record-pipeline.png)

Use functions at this point in the pipeline to transform the [data record object](#data-record-object) and its values before it's processed.

For more information, see [about-data-transformation-functions](https://docs.tealium.com/about-data-transformation-functions/).

### Custom actions

Custom action functions execute after the data record is processed, as shown in the following data pipeline diagram:

![](https://docs.tealium.com/images/server-side/functions-data-record-pipeline.png)

Use functions at this point in the pipeline as activations to send the data record to other systems.


<blockquote>
At this point in the data pipeline, modifications to the `dataRecord` object have no effect on other parts of the system.
</blockquote>


## Runtime version

The runtime version for data record transformation functions is the same as for event data, but includes the following changes:

* The `crypto-es` library is removed and replaced with [`tealium/crypto`](https://docs.tealium.com/function-modules/#crypto).

The runtime version for custom actions is the same as [event and visitor functions V3](https://docs.tealium.com/event-visitor-functions-v3/), but includes the following changes:

* The `track` library has been removed.
* The data record cannot be sent back to Tealium as a new event.

## transform() function

When you create a transformation data record function, the `$.dataSourceId` field must be used as a condition for the trigger rule. Use this condition to reference the data source key from a cloud data source.

Example:

[
  [
    {
      "input": "$.dataSourceId",
      "operator": "equals",
      "filter": "aq68ur"
    }
  ]
]


After you select a cloud data source and set the trigger rule, the following default code appears in the **Code** tab of the functions code editor:

```js
import flatten from "tealium/util/flatten/v2";

// "transform" function allows you to access data record and apply changes
transform((dataRecord) => {
    // change are applied via the mutation of the original record
    console.log(JSON.stringify(flatten(dataRecord), null, 2));
})
```

## activate() function

When you create a custom action data record function, the default code is shown in the **Code** tab of the functions code editor:

![](https://docs.tealium.com/images/early-access/cloudstream/cloudstream_function_details.png)

 This code contains the `activate()` function and its input parameters.

```js
activate(async ({ dataRecord, helper }) => {
  ...
});
```

Data record functions have a [`dataRecord object`](#data-record-object) and `helper` object.

The `helper` parameter provides `helper.getAuth()` and `helper.getGlobalVariable()` for getting authorization and retrieving global variables. For more information, see .


<blockquote>
Authentication tokens can only be referenced by a function within an HTTP request. If you try to reference the token outside of an HTTP request, the token is replaced by a UUID placeholder.
</blockquote>


## Data record object


<blockquote>
For transformation functions used with Tealium Collect, see [Event parameter](https://docs.tealium.com/transforms-event-parameter/).
</blockquote>


The `dataRecord` object is available for CloudStream functions and cloud data sources and contains the following properties:

| Property | Data type | Description |
| -------- | --------- | ----------- |
| `account` | string | Tealium account name. |
| `data` | object | The data record queried from the cloud data source, referenced at `dataRecord.data.udo`. |
| `event_id` | string | Tealium event ID. |
| `post_time` | number | Timestamp indicating when the data record was queried. |
| `profile` | string | Tealium profile name. |
| `dataSourceId` | string | The ID of the data source.|

Example data record object:

```json
{
  "account": "your-account",
  "profile": "your-profile",
  "data": {
    "udo": {
      "CDW_Column1_Timestamp": 1753077016157,
      "CDW_Column2_Id": 10,
      "CDW_Column3_EmailAddress": "user@example.com",
      "_dc_ttl_": 60000,
      "tealium_datasource": "abcdefg",
      "tealium_event": "data_ingestion"
    }
  },
  "dataSourceId": "abcdefg",
  "event_id": "cf8bd406-787b-4fe9-8b45-7782e6663708",
  "post_time": 1753774131897,
}
```

## Example

This is an example data record function that uses the Tealium Crypto library to hash an email address attribute (`CDW_Column3_EmailAddress`) from the data record and then send the data record to a webhook.

```javascript
import C from "tealium/crypto";

const send = async (data) => {
        console.log("Sending: " + JSON.stringify(data, null, 2));

        return fetch("https://example.com/example-webhook/", {
        method: 'POST',
        headers: {
            'Accept': 'application/json',
            'Content-Type': 'application/json'
        },
        body: JSON.stringify(data)
});
}

activate(async ({ dataRecord }) => {
    const data = { ...dataRecord.data.udo  };

    data.tc_email = C.SHA3(dataRecord.data.udo.CDW_Column3_EmailAddress).toString(C.enc.Hex);

try {
    await send(data);
    } catch (e) {
        console.error("Failed to send the data. " + e);
    }
});