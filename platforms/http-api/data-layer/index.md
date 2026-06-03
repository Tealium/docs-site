---
title: Data Layer
description: Learn about the data layer variables from the HTTP API library.
url: https://docs.tealium.com/platforms/http-api/data-layer/
---
## Standard Parameters

Tealium Collect supports the following standard parameters in each request:

| Parameter | Description |
| --- | --- |
| `tealium_account` | The name of your Tealium account. |
| `tealium_profile` | The name of your Tealium profile. The default value is `main`. |
| `tealium_datasource` | (Optional) The data source key. For more information, see [ Data Sources](). |
| `tealium_event` | Recommended. The name of the event for tracking purposes. |
| `tealium_visitor_id` | Required for Tealium AudienceStream. An anonymized and unique identifier for the visitor associated with the event.  |
| `tealium_trace_id` | (Optional) For use with [Trace](). |

The format of the request varies depending on the HTTP method used. In the examples below placeholder values are represented with curly braces in the following format: `{VALUE}`.

## Custom Event Parameters

Additional event attributes are sent as custom parameters according to your tracking needs. Define these parameters as [event attributes in the Tealium Customer Data Hub]().
