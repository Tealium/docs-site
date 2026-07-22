---
title: Using Tealium Functions for Acxiom Identity Resolution
description: This article describes how to use a visitor function to retrieve probabalistic identity data from the Acxiom identity provider and save it in the visitor profile.
url: https://docs.tealium.com/industries/tealium-identity-partners/acxiom-identity-resolution/
---
We recommend using a visitor function to capture the data from Acxiom. For more information on visitor functions, see [Event and Visitor Functions](https://docs.tealium.com/server-side/functions/event-visitor-functions/about/).

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

1.  Navigate to **Transform > Functions**.
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

For more information on creating a function, see [Managing Functions](https://docs.tealium.com/server-side/functions/manage-functions/create-function/).

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


<blockquote>
This code is currently in beta.
</blockquote>


```js
// In an event scoped function, the following modules are available for use: event, auth
import { event, store, tealium } from "tealium";
(async () => {
    
    // These endpoints will be specific to your setup with Acxiom.
    const access_url="https://mydomain.com/metrics/access_token"
    const query_url="https://mydomain.com/metrics"
    const query_name="demo_dsapi_match"

    // Uncomment this to find out exactly what is available to use in your event object
    //console.log('Data available:\n', JSON.stringify(event, null, 2));

    const data = {};
    data.tealium_account = event?.data?.udo?.tealium_account;
    data.tealium_profile = event?.data?.udo?.tealium_profile;
    data.visitor_id = event?.data?.udo?.visitor_id;
    data.trace_id = event?.data?.firstparty_tealium_cookies?.trace_id;
    data.acxiom_real_id = event?.data?.udo?.acxiom_real_id || "";
    data.customer_email = event?.data?.udo?.customer_email;
    data.customer_first_name = event?.data?.udo?.customer_first_name;
    data.customer_last_name = event?.data?.udo?.customer_last_name;
    data.customer_full_name = `${data.customer_first_name} ${data.customer_last_name}`

    // Check if acxiom_real_id is available
    // if (typeof data.acxiom_real_id === "undefined") {
    //     console.error("acxiom_entity_id is unavailable.");
    //     return;
    // }

    // Pull in refresh token from global variables
    const refresh_token = store.get("acxiom_refresh_token")
    console.log("refresh_token: ", refresh_token)

    // Generate access token
    const access_token_request = await fetch(access_url, {
        method: "POST",
        headers: {
            "Content-Type": "application/json",
            "Authorization": `Bearer ${refresh_token}`
        },
        body: `{"grant_type":"refresh_token","refresh_token":"${refresh_token}"}`
    })
    .catch((error) => {
        console.error('Error:', error);
    });
    const access_token_response = await access_token_request.json();
    // console.log("access_token_response:", JSON.stringify(access_token_response));
    const access_token = access_token_response.jwt_token;
    // console.log("access_token: ", access_token)

    // Fetch query_execution_id from Acxiom PAIL with acxiom_real_id
    const response = await fetch(`${query_url}/named_queries/${query_name}/execute`, {
        method: "POST",
        redirect: "follow",
        headers: {
            "Content-Type": "application/json",
            "Authorization": `Bearer ${access_token}`
        },
        body: `{
            "realID": "${data?.acxiom_real_id}", 
            "address": "${data?.customer_address}", 
            "phone": "${data?.customer_phone}", 
            "email": "${data?.customer_email}", 
            "fullName": "${data?.customer_full_name}"
        }`
    })
    .then(res => {
        console.log("Res: ", JSON.stringify(res))
        return res
    })
    // .then(response => console.log("Response: ", JSON.stringify(response)))
    .catch(error => console.error('Error: ', error.message));
    const body = await response.json();
    const query_execution_id = body.query_execution_id
    
    // console.log("Status: " + response.status);
    console.log("Body: " + JSON.stringify(body, null, 2));

    // Check if Acxiom response data is available
    if (!response.ok) {
        console.error("Acxiom response data is unavailable.");
        return;
    }

    // Fetch data from Acxiom PAIL with query_execution_id
    const payload = await fetch(`${query_url}/query_executions/${query_execution_id}`, {
        method: "GET",
        headers: {
            "Content-Type": "application/json",
            "Authorization": `Bearer ${access_token}`
        }
    })
    .then(res => {
        console.log("Res: ", JSON.stringify(res))
        return res
    })
    // .then(response => response.json())
    // .then(response => console.log("Response: ", JSON.stringify(response)))
    .catch(err => console.error(err));

    const user_data = await payload.json();
    console.log("user_data: ", JSON.stringify(user_data))

    let data_object = {};
    for (let i=0; i < user_data.column_info.length; i++) {
        data_object[user_data.column_info[i].name] = user_data.data[0][i]
    }
    // data_object = JSON.stringify(data_object)

    let newEvent = {};
    newEvent = { ...data_object }
    newEvent.tealium_event = "acxiom_function_event";
    newEvent.visitor_id = data.visitor_id;
    newEvent.tealium_trace_id = data?.tealium_trace_id;
    newEvent.customer_email = data_object?.email;
    
    console.log("newEvent: " + JSON.stringify(newEvent, null, 2));

    // Send data received from Acxiom to Tealium
    tealium
        .sendCollectEvent(newEvent, data.tealium_account, data.tealium_profile)
        .then(response => {
            console.log('Status code: ', response.status);
            return response;
        })
        .then(data => console.log('Result: ', JSON.stringify(data, null, 2)))
        .catch(error => console.error('Error: ', error.message));
})();
```
