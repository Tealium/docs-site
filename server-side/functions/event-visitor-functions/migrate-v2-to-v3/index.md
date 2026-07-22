---
title: Migrate a V2 function to the V3 runtime
description: New event and visitor functions use the **Action V3** runtime. Existing functions that use the **Action V2** runtime need to be migrated to the **Action V3** runtime. This article provides information on the migration process.
url: https://docs.tealium.com/server-side/functions/event-visitor-functions/migrate-v2-to-v3/
---
## How V3 and V2 functions differ

Event and visitor functions that use the V3 runtime differ from V2 functions as follows:

* **Parameters and named exports** &ndash; Input data is provided as parameters instead of named exports.
  * An event function has two parameters: `event` and `helper`.  
  * A visitor function has three parameters: `visitor`, `visit`, and `helper`.
*  **Helper functions** &ndash; The `helper` object is used to get an authentication token ID or retrieve global variables.
    * `auth.get()` has been replaced with `helper.getAuth()`.
    * `store.get()` has been replaced with `helper.getGlobalVariable()`.
* **Collect event**
  * `tealium.sendCollectEvent()` has been replaced by `track()`, which uses named parameters.



<blockquote>
Data transformation functions use the **Transformation V0** runtime and are not affected by the release of the V3 runtime.
</blockquote>


### Example V2 function 

The following code examples show a V2 event function that sends an event to the collect endpoint and the V3 version of this event function.



```js
import { event, tealium } from "tealium";
(async () => {
    const searchQuery = new URLSearchParams({ path: event.data.dom.pathname, query: event.data.dom.search_query });
    
    const newEvent = await fetch(`https://getnew.event.com?${searchQuery}`)
        .then(response => {
            if (!response.ok) {
                throw new Error(`Network response was not ok. Status code: ${response.status}.`);
            }
            return response.json();
        });
    
    tealium.sendCollectEvent(
        newEvent,
        event.account,
        event.profile,
        'abc123')
        .then(response => {
            if(!response.ok){
                throw new Error(`Network response was not ok. Status code: ${response.status}.`);
            }
            return response.text();
        })
        .then(data => console.log('Result : ', data))
        .catch(error => console.error('Error:', error.message));
})();
```


```js
activate(async ({ event }) => {  
    const searchQuery = new URLSearchParams({ path: event.data.dom.pathname, query: event.data.dom.search_query });
        
    const newEvent = await fetch(`https://getnew.event.com?${searchQuery}`)
        .then(response => {
            if (!response.ok) {
                throw new Error(`Network response was not ok. Status code: ${response.status}.`);
            }
            return response.json();
        });
        
    track(newEvent, {
        tealium_account: event.account,
        tealium_profile: event.profile,
        tealium_datasource: 'abc123'
        })
        .then(response => {
            if(!response.ok){
                throw new Error(`Network response was not ok. Status code: ${response.status}.`);
            }
            return response.text();
        })
        .then(data => console.log('Result : ', data))
        .catch(error => console.error('Error:', error.message));
})();
```



## Create a V3 function

To migrate an event or visitor function to V3, create a V3 event or visitor function, depending on the type of function to be migrated. For more information, see [Create a function](). Then do the following:

1. In the code editor, delete all of the default code for the V3 function, then add the following event or visitor code, which is an empty function.  
We will add the function code in the next step, then modify the code. 


```js
activate(async ({ event }) => {  

});
```


```js
activate(async ({ visitor, visit }) => {  

});
```



1. Copy the code from the V2 function, starting after the first line of the function, shown below:  
    ```js
    (async (event, helper) => {
    ```  
    and ending above the last line of the function:
    ```js
    })();
     ```  
1. Paste the copied code into the empty V3 function, between the `activate` line and the ending line `});`.

## Update the function code

If your function uses libraries or helper functions, or sends events to Tealium Collect, the code copied into the empty function needs to be modified as described in the following sections.

### Send events to Tealium Collect

The example function uses `tealium.sendCollectEvent()`. This call needs to be replaced with a `track()` call. The examples below show the V2 `tealium.sendCollectEvent()` call and the V3 `track()` call.



```js
import { event, tealium } from 'tealium';

(async () => {
    const newEvent = { data: event.data.udo };

    tealium.sendCollectEvent(newEvent,
        event.account,
        event.profile,
        'abc123')
    ...
})();
```


```js
activate(({ event }) => {
    const newEvent = { data: event.data.udo };

    track(newEvent, {
        tealium_account: event.account,
        tealium_profile: event.profile,
        tealium_datasource: 'abc123'
    })
    ...
})
```



In the `track()` call, replace `'abc123'` with your data source key.

### Use libraries

If your V2 function uses libraries, such as CrytpoES, add the import line before the `activate` line.



```js
import { event, tealium } from "tealium";
import CryptoES from 'crypto-es';
...
```


```js
import CryptoES from 'crypto-es';
activate(async ({ event, helper }) => {  
    ...
});
```  



### Authentication tokens and global variables

If your V2 function uses authentication tokens or global variables, add `helper` to the function parameters in the `activate` line of the V3 function. For example:  

```js
activate(async ({ event, helper }) => {
});
```

Replace any instances of `auth.get()` in the V2 code with `helper.getAuth()`. For example:



```js
import { auth } from 'tealium';

const token = auth.get("myAuthToken");
```


```js
activate(({event, helper }) => {
    const token = helper.getAuth("myAuthToken");
})
```




<blockquote>
Authentication tokens can only be referenced by a function within an HTTP request. If you try to reference the token outside of an HTTP request, the token is replaced by a UUID placeholder.
</blockquote>


Replace any instances of `store.get()` with `helper.getGlobalVariable()`. For example: 



```js
import {store } from 'tealium';

const gVar = store.get("myGlobalVar");
```


```js
activate(({event, helper }) => {    
    const gVar = helper.getGlobalVariable("myGlobalVar");
})
```


