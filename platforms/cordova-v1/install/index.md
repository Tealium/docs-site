---
title: Install
description: Learn to install Tealium for Cordova.
url: https://docs.tealium.com/platforms/cordova-v1/install/
---
This is the previous version (1.x) of Tealium for Cordova.  
For the current version, see [Tealium for Cordova 2.x](/platforms/cordova/).

## Requirements

* Apache Cordova (7.0.0&#43;)
* CocoaPods

## Libraries

The plugin includes the following Tealium libraries:

* [Tealium for iOS](/platforms/ios-objective-c/)
* [Tealium for Android](/platforms/android-java/)

As of version 1.1.1&#43;, framework files are no longer included in the plugin. Instead, the respective dependency managers are used for iOS and Android.

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
cd &lt;YOUR_PROJECT_FOLDER&gt;/
cordova platform add &lt;PLATFORM&gt;
cordova plugin add &lt;/LOCAL_PATH_TO_TEALIUM_PLUGIN/&gt;
cordova build &lt;PLATFORM&gt;
```

## Initialize

The [`init()`](/platforms/cordova-v1/api/#init) method initializes the Tealium Cordova plugin, as shown in the following example:

```js
tealium.init({
    account                : &#34;ACCOUNT&#34;,
    profile                : &#34;PROFILE&#34;,
    environment            : &#34;ENVIRONMENT&#34;,
    datasource             : &#34;DATASOURCE&#34;,
    instance               : &#34;INSTANCE&#34;,
    isLifecycleEnabled     : &#34;TRUE_OR_FALSE&#34;,
    isCrashReporterEnabled : &#34;TRUE_OR_FALSE&#34;,
    logLevel               : tealium.logLevels.DEV,
    collectDispatchProfile : &#34;DISPATCH_PROFILE&#34;,
    collectDispatchURL     : &#34;DISPATCH_URL&#34;});
```

By default, the core iOS and Android libraries send Tealium Collect data to the &#34;main&#34; profile of your account. To direct Tealium Collect to a different endpoint, either override the profile or the endpoint URL.

Override Profile example:  
```js
tealium.init({
    account                : &#34;ACCOUNT&#34;,
    profile                : &#34;PROFILE&#34;,
    environment            : &#34;ENVIRONMENT&#34;,
    instance               : window.tealium_instance,
    collectDispatchProfile : &#34;PROFILE&#34;});
```

Override Endpoint URL example:  
```js
tealium.init({
    account            : &#34;ACCOUNT&#34;,
    profile            : &#34;PROFILE&#34;,
    environment        : &#34;ENVIRONMENT&#34;,
    instance           : window.tealium_instance,
    collectDispatchURL : &#34;https://collect.tealiumiq.com/vdata/i.gif?tealium_account=ACCOUNT&amp;tealium_profile=PROFILE&#34;});
```

## Build Tips

If you have any issues building your app and need to remove and re-add the platform, run the following command, where `PLATFORM` is either `&#34;android&#34;` or `&#34;ios&#34;`:
```bash
cordova platform rm PLATFORM
cordova platform add PLATFORM
```

This usually resolves spurious XCode code signing errors when building for a physical device.

If you experience any issues with CocoaPods while running your build, and want to clear your local CocoaPods cache, run the following command:
```bash
pod cache clean --all &amp;&amp; pod repo update
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

Tealium&#39;s Cordova plugin provides support for the [Ionic Framework](https://ionicframework.com/docs/native/tealium). To install run the following commands:  
```bash
ionic cordova plugin add tealium-cordova-plugin
npm install @ionic-native/tealium
```

The following examples demonstrates usage of the Ionic Framework:

```js
import { Tealium, TealConfig } from &#39;@ionic-native/tealium/ngx&#39;;

constructor(private tealium: Tealium) { }

//...

let tealConfig: TealConfig = {
   account: &#34;ACCOUNT&#34;,
   profile: &#34;PROFILE&#34;,
   environment: &#34;ENVIRONMENT&#34;,      // one of &#34;dev&#34;, &#34;qa&#34; or &#34;prod&#34;
   isLifecycleEnabled: &#34;true&#34;,      // enable lifecycle tracking
   isCrashReporterEnabled: &#34;false&#34;, // disable crash reporter (Android only)
   instance: &#34;INSTANCE&#34;             // use the same instance name for all subsequent API calls
}

this.tealium.init(tealConfig).then(()=&gt;{
   this.tealium.trackView({&#34;screen_name&#34;: &#34;homescreen&#34;});
});
```
