---
title: Install Referrer Module
description: Provides a Cordova wrapper for the native Android Install Referrer module.
url: https://docs.tealium.com/platforms/cordova-v1/module-list/install-referrer/
---
## Install


<blockquote>
This feature is available as a separate NPM package.
</blockquote>


To install the Install Referrer module:

1. Navigate to your Cordova app's directory in a terminal window.

2. Run the following command:
      ```bash
      cordova plugin add tealium-cordova-installreferrer
      ```

## Initialize

To initialize the Install Referrer module:

1. Edit the JavaScript file where you instantiate the main Tealium plugin, after calling the [`tealium.init()`](https://docs.tealium.com/platforms/cordova-v1/api/#init) method.

2. Add the following code:  
      ```javascript
      function tealiumInit(account, profile, environment, instance){
      var ir;
      tealium.init({...});
      // check if installreferrer is installed and available
      ir = window.tealiumInstallReferrer;
      if (ir) {
            // init install referrer and store any received values as persistent data
            ir.setPersistent(instance);
      }
      }
      ```

## Test

Once the plugin has been installed, test it by manually triggering a system broadcast.

Substitute `com.tealium.sample` with the RDNS bundle identifier for your app (unless testing with the Tealium sample app).

```bash
adb shell
am broadcast -a com.android.vending.INSTALL_REFERRER -n "com.tealium.sample/com.tealium.installreferrer.InstallReferrerReceiver" --es "referrer" "utm_source=mysource&utm_medium=mymedium&utm_term=myterm&utm_content=46b25e284dc36d5a7ef8f0e6b393febe3fcc8327&utm_campaign=mycampname"
```

## Uninstall

To uninstall the Install Referrer module:

1. Run the following command:
      ```bash
      cordova plugin rm tealium-cordova-installreferrer
      ```

2. Delete the Install Referrer data from persistent storage:
      ```javascript
      tealium.removePersistent("install_referrer", <your tealium instance name>);
      ```
