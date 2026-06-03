---
title: About publishing
url: https://docs.tealium.com/iq-tag-management/save-publish/about-publishing/
---
Publishing is an optional and additional action during the save process. When you publish changes, the files associated with the account profile are regenerated to include the current configuration.

## Publishing timing

The Tealium content delivery network (CDN) is optimized to refresh files immediately to minimize delays while publishing and testing.

Time-to-live (TTL) settings and caching by your browser will cause your browser to load old versions of files. To resolve this, clear or disable your browser cache. For more information about Tealium and browser caching, see .

#### Updated immediately

After publishing, the following files are immediately propagated through the CDN:

* `utag.js`
* `utag.#.js`

#### Updated up to five minutes later

Publishing the following items will takes up to five minutes to propagate through the CDN:

* `utag.sync.js`
* `utag.js` and `utag.#.js` files on `.cn` and `.eu` domains
* `utag.js` and `utag.#.js` files on first-party domains



## Publish environments

Publish environments provide separate instances of the Universal Tag (`utag.js`) to install on your production and non-production sites. There are three publish environments to support a proper release cycle: **Dev**, **QA**, and **Prod**. Each environment uses a separate file for your different website environments. Using separate environments lets you test changes before releasing them directly to your production site.

There are three default publish environments which correspond to three instances of the Universal Tag (`utag.js`):

*  **Dev**: `/utag/YOUR-ACCOUNT/YOUR-PROFILE/dev/utag.js`  
An environment for developing new tags and features.
*  **QA**: `/utag/YOUR-ACCOUNT/YOUR-PROFILE/qa/utag.js`  
An environment for testing and validation.
*  **Prod**: `/utag/YOUR-ACCOUNT/YOUR-PROFILE/prod/utag.js`  
The environment of your live production site.

For example, the file from the Prod environment should be installed on your production site:

```bash
https://tags.tiqcdn.com/utag/YOUR-ACCOUNT/main/prod/utag.js
```

The file from the QA environment should be installed on your non-production sites (QA/Stage):

```bash
https://tags.tiqcdn.com/utag/YOUR-ACCOUNT/main/qa/utag.js
```

If you need additional environments, use [custom publish environments]().