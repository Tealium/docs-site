---
title: Using Tealium Functions for Acxiom Identity Resolution
description: This article describes how to use a visitor function to retrieve probabalistic identity data from the Acxiom identity provider and save it in the visitor profile.
url: https://docs.tealium.com/industries/tealium-identity-partners/acxiom-identity-resolution/
---
We recommend using a visitor function to capture the data from Acxiom. For more information on visitor functions, see [Event and Visitor Functions](/server-side/functions/event-visitor-functions/about/).

The visitor function does the following:

*   Requests the additional data from Acxiom.
*   Sends an event containing the additional data and `tealium_visitor_id` to Tealium Collect.

The EventStream attributes and visitor attributes are enriched by the event sent from the function.

## Prerequisites

*   Tealium EventSteam and Tealium Functions.
*   The Tealium Collect API as a data source.
*   Visitor attributes to store the additional information.
*   An event specification titled `acxiom_function_event` with the attributes required to enrich the visitor attributes.
*   An enrichment to set the visitor attributes to the value of the event attributes.

The function works best when the Acxiom Real Tag tag is installed. This identifier increases the confidence rating for the visitor.

## Creating a function to process the event

To create the function:

1.  Navigate to **Transform &gt; Functions**.
2.  Click **Add Function**.
3.  Enter a name for the function.
4.  Enter notes to describe the function.
5.  Select the **Processed Event** trigger.
6.  Select the event feed for the trigger.
7.  Click **Continue**.
8.  Enter the sample code below into the **Code** box.
9.  Customize the code as necessary for your configuration.
10.  Save the function.

You can test the function with the **Test** feature and a tool such as Postman API Workbench.

For more information on creating a function, see [Managing Functions](/server-side/functions/manage-functions/create-function/).

## Example function code

The test example function included below attempts to match a visitor profile based off of the attributes you send to it:

| Attribute | Description |
| --------- | ----------- |
| `acxiom_function_event` | Event Spec name |
| `realId`   | Acxiom rTag |
| `address`  | User’s address |
| `phone`    | User’s phone number |
| `email`    | User’s email address |
| `fullName` | User’s full name |

The function returns any additional user data for profile enrichment.

This code is currently in beta.

