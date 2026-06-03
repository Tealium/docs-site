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
|Braze Web SDK Tag|  With the Braze Web SDK, you can: &lt;ul&gt;&lt;li&gt;Collect session data&lt;/li&gt;&lt;li&gt;Identify users (with the Tealium unified data layer)&lt;/li&gt;&lt;li&gt;Record purchases and custom events through a web/mobile browser.&lt;/li&gt;&lt;/ul&gt; Implementing the Braze Web SDK enables you to create a more complete view of your users across web and mobile channels. You can also use the Web SDK to engage with your users by sending in-app web messages and web push notifications. |  Tealium iQ Tag Management |  [Braze Web SDK Tag Setup Guide]() |

## Server-side integration

The following table lists descriptions and prerequisites for the server-side Braze integration types and provides links to detailed setup documentation.

|Integration Type| What to Expect from this Integration| Product Requirements| Setup Guides|
|---| ---| ---| ---|
|Braze Connector|  This Braze integration lets you further enrich your Braze data through AudienceStream and/or EventStream to build real-time, personalized, omnichannel experiences with your customers. The **Track User** action contains functionality that is the same for AudienceStream and EventStream. As a best practice, we recommend using User Attribute features with AudienceStream and Event and Purchase features with EventStream. Use cases that do not fit these criteria may ignore this best practice. |  Tealium EventStream and/or Tealium AudienceStream |  [Braze Connector Setup Guide]() |

## Mobile Integration

The following table lists descriptions and prerequisites for mobile Braze integration types and provides links to detailed setup documentation.

|Integration Type| What to Expect from this Integration| Product Requirements| Setup Guides|
|---| ---| ---| ---|
|Braze Remote Commands|  This Braze integration uses the following: &lt;ul&gt;&lt;li&gt;**Native Braze SDK** - A remote command module that wraps the Braze methods.&lt;/li&gt;&lt;li&gt;**Braze Remote Command Tag** - A tag that translates event tracking into native Braze calls.&lt;/li&gt;&lt;/ul&gt; This solution leverages the convenience of Tag Management to configure a native Braze implementation without having to add vendor-specific code to your app. Adding the Braze remote command module to your app automatically installs and builds the required Braze libraries. If you are using a dependency manager installation, there is no need to install the Braze SDK separately. |  Tealium iQ Tag Management |  [Remote Command: Braze](https://docs.tealium.com/platforms/remote-commands/integrations/braze/) |
