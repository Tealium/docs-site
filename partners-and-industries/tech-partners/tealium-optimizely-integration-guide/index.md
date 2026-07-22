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
| **Optimizely Tag** <ul><li>Asynchronous</li><li>Synchronous</li></ul> | Tealium Optimizely Asynchronous and Synchronous tag integrations allow you to quickly and easily deploy Optimizely web projects by configuring Optimizely in Tealium iQ Tag Management. Asynchronous tags are loaded simultaneously, whereas synchronous tags are loaded sequentially, one after another.|  **Tealium** <ul><li>Tealium iQ Tag Management (Required)</li></ul> **Optimizely** <ul><li>Optimizely Account (Required)</li></ul> |  See the following setup guides: <ul><li>[Asynchronous](https://docs.tealium.com/optimizely-asynchronous-tag/)</li><li>[Synchronous](https://docs.tealium.com/optimizely-sync-tag/)</li></ul> |

### Server-Side integrations

The following table lists descriptions and prerequisites for the server-side Optimizely Integration types and provides links to detailed setup documentation.

|Integration Type| What to Expect from this Integration| Product Requirements| Setup Guides|
|---| ---| ---| ---|
| **Optimizely Events** | Integrating with Tealium Optimizely Events lets you send online and offline event data to Optimizely through Tealium EventStream. This method benefits all Optimizely products by allowing a comprehensive view of the customer for improved insights into conversions and campaign analytics that can be used to benefit the entire customer lifecycle experience.|  **Tealium** <ul><li>EventStream and/or AudienceStream (Required)</li></ul> **Optimizely** <ul><li>Optimizely Web or Full Stack (Required)</li></ul> |  See the following setup guide: <ul><li>[Optimizely Events Connector Setup Guide (BETA)](https://docs.tealium.com/optimizely-events-connector/)</li></ul> |
| **Optimizely Dynamic Customer Profiles** <br> | Integrating with Optimizely Dynamic Customer Profiles creates a single, actionable view of the customer by providing Optimizely with online and offline first-party data. By leveraging the Tealium AudienceStream Customer Data Platform (CDP), you can build profiles and audiences within Tealium that Optimizely and other channels can take action on. This integration allows mutual Tealium and Optimizely customers to deliver consistent, personalized web and mobile experiences for their most valuable customers, and measure the impact of the resulting experiences.|  **Tealium** <ul><li>EventStream and/or AudienceStream (Required)</li></ul> **Optimizely** <ul><li>Optimizely Web or Full Stack (Required)</li></ul> |  See the following setup guide: <ul><li>[Optimizely DCP Connector Setup Guide](https://docs.tealium.com/optimizely-dcp-connector/)</li></ul> |

## Additional resources

* [Optimizely Event API: Getting Started](https://docs.developers.optimizely.com/web/docs/getting-started-event-api)
* [Optimizely: Create Audiences with Dynamic Customer Profiles](https://help.optimizely.com/Target_Your_Visitors/Personalization%3A_Create_Audiences_with_Dynamic_Customer_Profiles)
* [Optimizely Integration with Tealium AudienceStream](https://docs.tealium.com/optimizely-integration-with-audiencestream/)
* [Integrating AudienceStream and Optimizely Full Stack](https://docs.tealium.com/integrating-audiencestream-and-optimizely-full-stack/)
* [Tealium Tool: Optimizely Helper](https://docs.tealium.com/optimizely-helper/)
