---
title: The Identity Partner Ecosystem
description: This article explains how the identity providers in Tealium’s Identity Partner Ecosystem work in the Tealium platform and how to use them.
url: https://docs.tealium.com/industries/tealium-identity-partners/about/
---
Tealium relies on deterministic information sources to use PII to stitch visitor data together into a visitor profile for a single customer view. However, you can use identity providers of first-party and third-party data, which often rely on probabilistic methods of identity resolution, to create high-quality insights about each visitor, prospect and customer. These probabilistic insights can be combined with data collected and profiles enriched by Tealium to enhance relationship data and provide personalized experiences to customers.

## What do Identity Providers do?

Tealium’s Identity Partners provide the following services:

* Collect first party and third party data into a single customer database. This can be used as a CRM itself, or used to enhance a CRM that a business owns.
* Collect, clean, and normalize first party data in an ongoing process to ensure the quality of their service.
* Integrate with UID2.0, the open source ID framework that will be replacing third-party cookies. For example, The Trade Desk offers UID 2.0, which allows the advertiser to share PII, and they send back a short-term anonymous identifier for ad targeting.
* Some data providers also provide AdTech and publisher-related features. These direct integrations with publisher platforms can support ad targeting, and others allow analysis of ad campaigns in privacy-compliant environments.

Tealium provides access to a large number of identity partner integrations across the platform: iQ Tag Management, EventStream, Data Source, AudienceStream, and Functions. Because it can be a lot of work pulling information from each of these sources and combining it into a clear vision of your visitor and customer profile, Tealium is here to make the process of integrating identity provider data from multiple sources smoother and easier.

### Deterministic vs Probabilistic

It is important to understand the difference between deterministic matching and probabailistic data models:

* Deterministic matching uses first-party data to link device-level data to the appropriate user profiles.
* Probabilistic models use predictive algorithms to link user data to an individual based on a confidence level.

The deterministic method uses PII (email, UID2.0, etc.) to identify the user. Tealium employs the deterministic model with visitor stitching.

Integrations with probabilistic identity programs typically require the use of Tealium’s functions to process returned data along with the confidence score.

## How it works

### Auth0 and CIAM

Auth0 uses the Customer Identity Access Management (CIAM) model:

![](/images/industries/screen-shot-2022-09-26-at-13.41.19.png)

When the user logs in to Auth0, their identity is confirmed by the Auth0 authorization server.

Tealium appears as an Auth0 action, which can be used through drag and drop integration.

The Auth0 data source appears under the new **Identity** category in Tealium.

### UID 2.0

The Trade Desk and other vendors use UID 2.0, which uses PII for deterministic identification. You will need to configure an enrichment and function code to assign a UID 2.0 to a visitor:

![](/images/industries/screen-shot-2022-09-26-at-13.41.53.png)

For more information, see [Using Tealium Functions to Generate a UID2.0 Token](/server-side/functions/event-visitor-functions/uid2/).

UID 2.0 cannot be used in the EU due to privacy restrictions.

### Acxiom and Merkle

As identity and data management solution providers, Acxiom and Merkle perform the following roles:

*   Provide customer data strategies, and additional optional services.
*   Require access to Functions and Tealium iQ Tag Management.
*   Cleanse and store first and third party data for businesses, which can group profiles into households, gather demographics, track NCOA (National Change of Address), and more.
*   Identify visitors through probabalistic methods to &#34;stitch deterministically, enrich probabalistically.&#34;

