---
title: Event and visitor function examples (V2)
description: This article provides example code for V2 event and visitor functions.
url: https://docs.tealium.com/server-side/functions/event-visitor-functions/function-examples-v2/
---
## Send event data with HTTP POST

The following example shows how to make an HTTP POST request to an endpoint with event data in the request body JSON.

```
// Send event data - HTTP POST
import {event} from 'tealium';

console.log(JSON.stringify(event));

fetch('https://webhook.site/87bb160f-475a-4258-b117-693bb2378a4d',
    {
        method: 'POST',
        body: JSON.stringify(event),
        headers: {
            'Content-Type': 'application/json'
        }
    })
    .then(response => {
        if (!response.ok) {
            throw new Error('Network response was not ok. Status code: ${response.status}.');
        }
        return response.json();
    })
    .then(data => console.log('Response:', JSON.stringify(data)))
    .catch(error => console.log('Error:', error.message));
```

## Send event data with HTTP GET

The following example shows how to make an HTTP GET request to an endpoint with event data as query string parameters.

```
// Send event data - HTTP GET
import {event} from 'tealium';

console.log(JSON.stringify(event));

fetch(encodeURI('https://webhook.site/87bb160f-475a-4258-b117-693bb2378a4d?param=${event.data}'))
    .then(response => {
        if (!response.ok) {
            throw new Error('Network response was not ok. Status code: ${response.status}.');
        }
        return response.json();
    })
    .then(data => console.log('Response:', JSON.stringify(data)))
    .catch(error => console.log('Error:', error.message));
```

## Send visitor data with HTTP POST

The following example shows how to make an HTTP POST request to an endpoint with visitor profile data in the request body JSON.

```
// Send visitor data - HTTP POST
import {visitor} from 'tealium';

console.log(JSON.stringify(visitor));
fetch('https://webhook.site/87bb160f-475a-4258-b117-693bb2378a4d',
    {
        method: 'POST',
        body: JSON.stringify(visitor), 
        headers: {
            'Content-Type': 'application/json'
        }
    })
    .then(response => {
        if (!response.ok) {
            throw new Error('Network response was not ok. Status code: ${response.status}.');
        }
        return response.json();
    })
    .then(data => console.log('Response:', JSON.stringify(data)))
    .catch(error => console.log('Error:', error.message));
```

## Send visitor data with HTTP GET

The following example shows how to make an HTTP GET request to an endpoint with visitor profile data as query string parameters.

```
// Send visitor data - HTTP GET
import {visitor} from 'tealium';

console.log(JSON.stringify(visitor));

fetch(encodeURI('https://webhook.site/87bb160f-475a-4258-b117-693bb2378a4d?param=${visitor.data}'))
    .then(response => {
        if (!response.ok) {
            throw new Error('Network response was not ok. Status code: ${response.status}.');
        }
        return response.json();
    })
    .then(data => console.log('Response:', JSON.stringify(data)))
    .catch(error => console.log('Error:', error.message));
```

## Send an event to Tealium Collect

The following example shows how to send an event to the Tealium Collect HTTP API.

```js
import {event, tealium} from 'tealium';

var newEvent = {‘key’: ‘value’};

tealium.sendCollectEvent(newEvent, 'newAccount', 'newProfile', 'datasourceId')
    .then(response => {
        if (!response.ok) {
            throw new Error(`Network response was not ok. Status code: ${response.status}.`);
        }

        console.log('Status code:', response.status);
        return response.text();
    })
    .then(data => console.log('Result:', data))
    .catch(error => console.error('Error:', error.message));
```

## Retrieve visitor data and send it to Tealium Collect

In this example, the function uses the IP address to get the location city, gets weather information for that city, and sends the city and weather information to the Tealium Collect HTTP API.

```
import { auth, visitor, event } from "tealium";

console.log(JSON.stringify(visitor));

const ip_stack_api_key = 'your_api_key',
      weather_api_key = 'your_weather_api_key',
      ip_address = visitor?.current_visit?.properties?.ip_address;

console.log(ip_address);
(async function() {
    if(ip_address) {
    try {
        // Use IP address to get location city
        let city_response = await fetch('https://api.ipstack.com/${ip_address}?access_key=${ip_stack_api_key}&format=1'),
        city_data = await city_response.json();
        console.log(JSON.stringify(city_data));
        // Use location city to get local weather
        let weather_response = await fetch(encodeURI('https://api.openweathermap.org/data/2.5/weather?q=${city_data.city}&appid=${weather_api_key}')),
            weather_data = await weather_response.json();
            console.log(JSON.stringify(weather_data));
        // Send city and weather description back into collect endpoint
        await fetch(encodeURI('https://collect.tealiumiq.com/event?tealium_account=cloud-functions-usecases&tealium_profile=main&tealium_visitor_id=${visitor._id}&lookup_city=${weather_data?.name}&weather=${weather_data?.weather?.[0]?.description}&country=isp=${city_data?.connection?.isp}'));
    } catch(e) {
        console.error(e);
        return false;
    }
    } else {
        console.error("Could not locate users IP address")
    }
})();
```

