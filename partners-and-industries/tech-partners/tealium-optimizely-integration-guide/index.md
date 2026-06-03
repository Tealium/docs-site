---
title: Tealium + Optimizely Integration Guide
description: This article describes how to get the most out of Tealium and Optimizely and enable the transmission of Tealium audiences and audience badges to Optimizely.
url: https://docs.tealium.com/partners-and-industries/tech-partners/tealium-optimizely-integration-guide/
---## How it works

The Optimizely platform includes technologies for modern software development, such as feature flags, A/B testing at scale, AI-powered personalization, and streaming analytics. Experiments and feature flags are run on the Optimizely platform to assist in understanding what works and what does not work, thus eliminating guesswork.

### Client-Side integrations

The following table lists the description and prerequisites for client-side integrations of the Optimizely tag and provides links to detailed setup documentation:

|Integration Type| What to Expect from this Integration| Product Requirements| Setup Guides|
|---| ---| ---| ---|
| **Optimizely Tag** &lt;ul&gt;&lt;li&gt;Asynchronous&lt;/li&gt;&lt;li&gt;Synchronous&lt;/li&gt;&lt;/ul&gt; | Tealium Optimizely Asynchronous and Synchronous tag integrations allow you to quickly and easily deploy Optimizely web projects by configuring Optimizely in Tealium iQ Tag Management. Asynchronous tags are loaded simultaneously, whereas synchronous tags are loaded sequentially, one after another.|  **Tealium** &lt;ul&gt;&lt;li&gt;Tealium iQ Tag Management (Required)&lt;/li&gt;&lt;/ul&gt; **Optimizely** &lt;ul&gt;&lt;li&gt;Optimizely Account (Required)&lt;/li&gt;&lt;/ul&gt; |  See the following setup guides: &lt;ul&gt;&lt;li&gt;[Asynchronous]()&lt;/li&gt;&lt;li&gt;[Synchronous]()&lt;/li&gt;&lt;/ul&gt; |

### Server-Side integrations

The following table lists descriptions and prerequisites for the server-side Optimizely Integration types and provides links to detailed setup documentation.

|Integration Type| What to Expect from this Integration| Product Requirements| Setup Guides|
|---| ---| ---| ---|
| **Optimizely Events** | Integrating with Tealium Optimizely Events lets you send online and offline event data to Optimizely through Tealium EventStream. This method benefits all Optimizely products by allowing a comprehensive view of the customer for improved insights into conversions and campaign analytics that can be used to benefit the entire customer lifecycle experience.|  **Tealium** &lt;ul&gt;&lt;li&gt;EventStream and/or AudienceStream (Required)&lt;/li&gt;&lt;/ul&gt; **Optimizely** &lt;ul&gt;&lt;li&gt;Optimizely Web or Full Stack (Required)&lt;/li&gt;&lt;/ul&gt; |  See the following setup guide: &lt;ul&gt;&lt;li&gt;[Optimizely Events Connector Setup Guide (BETA)]()&lt;/li&gt;&lt;/ul&gt; |
| **Optimizely Dynamic Customer Profiles** &lt;br&gt; | Integrating with Optimizely Dynamic Customer Profiles creates a single, actionable view of the customer by providing Optimizely with online and offline first-party data. By leveraging the Tealium AudienceStream Customer Data Platform (CDP), you can build profiles and audiences within Tealium that Optimizely and other channels can take action on. This integration allows mutual Tealium and Optimizely customers to deliver consistent, personalized web and mobile experiences for their most valuable customers, and measure the impact of the resulting experiences.|  **Tealium** &lt;ul&gt;&lt;li&gt;EventStream and/or AudienceStream (Required)&lt;/li&gt;&lt;/ul&gt; **Optimizely** &lt;ul&gt;&lt;li&gt;Optimizely Web or Full Stack (Required)&lt;/li&gt;&lt;/ul&gt; |  See the following setup guide: &lt;ul&gt;&lt;li&gt;[Optimizely DCP Connector Setup Guide]()&lt;/li&gt;&lt;/ul&gt; |

## Additional resources

* [Optimizely Event API: Getting Started](https://docs.developers.optimizely.com/web/docs/getting-started-event-api)
* [Optimizely: Create Audiences with Dynamic Customer Profiles](https://help.optimizely.com/Target_Your_Visitors/Personalization%3A_Create_Audiences_with_Dynamic_Customer_Profiles)
* [Optimizely Integration with Tealium AudienceStream]()
* [Integrating AudienceStream and Optimizely Full Stack]()
* [Tealium Tool: Optimizely Helper]()
