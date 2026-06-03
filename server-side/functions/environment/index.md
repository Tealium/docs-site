---
title: Execution environment and rate limits
description: This article provides information on the execution environment, rate limits, and execution limits for functions.
url: https://docs.tealium.com/server-side/functions/environment/
---
## Execution environment

The execution environment for functions is built on the [GraalVM](https://www.graalvm.org/&#34;) JavaScript runtime and runs ECMAScript 2020-compatible code.

### Function limitations

* Functions cannot use third-party libraries except the libraries listed in [APIs and libraries for functions]().
* Functions can use up to 32 MB of memory.  
If a function attempts to use more than 32 MB, the following error is written to the log:  
`Exception 400 BAD REQUEST - OutOfMemoryError: memory limit 32 mb is exceeded.`
* The maximum function size is 64 KB, which is approximately 1500 lines of code.  
Functions larger than 64 KB cannot be saved until the size has been reduced.
* Function log messages are limited as follows:  
    * **Limit per function per account**: 5 MB of log messages per minute. If this limit is reached, logging for the function is throttled for 1 minute. When a function is throttled, information messages are not written to the log. Error and warning messages continue to be written to the log. Full logging resumes after 1 minute.
    * **Account limit for all functions**: 50 MB of log messages per minute. Currently, logging will not be throttled. If this limit is exceeded, Tealium may request that you limit the number of log messages.

### Runtime Versions

The execution environment for functions, referred to as the runtime version, varies depending on the function type, as follows:

 * **Data Transformation Functions**: The current runtime version is Transformation V0. For more information, see [About Data Transformation Functions]().
 * **Event and Visitor Functions**: The latest runtime version is Action V3. Existing functions use Action V2, which is deprecated. For more information, see the following:  
     * [Event and visitor functions V2]()
     * [Event and visitor functions V3]()
     * [Migrate a V2 function to V3]()
 * **CloudStream Data Record Transformation Functions**: The current runtime version is Transformation V1.
 * **CloudStream Data Record Functions**: The latest runtime version is CLS Action V1.

The runtime version for a function is shown in the **Code** tab of the code editor, as shown below: ![](/images/server-side/functions-runtime-version-location.png)

Runtime versions may be updated to provide new features. When a new runtime version is available, a message similar to the following is displayed on the **Functions Overview** page: ![](/images/server-side/functions-new-runtime-available.png)

As Tealium releases new runtime versions, older versions will be deprecated, and will eventually become obsolete. A message is displayed on the **Functions Overview** screen and on the **Code** tab for a function when the runtime version in use is deprecated or becomes obsolete.

## Execution time limits for event and data record transformation functions

Data transformation functions have the following execution limits:

* 1 hour of execution time per minute OR
* 250,000 invocations per minute (15 million per hour)
* 150 milliseconds of execution time for each function invocation  
    If a function exceeds the 150 milliseconds execution time, the following error is written to the log:  
    `Invocation timeout limit of 150 milliseconds is exceeded`

These execution limits are based on the account and the region. The sum of the execution time and the number of invocations for all functions in an account for a region cannot exceed these limits.

If either limit is exceeded, function execution is briefly stopped (throttled). The following message is displayed in the **Functions Overview** and a yellow alert icon is displayed next to a throttled function, as follows:

![](/images/server-side/throttle-msg.png)

For information on how to view details for throttled functions, see [View function statistics]().

## Execution time limits for event, visitor, and data record functions

Event, visitor, and data record functions have the following execution limits:

* Execution rate: 180,000 invocations per minute
* Execution time: 8 hours per minute
* Execution time for each function invocation: 10 seconds  
If a function exceeds the 10 seconds execution time, the following error is written to the log:  
`Exception 504 - Invocation timeout limit of 10000 milliseconds is exceeded.`

## Trace limits

When testing functions with trace, function calls are limited to 15 per minute.

## Execution rate and execution time: example 1

In this example, we assume a function that communicates with external APIs takes about 100 ms per invocation. In addition, we assume there is only one function configured for the account and the average execution rate of this function is 1000 invocations per second.

The execution rate and execution time within a 1-minute time window are as follows:

Execution rate = 1000 * 60 * 1 min = **execution rate of 60,000 invocations per minute**

Execution time = 1000 invocations/second * 100 ms / 1000 = 100 minutes = **1.66 hours execution time per minute**

In this case, the execution rate and execution time are both below the limits.

## Execution rate and execution time: example 2

In this example, we assume that external API performance temporarily degrades, and the function execution time is 800 ms per invocation. That means that the execution time is increased by 8.

Execution time = (1000 inv/s * 100 ms / 1000) * 8 = 800 minutes = **13.28 hours of execution time per minute**.

The execution time in this case is 13.28 hours per minute, which is greater than 8 hours/minute maximum. Function invocations may be throttled.