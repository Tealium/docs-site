---
title: Crash Reporter Module
description: Provides a Cordova wrapper for the native Android Crash Reporter module (iOS is not supported at this time).
url: https://docs.tealium.com/platforms/cordova-v1/module-list/crash-reporter/
---
## Install

To install the Crash Reporter module:

1. Navigate to your Cordova app's directory in a terminal window.

2. Run the following command:
      ```bash
      cordova plugin add tealium-cordova-crashreporter
      ```

## Initialize

No explicit initialization of the Crash Reporter module is required.

It is instantiated by the core Tealium plugin if the `isCrashReporterEnabled` parameter is set in the config object, as shown in the following example::

```javascript
function tealiumInit(account, profile, environment, instance) {
    tealium.init({
       account : account,
       profile : profile,
       environment : environment,
       instance : instance,
       isLifecycleEnabled: "true",
       isCrashReporterEnabled: "true"
    });
}
```

## Test

The JavaScript API exposes a method to force a crash to be triggered. To avoid accidental triggering of a crash in production, this method is hard-coded to work only if the following conditions are met:

*   The environment is set to `dev`
*   Crash Reporter module is installed
*   Crash Reporter module was successfully initialized
*   The variable `forceCrash` is present in the data layer

If the preceding conditions are met, trigger a crash by issuing a tracking call containing the variable `forceCrash` with the [`trackView()`](https://docs.tealium.com/platforms/cordova-v1/api/#trackview) method:

```javascript
tealium.trackView({"forceCrash":"true"});
```

## Uninstall

To uninstall the Crash Reporter module:

1. Run the following command:
      ```bash
      cordova plugin rm tealium-cordova-crashreporter
      ```  

2. Remove the `isCrashReporterEnabled` flag from the config object when initializing the main Tealium plugin.
