---
title: Event and visitor functions examples (V3)
description: This article provides example code for V3 event and visitor functions.
url: https://docs.tealium.com/server-side/functions/event-visitor-functions/v3-function-examples/
---
## Send event data with HTTP GET

The following example shows how to make an HTTP GET request to an endpoint with event data as query string parameters.

```js
activate(({ event }) =&gt; {
    console.log(JSON.stringify(event));

    fetch(encodeURI(`https://webhook.site/87bb160f-475a-4258-b117-693bb2378a4d?param=${event.data}`))
        .then(response =&gt; {
            if (!response.ok) {
                throw new Error(`Network response was not ok. Status code: ${response.status}.`);
            }
            return response.json();
        })
        .then(data =&gt; console.log(&#39;Response:&#39;, JSON.stringify(data)))
        .catch(error =&gt; console.log(&#39;Error:&#39;, error.message)); 
})
```

## Send visitor data with HTTP POST

The following example shows how to make an HTTP POST request to an endpoint with visitor profile data in the request body JSON.

```js
activate(({ visitor }) =&gt; {
    console.log(JSON.stringify(visitor));

    fetch(&#39;https://webhook.site/87bb160f-475a-4258-b117-693bb2378a4d&#39;,
        {
            method: &#39;POST&#39;,
            body: JSON.stringify(visitor), 
            headers: {
                &#39;Content-Type&#39;: &#39;application/json&#39;
            }
        })
        .then(response =&gt; {
            if (!response.ok) {
                throw new Error(`Network response was not ok. Status code: ${response.status}.`);
            }
            return response.json();
        })
        .then(data =&gt; console.log(&#39;Response:&#39;, JSON.stringify(data)))
        .catch(error =&gt; console.log(&#39;Error:&#39;, error.message));
})
```

## Send visitor data with HTTP GET

The following example shows how to make an HTTP GET request to an endpoint with visitor profile data as query string parameters.

```js
activate(({ visit }) =&gt; {
    console.log(JSON.stringify(visit)); // notice separate visit property

    fetch(encodeURI(`https://webhook.site/87bb160f-475a-4258-b117-693bb2378a4d?param=${visit.creation_ts}`))
        .then(response =&gt; {
            if (!response.ok) {
                throw new Error(`Network response was not ok. Status code: ${response.status}.`);
            }
            return response.json();
        })
        .then(data =&gt; console.log(&#39;Response:&#39;, JSON.stringify(data)))
        .catch(error =&gt; console.log(&#39;Error:&#39;, error.message));
})
```

## Send an event to the Tealium Collect HTTP API

The following example shows how to fetch data and send an event to Tealium Collect.

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
            tealium_datasource: &#39;p9v81m&#39;
        })
        .then(response =&gt; {
            if(!response.ok){
                throw new Error(`Network response was not ok. Status code: ${response.status}.`);
            }
            return response.text();
        })
        .then(data =&gt; console.log(&#39;Result : &#39;, data))
        .catch(error =&gt; console.error(&#39;Error:&#39;, error.message));
})
```

## Use an authentication access token in a call to a service provider

This example uses OAuth 2.0 authentication to make API calls to Google Firebase Cloud Messaging. The access token, which is created when you add OAuth2.0 authentication to a function, is passed as a parameter to `helper.getAuth()`. The following figure shows the access token for this example function:
![](/images/server-side/functions-editor-advanced-tab.png)

The following code examples show how to call `helper.getAuth()` to retrieve the authentication when making an API call to send a message with firebase cloud messaging:



```js
activate(async ({ visitor, helper }) =&gt; {
  const response = await fetch(
    &#34;https://fcm.googleapis.com/v1/projects/YOURPROJECT/messages:send&#34;,
    {
      method: &#34;POST&#34;,
      headers: {
        &#39;Authorization&#39;: &#39;Bearer &#39;&#43;helper.getAuth(&#39;firebase_cloud_messaging&#39;),
        &#39;Content-Type&#39;: &#39;application/json&#39;
      },
      body:body
    }
  );
});
```


```js
const response = await fetch(
  &#34;https://fcm.googleapis.com/v1/projects/YOURPROJECT/messages:send&#34;,
  {
    method: &#34;POST&#34;,
    headers: {
      `Authorization&#39;: &#39;Bearer &#39;&#43;auth.get(&#39;firebase_cloud_messaging&#39;),
      &#39;Content-Type&#39;: &#39;application/json&#39;
    },
    body:body
  }
);
```



Authentication tokens can only be referenced by a function within an HTTP request. If you try to reference the token outside of an HTTP request, the token is replaced by a UUID placeholder.

## Get the value of a global variable

The following code example shows how to use `helper.getGlobalVariable()` to retrieve a global variable, `Cloud_function_URL`, that contains the URL for a Google cloud function, and then use this URL to invoke the Google cloud function.

```js
const cfunction_url = helper.getGlobalVariable(&#34;Cloud_function_URL&#34;);

let headers = {
            &#34;content-type&#34;: &#34;application/json&#34;,
            &#34;mute-http-exceptions&#34;: &#34;true&#34;
        };

// code to populate body parameter goes here

const response = await fetch(cfunction_url, {
            method: &#34;POST&#34;,
            headers: headers,
            body: body
        });
```

For information on creating a global variable, see [Add a global variable for event or visitor functions]().

## Get an attribute name or attribute value by attribute ID

Attribute names can be changed, which can cause problems when code references attributes by name. When  the attribute name is changed, the attribute ID is not changed. To avoid problems with attribute names changing, you can reference attributes by ID by using the `getAttrNameById()` and `getAttrValueByID()` methods provided by the `event`, `visitor`, and `visit` objects.

We recommend using the `getAttrValueByID()` method sparingly. This method recursively searches the properties of the event or visitor object to locate the value. If your event or visitor object is complex, this operation may increase the computation time of your function invocation.

When you add `getAttrNameById()` or `getAttrValueByID()` to a function, the code completion feature helps you select the attribute ID to use in the method. For example, if you enter the following in the code editor, when you enter the opening parenthesis, the code completion feature shows a list of attributes and associated IDs: ![](/images/server-side/functions-code-completion-attr-name.png)

You can enter part of the attribute name to filter the list. When you select an attribute, its ID is added to your code after the parenthesis.