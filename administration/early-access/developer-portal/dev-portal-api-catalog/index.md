---
title: Developer Portal API catalog
description: Browse, search, and explore available Tealium APIs in the Developer Portal.
url: https://docs.tealium.com/administration/early-access/developer-portal/dev-portal-api-catalog/
---
The API Catalog is the central discovery hub in the [Tealium Developer Portal](https://app.tealiumapis.com/). From the catalog, you can browse all published APIs, read reference documentation, review available plans and security types, and begin the subscription workflow.

## Browse the catalog

The catalog displays all published APIs as cards. Each card shows:

* API name and version
* Short description of the API purpose
* Support end date (for example, "Supported until Jul 2028")
* An MCP badge, if the API supports Model Context Protocol

## Search and filter

Use the search bar to find APIs by name or description. You can also filter the catalog by:

* **MCP**: Show only APIs that support Model Context Protocol.
* **Version**: When multiple versions of an API exist, switch between them using the version picker.
* **Category**: Browse APIs organized into logical categories.

## API lifecycle

API versioning is based on lifecycle status. For details on lifecycle stages and how versioning works, see [API versioning](https://docs.tealium.com/dev-portal-api-versioning/) and [API lifecycle](https://docs.tealium.com/dev-portal-api-lifecycle/).

## API details

Click any API card to open its detail page. The detail page is organized into tabs:

* **Description:** API description and overview.
* **Overview:** Version, status, and owner information.
* **Plans:** All available subscription plans with their security type and validation mode (Auto or Manual). Tealium APIs use OAuth 2.0 client credentials. Other security types (JWT, API Key, Keyless) may appear on some plans. For information on subscribing to an API, see [Applications](https://docs.tealium.com/dev-portal-applications/).
* **REST Endpoints:** All available endpoints grouped by resource. Expand a group to view individual operations.
* **MCP:** Available MCP tools with purpose, required parameters, and expected behavior documented for each tool.
* **Documentation:** Links to the API documentation in the Tealium Developer Portal. From the reference documentation you can:
  * View all endpoints with their HTTP methods, paths, and descriptions.
  * Inspect request and response schemas with example payloads.
  * Identify required and optional parameters.
  * Review authentication requirements for each endpoint.
  * Generate a bearer token for testing.
  
  For more information, see [API Reference](https://docs.tealium.com/dev-portal-api-reference/).

