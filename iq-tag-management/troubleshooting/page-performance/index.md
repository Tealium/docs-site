---
title: Page performance
description: Page performance measures how quickly a web page loads and renders in the browser. The primary purpose of page performance is to optimize the user experience.
url: https://docs.tealium.com/iq-tag-management/troubleshooting/page-performance/
---
It's [no secret](https://www.nngroup.com/articles/website-response-times/) that a slow-loading page is a good way to lose visitors from your site, so maximizing page performance is generally considered a worthwhile endeavor.

As you begin to evaluate page performance, one thing becomes clear: there are a wide variety of factors that affect the speed of a loading page:

* Network latency
* File compression
* Browser caching
* CSS
* Fonts
* Inline JavaScript

Tagging (loading JavaScript files) is just one of the factors of this complex process and will be the focus of this article. More specifically, we will explore the contributing factors to perceived page performance and what controls can be used within the iQ Tag Management console. Specifically, the focus is on two concepts that are most relevant to tagging and performance:

* Asynchronous JavaScript
* DOM-Ready Event

## Perceived load time vs. actual load time

Before we begin, it's worth mentioning the difference between perceived load time and actual load time. The actual load time is traditionally a measurement from the browser that indicates when all of the assets of a web page have been processed. The perceived load time, arguably the more important of the two, is a measurement of when the web page is visually rendered and available to the user.