```js
// In an event scoped function, the following modules are available for use: event, auth
import { event, store, tealium } from &#34;tealium&#34;;
(async () =&gt; {
    
    // These endpoints will be specific to your setup with Acxiom.
    const access_url=&#34;https://mydomain.com/metrics/access_token&#34;
    const query_url=&#34;https://mydomain.com/metrics&#34;
    const query_name=&#34;demo_dsapi_match&#34;

    // Uncomment this to find out exactly what is available to use in your event object
    //console.log(&#39;Data available:\n&#39;, JSON.stringify(event, null, 2));

    const data = {};
    data.tealium_account = event?.data?.udo?.tealium_account;
    data.tealium_profile = event?.data?.udo?.tealium_profile;
    data.visitor_id = event?.data?.udo?.visitor_id;
    data.trace_id = event?.data?.firstparty_tealium_cookies?.trace_id;
    data.acxiom_real_id = event?.data?.udo?.acxiom_real_id || &#34;&#34;;
    data.customer_email = event?.data?.udo?.customer_email;
    data.customer_first_name = event?.data?.udo?.customer_first_name;
    data.customer_last_name = event?.data?.udo?.customer_last_name;
    data.customer_full_name = `${data.customer_first_name} ${data.customer_last_name}`

    // Check if acxiom_real_id is available
    // if (typeof data.acxiom_real_id === &#34;undefined&#34;) {
    //     console.error(&#34;acxiom_entity_id is unavailable.&#34;);
    //     return;
    // }

    // Pull in refresh token from global variables
    const refresh_token = store.get(&#34;acxiom_refresh_token&#34;)
    console.log(&#34;refresh_token: &#34;, refresh_token)

    // Generate access token
    const access_token_request = await fetch(access_url, {
        method: &#34;POST&#34;,
        headers: {
            &#34;Content-Type&#34;: &#34;application/json&#34;,
            &#34;Authorization&#34;: `Bearer ${refresh_token}`
        },
        body: `{&#34;grant_type&#34;:&#34;refresh_token&#34;,&#34;refresh_token&#34;:&#34;${refresh_token}&#34;}`
    })
    .catch((error) =&gt; {
        console.error(&#39;Error:&#39;, error);
    });
    const access_token_response = await access_token_request.json();
    // console.log(&#34;access_token_response:&#34;, JSON.stringify(access_token_response));
    const access_token = access_token_response.jwt_token;
    // console.log(&#34;access_token: &#34;, access_token)

    // Fetch query_execution_id from Acxiom PAIL with acxiom_real_id
    const response = await fetch(`${query_url}/named_queries/${query_name}/execute`, {
        method: &#34;POST&#34;,
        redirect: &#34;follow&#34;,
        headers: {
            &#34;Content-Type&#34;: &#34;application/json&#34;,
            &#34;Authorization&#34;: `Bearer ${access_token}`
        },
        body: `{
            &#34;realID&#34;: &#34;${data?.acxiom_real_id}&#34;, 
            &#34;address&#34;: &#34;${data?.customer_address}&#34;, 
            &#34;phone&#34;: &#34;${data?.customer_phone}&#34;, 
            &#34;email&#34;: &#34;${data?.customer_email}&#34;, 
            &#34;fullName&#34;: &#34;${data?.customer_full_name}&#34;
        }`
    })
    .then(res =&gt; {
        console.log(&#34;Res: &#34;, JSON.stringify(res))
        return res
    })
    // .then(response =&gt; console.log(&#34;Response: &#34;, JSON.stringify(response)))
    .catch(error =&gt; console.error(&#39;Error: &#39;, error.message));
    const body = await response.json();
    const query_execution_id = body.query_execution_id
    
    // console.log(&#34;Status: &#34; &#43; response.status);
    console.log(&#34;Body: &#34; &#43; JSON.stringify(body, null, 2));

    // Check if Acxiom response data is available
    if (!response.ok) {
        console.error(&#34;Acxiom response data is unavailable.&#34;);
        return;
    }

    // Fetch data from Acxiom PAIL with query_execution_id
    const payload = await fetch(`${query_url}/query_executions/${query_execution_id}`, {
        method: &#34;GET&#34;,
        headers: {
            &#34;Content-Type&#34;: &#34;application/json&#34;,
            &#34;Authorization&#34;: `Bearer ${access_token}`
        }
    })
    .then(res =&gt; {
        console.log(&#34;Res: &#34;, JSON.stringify(res))
        return res
    })
    // .then(response =&gt; response.json())
    // .then(response =&gt; console.log(&#34;Response: &#34;, JSON.stringify(response)))
    .catch(err =&gt; console.error(err));

    const user_data = await payload.json();
    console.log(&#34;user_data: &#34;, JSON.stringify(user_data))

    let data_object = {};
    for (let i=0; i &lt; user_data.column_info.length; i&#43;&#43;) {
        data_object[user_data.column_info[i].name] = user_data.data[0][i]
    }
    // data_object = JSON.stringify(data_object)

    let newEvent = {};
    newEvent = { ...data_object }
    newEvent.tealium_event = &#34;acxiom_function_event&#34;;
    newEvent.visitor_id = data.visitor_id;
    newEvent.tealium_trace_id = data?.tealium_trace_id;
    newEvent.customer_email = data_object?.email;
    
    console.log(&#34;newEvent: &#34; &#43; JSON.stringify(newEvent, null, 2));

    // Send data received from Acxiom to Tealium
    tealium
        .sendCollectEvent(newEvent, data.tealium_account, data.tealium_profile)
        .then(response =&gt; {
            console.log(&#39;Status code: &#39;, response.status);
            return response;
        })
        .then(data =&gt; console.log(&#39;Result: &#39;, JSON.stringify(data, null, 2)))
        .catch(error =&gt; console.error(&#39;Error: &#39;, error.message));
})();
```
