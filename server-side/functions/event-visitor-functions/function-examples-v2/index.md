---
title: Event and visitor function examples (V2)
description: This article provides example code for V2 event and visitor functions.
url: https://docs.tealium.com/server-side/functions/event-visitor-functions/function-examples-v2/
---
## Send event data with HTTP POST

The following example shows how to make an HTTP POST request to an endpoint with event data in the request body JSON.

```
// Send event data - HTTP POST
import {event} from &#39;tealium&#39;;

console.log(JSON.stringify(event));

fetch(&#39;https://webhook.site/87bb160f-475a-4258-b117-693bb2378a4d&#39;,
    {
        method: &#39;POST&#39;,
        body: JSON.stringify(event),
        headers: {
            &#39;Content-Type&#39;: &#39;application/json&#39;
        }
    })
    .then(response =&gt; {
        if (!response.ok) {
            throw new Error(&#39;Network response was not ok. Status code: ${response.status}.&#39;);
        }
        return response.json();
    })
    .then(data =&gt; console.log(&#39;Response:&#39;, JSON.stringify(data)))
    .catch(error =&gt; console.log(&#39;Error:&#39;, error.message));
```

## Send event data with HTTP GET

The following example shows how to make an HTTP GET request to an endpoint with event data as query string parameters.

```
// Send event data - HTTP GET
import {event} from &#39;tealium&#39;;

console.log(JSON.stringify(event));

fetch(encodeURI(&#39;https://webhook.site/87bb160f-475a-4258-b117-693bb2378a4d?param=${event.data}&#39;))
    .then(response =&gt; {
        if (!response.ok) {
            throw new Error(&#39;Network response was not ok. Status code: ${response.status}.&#39;);
        }
        return response.json();
    })
    .then(data =&gt; console.log(&#39;Response:&#39;, JSON.stringify(data)))
    .catch(error =&gt; console.log(&#39;Error:&#39;, error.message));
```

## Send visitor data with HTTP POST

The following example shows how to make an HTTP POST request to an endpoint with visitor profile data in the request body JSON.

```
// Send visitor data - HTTP POST
import {visitor} from &#39;tealium&#39;;

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
            throw new Error(&#39;Network response was not ok. Status code: ${response.status}.&#39;);
        }
        return response.json();
    })
    .then(data =&gt; console.log(&#39;Response:&#39;, JSON.stringify(data)))
    .catch(error =&gt; console.log(&#39;Error:&#39;, error.message));
```

## Send visitor data with HTTP GET

The following example shows how to make an HTTP GET request to an endpoint with visitor profile data as query string parameters.

```
// Send visitor data - HTTP GET
import {visitor} from &#39;tealium&#39;;

console.log(JSON.stringify(visitor));

fetch(encodeURI(&#39;https://webhook.site/87bb160f-475a-4258-b117-693bb2378a4d?param=${visitor.data}&#39;))
    .then(response =&gt; {
        if (!response.ok) {
            throw new Error(&#39;Network response was not ok. Status code: ${response.status}.&#39;);
        }
        return response.json();
    })
    .then(data =&gt; console.log(&#39;Response:&#39;, JSON.stringify(data)))
    .catch(error =&gt; console.log(&#39;Error:&#39;, error.message));
```

## Send an event to Tealium Collect

The following example shows how to send an event to the Tealium Collect HTTP API.

```js
import {event, tealium} from &#39;tealium&#39;;

var newEvent = {‘key’: ‘value’};

tealium.sendCollectEvent(newEvent, &#39;newAccount&#39;, &#39;newProfile&#39;, &#39;datasourceId&#39;)
    .then(response =&gt; {
        if (!response.ok) {
            throw new Error(`Network response was not ok. Status code: ${response.status}.`);
        }

        console.log(&#39;Status code:&#39;, response.status);
        return response.text();
    })
    .then(data =&gt; console.log(&#39;Result:&#39;, data))
    .catch(error =&gt; console.error(&#39;Error:&#39;, error.message));
```

## Retrieve visitor data and send it to Tealium Collect

In this example, the function uses the IP address to get the location city, gets weather information for that city, and sends the city and weather information to the Tealium Collect HTTP API.

```
import { auth, visitor, event } from &#34;tealium&#34;;

console.log(JSON.stringify(visitor));

const ip_stack_api_key = &#39;your_api_key&#39;,
      weather_api_key = &#39;your_weather_api_key&#39;,
      ip_address = visitor?.current_visit?.properties?.ip_address;

console.log(ip_address);
(async function() {
    if(ip_address) {
    try {
        // Use IP address to get location city
        let city_response = await fetch(&#39;https://api.ipstack.com/${ip_address}?access_key=${ip_stack_api_key}&amp;format=1&#39;),
        city_data = await city_response.json();
        console.log(JSON.stringify(city_data));
        // Use location city to get local weather
        let weather_response = await fetch(encodeURI(&#39;https://api.openweathermap.org/data/2.5/weather?q=${city_data.city}&amp;appid=${weather_api_key}&#39;)),
            weather_data = await weather_response.json();
            console.log(JSON.stringify(weather_data));
        // Send city and weather description back into collect endpoint
        await fetch(encodeURI(&#39;https://collect.tealiumiq.com/event?tealium_account=cloud-functions-usecases&amp;tealium_profile=main&amp;tealium_visitor_id=${visitor._id}&amp;lookup_city=${weather_data?.name}&amp;weather=${weather_data?.weather?.[0]?.description}&amp;country=isp=${city_data?.connection?.isp}&#39;));
    } catch(e) {
        console.error(e);
        return false;
    }
    } else {
        console.error(&#34;Could not locate users IP address&#34;)
    }
})();
```