## Get a Facebook authentication token

The following code example shows how to get a Facebook authentication token:

```
import { auth } from 'tealium';
const token = auth.get('facebook_token');

fetch('https://graph.facebook.com/v8.0/act_12345678/customaudiences??access_token=${token}&fields=approximate_count%2Csubtype%2Cname%2Cdata_source&limit=10')
  .then(response => response.json())
  .then(data => console.log('Data:', data))
  .catch(error => console.log('Error:', error.message));
```
## Send data to Facebook

This example shows how to send event data to the Facebook Graph or Marketing API to create a campaign. For more information on Facebook campaigns, see [https://developers.facebook.com/docs/marketing-api/reference/ad-campaign-group).](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign-group).

```
import {auth, event} from 'tealium';

const ACT_ID = 11111111111;
const ACCESS_TOKEN = auth.get("facebook_token");

fetch('https://graph.facebook.com/v8.0/act_${ACT_ID}/campaigns?access_token=${ACCESS_TOKEN}',
    {
        method: 'POST',
        body: 'name=${event.data}&objective=PAGE_LIKES&status=PAUSED&special_ad_categories=[]'
    })
    .then(response => {
            if (!response.ok) {
                throw new Error('Network response was not ok. Status code: ${response.status}.');
            }
            return response.json();
        })
    .then(data => console.log('Response:', JSON.stringify(data)))
    .catch(error => console.log('Error:', error.message));
```

## Create a Facebook campaign

This example shows how to create a Facebook campaign.

```
import { auth } from "tealium";

const ACT_ID = 11111111111;
const ACCESS_TOKEN = auth.get("facebook_token");

(async function () {
    console.time('function');
    try {
        console.log('Creating campaign...');
        let campaignId = await createCampaign({ campaignName: 'My Campaign' });
        console.log('Campaign ID', campaignId);

        console.log('Creating custom audience...');
        let customAudienceId = await createCustomAudience({ caName: 'My_Audience' });
        console.log('Custom Audience ID', customAudienceId);

        console.log('Creating ad set...');
        customAudienceId = 23846304008770411;
        let adSetId = await createAdSet({ campaignId: campaignId, customAudienceId: customAudienceId });
        console.log('Ad Set ID', adSetId);

        console.log('Creating ad creative...');
        // let adCreativeId = await createAdCreative();
        // current API call not working, use an ID created manually before
        let adCreativeId = 'adCreativeId';
        console.log('AdCreative ID ', adCreativeId);

        console.log('Creating ad...');
        let adId = await createAd({ adsetId: adSetId, adCreativeId: adCreativeId });
        console.log('Ad ID', adId);
        console.timeEnd('function');
    } catch (error) {
        console.log(error);
    }
})();

async function createAd({ adsetId, adCreativeId }) {
    const params = {
        'status': 'PAUSED',
        'adset_id': adsetId,
        'name': 'My Ad',
        'creative': { 'creative_id': adCreativeId },
    };

    let result = await fetch('https://graph.facebook.com/v7.0/act_${ACT_ID}/ads?access_token=${ACCESS_TOKEN}',
        {
            method: 'POST',
            body: jsonToRequestBodyString(params)
        });
    let json = await result.json();
    return json.id;
}

async function createAdSet({ campaignId, customAudienceId }) {
    const params = {
        'name': 'AdSet',
        'lifetime_budget': '1000',
        'start_time': '2020-07-01T23:41:41-0800',
        'end_time': '2020-07-07T23:41:41-0800',
        'campaign_id': campaignId,
        'bid_amount': '1',
        'billing_event': 'IMPRESSIONS',
        'optimization_goal': 'LINK_CLICKS',
        'targeting': {
            "geo_locations": {
                "countries": ["US"],
            },
            "age_min": 25,
            "age_max": 40,
            "custom_audiences": [{ "id": customAudienceId }]
        },
        'status': 'PAUSED'
    };
    let result = await fetch('https://graph.facebook.com/v7.0/act_${ACT_ID}/adsets?access_token=${ACCESS_TOKEN}',
        {
            method: 'POST',
            body: jsonToRequestBodyString(params)
        });
    let json = await result.json();
    return json.id;
}

async function createCustomAudience({ caName }) {
    const params = {
        'name': caName,
        'subtype': 'CUSTOM',
        'description': 'People who purchased on my website',
        'customer_file_source': 'USER_PROVIDED_ONLY',
    };
    let result = await fetch('https://graph.facebook.com/v7.0/act_${ACT_ID}/customaudiences?access_token=${ACCESS_TOKEN}',
        {
            method: 'POST',
            body: jsonToRequestBodyString(params)
        });
    let json = await result.json();
    return json.id;
}

async function createCampaign({ campaignName }) {
    const params = {
        'objective': 'LINK_CLICKS',
        'status': 'PAUSED',
        'buying_type': 'AUCTION',
        'name': campaignName,
        'special_ad_categories': 'NONE'
    };
    let result = await fetch('https://graph.facebook.com/v8.0/act_${ACT_ID}/campaigns?access_token=${ACCESS_TOKEN}',
        {
            method: 'POST',
            body: jsonToRequestBodyString(params)
        });
    let json = await result.json();
    return json.id;
}

function jsonToRequestBodyString(json) {
    return Object.keys(json).map(function (key) {
        return encodeURIComponent(key) + '=' +
            ((typeof json[key] === 'string' || json[key] instanceof String) ? encodeURIComponent(json[key]) : JSON.stringify(json[key]));
    }).join('&');
}
```

## Use the fetch() API to make HTTP requests

The fetch API is available for functions to make HTTP requests, as shown in the following example. For more information, see [Fetch](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/fetch).

```
fetch('https://restcountries.eu/rest/v2/name/usa')
  .then(response => {
    if (!response.ok) {
      throw new Error(`Network response was not ok. Status code: ${response.status}.`);
    }
    return response.json();
  })
  .then(data => console.log('Capital:', data[0].capital))
  .catch(error => console.log('Error:', error.message));
```

The following example shows fetching a resource from the network, returning a promise that is fulfilled when the response is available.

```
const fetchResponsePromise = fetch(resource [, init])
```

The Request interface of the Fetch API represents a resource request and is defined as follows:

```
const myRequest = new Request(input[, init]);
```

Functions can use the Headers interface of the Fetch API to perform various actions on HTTP request and response headers. Headers() is defined as follows:

```
const myHeaders = new Headers(init);
```

The Response interface of the Fetch API represents the response to a request and is defined as follows:

```
const myResponse = new Response(body, init);
```

The following browser-specific functionality is not supported:

*   cache
*   credentials
*   referrer
*   referrerPolicy
*   signal
*   keepalive
*   redirect
*   mode

## Use URLSearchParams methods to build a URL query string

The URLSearchParams interface defines utility methods to work with the query string of a URL. This example shows using URLSearchParams to build a query string for a URL.

```
function jsonToURLSearchParams(data) {    const params = new URLSearchParams();    buildURLSearchParams(params, data);    return params;}function buildURLSearchParams(params, data, parentKey) {
    if (data && typeof data === 'object' && !(data instanceof Date)) {
        Object.keys(data).forEach(key => {
            buildURLSearchParams(params, data[key], parentKey ? `${parentKey}[${key}]` : key);
        });
    } else {
        const value = data == null ? '' : data;

        params.append(parentKey, value);
    }
}
```

## Get the value of a global variable

The following code example shows how to use `store.get()` to retrieve a global variable, `Cloud_function_URL`, that contains the URL for a Google cloud function, and then use this URL to invoke the Google cloud function.

```
const cfunction_url = store.get("Cloud_function_URL");
 
let headers = {
            "content-type": "application/json",
            "mute-http-exceptions": "true"
        };
 
// code to populate body parameter goes here

const response = await fetch(cfunction_url, {
            method: "POST",
            headers: headers,
            body: body
        });
```

## Get an attribute name or value by attribute ID

Attribute names can be changed, which can cause problems when code references attributes by name. When  the attribute name is changed, the attribute ID is not changed. To avoid problems with attribute names changing, you can reference attributes by ID by using the `getAttrNameById()` and `getAttrValueByID()` methods provided by the `event` and `visitor` objects. The following example shows how this works.


<blockquote>
We recommend using the `getAttrValueByID()` method sparingly. This method recursively searches the properties of the event or visitor object to locate the value. If your event or visitor object is complex, this operation may increase the computation time of your function invocation.
</blockquote>


When you add `getAttrNameById()` or `getAttrValueByID()` to a function, the code completion feature helps you select the attribute ID to use in the method. For example, if you enter the following in the code editor, when you enter the opening parenthesis, the code completion feature shows a list of attributes and associated IDs: ![](https://docs.tealium.com/images/server-side/functions-code-completion-attr-name.png)

You can enter part of the attribute name to filter the list. When you select an attribute, its ID is added to your code after the parenthesis.