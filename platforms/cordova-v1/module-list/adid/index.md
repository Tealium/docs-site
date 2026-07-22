---
title: Ad Identifier Module
description: Provides a Cordova wrapper for the native Android Ad Identifier module and the iOS Advertising Identifier (IDFA).
url: https://docs.tealium.com/platforms/cordova-v1/module-list/adid/
---
## Install

To install the Ad Identifier module:

1. Navigate to your Cordova app's directory in a terminal window

2. Run the following command:
      ```bash
      cordova plugin add tealium-cordova-adidentifier
      ```


<blockquote>
The Ad Identifier module has a dependency on the Google Play Services Ads module. Add your [AdMob App ID](https://developers.google.com/admob/android/quick-start) to your app's `AndroidManifest.xml` file to prevent the app from crashing during startup.
</blockquote>


## Initialize

To initialize the Ad Identifier module:

1. Edit the JavaScript file, where you instantiate the main Tealium plugin, after calling `tealium.init`.

2. Add the following code:  
      ```javascript
      function tealiumInit(account, profile, environment, instance){
      var ai;
      tealium.init({...});
      // check if installreferrer is installed and available

      ai = window.tealiumAdIdentifier;
      if (ai) {
            ai.setPersistent(instance);
      }
      }
      ```

## Data Layer
The Ad Identifier module adds the following variables to the data layer:

**Android**
* `google_adid`

**iOS**
* `device_advertising_id`
* `device_advertising_vendor_id`
*  `device_advertising_enabled`

## Uninstall

To uninstall the Ad Identifier module:

1. Run the following command:
      ```bash
      cordova plugin rm tealium-cordova-adidentifier
      ```

2. Delete the Ad Identifier data from persistent storage:
      ```javascript
      // android only
      tealium.removePersistent("google_adid", <your tealium instance name>);

      // ios only
      tealium.removePersistent("device_advertising_id", <your tealium instance name>);
      tealium.removePersistent("device_advertising_vendor_id", <your tealium instance name>);
      tealium.removePersistent("device_advertising_enabled", <your tealium instance name>);
      ```
