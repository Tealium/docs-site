---
title: About Moments API
description: Moments API is a high-performance, configurable endpoint that retrieves a targeted slice of live visitor context for real-time personalization, AI systems, and cross-channel experiences.
url: https://docs.tealium.com/server-side/moments-api/about/
---
Contact your account manager to enable Moments API for your account.

Moments API is a composable AudienceStream API that retrieves a fast, targeted slice of live visitor context. Instead of returning a full visitor profile, it returns only the audiences, badges, and attributes your app, service workflow, or AI system needs for a specific decision or experience. Integrate Moments API into your Tealium client-side applications, wherever `utag.js` is installed, in Tealium for Mobile, or into any agentic AI framework such as LangChain via the [managed MCP server](#mcp-server).

## How it works

Moments API uses configurations called _engines_ that let you customize API responses to retrieve only the data you need for current visitors. For example, instead of retrieving an entire visitor profile, Moments API retrieves only the audience, badge, and attribute data you select in the engine configuration.

After you configure the engine, Moments API creates a unique endpoint that you integrate into your workflow.

### Use cases

Moments API can be used any time you need real-time visitor data for personalized experiences, including:

* Personalization (first-page and beyond), including anonymous visitor lookup before an active session is established.
* Next best action in combination with data enrichment logic.
* Customer service and cross-channel experiences using visitor ID lookups across devices and channels.
* AI and agent-based systems via the managed MCP server.
* Enterprise-grade API management and compliance.

For example, when a visitor returns to your website or app, a request is made to the unique Moments API endpoint for visitor data. Moments API is optimized to provide only the data you need, so the API sends a real-time, streamlined response back to your app. With that critical data, you can activate additional logic to trigger personalized experiences for your visitor.

![](/images/early-access/moments-api-workflow.png)

### Engines

Moments API engines let you configure the visitor data to store in each unique endpoint and the domains allowed to access those endpoints.

When you configure an engine, you select only the audiences, badges, and attributes necessary for your use case. The Moments API engine shows you the JSON response as you build it, which lets you verify the accuracy and scope of your requests. 

Data for visitors becomes available after you enable the engine and visitors log active sessions and generate events in the system. For example, when a visitor visits your site, Moments API determines if the new visitor events impact the audiences, badges, and attributes defined in your engine configuration. Data is written to a unique data store for each engine only when visitor data needs to be updated.

Engines update their data stores in real-time, so the API endpoint data remains up-to-date as visitors interact with your brand.

By default, you can enable up to 10 engines per profile so that you can create a customized engine for each specific business case. If you need to enable additional engines, contact Tealium Support.

### Reads and writes

A _read_ is a request to retrieve visitor data from an engine. A read is counted towards your quota regardless of whether data is found. If Tealium rejects a read due to rate limiting, you are not charged.

A _write_ is an update to visitor profile data stored by Moments API for an engine. For stitched visitors, Moments API executes a separate write for each associated visitor ID, such as anonymous IDs and configured visitor ID values. The total number of writes depends on the number of engines and the number of associated visitor IDs linked to the stitched visitor.

For example, a visitor visits a site from two devices, which results in two anonymous IDs:

* Desktop anonymous ID `tealium_visitor_id` = `abc123`.
* Mobile anonymous ID `tealium_visitor_id` = `bcd234`.

These result in two visitor profiles, A and B:

![](/images/server-side/visitor-stitching-example-first-visit.png)
![](/images/server-side/visitor-stitching-example-second-visit.png)  

The visitor&#39;s email address is `user@example.com`, which populates the configured visitor ID attribute and is used to stitch the profiles associated with both devices into a new master profile (C).

![](/images/server-side/visitor-stitching-profile-c-created.png)

If the account has a single engine and the visitor has an attribute that qualifies it for writing, the system writes that data one time for each visitor profile:

* If visitor ID lookups are enabled, 3 writes (3 visitor profiles × 1 engine).
* If visitor ID lookups are disabled, 2 writes (2 visitor profiles × 1 engine).

![](/images/server-side/moments-api/moments-api-visitor-stitching-1.png)

If the account has five identically configured engines and the visitor has an attribute that qualifies it for writing, the system writes that data five times for each visitor profile:

* If visitor ID lookups are enabled, 15 writes (3 visitor profiles × 5 engines).
* If visitor ID lookups are disabled, 10 writes (2 visitor profiles × 5 engines).

![](/images/server-side/moments-api/moments-api-visitor-stitching-2.png)

For more information about visitor stitching, see .

### Endpoints

Moments API creates a unique endpoint for each engine. Visitor data is returned as a JSON object. 

Tealium has benchmarked the average Moments API endpoint performance at 60 ms for payload sizes of 1 kB and smaller. 

To retrieve visitor data, configure a [Tealium iQ Advanced JavaScript Code Extension]() to make a request to the [Moments API endpoint](). 

Data is not available for visitors that have not had an active session since turning on the engine.

### MCP server

The Moments API managed MCP server provides AI systems and LLMs with secure, real-time access to visitor profile data using the Model Context Protocol (MCP). Because Tealium hosts and manages the server, there is no infrastructure to deploy or maintain. AI agents connect to the server to retrieve targeted customer context for personalization, analytics, and automation. 

The server supports both anonymous ID and visitor ID attribute lookups, matching the same retrieval methods available through the standard endpoint.

For more information, see .

### Visitor identifiers

Moments API endpoints support GET requests that use both the Tealium anonymous ID and a visitor ID attribute to retrieve visitor data. 

* **Anonymous ID**: A unique and anonymous value assigned to a visitor on each visit to a site or each use of an app. The anonymous ID tracks a visitor over multiple visits from the same browser or app, but not across different browsers or devices.
* **Visitor ID attribute**: A special attribute type in AudienceStream that gets its value from a user identifier and is used in visitor stitching. 

For more information, see [Anonymous IDs, user identifiers, and visitor ID attributes]().

### Governance

Moments API includes built-in controls for secure, production-grade deployment:

* **No PII access**: Attributes designate as [restricted data]() cannot be included in API responses.
* **Domain allow lists**: Restrict which domains can query your engine endpoints.
* **Permissions**: Control who can create, edit, or delete engines using role-based access.
* **Purge data**: Delete outdated engine data at any time without affecting visitor records.

For details, see [Domain allowlist](#domain-allowlist), [Permissions](#permissions), and [Purge data](#purge-data).

## Limits

The Moments API has the following default limits:

* Read rate limit per profile across all engines: 200 requests/second/profile
* Maximum enabled engines per profile: 10
* Maximum size of Moments API data that can be stored per visitor per engine: 1 kB If your visitor attribute data exceeds the data store limit, it is not stored for that visitor.
* Data available in Moments API endpoint: 30-day retention if no new events are processed

If you need higher limits for your use case, contact your Tealium account manager.

## Purge data

Moments API lets you delete outdated data from an endpoint using the purge data feature.

The following examples describe situations in which you may want to purge data from an endpoint:

* Renaming or deleting an audience, badge, or attribute included in your engine configuration.
* Changing the personally identifiable information (PII) status of an attribute. If you change the PII status of an attribute, sensitive information may still be stored in the API endpoint.
* Removing an audience, badge, or attribute from an engine configuration.

If an audience, badge, or attribute used in an engine is deleted from AudienceStream or the engine configuration, that item is no longer populated in the endpoint moving forward. Engine data that contains the removed attributes are unchanged. In general, if removing a dependency causes breaking changes in your endpoint integration, you may want to purge the engine data. 

Purging data only deletes Moments API engine data. Visitor records in AudienceStream are not affected.

For more information about purging engine data, see [Manage Moments API engines &gt; Purge data](). 

## Domain allowlist

We recommend creating a domain allowlist only after you test the API endpoint.

An allowlist prevents untrusted domains from making requests to your Moments API endpoints. Add specific domains to the allowlist when you configure the engine. 

Moments API allows or restricts calls to the endpoint by comparing the domain in the `Referer` HTTP request header to the allowlist defined in the Moments API engine:

* Domains match: The request is processed.
* Domains do not match: The request is not processed and returns a 403 error.

If you do not list any domains, all domains are allowed.

### Subdomains

When you add a domain to the allow list, all of its subdomains are automatically included. For example, if you allow `example.com`, any subdomain that matches `*.example.com` is included.

## Permissions

Moments API functionality is managed through the following permission levels:

* **Create, edit, delete engines and purge engine data** 
  * Editor or publisher legacy permissions 
  * Write or delete access in platform permissions  
* **View engine list**
  * Viewer legacy permissions or read access in platform permissions

## Moments API compared with Data Layer Enrichment API

Both Moments API and [Data Layer Enrichment API]() let you retrieve live visitor data, but the use cases, configurations, and implementations are different. Refer to the following comparison to learn more about the differences between these two visitor profile data retrieval methods.

| | **Moments API**| **Data Layer Enrichment API**|
|---|---|---|
|**Use case**| Real-time access to current visitor data for first-page personalization and beyond.| Live visitor data available in real-time to near-real-time after an initial processed event.|
|**Rates**| 200 requests/second | - |
|**Active visitor session required** | No | Yes|
|**Available data**| Audience, badge, or [supported attribute data types]().&lt;br&gt; Names and IDs of audiences and badges available. | Attributes other than visitor IDs, funnels, and timelines, listed by attribute IDs. For badges and audiences, names are available.&lt;br&gt;For badge names, combine with [Profile Definition API]().|
|**Lookup ID**| Tealium anonymous ID or visitor ID attribute value | Tealium anonymous ID|
|**Authenticated endpoint**| No| No|
|**Access to PII** | No | No |
|**Custom response object** | Yes | No|
|**Implementation**|API| API or Tealium Collect tag|

## Get started

A workflow using Moments API includes the following steps:

1. Consider what audiences, badges, and attributes you need to create personalized experiences.
1. Create a Moments API engine to populate your customized endpoint with the visitor data you need.
1. Integrate the endpoint into your Tealium client-side applications, wherever utag.js is installed, or in Tealium for Mobile. 
1. Gather and activate your data.

