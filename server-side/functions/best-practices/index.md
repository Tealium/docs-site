---
title: Functions best practices
description: This article provides best practices for functions to avoid exceeding the memory and execution time limits.
url: https://docs.tealium.com/server-side/functions/best-practices/
---
## Run tests to determine execution time

Data transformation functions are limited to 150 ms of execution time. Event and visitor functions are limited to 10 seconds of execution time.

There are a lot of factors that affect function execution time. To verify that a function can execute in the allowed time, run several tests with the expected event payload.

## Normalize the universal data object (UDO)

The data layer contains basic information about the page where the event occurred. The UDO is a more dynamic structure that contains information for specific event type, which means the size of the event may vary. The recommended maximum event size is 50 KB. To keep the data compact, remove redundant data entries. If the same data occurs in multiple fields (for example, in the data layer and in the UDO), it is a candidate for removal from the UDO. If a chunk of data is not required for a particular event type, it is also a candidate for removal from the event UDO.

## Use partial import for standard modules

The execution environment provides standard modules that support partial import, including CryptoES.

Import only the required functionality for a module, instead of importing the entire module. For example:

```
import { MD5 } from 'crypto-es/lib/md5.js';
```

## Avoid the use of debugging log messages

Before publishing a function to your production environment, remove or comment out `console.log` messages that are used for debugging purposes.

For example, avoid using `JSON.stringify` to send the entire event to the log. Use log messages for specific variables instead, as shown in the following example:

```
console.log(event.data.udo.property_to_track);
```

## Use the flatten() built-in module

The built-in `flatten()` module can be used to flatten any nested object, which is particularly useful for data transformation functions. Transformation functions can work with nested data structures, such as arrays of objects or nested objects, but need to flatten the incoming event so that it does not contain nested data structures.

## Use JavaScript optimizations

Use JavaScript optimizations for intensive tasks, such as iterating over an array or object properties.

### Example of iterating over an array

```js
const array = [1, 2, 3];
const arrayLength = array.length;

for (let i = 0; i < arrayLength; i++) {
    const arrayItem = array[i];
}
```

### Example of iterating over object properties

```js
const obj = { a: 1, b: 2, c: 3 };
const keys = Object.getOwnPropertyNames(obj);
const keysLength = keys.length;

for (let i = 0; i < keysLength; i++) {
    const keyName = keys[i];
    const value = obj[keyName];
}
```

## Reference authentication tokens only within HTTP requests

Authentication tokens are available only when a function runs within the context of an HTTP request. If you reference an authentication token outside of an HTTP request, the system replaces the token with a UUID placeholder.

```js
// Correct: Access token inside HTTP request handler
activate(async ({ visitor, helper }) => {
  const response = await fetch(
    "https://fcm.googleapis.com/v1/projects/YOURPROJECT/messages:send",
    {
      method: "POST",
      headers: {
        'Authorization': 'Bearer ' + helper.getAuth('firebase_cloud_messaging'),
        'Content-Type': 'application/json'
      },
      body:body
    }
  );
});
}

// Incorrect: Access token outside HTTP request handler
const token = helper.getAuth('firebase_cloud_messaging'); // This will be replaced by a UUID placeholder
```