## Get a Facebook authentication token

The following code example shows how to get a Facebook authentication token:

```
import { auth } from &#39;tealium&#39;;
const token = auth.get(&#39;facebook_token&#39;);

fetch(&#39;https://graph.facebook.com/v8.0/act_12345678/customaudiences??access_token=${token}&amp;fields=approximate_count%2Csubtype%2Cname%2Cdata_source&amp;limit=10&#39;)
  .then(response =&gt; response.json())
  .then(data =&gt; console.log(&#39;Data:&#39;, data))
  .catch(error =&gt; console.log(&#39;Error:&#39;, error.message));
```
## Send data to Facebook

This example shows how to send event data to the Facebook Graph or Marketing API to create a campaign. For more information on Facebook campaigns, see [https://developers.facebook.com/docs/marketing-api/reference/ad-campaign-group).](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign-group).

```
import {auth, event} from &#39;tealium&#39;;

const ACT_ID = 11111111111;
const ACCESS_TOKEN = auth.get(&#34;facebook_token&#34;);

fetch(&#39;https://graph.facebook.com/v8.0/act_${ACT_ID}/campaigns?access_token=${ACCESS_TOKEN}&#39;,
    {
        method: &#39;POST&#39;,
        body: &#39;name=${event.data}&amp;objective=PAGE_LIKES&amp;status=PAUSED&amp;special_ad_categories=[]&#39;
    })
    .then(response =&gt; {
            if (!response.ok) {
                throw new Error(&#39;Network response was not ok. Status code: ${response.status}.&#39;);
            }
            return response.json();
        })
    .then(data =&gt; console.log(&#39;Response:&#39;, JSON.stringify(data)))
    .catch(error =&gt; console.log(&#39;Error:&#39;, error.message));
```

## Create a Facebook campaign

This example shows how to create a Facebook campaign.

```
import { auth } from &#34;tealium&#34;;

const ACT_ID = 11111111111;
const ACCESS_TOKEN = auth.get(&#34;facebook_token&#34;);

(async function () {
    console.time(&#39;function&#39;);
    try {
        console.log(&#39;Creating campaign...&#39;);
        let campaignId = await createCampaign({ campaignName: &#39;My Campaign&#39; });
        console.log(&#39;Campaign ID&#39;, campaignId);

        console.log(&#39;Creating custom audience...&#39;);
        let customAudienceId = await createCustomAudience({ caName: &#39;My_Audience&#39; });
        console.log(&#39;Custom Audience ID&#39;, customAudienceId);

        console.log(&#39;Creating ad set...&#39;);
        customAudienceId = 23846304008770411;
        let adSetId = await createAdSet({ campaignId: campaignId, customAudienceId: customAudienceId });
        console.log(&#39;Ad Set ID&#39;, adSetId);

        console.log(&#39;Creating ad creative...&#39;);
        // let adCreativeId = await createAdCreative();
        // current API call not working, use an ID created manually before
        let adCreativeId = &#39;adCreativeId&#39;;
        console.log(&#39;AdCreative ID &#39;, adCreativeId);

        console.log(&#39;Creating ad...&#39;);
        let adId = await createAd({ adsetId: adSetId, adCreativeId: adCreativeId });
        console.log(&#39;Ad ID&#39;, adId);
        console.timeEnd(&#39;function&#39;);
    } catch (error) {
        console.log(error);
    }
})();

async function createAd({ adsetId, adCreativeId }) {
    const params = {
        &#39;status&#39;: &#39;PAUSED&#39;,
        &#39;adset_id&#39;: adsetId,
        &#39;name&#39;: &#39;My Ad&#39;,
        &#39;creative&#39;: { &#39;creative_id&#39;: adCreativeId },
    };

    let result = await fetch(&#39;https://graph.facebook.com/v7.0/act_${ACT_ID}/ads?access_token=${ACCESS_TOKEN}&#39;,
        {
            method: &#39;POST&#39;,
            body: jsonToRequestBodyString(params)
        });
    let json = await result.json();
    return json.id;
}

async function createAdSet({ campaignId, customAudienceId }) {
    const params = {
        &#39;name&#39;: &#39;AdSet&#39;,
        &#39;lifetime_budget&#39;: &#39;1000&#39;,
        &#39;start_time&#39;: &#39;2020-07-01T23:41:41-0800&#39;,
        &#39;end_time&#39;: &#39;2020-07-07T23:41:41-0800&#39;,
        &#39;campaign_id&#39;: campaignId,
        &#39;bid_amount&#39;: &#39;1&#39;,
        &#39;billing_event&#39;: &#39;IMPRESSIONS&#39;,
        &#39;optimization_goal&#39;: &#39;LINK_CLICKS&#39;,
        &#39;targeting&#39;: {
            &#34;geo_locations&#34;: {
                &#34;countries&#34;: [&#34;US&#34;],
            },
            &#34;age_min&#34;: 25,
            &#34;age_max&#34;: 40,
            &#34;custom_audiences&#34;: [{ &#34;id&#34;: customAudienceId }]
        },
        &#39;status&#39;: &#39;PAUSED&#39;
    };
    let result = await fetch(&#39;https://graph.facebook.com/v7.0/act_${ACT_ID}/adsets?access_token=${ACCESS_TOKEN}&#39;,
        {
            method: &#39;POST&#39;,
            body: jsonToRequestBodyString(params)
        });
    let json = await result.json();
    return json.id;
}

async function createCustomAudience({ caName }) {
    const params = {
        &#39;name&#39;: caName,
        &#39;subtype&#39;: &#39;CUSTOM&#39;,
        &#39;description&#39;: &#39;People who purchased on my website&#39;,
        &#39;customer_file_source&#39;: &#39;USER_PROVIDED_ONLY&#39;,
    };
    let result = await fetch(&#39;https://graph.facebook.com/v7.0/act_${ACT_ID}/customaudiences?access_token=${ACCESS_TOKEN}&#39;,
        {
            method: &#39;POST&#39;,
            body: jsonToRequestBodyString(params)
        });
    let json = await result.json();
    return json.id;
}

async function createCampaign({ campaignName }) {
    const params = {
        &#39;objective&#39;: &#39;LINK_CLICKS&#39;,
        &#39;status&#39;: &#39;PAUSED&#39;,
        &#39;buying_type&#39;: &#39;AUCTION&#39;,
        &#39;name&#39;: campaignName,
        &#39;special_ad_categories&#39;: &#39;NONE&#39;
    };
    let result = await fetch(&#39;https://graph.facebook.com/v8.0/act_${ACT_ID}/campaigns?access_token=${ACCESS_TOKEN}&#39;,
        {
            method: &#39;POST&#39;,
            body: jsonToRequestBodyString(params)
        });
    let json = await result.json();
    return json.id;
}

function jsonToRequestBodyString(json) {
    return Object.keys(json).map(function (key) {
        return encodeURIComponent(key) &#43; &#39;=&#39; &#43;
            ((typeof json[key] === &#39;string&#39; || json[key] instanceof String) ? encodeURIComponent(json[key]) : JSON.stringify(json[key]));
    }).join(&#39;&amp;&#39;);
}
```

## Use the fetch() API to make HTTP requests

The fetch API is available for functions to make HTTP requests, as shown in the following example. For more information, see [Fetch](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/fetch).

```
fetch(&#39;https://restcountries.eu/rest/v2/name/usa&#39;)
  .then(response =&gt; {
    if (!response.ok) {
      throw new Error(`Network response was not ok. Status code: ${response.status}.`);
    }
    return response.json();
  })
  .then(data =&gt; console.log(&#39;Capital:&#39;, data[0].capital))
  .catch(error =&gt; console.log(&#39;Error:&#39;, error.message));
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
    if (data &amp;&amp; typeof data === &#39;object&#39; &amp;&amp; !(data instanceof Date)) {
        Object.keys(data).forEach(key =&gt; {
            buildURLSearchParams(params, data[key], parentKey ? `${parentKey}[${key}]` : key);
        });
    } else {
        const value = data == null ? &#39;&#39; : data;

        params.append(parentKey, value);
    }
}
```

## Get the value of a global variable

The following code example shows how to use `store.get()` to retrieve a global variable, `Cloud_function_URL`, that contains the URL for a Google cloud function, and then use this URL to invoke the Google cloud function.

```
const cfunction_url = store.get(&#34;Cloud_function_URL&#34;);
 
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

## Get an attribute name or value by attribute ID

Attribute names can be changed, which can cause problems when code references attributes by name. When  the attribute name is changed, the attribute ID is not changed. To avoid problems with attribute names changing, you can reference attributes by ID by using the `getAttrNameById()` and `getAttrValueByID()` methods provided by the `event` and `visitor` objects. The following example shows how this works.

We recommend using the `getAttrValueByID()` method sparingly. This method recursively searches the properties of the event or visitor object to locate the value. If your event or visitor object is complex, this operation may increase the computation time of your function invocation.

When you add `getAttrNameById()` or `getAttrValueByID()` to a function, the code completion feature helps you select the attribute ID to use in the method. For example, if you enter the following in the code editor, when you enter the opening parenthesis, the code completion feature shows a list of attributes and associated IDs: ![](/images/server-side/functions-code-completion-attr-name.png)

You can enter part of the attribute name to filter the list. When you select an attribute, its ID is added to your code after the parenthesis.