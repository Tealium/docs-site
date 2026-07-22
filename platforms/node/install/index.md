---
title: Install
description: Learn to install Tealium for Node.js
url: https://docs.tealium.com/platforms/node/install/
---The `tealium-collect` module for Node.js sends event data to the Tealium Customer Data Hub through the [Tealium HTTP API](https://docs.tealium.com/platforms/http-api/). Use the module in server-side applications or in a browser.

## Requirements

* [Tealium Customer Data Hub account](https://docs.tealium.com/introduction-to-customer-data-hub/)

## Install

To install the Tealium Collect module for Node.js with NPM, run the following command:  
```bash
npm install tealium-collect
```
The install automatically includes the dependency module `tealium`.

## Initialize

1. Import the modules:  
      ```javascript
      var Tealium = require('tealium');
      var tealiumCollect = require('tealium-collect');
      ```

2. Initialize the `Tealium` instance with the [`Tealium()`](https://docs.tealium.com/platforms/node/api/#tealium) constructor method:
      ```javascript
      var config = {
            "account"    : "ACCOUNT",
            "profile"    : "PROFILE",
            "datasource" : "DATASOURCE"
      };
      var tealium = Tealium(config);
      ```

3. Call the [`addModule()`](https://docs.tealium.com/platforms/node/api/#addmodule) method to add the Tealium Collect module :  
      ```javascript
      tealium.addModule(tealiumCollect);
      ```
