---
title: About functions
description: Functions are small blocks of JavaScript code that you can use to extend Tealium functionality. This article provides information on function types and the key benefits of functions.
url: https://docs.tealium.com/server-side/functions/about/
---
## Function types

Tealium currently supports the following function types:

* **Data Transformation Functions**: Functions that are triggered after an event is received by Tealium Collect and when the trigger conditions for the function are met.
For more information, see [About Data Transformation Functions]().
* **Event Functions**: Functions that are triggered after an event is processed. For more information, see [About Event and Visitor Functions]().
To use functions that are triggered by processed events, you must have Tealium EventStream API Hub enabled. For more information, see [Introduction to EventStream]().
* **Visitor Functions**: Functions that are triggered after a visitor is processed. For more information, see [About Event and Visitor Functions](). To use functions that are triggered by processed visitors, you must have Tealium AudienceStream CDP enabled. For more information, see [Introduction to AudienceStream]().
<!-- * **Data Record Functions**: Functions that are triggered after a data record is processed. To use functions that are triggered by processed data records, you must have a CloudStream profile. For more information, see [About CloudStream](). -->

## Key benefits

Functions provides a serverless environment that lets you extend the functionality of the Customer Data Hub to suit your needs.

### Serverless environment

In the serverless functions environment, functions are hosted on the Tealium Platform. Tealium manages the servers and platform software and you can focus on implementing functions for your unique data needs. Resources, such as memory, are allocated automatically each time a function is invoked. For more information, see [execution environment and rate limits]().

### Extend the Customer Data Hub

You can use data transformation functions to modify incoming event data. For example, a data transformation function can flatten nested objects, remove sensitive data, or populate variables in the event object.

You can use event and visitor functions to retrieve data from other systems, augment Tealium data, or send data to other endpoints. If a function modifies visitor or event data, the changes are local to the function and do not affect the Tealium data. Functions can send the modified data to Tealium Collect, where it is processed again and the changes are reflected in Tealium data.


<blockquote>
There is a cost associated with sending event or visitor data to the Tealium Collect endpoint because the number of events is increased each time data is sent. For more information, see [Billing estimation](https://docs.tealium.com/understanding-the-usage-report/#billing-estimation).
</blockquote>

