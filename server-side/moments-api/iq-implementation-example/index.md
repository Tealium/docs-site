---
title: Moments API and iQ Tag Management example implementation guide
description: See an example solution that integrates Moments API into your Tealium iQ Tag Management installation.
url: https://docs.tealium.com/server-side/moments-api/iq-implementation-example/
---
## How it works

Moments API creates a unique endpoint that you can integrate into your websites or applications.

Complete the following steps to implement Moments API into your Tealium workflow using the [Tealium iQ Advanced JavaScript Code Extension](https://docs.tealium.com/advanced-javascript-code-extension/). The following example uses Fetch API to request the visitor’s data from the Moments API, but other JavaScript options, such as `XMLHttpRequest`, are also supported. 

## Step 1: Get the visitor ID

Parse the `v_id` from the Tealium `utag_main` cookie.

Copy the following code, depending on your version of `utag.js`, into the extension. 

* **Title**: Parse identifier from utag.js cookie [Moments API]
* **Scope**: Pre Loader
* **Type**: Advanced JavaScript

### `utag.js` 4.50+ 


<blockquote>
If you use the `split_cookie=false` option, use the [`utag.js` 4.49 and below](#utag-js-4-49-and-below) code examples.
</blockquote>


```js
read_utag_cookies = function() {
  if(!document.cookie || document.cookie === "") {
    return {};
  }
  var cookies = document.cookie.split("; ");
  return cookies.reduce(function(result, cookie) {
    var kv = cookie.split("=");
    if(kv[0].startsWith("utag_")) {
      var cookie_name = kv[0].split("_")[1];
      var cookie_name_with_tag = "utag_" + cookie_name;
      var name_trimmed = kv[0].replace(cookie_name_with_tag+"_", "");
      result[name_trimmed] = String(kv[1]).replace(https://docs.tealium.com/%3b/g, ';')
    }
    return result;
  }, {});
}
var utag_cookies = read_utag_cookies();
//save the Tealium Visitor ID in memory
var moments_identifier = utag_cookies["v_id"] || null
```

### `utag.js` 4.49 and below {#utag-js-4-49-and-below}

```js
function getCookie(cname) {
    let name = cname + "=";
    let decodedCookie = decodeURIComponent(document.cookie);
    let ca = decodedCookie.split(';');
    for (let i = 0; i < ca.length; i++) {
        let c = ca[i];
        while (c.charAt(0) == ' ') {
            c = c.substring(1);
        }
        if (c.indexOf(name) == 0) {
            return c.substring(name.length, c.length);
        }
    }
    return "";
}

// Extracting the visitor ID from the utag_main cookie
var utag_cookie = getCookie("utag_main");

//save the Tealium Visitor ID in memory

var moments_identifier = utag_cookie.split("v_id:")[1].split("$")[0] || "";
```

## Step 2: Call Moments API

Request the Moments API endpoint and store the response data in local storage to be used for onsite marketing activities and personalization. 

Add the following template code to another Advanced JavaScript extension and update it according to your account and target engine. The code maps the `moments_identifier` variable assigned in the previous extension to the identifier parameter of the API’s URL endpoint. 


<blockquote>
Ensure this code loads after the previous JavaScript extension according to the [Order of Operations](https://docs.tealium.com/order-of-operations/).
</blockquote>


* **Title**: [Moments API]
* **Scope**: Pre Loader
* **Type**: Advanced JavaScript

```js
// Assign the engine ID you want to request 
var engine_id = "your_engine_id"; 


// suppressNotFound is an optional parameter 

// Set to false for HTTP 404 when visitor is not found 
// var suppressNotFound = true;

// Construct the API URL
// This example does not include optional parameters
// Add optional parameters, if required

var apiUrl = "MOMENTS_API_ENDPOINT_URL" + moments_identifier;

// Example: "https://personalization-api.us-west.prod.tealiumapis.com/personalization/accounts/example/profiles/main/engines/abc123/visitors/" + "0123456789"

// Add function for writing the Moments API response to localStorage
function writeToLocalStorage(obj, engineId) {
    // Prefix for localStorage keys
    const prefix = 'moments_' + engineId + '_';

    // Function to save an object property to localStorage
    const saveToLocalStorage = (key, value) => {
        localStorage.setItem(prefix + key, JSON.stringify(value));
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
    .then(response => {
        if (!response.ok) {
            throw new Error('Network response was not ok');
        }
        return response.json();
    })
    .then(data => {
        // Handle the response data
        if (data) {
        // set the data to localStorage, categorised by grouping. For example, attributes, badges, and audiences.
        writeToLocalStorage(data, engine_id) 
            
        }
    })
    .catch(error => console.error('Moments API error:', error));
//

```

## Step 3: Integrate into your workflow

Integrate the data with an onsite performance or personalization vendor according to your use case.


<blockquote>
To optimize the DNS request process, consider using DNS prefetching. For more information, see [The Chromium Projects > DNS Prefetching](https://www.chromium.org/developers/design-documents/dns-prefetching/).
</blockquote>
 
