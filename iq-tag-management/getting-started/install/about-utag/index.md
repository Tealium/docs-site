---
title: About the Universal Tag (utag.js)
description: Learn how the Tealium Universal tag (`utag.js`) and  vendor library files are loaded in the page.
url: https://docs.tealium.com/iq-tag-management/getting-started/install/about-utag/
---
## Hosted files

All tag configuration and business logic saved in your account is converted to JavaScript code and published to a file named `utag.js`. This file is specific to your account and is hosted on Tealium's servers.

Tealium's server infrastructure is designed to deliver these files to your website as quickly as possible. When the Universal Tag code snippet is executed by your webpage, a request is made to Tealium's servers, the file is downloaded into the page and the code is run. As soon as `utag.js` is loaded on your page it begins executing code to prepare to fire your tags.

Learn more about the [order of operations](https://docs.tealium.com/order-of-operations/) to understand how the Universal Tag `utag.js` loads.

## Page data

In addition to the dynamic data that your site populates into `utag_data`, the `utag.js` library automatically gathers other various data values from the page and combines them into one central data object to be made available to your tags and load rules. The following page elements are captured:

*   Query String Parameters
*   First-Party Cookies
*   JavaScript Variables
*   Meta Data Elements

The final data object are used to power your load rules and tags.

## Load rules

[Load rules](https://docs.tealium.com/about-load-rules/) are precise conditions that determine when to load a tag. Generally made up of one or more conditions, a load rule has to be satisfied to load the tag to which it is applied. The full list of variables from the data object are used to evaluate the load rules and determine which tags load on the page. Load Rules are JavaScript code evaluated client-side, in the browser.

## Events

[Events](https://docs.tealium.com/about-events/) are triggers that help collect data. They listen for the viewer to perform an action on a page, and then send that information to the data layer. For example, if you want to check how many times a certain product has been viewed, you can use an event that fires each time a product page is viewed. You can also use them to record user interactions with website elements, such as when particular elements are visible. Event triggers use load rules to determine whether they are loaded on a page along with the tags. Events are JavaScript code evaluated client-side, in the browser.

## Load tags

The code needed to load and run a vendor tag is also published to Tealium and stored in a tag configuration file numbered according to the UID of the tag, such as `utag.1.js`. Visitors' browsers send HTTP requests to the Tealium server to get each tag configuration file when they go to a web page.

While this file contains the settings and configuration for the vendor, it might not contain the vendor's JavaScript file. If so, an additional HTTP request is made to fetch the vendor's code. These requests are made asynchronously to minimize the impact on the time to render the page.

Here is a simple example showing how one tag, Google Analytics, is loaded into the page:

![](https://docs.tealium.com/images/platforms/javascript/utag-network-files.png)

*   **`utag.js`** (`tags.tiqcdn.com`) - the Tealium iQ Tag Management JavaScript library
*   **`utag.1.js`** (`tags.tiqcdn.com`) - the Tealium tag configuration file for Google Analytics
*   **`analytics.js`** (`www.google-analytics.com`) - the Google Analytics JavaScript library


<blockquote>
Improve page performance by [bundling tags](https://docs.tealium.com/tag-advanced-settings/) to reduce the number of HTTP requests coming from your page.
</blockquote>


## Run Tags

Once all tag files are loaded and the DOM Ready event is reached, the tracking beacons are triggered. The vendor code runs the same as if it was outside of Tealium, so the resulting HTTP requests is easy to identify.

For example, Google Analytics is identified in the network request by the following two items: the `analytics.js` script and the collect image pixel. These same network requests occur even when Google Analytics is loaded by iQ Tag Management, as seen here:

![](https://docs.tealium.com/images/platforms/javascript/utag-vendor-pixel.png)
