---
title: Client-Side
description: Learn about the capabilities of the client-side solution.
url: https://docs.tealium.com/platforms/getting-started-mobile/client-side/
---
## Web

Tealium iQ Tag Management is a client-side solution that saves your vendor tag configuration and business logic to a static JavaScript named `utag.js`. As visitors browse your site this file is loaded and run in the browser (client-side) to determine which vendor tags to load and how to send their data. After these files are retrieved by the browser they are cached for subsequent page views to optimize network traffic and page performance.

Learn more about [how iQ Tag Management works](https://docs.tealium.com/how-tealium-iq-works/).


## Mobile

In iQ Tag Management you use a separate [mobile profile](https://docs.tealium.com/creating-a-mobile-profile/), one for iOS and one for Android, to manage the tags and configuration for your mobile app. A mobile profile generates a file named `mobile.html` that is published to the following path at Tealium:

`http://tags.tiqcdn.com/utag/ACCOUNT/PROFILE/ENVIRONMENT/mobile.html`

When you add Tealium to your mobile app, the client-side solution uses a hidden webview to load `mobile.html`, which is optimized for mobile devices. This page contains settings that control the behavior of the Tealium SDK and it loads `utag.js` to run your tag configuration.

Sample contents of `mobile.html`:

```html
<!DOCTYPE html>
<!--tealium tag management - mobile.webview ut4.0.201905291649, Copyright 2019 Tealium.com Inc. All Rights Reserved.-->
<html>
<head><title>Tealium Mobile Webview</title></head>
<body>
<script type="text/javascript">
var utag_cfg_ovrd={noview:true};
var mps = {
    "5": {
        "_is_enabled":"true",
        "battery_saver":"true",
        "dispatch_expiration":"-1",
        "enable_collect":"false",
        "enable_s2s_legacy":"false",
        "enable_tag_management":"true",
        "event_batch_size":"1",
        "minutes_between_refresh":"15.0",
        "offline_dispatch_limit":"100",
        "override_log":"",
        "wifi_only_sending":"false"
    },
    "_firstpublish":"true"
}
</script>
<script type="text/javascript" src="//tags.tiqcdn.com/utag/ACCOUNT/PROFILE/ENVIRONMENT/utag.js"></script>
</body>
</html>
```

This client-side solution lets you follow the traditional tag management workflow to deploy tags to your app and to adjust mobile settings related to tracking behavior.

The following diagram illustrates how iQ Tag Management loads your vendor tag configuration as visitors use your mobile app. This example shows how the Tealium SDK converts a tracked purchase event to a JavaScript tracking call in the hidden webview. Your vendor tags run in the hidden webview, just as they would on a mobile web page, and tracking data is transmitted directly from the app (client-side) to the vendor.

![](https://docs.tealium.com/images/platforms/getting-started-mobile/tag_management_data_flow_diagram.png)

### Benefits

The client-side approach has the following benefits:

* **Tag Vendor Support**
Since the client-side solution is deployed using iQ Tag Management, you have access to the existing tag marketplace integrations.
* **Data Layer Customization**
More options for data layer customization using [extensions](https://docs.tealium.com/about-extensions/).

### Considerations

Keep in mind the following considerations:

* **WebView Behavior**
The native webviews are provided by the iOS/Android APIs and may exhibit behavior beyond the control of Tealium.
* **Memory Usage**
The native webview results in slightly more memory usage in the app.
* **Network Traffic**
The more tags you deploy to your app, the more network traffic is generated due to the loading of vendor JavaScript tags and their resulting tracking pixels.

## Use Cases

The client-side solution is best for the following scenarios.

### iQ Tag Management Only
You are only subscribed to iQ Tag Management and do not have access to Tealium EventStream.

### Complex Analytics
You have a complex analytics implementation and either do not have the resources to add the required data layer or have a short timeline to deploy. The ability to run extension using the client-side Tag Management solution lets you manipulate the built-in data layer for your analytics needs and offload costly development time on your native app to the rapid configuration effort in iQ Tag Management.

### Required Vendor SDK
You require mobile-specific features from a third-party vendor SDK, such as Firebase, push notifications, content modification, or attribution fingerprinting. The client-side solution offers [remote commands](https://docs.tealium.com/platforms/remote-commands/), a way to trigger native code blocks from within the hidden webview and configured within iQ Tag Management.

## Supported Libraries

The following platforms support the Tag Management client-side solution:

* [Tealium for Android](https://docs.tealium.com/platforms/android-java/)
* [Tealium for Cordova](https://docs.tealium.com/platforms/cordova/)
* [Tealium for iOS](https://docs.tealium.com/platforms/ios-swift/)
* [Tealium for React Native](https://docs.tealium.com/platforms/react-native/)
* [Tealium for Xamarin](https://docs.tealium.com/platforms/xamarin/)

## Tealium Collect Tag

The [Tealium Collect Tag](https://docs.tealium.com/tealium-collect-tag/) sends data to the Tealium Customer Data Hub server-side product EventStream. This tag is the client-side solution for the [native Collect Module](https://docs.tealium.com/platforms/getting-started-mobile/server-side/#tealium-collect-module). Using both in your app doubles your usage volume and result in additional charges on your account.

The primary benefit of the client-side Tealium Collect tag is the ability to use extensions to customize the data layer prior to collection.

