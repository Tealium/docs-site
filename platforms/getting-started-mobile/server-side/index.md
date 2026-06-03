---
title: Server-Side
description: Learn about implementing a server-side solution for mobile.
url: https://docs.tealium.com/platforms/getting-started-mobile/server-side/
---
## Tealium Collect

To make use of the server-side products in the Tealium Customer Data Hub you must add the Tealium Collect service to your installation.

Tealium Collect is activated using one of these methods:

* Tealium Collect tag in Tealium iQ Tag Management
* Tealium Collect module in your app

Once added, Tealium Collect sends HTTPS requests to the Customer Data Hub data collection servers for use with the following server-side products:

* [Tealium EventStream]()
* [Tealium AudienceStream]()
* [Tealium EventStore]()
* [Tealium AudienceDB &amp; EventDB]()

Tealium Collect offers many benefits to a mobile application. If you have Tealium EventStream and the Collect module installed, then third-party vendor SDKs may be removed from your app and implemented as server-side connectors instead. Offloading vendors to an API hub such as EventStream helps to reduce app size, minimize network traffic, and conserve battery power on the device.

The following diagram illustrates how the Tealium SDK uses Tealium Collect to transmit events directly to EventStream and AudienceStream using HTTPS requests so you can send data to vendors or put visitors into audiences, assign badges, and apply attributes.

![](/images/platforms/getting-started-mobile/tealium_collect_data_flow_diagram.png)

### JavaScript Tag

The Tealium Collect tag is added to your iQ Tag Management configuration and executed on the device within the Tag Management module. The JavaScript tag runs in the hidden webview and dispatches tracking calls to the Tealium servers.

**Recommended For:**

* Installations that already use the Tag Management module
* Implementations that require data layer customizations using extensions

Learn more about [how to set up the Tealium Collect tag]().

### Native Module

The Tealium Collect module is enabled using the [mobile publish settings]() of your iQ account. The Collect module runs as native code in your app and dispatches tracking calls directly to the Tealium servers using HTTPS.

**Recommended For:**

* A simple, light-weight installation.
* Installations without access to iQ Tag Management.

For the Swift library, Tealium Collect must be enabled and disabled in the native code.

### Data Layer Enrichment (DLE)

Tealium AudienceStream offers the added benefit of returning visitor profile data to Tealium Collect with a feature called [Data Layer Enrichment (DLE)](). In the Collect module, use DLE to personalize your app based on the returned visitor attributes.

In Tealium iQ Tag Management, with the Collect tag running, the hidden webview `mobile.html` provides access to DLE visitor attributes. These attributes are accessible when configuring extension, loading rules, etc. A [remote command](/platforms/remote-commands/) is required to communicate between the webview and mobile app for in-app personalization based on DLE values.

The [VisitorService module for Swift](/platforms/ios-swift/module-list/visitor-service/) also adds the visitor profile to the data layer.
