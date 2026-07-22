---
title: Install
description: Learn how to install Tealium for Cordova.
url: https://docs.tealium.com/platforms/cordova/install/
---
## Requirements

* Apache Cordova (9.0.0+)

## Libraries

The plugin includes the following Tealium libraries:

* [Tealium for iOS](https://docs.tealium.com/platforms/ios-swift)
* [Tealium for Android](https://docs.tealium.com/platforms/android-kotlin/)

## Sample Apps

To help to familiarize yourself with our library, the tracking methods, and best practice implementation, explore the Tealium for Cordova [sample app](https://github.com/Tealium/cordova-plugin/tree/master/TealiumCordovaSample).

## Install

To install the Tealium library for Cordova, run the following command in your Cordova app project:




```js
cordova plugin add tealium-cordova-plugin
```




```js
ionic cordova plugin add tealium-cordova-plugin
npm install @awesome-cordova-plugins/core
npm install @awesome-cordova-plugins/tealium
```




## Initialize

The [`initialize()`](https://docs.tealium.com/platforms/cordova/api/#initialize) method initializes the Tealium Cordova plugin, as shown in the following examples:





```js
var Environment = tealium.utils.Environment;
var Collectors = tealium.utils.Collectors;
var Dispatchers = tealium.utils.Dispatchers;
var ConsentPolicy = tealium.utils.ConsentPolicy;

var config = {
    account: 'ACCOUNT',
    profile: 'PROFILE',
    environment: Environment.dev,
    dispatchers: [
        Dispatchers.Collect,
        Dispatchers.TagManagement,
        Dispatchers.RemoteCommands
    ],
    collectors: [
        Collectors.AppData,
        Collectors.DeviceData,
        Collectors.Lifecycle,
        Collectors.Connectivity
    ],
    consentLoggingEnabled: true,
    // consentExpiry: {
    //     'time': 10,
    //     'unit': 'days'
    // },
    // consentPolicy: ConsentPolicy.gdpr,
    lifecycleAutotrackingEnabled: true,
    batchingEnabled: false,
    visitorServiceEnabled: true,
    useRemoteLibrarySettings: true
};
window.tealium.initialize(config, function(success) {
    if (success) {
      console.log("Tealium initialized successfully");
    }
})
```




```js
import {Collectors, Dispatchers, LogLevel, Tealium, TealiumConfig,  TealiumEnvironment, TealiumEvent, TealiumView} from '@awesome-cordova-plugins/tealium';

let config: TealiumConfig = {
    account: 'ACCOUNT',
    profile: 'PROFILE',
    environment: TealiumEnvironment.dev,
    dispatchers: [
        Dispatchers.Collect,
        Dispatchers.TagManagement,
        Dispatchers.RemoteCommands
    ],
    collectors: [
        Collectors.AppData,
        Collectors.DeviceData,
        Collectors.Lifecycle,
        Collectors.Connectivity
    ],
    consentLoggingEnabled: true,
    // consentExpiry: {
    //     'time': 10,
    //     'unit': TimeUnit.days
    // },
    // consentPolicy: ConsentPolicy.gdpr,
    lifecycleAutotrackingEnabled: true,
    visitorServiceEnabled: true,
    useRemoteLibrarySettings: true
};


Tealium.initialize(tealConfig).then(()=>{
    console.log("Tealium initialized successfully");
});
```



