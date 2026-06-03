---
title: Troubleshooting
description: Learn about the various methods for validating your mobile installation.
url: https://docs.tealium.com/platforms/getting-started-mobile/troubleshooting/
---
## Basics

When testing mobile apps, we recommend that you only test in the Tealium `dev` environment, and not in `prod`. Also, use a build of the app specifically designed for testing. If you must use a production build for testing, such as when you test an app&#39;s appearance in the App Store or Play Store, see the [Charles Proxy](#charles-proxy) section below on switching environments to avoid making changes to the live application.

When publishing changes while debugging, you are subject to the five minute expiry time in Tealium&#39;s cache. During this time, the `utag.js` files are refreshed on Tealium&#39;s servers after you publish.

Each time you launch the app from a cold start (app was previously swiped away from the app tray), the Tealium SDK checks for new files, and subsequently every 15 minutes by default (controlled by [mobile publish settings](). However, if less than five minutes have passed since publishing, restarting the app does not always work until after the five minute expiry time. Switching between the `dev` and `qa` environments while testing may alleviate this problem, because the cache on the environment expires if not used within the last five minutes, and the new file becomes available immediately.

## Tealium EventStream Live Events

The **Live Events** feature in Tealium EventStream is available to all Tealium customers for the purpose of debugging mobile installations.

If you use this troubleshooting method in a production environment, you may be charged for the volume usage. Be sure to disable this feature before your app goes live.

Use one of the following methods to enable the event collection feature.

#### Option 1 - Tealium Collect Tag

Add the [Tealium Collect tag]() from the tag marketplace. In the **Advanced Settings** of the tag, toggle off the QA and Prod environments to avoid publishing the tag to production and incurring usage charges. Requests are sent out from the app as encoded JSON data in a POST request, so this method is more difficult to use in conjunction with Charles Proxy, but the advantage is that you are able to see all data from the webview, including cookie data and variables modified by extensions. If you do not enter a specific profile in the tag configuration, data is sent to the same profile the app is targeting. If you want to send data to a specific profile, see the [Tealium collect tag setup guide]().

#### Option 2 - Tealium Collect Module

In your Tealium iQ account, go to the **Mobile Publish Settings** and enable **Tealium Collect**. The advantage to this method is that data is transmitted as a `GET` request, and each data variable is added to the query string in the form of easily-readable query parameters. This method is best if you intend to use Charles Proxy to inspect the data. Be sure to turn this setting off before pushing app to production to avoid unexpected usage charges. Only the exact data that was passed to Tealium by the app developers is seen, and not the data from the webview in this request such as cookie data or extension-generated data.

By default, data sent using this feature is sent to the &#34;main&#34; profile in your account and not the currently selected profile in your app. To adjust this behavior, override the dispatch URL using the following code snippets in your app, and substitute the appropriate account and profile combination:



```java
Tealium.Config config = Tealium.Config.create(application, &#34;[ACCOUNT]&#34;, &#34;[PROFILE]&#34;, &#34;ENVIRONMENT&#34;);config.setOverrideCollectDispatchUrl(&#34;https://collect.tealiumiq.com/vdata/i.gif?tealium_account=[ACCOUNT]&amp;tealium_profile=[PROFILE]&#34;);
```


```obj-c
TEALConfiguration *configuration = [TEALConfiguration configurationWithAccount:@&#34;[account]&#34;profile:@&#34;[profile]&#34; environment:@&#34;dev&#34;];[configuration setOverrideCollectDispatchURL:@&#34;https://collect.tealiumiq.com/vdata/i.gif?tealium_account=[account]&amp;tealium_profile=[profile]&#34;];
```



After you have configured one of the collection methods above, log in to EventStream and go to **Live Events** to see the incoming events.

For more information, see [Live Events]().

## Charles Proxy

The Charles web debugging proxy inspects all HTTP and SSL/HTTPS traffic between your device and a third-party service that you have configured through Tealium iQ Tag Management.

Set up Charles to proxy your [Android](/platforms/android-kotlin/charles-proxy-android) or [iOS](/platforms/ios-swift/charles-proxy-iosdevice) device.

#### Switching Tealium Environments

You may need to switch from the default environment the app is targeting (for example, `prod`) to a different environment to view your changes. To switch environments, add a custom mapping in Charles Proxy (or other proxy tool such as Fiddler), which transparently switch out the files that are being served to the app. For example, the app requests the `prod` `utag.js` file (`https://tags.tiqcdn.com/utag/tealiummobile/demo/prod/utag.js`), but Charles proxy serves back the `dev` `utag.js` (`https://tags.tiqcdn.com/utag/tealiummobile/demo/dev/utag.js`)

The following configuration steps switch to a different Tealium environment:

1. Open Charles Proxy and go to **Tools &gt; Map Remote**. In the **Map Remote Settings** screen, check **Enable Map Remote** and then click **Add**.
1. In the **Host** box, paste `https://tags.tiqcdn.com/utag/&lt;account&gt;/&lt;profile&gt;/prod/*`, substituting your account and profile into the URL. After pasting, move your cursor and click in the **Port** or **Path** field of the **Map From** section, and Charles automatically separates the URL into its component parts.
1. In the **Map To** section, perform the same process again, this time changing the environment from `prod` to `dev` (or `qa`) in the URL, depending on which environment you want to target. Remove the asterisks character from the end of the URL, for example:  `https://tags.tiqcdn.com/utag/&lt;account&gt;/&lt;profile&gt;/dev/`
1. Click **OK** to complete the setup.

Charles Proxy now switches all requests from the `prod` environment to the `dev` environment. To switch back to the app&#39;s default environment, disable or delete the **Map Remote** rule, or turn off the proxy on your device.

Exit the app and relaunch it for this setting to take effect.

#### Traffic Inspection

The following table lists common examples of requests to inspect using Charles proxy:

| Request | Description |
| :-- | :-- |
| `\*.tealiumiq.com` | These hits are sent if you&#39;re using Tealium AudienceStream&#39;s Live Events feature for debugging, as described in Option 1 above. |
| `mobile.html` | Initial hit retrieving settings from Tealium. |
| `google-analytics.com, collect.gif` | If using Google Analytics, hits are sent to `collect.gif`, and the query parameters is inspected. |
| `/b/ss` | This filter picks up all hits to Adobe Analytics, and Context Data and/or props/eVars is shown in the query string. |
| `tags.tiqcdn.com` | To see which of your Tealium tags have fired, look for hits to this server. If you don&#39;t have bundling enabled, then you&#39;ll see individual files for each tag (for example, the tag with UID 123 is `utag.123.js`). Be aware that if the files are cached, they won&#39;t necessarily show in your Charles Proxy session, even if they have fired, so this is not always the most accurate way of testing. |

## Trace

For more information, see [trace](/platforms/getting-started-mobile/trace/).

## Analytics Tools

To set up Google Analytics to troubleshoot your configuration, use the following steps:

1. Set up a test Google Analytics account for yourself, and note the property ID (for example, `UA-12345678-1`).
1. Add the [Google Analytics]() tag through Tealium IQ, entering your new property ID in the relevant configuration field.
1. Enable screen views in the GA tag, and map one of your data variables to `screenName`.
1. (Optional) Set up a custom event in GA by mapping any two variables to **Event Action** and **Event Category** respectively. If the app is functioning correctly, screen views and custom events appear in your Google Analytics account. A custom event is automatically generated so long as **Event Category** and **Event Action** are set, and it doesn&#39;t matter which specific data you pass to these variables for test purposes.

## Device Logs

#### Standard Device Logs



1.  Install Android Studio on your machine.
1.  [Enable USB Debugging](https://developer.android.com/studio/debug/dev-options#enable) on your Android device.
1.  Launch Android Studio on your PC/Mac, and ensure that **Android Monitor** (v3.1 and earlier) or **Run** (v3.2 and later) is displayed at the bottom of the screen. If neither of those options appear, go to **View &gt; Tool Windows &gt; Android Monitor/Run** to show one of them.
1.  Connect your Android device with a USB cable. The logs from your device in the console become available. This shows the output from all apps, including the Android system itself, and if you are testing a production build, it is likely that only critical errors/crashes are logged.
1. If you have version Android Studio 3.2 or later installed, there are a number of [other tools](https://developer.android.com/studio/profile/monitor) with the ability to debug/validate/troubleshoot.


1.  Install XCode on your machine.
1.  Connect your iPhone/iPad with a lightning cable.
1.  Go to **Window &gt; Devices and Simulators &gt; Devices** and select your device from the list.
1.  To see the device console, click the up-triangle at the bottom left of the right-hand panel. The console displays logs from all apps on the device. If the app is a production build, it is likely that only critical errors and crashes are logged.



 If you filter the console with `tealium`, you might see these logs more clearly. 

#### Tealium Debug Logs



1.  Open Android Studio and plug in your device.
1.  Set the Tealium Debug Level to the most verbose setting (`dev`) by calling the `.setForceOverrideLogLevel()` method (for example, `.setForceOverrideLogLevel(&#34;dev&#34;);`).
1.  Run your project and view the output in the Logcat console. The publish settings, configuration settings, and payload is displayed on the console.

 If you filter Logcat with &#34;Sent queued dispatch&#34; you might see these logs more clearly. 



1.  Open Xcode and plug in your device.
1.  Set the Tealium Debug Level to the most verbose setting (`dev`) by calling the `.setLogLevel()` method.
	* iOS: `[tealConfig setLogLevel: TEALLogLevelDev];`
	* Swift: `setLogLevel(logLevel: TealiumLogLevel)`
1.  Run your project and view the output in the `lldb` console. The publish settings, configuration settings, and payload is displayed on the console.

 If you filter your IDE console with `datasources payload`, you might see these logs more clearly. 



## Debugging mobile.html

This section shows how to troubleshoot a mobile implementation of Tealium iQ Tag Management through the published file `mobile.html`.

When you activate a mobile profile in Tealium iQ, a file named `mobile.html` is published to the following path:

`http://tags.tiqcdn.com/utag/{ACCOUNT}/{PROFILE}/{ENVIRONMENT}/mobile.html`

The native module library uses this file to receive mobile publish settings and to facilitate the Tag Management module. This file is useful to perform some basic troubleshooting of your mobile implementation.

#### Inspecting mobile.html

The behavior of `utag.js` on the `mobile.html` page is similar to that of a standard desktop website page. The `utag.js` file is loaded and subsequent vendor tags are executed.

To inspect the `mobile.html` page:

1.  In a new browser window, load the `mobile.html` URL for your iQ profile.
1.  Open the developer tools or web console of the browser to inspect the page source.

From here, you can perform many of the same troubleshooting techniques that are used for a website with Tealium&#39;s `utag.js` installed.

#### Verifying the Publish Timestamp

The first thing to verify is that your most recently published changes are being loaded in `mobile.html`. You can verify the changes by matching the timestamp from the HTML source to the timestamp from the iQ Versions screen.

To verify the publish timestamp:

1.  At the top of the page source of `mobile.html`, look for the published timestamp on the first line. The timestamp in `mobile.html` has the following pattern: `ut.4.0.YYYYMMDDHHMM`. (Time is always in GMT)
1.  In your iQ profile, go the **Versions** screen and find the most recently published version of the same environment. The timestamp of this publish matches the timestamp found inside `mobile.html`.

#### Inspecting Mobile Publish Settings JavaScript Object

The `mobile.html` page uses a JavaScript object named `mps` to store the values of the [mobile publish settings](). Inspect this object to verify your settings.

To inspect the `mps` object:

1.  Enter `mps` into the web console.
1.  The properties marked `4` and `5` correspond to versions 4.x and 5.x of your mobile library respectively.

#### Simulating Tracking Calls

The behavior of `utag.js` on this page is similar to that of a standard desktop website page. Watch the network activity to see which `utag.\*.js` files are loaded and trigger tracking calls from the browser console to verify that your tags are working as expected.

To simulate tracking calls in `mobile.html`:

1.  From the browser console, enter `utag.view({screen_title : &#34;Test Page&#34;})`.
1.  Go to the **Network Activity** screen to inspect the outgoing vendor tracking activity.

## Remote Debugging

Advanced users are able to debug the hidden webview using Chrome or Safari remote web inspector.




Ensure the app is configured to allow [remote debugging](https://developer.chrome.com/docs/devtools/remote-debugging/webviews/) of the Tealium webview (Must be done by the app developer at build time).

Navigate to [chrome://inspect/#devices](chrome://inspect/#devices) on a Chrome Browser

Ensure your device is connected to your machine with a USB cable.

In the list of web pages, look for the one hosted on `tags.tiqcdn.com`. This page is the Tealium webview (`mobile.html`), which is inspected in the same way as described above. Whenever the app triggers a view or link request, any breakpoints you have set in your JavaScript tag templates are hit, and the value of the data layer is inspected as if it were a desktop website.




If you are using iOS 16.4 or later, you must manually set the webview to inspectible. Use the `getTagManagementWebView()` API call to set the `isInspectable` property. For more information, see [Tealium API reference](/platforms/ios-swift/api/tealium/#gettagmanagementwebview).

Follow Apple&#39;s [Safari Developer Guide](https://developer.apple.com/library/content/documentation/AppleApplications/Conceptual/Safari_Developer_Guide/GettingStarted/GettingStarted.html) to enable the web inspector in Safari for Mac OSX and in the iPhone/iPad&#39;s device settings.

When you are able see your device on the **Develop** menu, open `tags.tiqcdn.com/utag/ACCOUNT/PROFILE/ENVIRONMENT/mobile.html` in the list of open web pages on the device, and then continue to follow the instructions in the [Debugging mobile.html](#debugging-mobilehtml) section above.

This procedure also works when using an iOS simulator to debug your app.&lt;br&gt;&lt;br&gt;You cannot debug web views in apps installed through the App Store or Apple Configurator. Web views can only be debugged if the app has been installed with XCode and run either on an iOS simulator or a physical testing device.


