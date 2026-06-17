---
title: About event and visitor functions
description: This article provides information on event and visitor functions.
url: https://docs.tealium.com/server-side/functions/event-visitor-functions/about/
---
Event and visitor functions run at the end of the data pipeline, after the event or visitor is processed. Use event and visitor functions to retrieve data from other systems, augment Tealium data, or send data to other endpoints.

![](/images/server-side/functions-event-visitor-flow.svg)

If your function needs authentication to access an external system, see [Add authentication to a function]().

At this point in the data pipeline, modifications to the event or visitor data have no effect on other parts of the system. To modify an event, use either event attribute enrichments or an event transformation function. To modify a visitor profile, use visitor attribute enrichments.

## Action V2 and Action V3 runtimes

The Action V2 runtime is obsolete and is no longer supported. Functions that use the V2 runtime are still executing but you cannot save code changes. To save code changes, you need to update the runtime version, which may require changes to the function code. For information on the required code changes, see [Migrate a V2 function to the V3 runtime]().

The input data for event and visitor functions varies depending on the function type (event or visitor) and the runtime version (Action V2 or Action V3). Functions that use the Action V2 runtime have named exports for input data. Functions that use the Action V3 runtime receive data as input parameters.

In addition, V2 and V3 event and visitor functions differ in how they do the following:
* Get authentication for a service provider.
* Send an event to Tealium Collect.
* Retrieve global variables.
* Get an attribute name or value by attribute ID.
* Make an HTTP request using the fetch() API.

For more information, see:

* [Migrate a V2 function to the V3 runtime]()
* [Event and visitor functions V2]()
* [Event and visitor functions V3]()  