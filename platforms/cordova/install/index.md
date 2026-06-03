---
title: Install
description: Learn how to install Tealium for Cordova.
url: https://docs.tealium.com/platforms/cordova/install/
---
## Requirements

* Apache Cordova (9.0.0&#43;)

## Libraries

The plugin includes the following Tealium libraries:

* [Tealium for iOS](/platforms/ios-swift)
* [Tealium for Android](/platforms/android-kotlin/)

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

The [`initialize()`](/platforms/cordova/api/#initialize) method initializes the Tealium Cordova plugin, as shown in the following examples:





```js
var Environment = tealium.utils.Environment;
var Collectors = tealium.utils.Collectors;
var Dispatchers = tealium.utils.Dispatchers;
var ConsentPolicy = tealium.utils.ConsentPolicy;

var config = {
    account: &#39;ACCOUNT&#39;,
    profile: &#39;PROFILE&#39;,
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
    //     &#39;time&#39;: 10,
    //     &#39;unit&#39;: &#39;days&#39;
    // },
    // consentPolicy: ConsentPolicy.gdpr,
    lifecycleAutotrackingEnabled: true,
    batchingEnabled: false,
    visitorServiceEnabled: true,
    useRemoteLibrarySettings: true
};
window.tealium.initialize(config, function(success) {
    if (success) {
      console.log(&#34;Tealium initialized successfully&#34;);
    }
})
```




```js
import {Collectors, Dispatchers, LogLevel, Tealium, TealiumConfig,  TealiumEnvironment, TealiumEvent, TealiumView} from &#39;@awesome-cordova-plugins/tealium&#39;;

let config: TealiumConfig = {
    account: &#39;ACCOUNT&#39;,
    profile: &#39;PROFILE&#39;,
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
    //     &#39;time&#39;: 10,
    //     &#39;unit&#39;: TimeUnit.days
    // },
    // consentPolicy: ConsentPolicy.gdpr,
    lifecycleAutotrackingEnabled: true,
    visitorServiceEnabled: true,
    useRemoteLibrarySettings: true
};


Tealium.initialize(tealConfig).then(()=&gt;{
    console.log(&#34;Tealium initialized successfully&#34;);
});
```



