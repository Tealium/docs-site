---
title: Install
description: Learn to install Tealium for Cordova.
url: https://docs.tealium.com/platforms/cordova-v1/install/
---

<blockquote>
This is the previous version (1.x) of Tealium for Cordova.  
For the current version, see [Tealium for Cordova 2.x](https://docs.tealium.com/platforms/cordova/).
</blockquote>


## Requirements

* Apache Cordova (7.0.0+)
* CocoaPods

## Libraries

The plugin includes the following Tealium libraries:

* [Tealium for iOS](https://docs.tealium.com/platforms/ios-objective-c/)
* [Tealium for Android](https://docs.tealium.com/platforms/android-java/)


<blockquote>
As of version 1.1.1+, framework files are no longer included in the plugin. Instead, the respective dependency managers are used for iOS and Android.
</blockquote>


## Sample Apps

To help to familiarize yourself with our library, the tracking methods, and best practice implementation, explore the Tealium for Cordova [sample app](https://github.com/Tealium/cordova-plugin/tree/master/TealiumSample).

## Install

Install Tealium for Cordova with NPM or manually.

### NPM

Node package manager (NPM) is the recommended installation type. The package name is `tealium-cordova-plugin`.

To install the plugin with NPM, run the following command from within your project directory:

```bash
cordova plugin add tealium-cordova-plugin
```

### Manual

If you cannot use NPM, you may install the plugins manually.

Run the following command on the Command-Line Interface (CLI):

```bash
cd <YOUR_PROJECT_FOLDER>/
cordova platform add <PLATFORM>
cordova plugin add </LOCAL_PATH_TO_TEALIUM_PLUGIN/>
cordova build <PLATFORM>
```

## Initialize

The [`init()`](https://docs.tealium.com/platforms/cordova-v1/api/#init) method initializes the Tealium Cordova plugin, as shown in the following example:

```js
tealium.init({
    account                : "ACCOUNT",
    profile                : "PROFILE",
    environment            : "ENVIRONMENT",
    datasource             : "DATASOURCE",
    instance               : "INSTANCE",
    isLifecycleEnabled     : "TRUE_OR_FALSE",
    isCrashReporterEnabled : "TRUE_OR_FALSE",
    logLevel               : tealium.logLevels.DEV,
    collectDispatchProfile : "DISPATCH_PROFILE",
    collectDispatchURL     : "DISPATCH_URL"});
```

By default, the core iOS and Android libraries send Tealium Collect data to the "main" profile of your account. To direct Tealium Collect to a different endpoint, either override the profile or the endpoint URL.

Override Profile example:  
```js
tealium.init({
    account                : "ACCOUNT",
    profile                : "PROFILE",
    environment            : "ENVIRONMENT",
    instance               : window.tealium_instance,
    collectDispatchProfile : "PROFILE"});
```

Override Endpoint URL example:  
```js
tealium.init({
    account            : "ACCOUNT",
    profile            : "PROFILE",
    environment        : "ENVIRONMENT",
    instance           : window.tealium_instance,
    collectDispatchURL : "https://collect.tealiumiq.com/vdata/i.gif?tealium_account=ACCOUNT&tealium_profile=PROFILE"});
```

## Build Tips

If you have any issues building your app and need to remove and re-add the platform, run the following command, where `PLATFORM` is either `"android"` or `"ios"`:
```bash
cordova platform rm PLATFORM
cordova platform add PLATFORM
```

This usually resolves spurious XCode code signing errors when building for a physical device.

If you experience any issues with CocoaPods while running your build, and want to clear your local CocoaPods cache, run the following command:
```bash
pod cache clean --all && pod repo update
```

## Uninstall

To remove the Tealium plugin, run the following command:
```bash
cordova plugin rm tealium-cordova-plugin
```

Remove the supplementary Tealium modules, if installed:

- `tealium-cordova-crashreporter`
- `tealium-cordova-adidentifier`
- `tealium-cordova-installreferrer`

## Ionic Framework

Tealium's Cordova plugin provides support for the [Ionic Framework](https://ionicframework.com/docs/native/tealium). To install run the following commands:  
```bash
ionic cordova plugin add tealium-cordova-plugin
npm install @ionic-native/tealium
```

The following examples demonstrates usage of the Ionic Framework:

```js
import { Tealium, TealConfig } from '@ionic-native/tealium/ngx';

constructor(private tealium: Tealium) { }

//...

let tealConfig: TealConfig = {
   account: "ACCOUNT",
   profile: "PROFILE",
   environment: "ENVIRONMENT",      // one of "dev", "qa" or "prod"
   isLifecycleEnabled: "true",      // enable lifecycle tracking
   isCrashReporterEnabled: "false", // disable crash reporter (Android only)
   instance: "INSTANCE"             // use the same instance name for all subsequent API calls
}

this.tealium.init(tealConfig).then(()=>{
   this.tealium.trackView({"screen_name": "homescreen"});
});
```