![](/images/industries/data-partners-&#43;-tealium---acxiom-(3).png)

### netID

After login or registration with a netID on a website, the user’s netID identity parameter is available to Tealium’s real-time data collection, enrichment, and activation capabilities.

When the user logs in on a website with netID authentication, their identity is confirmed by the netID authentication API. The identity parameter `tpid` from the API `READ SERVICE` response can be persisted in the Tealium data layer.

* Use netID within Tealium iQ load rules and tag variable mapping for client-side activation to your advertising technologies, where supported.
* Use netID within Tealium EventStream rules, event feeds, and connector attribute mappings for server-side activation to your advertising technologies, where supported.
* Use netID to enrich Tealium AudienceStream visitor profiles and to map connector attributes for customer profile-based activation and suppression across your advertising technologies, where supported.

## How you can use Identity Providers

You can use an identity provider to immediately share PII such as phone numbers and email addresses with Tealium to enrich customer profiles. This lets you turn anonymous visitors into known visitors or customers.

Because data providers constantly clean and normalize their data, you can use this information to help clean your own data.

As third party cookies are deprecated, anonymous retargeting will no longer be possible. So sharing one or more pieces of PII with AdTech ID partners allows identification and targeting of that individual across publishers and domains.

Many customers have already hired third-party identity providers to improve their visitor profiles. The Tealium Identity Marketplace can help simplify the process of subscribing to, importing, and incorporating this data.

## Identity Tags, Connectors, and Data Sources

The **Identity** category in each of the **Tags**, **Connectors**, and **Data Sources** interfaces lists all of the available identifier resources for that part of the platform.

### Identity and Data Management Solutions

| Partner | Integration Type | Summary                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | Documentation Link                                                                                                                                    |
|:--------|:-----------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------|
| Acxiom  | Tag              | &lt;ul&gt;&lt;li&gt;First-party tag implemented across brand’s owned and paid media.&lt;/li&gt;&lt;li&gt;Provides a unified and consistent identity across owned and paid media.&lt;/li&gt;&lt;li&gt;Allows for linkages to be built by both deterministic and probabilistic signals.&lt;/li&gt;&lt;li&gt;Operates as a fully first-party solution, meaning running off of the client’s own domain and with no data sharing with other entities.&lt;/li&gt;&lt;li&gt;Able to resolve identities even in the absence (or non-acceptance) of cookies&lt;/li&gt;&lt;/ul&gt; | [Acxiom Real Identity rTag Setup Guide](/client-side-tags/acxiom-real-identity-rtag/) |
| Auth0   | Data Source      | An action within the Auth0 integration market that sends user data from Auth0 upon login                                                                                                                                                                                                                                                                                                                                                                                                         | [Tealium Integrations at Auth0](https://marketplace.auth0.com/integrations/tealium)                                                                   |
| Merkle  | Tag              | Merkury uses an organization’s first-party CRM data and valuable interactions such as logins, outbound email campaigns and media reach to create and grow a universe of person-based IDs. Tealium IQ’s data mapping feature lets you control which data points are shared with Merkury.                                                                                                                                                                                                     | [Merkle Merkury Tag Setup Guide](/client-side-tags/merkle-merkury-tag/)                       |
| netID  | Data Layer (UDO object)              | To implement the netID Login Standard, netID partners implement the netID browser-based Javascript API request on their website, and persist netID identity and privacy properties in browser storage, such as first-party-cookies, localStorage, or sessionStorage, where Tealium can pick them up for downstream activation.                                                                                                                                                                                                    | [netID Implementation Guide]()                   |

### Advertising Identity Services

| Partner              | Integration Type | Summary                                                                                                                                                                                                         | Documentation Link                                                                                                                                                                                          |
|:---------------------|:-----------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Criteo               | Tag              | Cookie Matching associates a cookie that identifies a Tealium visitor to the cookie that identifies the user for Criteo.                                                                                        | [Criteo Cookie Matching Service Tag Setup Guide](/client-side-tags/criteo-cookie-matching-service-tag/)                                             |
| Criteo               | Connector        | Audience Match is a flexible customer targeting solution.                                                                                                                                                       | [Criteo Audiences Connector Setup Guide](/server-side-connectors/criteo-audiences-connector/)                                             |
| Epsilon              | Tag              | Returns a list of partner pixel URLs that, when called by the browser, synchronize IDs with exchanges. This allows users can to be identified and messaged after they leave your site.                          | [Epsilon Partner Sync Web Service Tag Setup Guide](/client-side-tags/epsilon-partner-sync-web-service-tag/)                                         |
| The Trade Desk (TDD) | Tag              | The Trade Desk Universal Pixel enables marketers to gain more visibility into user data, and analyze reporting at a more granular level.                                                                        | [Trade Desk Universal Pixel Setup Guide for Tealium iQ](/client-side-tags/the-trade-desk-universal-pixel-tag/)                               |
| The Trade Desk (TDD) | Connector        | The Trade Desk Connector can be used for posting enriched Visitor Profiles and Audiences to TDD for more personalized advertising campaigns.                                                                    | [The Trade Desk Cookie Matching Service Tag Setup Guide](/client-side-tags/the-trade-desk-cookie-matching-service-tag/) (used with UID2.0 Function) |
| The Trade Desk (TDD) | Function         | UID2.0 is an open source identifier that replaces third-party cookies.                                                                                                                                            | [The Trade Desk Connector Setup Guide](/server-side-connectors/the-trade-desk-connector/) (used with UID2.0 Function)                               |

### Identity provider privacy restrictions:

Identity Partners have limitations on where they can operate due to legislation such as the GDPR. Each partner will have different capabilities (for example, Merkle is Global, while the TDD UID2.0 cannot be used within the EU).

* Acxiom - [GDPR](https://www.acxiom.com/data-privacy-ethics/gdpr/)
* Auth0 - [Auth0 General Data Protection Regulation Compliance](https://auth0.com/docs/secure/data-privacy-and-compliance/gdpr)
* Criteo - [GDPR: What You Need to Know | Criteo](https://www.criteo.com/blog/gdpr-need-know-criteo/)
* Epsilon - [GDPR: Steps towards compliance](https://www.epsilon.com/emea/insights/blog/gdpr-steps-towards-compliance)
* Merkle - [Data Protection Statement](https://merkleinc.ch/en/data-protection)
* Tapad - [Privacy Notice - Global](https://www.tapad.com/global-privacy-notice)
* TDD - [UnifiedID2](https://github.com/UnifiedID2/)

## How to implement an identity provider

To implement identity providers:

* For The Trade Desk and UID 2.0, see [Using Tealium Functions to Generate a UID2.0 Token](/server-side/functions/event-visitor-functions/uid2/).
* For Acxiom, see [Using Tealium Functions for Acxiom Identity Resolution](../acxiom-identity-resolution/).
* For netID, see [netID Implementation Guide]().

We will add more function examples soon.