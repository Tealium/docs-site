---
title: How Tealium files are cached
url: https://docs.tealium.com/iq-tag-management/getting-started/file-cache/
---
Files served from Tealium set the `Cache-Control` header to tell the browser how long to cache a file before checking for a newer version. When the cache time period (sometimes called TTL for "time to live") has expired, the browser sends a header request to Tealium's servers to check if the file has been modified. If it has, the browser fetches the latest file, otherwise it continues to use the cached file.

The Universal Tag (`utag.js`) has a short TTL to ensure that when you publish in Tealium iQ Tag Management, your website visitors get the latest version of the `utag.js` files as quickly as possible.

## Browser cache times

Here are the browser cache expiration times for files published from iQ Tag Management:

|Tealium Files| Cache Expiration (TTL)|
|---| ---|
|`utag.js`| 5 minutes|
|`utag.#.js`| 5 minutes|
|`utag.sync.js`| 5 minutes|
|`mobile.html`| 1 hour (qa/prod)<br>5 minutes (dev)|

## Universal Tag caching

In versions of the Universal Tag prior to 4.26, all `utag.js` files were refreshed after a publish. After every publish, the `utag.js` files invalidated their cache, causing the browser to make unnecessary network calls to fetch unmodified files, which affected page load performance.

Starting with [version 4.26 and later](https://docs.tealium.com/release-notes/?filter=tealium-universal-tag#tealium-universal-tag-2014-01-01) the browser, resulting in fewer network calls and improved page load performance.


<blockquote>
For more information about updating the `utag.js` template, see our knowledge base article [Best Practices for Updating to the Latest Version of utag.js](https://support.tealiumiq.com/en/support/solutions/articles/36000363470).
</blockquote>


## How it works

The caching behavior is controlled by a timestamp parameter named `utv`, called a "cache busting" parameter, that is appended to the URLs of the published files. The cache busting parameter changes the URL of the file, which forces the browser to update its cached version of the file. For version 4.39+ of the Universal Tag, the value of the `utv` parameter contains a timestamp and a version number.

Cache busting parameter values by version of the Universal Tag:

|Versions| Description| Example|
|---| ---| ---|
|v4.26 - v4.38| Timestamp does not include a version number| `utag.#js?utv=201510202208`|
|v4.39+| Timestamp is prepended by a version number| `utag.#.js?utv=ut4.39.201510202208`|

Unchanged `utag.#.js` files remain cached in the browser because their timestamp values don't change between publishes.


<blockquote>
The [Currency Converter Extension](https://docs.tealium.com/currency-converter-extension/) is never cached.
</blockquote>


## Example

The following example modifies or adds a tag with the UID #4, deactivates tag #1, and makes no changes to tag #2 and tag #3.

![](https://docs.tealium.com/images/iq-tag-management/example-tags.png)

In the publish URLs view of the web console, notice that `utag.4.js` was fetched from the servers since it's a new or modified file. Both `utag.2.js` and `utag.3.js` were fetched from the cache, since they were unmodified. `utag.1.js` was not loaded on the page because it was deactivated.

![](https://docs.tealium.com/images/iq-tag-management/timestamps-on-qa.png)
