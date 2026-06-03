---
title: Migrate a V2 function to the V3 runtime
description: New event and visitor functions use the **Action V3** runtime. Existing functions that use the **Action V2** runtime need to be migrated to the **Action V3** runtime. This article provides information on the migration process.
url: https://docs.tealium.com/server-side/functions/event-visitor-functions/migrate-v2-to-v3/
---
## How V3 and V2 functions differ

Event and visitor functions that use the V3 runtime differ from V2 functions as follows:

* **Parameters and named exports** &amp;ndash; Input data is provided as parameters instead of named exports.
  * An event function has two parameters: `event` and `helper`.  
  * A visitor function has three parameters: `visitor`, `visit`, and `helper`.
*  **Helper functions** &amp;ndash; The `helper` object is used to get an authentication token ID or retrieve global variables.
    * `auth.get()` has been replaced with `helper.getAuth()`.
    * `store.get()` has been replaced with `helper.getGlobalVariable()`.
* **Collect event**
  * `tealium.sendCollectEvent()` has been replaced by `track()`, which uses named parameters.


Data transformation functions use the **Transformation V0** runtime and are not affected by the release of the V3 runtime.

### Example V2 function 

The following code examples show a V2 event function that sends an event to the collect endpoint and the V3 version of this event function.



```js
import { event, tealium } from &#34;tealium&#34;;
(async () =&gt; {
    const searchQuery = new URLSearchParams({ path: event.data.dom.pathname, query: event.data.dom.search_query });
    
    const newEvent = await fetch(`https://getnew.event.com?${searchQuery}`)
        .then(response =&gt; {
            if (!response.ok) {
                throw new Error(`Network response was not ok. Status code: ${response.status}.`);
            }
            return response.json();
        });
    
    tealium.sendCollectEvent(
        newEvent,
        event.account,
        event.profile,
        &#39;abc123&#39;)
        .then(response =&gt; {
            if(!response.ok){
                throw new Error(`Network response was not ok. Status code: ${response.status}.`);
            }
            return response.text();
        })
        .then(data =&gt; console.log(&#39;Result : &#39;, data))
        .catch(error =&gt; console.error(&#39;Error:&#39;, error.message));
})();
```


```js
activate(async ({ event }) =&gt; {  
    const searchQuery = new URLSearchParams({ path: event.data.dom.pathname, query: event.data.dom.search_query });
        
    const newEvent = await fetch(`https://getnew.event.com?${searchQuery}`)
        .then(response =&gt; {
            if (!response.ok) {
                throw new Error(`Network response was not ok. Status code: ${response.status}.`);
            }
            return response.json();
        });
        
    track(newEvent, {
        tealium_account: event.account,
        tealium_profile: event.profile,
        tealium_datasource: &#39;abc123&#39;
        })
        .then(response =&gt; {
            if(!response.ok){
                throw new Error(`Network response was not ok. Status code: ${response.status}.`);
            }
            return response.text();
        })
        .then(data =&gt; console.log(&#39;Result : &#39;, data))
        .catch(error =&gt; console.error(&#39;Error:&#39;, error.message));
})();
```



## Create a V3 function

To migrate an event or visitor function to V3, create a V3 event or visitor function, depending on the type of function to be migrated. For more information, see [Create a function](). Then do the following:

1. In the code editor, delete all of the default code for the V3 function, then add the following event or visitor code, which is an empty function.  
We will add the function code in the next step, then modify the code. 


```js
activate(async ({ event }) =&gt; {  

});
```


```js
activate(async ({ visitor, visit }) =&gt; {  

});
```



1. Copy the code from the V2 function, starting after the first line of the function, shown below:  
    ```js
    (async (event, helper) =&gt; {
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
import { event, tealium } from &#39;tealium&#39;;

(async () =&gt; {
    const newEvent = { data: event.data.udo };

    tealium.sendCollectEvent(newEvent,
        event.account,
        event.profile,
        &#39;abc123&#39;)
    ...
})();
```


```js
activate(({ event }) =&gt; {
    const newEvent = { data: event.data.udo };

    track(newEvent, {
        tealium_account: event.account,
        tealium_profile: event.profile,
        tealium_datasource: &#39;abc123&#39;
    })
    ...
})
```



In the `track()` call, replace `&#39;abc123&#39;` with your data source key.

### Use libraries

If your V2 function uses libraries, such as CrytpoES, add the import line before the `activate` line.



```js
import { event, tealium } from &#34;tealium&#34;;
import CryptoES from &#39;crypto-es&#39;;
...
```


```js
import CryptoES from &#39;crypto-es&#39;;
activate(async ({ event, helper }) =&gt; {  
    ...
});
```  



### Authentication tokens and global variables

If your V2 function uses authentication tokens or global variables, add `helper` to the function parameters in the `activate` line of the V3 function. For example:  

```js
activate(async ({ event, helper }) =&gt; {
});
```

Replace any instances of `auth.get()` in the V2 code with `helper.getAuth()`. For example:



```js
import { auth } from &#39;tealium&#39;;

const token = auth.get(&#34;myAuthToken&#34;);
```


```js
activate(({event, helper }) =&gt; {
    const token = helper.getAuth(&#34;myAuthToken&#34;);
})
```



Authentication tokens can only be referenced by a function within an HTTP request. If you try to reference the token outside of an HTTP request, the token is replaced by a UUID placeholder.

Replace any instances of `store.get()` with `helper.getGlobalVariable()`. For example: 



```js
import {store } from &#39;tealium&#39;;

const gVar = store.get(&#34;myGlobalVar&#34;);
```


```js
activate(({event, helper }) =&gt; {    
    const gVar = helper.getGlobalVariable(&#34;myGlobalVar&#34;);
})
```