This topic of what to measure is quite technical and has been researched by industry experts such as [WebPagetest](https://sites.google.com/a/webpagetest.org/docs/using-webpagetest/metrics/speed-index), Google's [PageSpeed Tools](https://developers.google.com/speed/pagespeed/), and Yahoo's [YSlow](http://yslow.org/).


<blockquote>
The iQ Tag Management JavaScript library (`utag.js`) is designed to have little or no impact on the perceived load time of a page.
</blockquote>


## Tealium files vs. third-party files

At the foundation of the Tealium solution is our file serving framework. This global and real-time solution ensures that Tealium's files are delivered to your visitors' browser at the quickest speed possible. The JavaScript loader (or wrapper) files contain the logic and configuration from your iQ Tag Management account and can be identified in your browser's network console by the names `utag.js` and `utag.#.js`. These are the files served by Tealium from the `tags.tiqcdn.com` domain.

Example browser network log of Tealium files:

![](https://docs.tealium.com/images/iq-tag-management/tealium-network-utag-files.jpg)

As the browser loads these Tealium files there might be additional requests for files that are required by your tag vendors. These files can be identified as coming from a domain other than `tags.tiqcdn.com` and with names other than `utag`.


<blockquote>
Tealium does not host or control the performance of third-party files.
</blockquote>


## Browser file cache

Browsers have their own methods of optimizing page performance, the most widely known is file caching. The browser will save a copy of a file so that it doesn't request the same content over the network repeatedly. This reduces network traffic and allows site pages to load more quickly once the initial assets are cached in the browser.

For more information, see [How Tealium files are cached]().

## Asynchronous JavaScript

Asynchronous JavaScript is a method for delaying the loading of non-essential elements to prioritize page rendering to the user. You can think of asynchronous requests in a page like a "To Do" list for the browser: when the browser doesn't have other, higher priority elements to render, it will process the items in its asynchronous "To Do" list. The opposite effect is achieved when using synchronous JavaScript, which behaves like a "Must Do" list for the browser: the browser must block the rendering of the page to process items in its synchronous "Must Do" list.

All modern tag vendors have switched to the asynchronous method, which is one of the most common ways to improve page load speed.

In iQ Tag Management, the `utag.js` loader file and all subsequently loaded tag files use the asynchronous method.

For more information, read: 

* [Synchronous vs. Asynchronous JavaScript](https://support.tealiumiq.com/en/support/solutions/articles/36000363409-synchronous-vs-asynchronous-javascript-sync-vs-async-)
* [Optimize JavaScript](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/page-speed-rules-and-recommendations#optimize_javascript_use)

## DOM-ready event

The DOM-ready event, also known as `DOMContentLoaded`, is the browser's way of indicating when it has completed the loading of the main content in the page. This event is commonly used as the trigger for loading non-essential elements of the page to ensure that the page renders as quickly as possible, which improves the perceived load time.

In iQ Tag Management, vendor tracking is delayed until the DOM-Ready event to minimize the impact on page rendering.

For more information, see: 

* [Understanding Order of Operations]()
* [DOMContentLoaded - Event reference | Mozilla Developer Network]()

## iQ Tag Management settings and best practices

There are several options in iQ Tag Management to help you control how JavaScript is loaded on your pages. Every website is different, so there isn't a single optimal solution for everyone. The default settings in iQ are balanced to have minimal impact on perceived load time and provide the greatest compatibility with the largest number of vendor tags.

### Code placement

Code placement refers to where in the HTML document the `utag.js` code snippet appears. There are two main locations where you might load JavaScript in your HTML: inside the `<head>` tag or inside the `<body>` tag. The Tealium `utag.js` file must be loaded inside the `<body>` tag.

Base HTML structure:

```html
<html>
<head>
    <!-- Script Files here -->
</head>
<body>
    <!-- Tealium utag.js asynchronous script here -->
    ....
</body>
</html>
```

The best practice is to place the `utag.js` code snippet at the top of the `<body>`. This position allows your tag management configuration to load asynchronously while the page continues to render so that your tags are ready to fire at the DOM-Ready event. The `utag.js` file can be placed lower in the `<body>` if needed. In general, this will result in delayed loading of tags and/or a slightly faster perceived load time.

For more information, see [utag.js code placement](https://docs.tealium.com/platforms/javascript/install).

### Ready Wait flag

The Ready Wait flag can be found in [the **Publish Configuration** area](). It controls when `utag.js` will begin executing. By default, this flag is **Off** and `utag.js` begins executing as soon as it loads into the page. When this flag is set to **On**, `utag.js` will wait for the DOM-Ready event before executing. You can deprioritize your tags in favor of possible gains in page load time by turning this flag on.


<blockquote>
Setting **Ready Wait Flag** to **On** could lead to lost tracking due to visitors navigating away from the page before the tags have loaded. Always perform thorough testing before releasing new settings to your live site.
</blockquote>


### File compression and minification

Files sent from Tealium's servers are compressed using the Brotli industry standard for most browsers. (Older browsers that can't handle Brotli use Gzip compression instead.) This ensures the JavaScript files (text files) are as small as possible upon delivery to the browser. This behavior cannot be changed. The code within those JavaScript files is also minified by default. Minification adds another step of compressing the code files to only their essential text by removing comment lines and white space. You can turn this setting off if needed for debugging purposes.

For more information, see [Minify Tag Templates setting]().

### Bundling

Bundling allows vendor tag code to be included in the main `utag.js` file to eliminate additional HTTP requests from the page. By default, the vendor tags configured in iQ Tag Management are loaded as separate files (for example, `utag.4.js`) into the page. This is done to minimize the risk of introducing a code error into the main `utag.js` file (for example, an error in one file will not affect the others). However, using separate files increases the number of HTTP requests the page makes to load your tags. And while the delivery of these files is optimized through Tealium's servers and browser caching, if you need to optimize further then bundling is an option to consider.

Here is a simple example where bundling tags resulted in an 80% improvement in load time for the files coming from Tealium.

#### Two vendor tags unbundled

* **Number of files:** 3 (utag.js, utag.1.js, utag.21.js)
* **Total Size:** 18.2 KB (9.1 + 5.0 + 4.1)
* **Total Time:** 100 ms (54 + 23 + 23)

![](https://docs.tealium.com/images/iq-tag-management/tlc-network-utag.jpg)

#### Two vendor tags bundled

* **Number of files:** 1 (utag.js)
* **Total Size:** 17 KB
* **Total Time:** 19 ms

![](https://docs.tealium.com/images/iq-tag-management/tlc-network-utag-bundle.jpg)

For more information, see [Bundling individual tags](https://docs.tealium.com/tag-advanced-settings/#bundle-flag) or [Bundling any tag using the **All Pages** load rule](https://docs.tealium.com/publish-configuration/#performance-optimization).

### Tag timing (tags)

As mentioned, the default behavior in `utag.js` is to wait for the DOM-Ready event before firing the vendor tags. The **Tag Timing** setting is a tag-level setting that controls this logic for individual tags. The default setting is **DOM Ready (default)**, which means "wait for DOM-Ready". When this flag is set to **Prioritized**, the individual tag will run as soon as possible (usually prior to DOM-Ready).

For more information, see [Tag timing for tags](https://docs.tealium.com/tag-advanced-settings/#tag-timing).

### Tag ordering

Your configured tags are loaded into the page in the same order as they appear in the iQ Tag Management console. You can drag and drop tags in the order you want them to load. The Tealium best practice is to put your analytics tag(s) and other high priority tags at the top of the list to ensure they are the first ones loaded.

For more information, see [Tag ordering](https://docs.tealium.com/manage-tags/#load-order).