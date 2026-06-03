---
title: Install
description: Learn to install Tealium for NativeScript.
url: https://docs.tealium.com/platforms/nativescript/install/
---
The Tealium NativeScript integration provides a set of cross-platform interfaces and configuration classes that interface with the native Tealium iOS and Android SDKs.

## Requirements

* Access to your native build environments
* [NativeScript Plugin](https://github.com/Tealium/tealium-nativescript-plugin) and tools installed
* [Android Studio](https://developer.android.com/studio/) or [Xcode](https://developer.apple.com/xcode/)

## Sample App

To help familiarize yourself with our library, the tracking methods, and best practice implementation, download the [NativeScript sample app](https://github.com/Tealium/tealium-nativescript-plugin/tree/main/apps/demo).

To run the sample app, run the command `npm i` to install all dependencies, and then run `npm start` in the root directory (`tealium-nativescript-plugin`). Depending on your platform, select `apps.demo.android` or `apps.demo.ios`.

There is currently a known issue with NativeScript on iOS where the initial app build fails. To build successfully, open the file `.xcworkspace` and go to **Project** &gt; **Build Settings** &gt; **Validate Workspace** and set the property to `Yes`.


## Install (NPM)

To install the Tealium library for NativeScript with NPM:

1. Navigate to the root of your NativeScript project.

2. Download and install the `@tealium/nativescript-plugin` package with the command:  
      ```bash
      npm i @tealium/nativescript-plugin
      ```

## TypeScript

After installation, import the Tealium module into your app&#39;s TypeScript code:  
```javascript
import { Tealium } from &#39;@tealium-nativescript/tealium&#39;;
import {
   TealiumConfig, TealiumView, TealiumEvent, ConsentCategories, Dispatchers, Collectors,ConsentPolicy,
   Expiry, ConsentStatus, TealiumEnvironment } from &#39;@tealium-nativescript/tealium/common&#39;;
```

## Initialize

After your app has been installed, initialize the `Tealium` instance with the `initialize()` method using [TealiumConfig](/platforms/nativescript/api/tealium-config/#tealiumconfig) initialization options:  

```javascript
let config: TealiumConfig = {
    account: &#39;ACCOUNT&#39;,
    profile: &#39;PROFILE&#39;,
    environment: TealiumEnvironment.dev,
    dispatchers: [
        Dispatchers.Collect,
        Dispatchers.RemoteCommands,
        Dispatchers.TagManagement
    ],
    collectors: [
        Collectors.AppData,
        Collectors.DeviceData,
        Collectors.Lifecycle,
        Collectors.Connectivity
    ],
    consentPolicy: ConsentPolicy.gdpr,
    visitorServiceEnabled: true
};

Tealium.initialize(config);
```

See the [API Reference](/platforms/nativescript/api/) for more information and additional configuration options.

## Supported Modules

### Collectors

Collectors are modules that gather supplemental information from the device and append it to the data layer before it&#39;s transmitted to the Tealium Customer Data Hub. Some collectors are included in the core library, while others are optional and installed as separate modules.

The following table lists the available collectors. Default collectors are denoted by a `*` next to the collector name.

| Collector Name | TealiumConfig Reference |
| --- | --- |
| `AppData`* | `Collectors.AppData`|
| `Connectivity`* | `Collectors.Connectivity`|
| `Device` | `Collectors.Device`|
| `Lifecycle` | `Collectors.Lifecycle`|

These modules are enabled or disabled using the [`TealiumConfig`](/platforms/nativescript/api/tealium-config/) `collectors` property.

### Dispatchers

Dispatchers are modules that send the data from your data layer to a Tealium endpoint. The following dispatchers are currently available:

| Dispatcher Name | TealiumConfig Reference |
| --- | --- |
| `Collect` | `Dispatchers.Collect`|
| `RemoteCommands` | `Dispatchers.RemoteCommands`|
| `TagManagement` | `Dispatchers.TagManagement`|

At least one dispatcher is required. If no dispatchers are specified, no tracking occurs.
