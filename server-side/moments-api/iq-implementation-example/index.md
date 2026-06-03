---
title: Moments API and iQ Tag Management example implementation guide
description: See an example solution that integrates Moments API into your Tealium iQ Tag Management installation.
url: https://docs.tealium.com/server-side/moments-api/iq-implementation-example/
---
## How it works

Moments API creates a unique endpoint that you can integrate into your websites or applications.

Complete the following steps to implement Moments API into your Tealium workflow using the [Tealium iQ Advanced JavaScript Code Extension](). The following example uses Fetch API to request the visitor’s data from the Moments API, but other JavaScript options, such as `XMLHttpRequest`, are also supported. 

## Step 1: Get the visitor ID

Parse the `v_id` from the Tealium `utag_main` cookie.

Copy the following code, depending on your version of `utag.js`, into the extension. 

* **Title**: Parse identifier from utag.js cookie [Moments API]
* **Scope**: Pre Loader
* **Type**: Advanced JavaScript

### `utag.js` 4.50&#43; 

If you use the `split_cookie=false` option, use the [`utag.js` 4.49 and below](#utag-js-4-49-and-below) code examples.

```js
read_utag_cookies = function() {
  if(!document.cookie || document.cookie === &#34;&#34;) {
    return {};
  }
  var cookies = document.cookie.split(&#34;; &#34;);
  return cookies.reduce(function(result, cookie) {
    var kv = cookie.split(&#34;=&#34;);
    if(kv[0].startsWith(&#34;utag_&#34;)) {
      var cookie_name = kv[0].split(&#34;_&#34;)[1];
      var cookie_name_with_tag = &#34;utag_&#34; &#43; cookie_name;
      var name_trimmed = kv[0].replace(cookie_name_with_tag&#43;&#34;_&#34;, &#34;&#34;);
      result[name_trimmed] = String(kv[1]).replace(/%3b/g, &#39;;&#39;)
    }
    return result;
  }, {});
}
var utag_cookies = read_utag_cookies();
//save the Tealium Visitor ID in memory
var moments_identifier = utag_cookies[&#34;v_id&#34;] || null
```

### `utag.js` 4.49 and below {#utag-js-4-49-and-below}

```js
function getCookie(cname) {
    let name = cname &#43; &#34;=&#34;;
    let decodedCookie = decodeURIComponent(document.cookie);
    let ca = decodedCookie.split(&#39;;&#39;);
    for (let i = 0; i &lt; ca.length; i&#43;&#43;) {
        let c = ca[i];
        while (c.charAt(0) == &#39; &#39;) {
            c = c.substring(1);
        }
        if (c.indexOf(name) == 0) {
            return c.substring(name.length, c.length);
        }
    }
    return &#34;&#34;;
}

// Extracting the visitor ID from the utag_main cookie
var utag_cookie = getCookie(&#34;utag_main&#34;);

//save the Tealium Visitor ID in memory

var moments_identifier = utag_cookie.split(&#34;v_id:&#34;)[1].split(&#34;$&#34;)[0] || &#34;&#34;;
```

## Step 2: Call Moments API

Request the Moments API endpoint and store the response data in local storage to be used for onsite marketing activities and personalization. 

Add the following template code to another Advanced JavaScript extension and update it according to your account and target engine. The code maps the `moments_identifier` variable assigned in the previous extension to the identifier parameter of the API’s URL endpoint. 

Ensure this code loads after the previous JavaScript extension according to the [Order of Operations](). 

* **Title**: [Moments API]
* **Scope**: Pre Loader
* **Type**: Advanced JavaScript

```js
// Assign the engine ID you want to request 
var engine_id = &#34;your_engine_id&#34;; 


// suppressNotFound is an optional parameter 

// Set to false for HTTP 404 when visitor is not found 
// var suppressNotFound = true;

// Construct the API URL
// This example does not include optional parameters
// Add optional parameters, if required

var apiUrl = &#34;MOMENTS_API_ENDPOINT_URL&#34; &#43; moments_identifier;

// Example: &#34;https://personalization-api.us-west.prod.tealiumapis.com/personalization/accounts/example/profiles/main/engines/abc123/visitors/&#34; &#43; &#34;0123456789&#34;

// Add function for writing the Moments API response to localStorage
function writeToLocalStorage(obj, engineId) {
    // Prefix for localStorage keys
    const prefix = &#39;moments_&#39; &#43; engineId &#43; &#39;_&#39;;

    // Function to save an object property to localStorage
    const saveToLocalStorage = (key, value) =&gt; {
        localStorage.setItem(prefix &#43; key, JSON.stringify(value));
    };

    // Loop through each top-level property in the object
    for (const key in obj) {
        if (obj.hasOwnProperty(key)) {
            saveToLocalStorage(key, obj[key]);
        }
    }
}


// Fetch the API

fetch(apiUrl)
    .then(response =&gt; {
        if (!response.ok) {
            throw new Error(&#39;Network response was not ok&#39;);
        }
        return response.json();
    })
    .then(data =&gt; {
        // Handle the response data
        if (data) {
        // set the data to localStorage, categorised by grouping. For example, attributes, badges, and audiences.
        writeToLocalStorage(data, engine_id) 
            
        }
    })
    .catch(error =&gt; console.error(&#39;Moments API error:&#39;, error));
//

```

## Step 3: Integrate into your workflow

Integrate the data with an onsite performance or personalization vendor according to your use case.

To optimize the DNS request process, consider using DNS prefetching. For more information, see [The Chromium Projects &gt; DNS Prefetching](https://www.chromium.org/developers/design-documents/dns-prefetching/). 
