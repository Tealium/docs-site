---
title: Tealium + Braze Integration Guide
description: This article describes how to get the most out of Tealium and Braze.
url: https://docs.tealium.com/partners-and-industries/tech-partners/tealium-braze-integration-guide/
---

[Braze](https://www.braze.com) is a comprehensive customer engagement platform for email, mobile, and web that powers relevant and memorable experiences between consumers and the brands they love. In 2019, Braze sent over 600 billion personalized emails, push notifications, in-app messages, SMS messages, and more to billions of consumers for leading brands like HBO, Walmart, and Postmates.

## Client-side integration

The following table lists descriptions and prerequisites for the client-side Braze integration types and provides links to detailed setup documentation.

|Integration Type| What to Expect from this Integration| Product Requirements| Setup Guides|
|---| ---| ---| ---|
|Braze Web SDK Tag|  With the Braze Web SDK, you can: <ul><li>Collect session data</li><li>Identify users (with the Tealium unified data layer)</li><li>Record purchases and custom events through a web/mobile browser.</li></ul> Implementing the Braze Web SDK enables you to create a more complete view of your users across web and mobile channels. You can also use the Web SDK to engage with your users by sending in-app web messages and web push notifications. |  Tag Management |  [Braze Web SDK Tag Setup Guide](https://docs.tealium.com/braze-web-sdk-tag/) |

## Server-side integration

The following table lists descriptions and prerequisites for the server-side Braze integration types and provides links to detailed setup documentation.

|Integration Type| What to Expect from this Integration| Product Requirements| Setup Guides|
|---| ---| ---| ---|
|Braze Connector|  This Braze integration lets you further enrich your Braze data through Customer Data Platform (CDP) and/or Event Streaming to build real-time, personalized, omnichannel experiences with your customers. The **Track User** action contains functionality that is the same for CDP and Event Streaming. As a best practice, we recommend using User Attribute features with CDP and Event and Purchase features with Event Streaming. Use cases that do not fit these criteria may ignore this best practice. |  Event Streaming and/or Customer Data Platform (CDP) |  [Braze Connector Setup Guide](https://docs.tealium.com/braze-connector/) |

## Mobile Integration

The following table lists descriptions and prerequisites for mobile Braze integration types and provides links to detailed setup documentation.

|Integration Type| What to Expect from this Integration| Product Requirements| Setup Guides|
|---| ---| ---| ---|
|Braze Remote Commands|  This Braze integration uses the following: <ul><li>**Native Braze SDK** - A remote command module that wraps the Braze methods.</li><li>**Braze Remote Command Tag** - A tag that translates event tracking into native Braze calls.</li></ul> This solution leverages the convenience of Tag Management to configure a native Braze implementation without having to add vendor-specific code to your app. Adding the Braze remote command module to your app automatically installs and builds the required Braze libraries. If you are using a dependency manager installation, there is no need to install the Braze SDK separately. |  Tag Management |  [Remote Command: Braze](https://docs.tealium.com/platforms/remote-commands/integrations/braze/) |
