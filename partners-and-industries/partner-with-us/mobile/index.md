---
title: Mobile
description: Learn how to integrate your mobile SDK with Tealium for Mobile.
url: https://docs.tealium.com/partners-and-industries/partner-with-us/mobile/
---


Are you a mobile vendor with an SDK that tracks app usage and visitor behavior? Do you want your users to enjoy the same convenience as those using tag management to easily add your SDK to their app? If so, this guide explains how to integrate with Tealium for Mobile to make it easy for developers to leverage an existing Tealium implementation to active your native SDK.

## What is Tealium for Mobile?

Tealium for Mobile is a complete solution for managing vendor integrations in the app or sending mobile customer data to the Tealium Customer Data Hub. Tealium users enjoy the benefits of tag management in a native app and the power of server-side data management with Tealium EventStream and Tealium AudienceStream.

[Learn more about Tealium for Mobile](/platforms/getting-started-mobile/).

## Remote Commands

A remote command is an integration that offers a native solution for loading your third-party SDK while maintaining the convenience of using iQ Tag Management to configure tracking options, all without needing to resubmit the app.

Tealium users with a mobile implementation can add the capabilities of your SDK simply by adding a remote command module that integrates its functionality. A remote command module takes the customer data and events being tracked by the main Tealium library and passes it to the corresponding methods of your SDK.

This simplifies the SDK implementation by avoiding the hassle of managing multiple SDK&#39;s that track much of the same data.

[Learn more about remote commands](/platforms/remote-commands/).

## FAQ

**What are the limitations of a remote command integration?**

Mobile developers may need to implement some SDK functions that Tealium does not offer. Examples of functionality that must be implemented directly include:

* In-App Personalization
* Push Notifications
* Uninstall Tracking

**Can a remote commands module initialize selectively?**

Yes, you can use load rules in iQ Tag Management to control when to initialize a vendor SDK.

## Become a Partner

[Contact us](https://tealium.com/tealium-partner-network/) to integrate your technology.
