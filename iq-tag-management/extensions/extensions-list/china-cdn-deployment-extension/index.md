---
title: China CDN Deployment Extension
description: The China CDN Deployment extension is a Pre Loader extension that runs before the Data Layer Processing. This extension determines a user's location (inside or outside China), which allows web site content to be sent to the user from the appropriate CDN.
url: https://docs.tealium.com/iq-tag-management/extensions/extensions-list/china-cdn-deployment-extension/
---
You can use this extension when you cannot modify the source code for a web site to add logic to determine the user’s location. This extension is also useful when a profile that primarily serves content from outside of China receives a small amount of traffic from within China.


<blockquote>
If a large amount of your traffic is from China and you can modify the source code for your web site, we recommend that you create a dedicated profile for the `.cn` domain and add a customized script to the HTML code you paste in each page. For more information, see [Update the code for your website](https://docs.tealium.com/load-utag-china/#update-the-code-for-your-website).
</blockquote>
 

## Prerequisites

* To create a draft of a China CDN Deployment extension, you need the **Manage JavaScript Code Extensions** account-level permission.

## How it works

The China CDN Deployment extension consists of a code editor pre-filled with JavaScript code that is executed during the pre-loader scope. This code contains logic to do the following:

* Determine the user's location based on their browser language, timezone, and IP address.
* Set a cookie with the best CDN for that user.

All subsequent site visits read the cookie value, if it is present, and fetch all utag content from the most specified CDN. Setting the cookie in the pre-loader scope means that the initial page request is served from the appropriate CDN.


<blockquote>
Page load speeds will be impacted if content is delivered to China from outside the Chinese network. However, after the initial page load and setting of the CDN cookie, the extension will deliver available resources from the China CDN to China-based users to speed up their requests.
</blockquote>


## Configuring the extension

When you add the China CDN Deployment extension to a profile, an Ace Editor window is displayed, which contains the default code for the extension. You can configure the `domainMap`, `languageMap`, and `gmtMap` variables for the extension. In addition, you can specify the `matchLogic` to determine a user's location.

### Setting up domain mapping

 If you have multiple domains associated with a profile, you use the `domainMap` variable to direct all domain traffic to a specific CDN.

```js
domainMap = {
    'www.yourwebsite.cn': 'cn'
},
```

### Adjusting language mapping

The `languageMap` variable lists the most common Chinese language variations and maps them to a single CDN.

```js
languageMap = {
    'zh': 'cn',
    'zh-HK': 'cn',
    'zh-CN': 'cn',
    'zh-TW': 'cn'
},
```

### Adjusting timezone mapping

The `gmtMap` variable specifies the Chinese time zone.

```js
gmtMap = {
    '-480': 'cn'
},
```

#### Adjusting the match logic

The default `matchLogic` variable for all defined variables requires them to all be true. Set it to `or` if only some of the variables need to be true.

```js
matchLogic = 'and'; // 'or'
```

### Turning IP location detection on or off

* If `locationTest` is true, fetch the users IP address and return a location.
* If `locationTestForce` is true, runs the location logic every time regardless of the cookie value or other match logic results.
* Both variables default to true to provide optimal location detection for every user session.

```js
 var locationTest = true; // Use location test logic
 var locationTestForce = true; // Use location test in all scenarios
```

### Adjusting the cookie duration and when to trigger a retest

The `retestTime` variable is specified in milliseconds and specifies when the retest is done to determine the user's location. The default is one day.

```js
var retestTime = 86400000; // 1 day

```
