---
title: Domain-Based Deployment Extension
description: Use the Domain-Based Deployment extension to load a QA or Dev version of the Universal Tag (utag.js) based on the hostname. This is typically used for validation purposes when you have the Prod instance of utag.js loading on your QA or Dev sites.
url: https://docs.tealium.com/iq-tag-management/extensions/extensions-list/domain-based-deployment-extension/
---
## Prerequisites

* See [About Extensions]().

## How it works

The Domain-Based Deployment extension loads a QA or Dev version of the Universal Tag (`utag.js`) based on hostname (the JavaScript window variable `location.hostname`). When `utag.js` loads in the page, the Domain-Based extension is executed immediately and checks the current hostname for matches to any of your declared environments. If there&#39;s a match, the appropriate environment version of `utag.js` is loaded.

## Using the extension

Once the extension is added, the following configuration options are available:

* **Dev Domains**: Enter the development environment domain that you want to use for testing. For example, `dev.tealium.com`.
* **QA Domains**: Enter the QA environment domain that you want to use for testing. For example, `qa.tealium.com`.

Click the plus button (**&#43;**) to add a new Dev/QA environment, or the minus button (**-**) to delete a Dev/QA environment.

## Example

Your production website contains the following script:

``` javascript
&lt;script type=&#34;text/javascript&#34;&gt;
(function(a,b,c,d){
a=&#39;https://tags.tiqcdn.com/utag/my_account/main/**prod**/utag.js&#39;;
b=document;c=&#39;script&#39;;d=b.createElement(c);d.src=a;d.type=&#39;text/java&#39;&#43;c;d.async=true;
a=b.getElementsByTagName(c)[0];a.parentNode.insertBefore(d,a);
})();
&lt;/script&gt;
```

In the example, the environment is **prod** (not **qa** or **dev**).

* When this `utag.js` file is loaded, the Domain-Based extension is executed immediately and checks to ensure that the current hostname is `dev.tealium.com` or `qa.tealium.com` (or other declared environment).
* If the hostname matches any of the declared environments, the appropriate environment is then loaded.

The following examples shows the `utag.js` files that would load for this example:

* **dev.tealium.com**
    ``` javascript
    &lt;script type=&#34;text/javascript&#34;&gt;
    (function(a,b,c,d){
    a=&#39;https://tags.tiqcdn.com/utag/my_account/main/**dev**/utag.js&#39;;
    b=document;c=&#39;script&#39;;d=b.createElement(c);d.src=a;d.type=&#39;text/java&#39;&#43;c;d.async=true;
    a=b.getElementsByTagName(c)[0];a.parentNode.insertBefore(d,a);
    })();
    &lt;/script&gt;
    ```

* **qa.tealium.com**
    ``` javascript
    &lt;script type=&#34;text/javascript&#34;&gt;
    (function(a,b,c,d){
    a=&#39;https://tags.tiqcdn.com/utag/my_account/main/**qa**/utag.js&#39;;
    b=document;c=&#39;script&#39;;d=b.createElement(c);d.src=a;d.type=&#39;text/java&#39;&#43;c;d.async=true;
    a=b.getElementsByTagName(c)[0];a.parentNode.insertBefore(d,a);
    })();
    &lt;/script&gt;
    ```

When you view the site traffic, if a non-production environment is detected, `/**prod**/utag.js` loads first and then `/**dev**/utag.js` or `/**qa**/utag.js`. Any subsequent `utag.#.js` files that load are served from the respective **Dev** or **QA** environment.
