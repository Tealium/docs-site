---
title: Functions code editor
description: This article provides information on the features of the functions code editor.
url: https://docs.tealium.com/server-side/functions/code-editor/
---
The Tealium Functions code editor provides tabs for creating, configuring, testing, and monitoring functions, as well as viewing logs and getting an authentication token.

![](https://docs.tealium.com/images/server-side/functions-code-editor.png)

## Code tab

When you create a new function, the **Code** tab displays example function code with explanations in comments. You can modify the example code, or replace it with your own code.

## Monitoring tab

The **Monitoring** tab displays the following function statistics for the last hour, 12 hours, day, 7 days, or 30 days:

* Invocations
* Average Execution Time
* Errors

## Logs tab

The **Logs** tab displays a list of log files from function execution. Log files are kept for 30 days. Functions can use the JavaScript console functions to write messages and errors to the log. For more information, see [JavaScript console API](https://docs.tealium.com/function-modules/#javascript-console-api).


## Configuration tab

Use the **Configuration** tab to change the function name, add or change notes about the function, or change the event or audience that triggers the function. The feed cannot be changed after the initial function configuration.

## Test tab

Use the **Test** tab to create a test payload and test your function. You can modify the example payload shown in the **Test** tab, or use test data from your website. For more information on obtaining test data from your website, see [Test Functions](). Test results and log files are available after the function is executed.

## Advanced tab

Use the **Advanced** tab to assign authentication tokens to a function.
