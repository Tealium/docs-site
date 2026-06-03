---
title: Function triggers
description: This article provides information on triggers for each function type.
url: https://docs.tealium.com/server-side/functions/triggers/
---
Functions are triggered by events at different points in the data pipeline, depending on the function type.

## Data transformation functions

Data transformation functions have custom triggers, which are rules that specify the conditions that trigger execution of a function. If the trigger conditions for a data transformation function are met, the function is invoked after the event or data record is collected from the data source and before the event or data record is processed, as shown in the following data pipeline diagram. Data transformation functions support all event types except for file import events.

![](/images/server-side/functions-transform-data-pipeline.png)

Only one function can be triggered by a custom trigger. If an event or data record matches more than one function trigger, the function with the oldest **Date Modified** is the only function that is triggered.

For more information, see [About Data Transformation Functions]().

## Event and visitor functions
&lt;!-- ## Event, visitor, and data record functions --&gt;

[Event functions]() are invoked after the event has been processed, as shown in the following data pipeline diagram:

![](/images/server-side/functions-event-data-pipeline.png)

[Visitor functions]() are invoked after the visitor has been processed, as shown in the following data pipeline diagram:

![](/images/server-side/functions-visit-visitor-data-pipeline.png)

&lt;!--&gt;

[CloudStream data record functions]() functions are invoked after the data record has been processed, as shown in the following data pipeline diagram:

![](/images/server-side/functions-data-record-pipeline.png)

--&gt;