---
title: Install
description: Learn to install Tealium for Node.js
url: https://docs.tealium.com/platforms/node/install/
---The `tealium-collect` module for Node.js sends event data to the Tealium Customer Data Hub through the [Tealium HTTP API](/platforms/http-api/). Use the module in server-side applications or in a browser.

## Requirements

* [Tealium Customer Data Hub account]()

## Install

To install the Tealium Collect module for Node.js with NPM, run the following command:  
```bash
npm install tealium-collect
```
The install automatically includes the dependency module `tealium`.

## Initialize

1. Import the modules:  
      ```javascript
      var Tealium = require(&#39;tealium&#39;);
      var tealiumCollect = require(&#39;tealium-collect&#39;);
      ```

2. Initialize the `Tealium` instance with the [`Tealium()`](/platforms/node/api/#tealium) constructor method:
      ```javascript
      var config = {
            &#34;account&#34;    : &#34;ACCOUNT&#34;,
            &#34;profile&#34;    : &#34;PROFILE&#34;,
            &#34;datasource&#34; : &#34;DATASOURCE&#34;
      };
      var tealium = Tealium(config);
      ```

3. Call the [`addModule()`](/platforms/node/api/#addmodule) method to add the Tealium Collect module :  
      ```javascript
      tealium.addModule(tealiumCollect);
      ```
