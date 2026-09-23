---
title: Developer Portal API reference
description: Browse API documentation, generate bearer tokens, and download Postman collections in the Tealium Developer Portal.
url: https://docs.tealium.com/administration/early-access/developer-portal/dev-portal-api-reference/
---
## Browse the API catalog

Go to **API Reference** in the Developer Portal and click an API card to open its documentation. 

Each API card shows a lifecycle status chip. When a version is approaching or past its End of Support date, the chip shows a countdown (for example, `EOL in 45d`) rather than a date. Full lifecycle dates appear in the banner on the API detail page. For more information, see [API lifecycle](https://docs.tealium.com/dev-portal-api-lifecycle/).

## Use interactive documentation

On an API reference page, you can:

* Browse endpoints in the sidebar.
* View request and response schemas and examples.
* Test the endpoint and send live requests directly from the browser. You need to generate a bearer token to use this feature. For more information, see [Generate a bearer token](#generate-a-bearer-token).
* View code snippets in multiple languages.
* Use MCP-enabled APIs directly from an MCP client.

## Use MCP-enabled APIs

APIs that support the Model Context Protocol (MCP) include an **MCP** tab on their reference page and an `MCP (N tools)` chip in the header. The MCP tab has three sections:

* **MCP Connection:** Shows the single endpoint for all MCP communication: `POST {gateway-url}{mcp-path}`. All MCP operations (initialize, tool listing, and tool calls) go through this one endpoint via JSON-RPC over HTTP POST. Copy the endpoint URL from the tab. Authentication uses the same OAuth 2.0 client credentials bearer token as the REST APIs. MCP does not have a separate authentication mechanism. Transport is Streamable HTTP.
* **Quick Start:** Copyable connection examples in TypeScript, Python, Java, and cURL.
* **Available Tools:** The tools exposed through the MCP endpoint, discoverable via `tools/list` and callable by name via `tools/call`.

## Use with Postman

### Download a Postman collection

1. Go to the API reference for the API.
1. Click the **⋮** menu in the bottom-right corner to open the speed dial.
1. Click the **Postman** icon. A `.json` collection file downloads automatically.

### Import into Postman

1. Open Postman and click **Import**.
1. Select the downloaded `.json` file.

The collection includes all endpoints, parameters, and request bodies, organized into folders by resource.

### Authenticate the collection

The collection uses an `{{access_token}}` variable for bearer token authentication. To configure it:

1. [Generate a bearer token](#generate-a-bearer-token).
1. In Postman, open **Collection Variables**.
1. Set the `access_token` value to your generated token.

All requests in the collection automatically include `Authorization: Bearer {{access_token}}`.

## Generate a bearer token from the API reference

Tokens expire after 2 hours.

### Signed in users (recommended)

Use this method if you are signed in and have a registered application with an active subscription to the API.

1. Expand an action and select an endpoint.
1. Click the **⋮** menu in the bottom-right corner, then click the **Bearer Token** key icon.
1. Select your application from the dropdown and click **Generate Token**.
1. Click **Copy Token** and close the drawer.
1. Paste the token into the **Token** field in the action screen, fill in any required parameters, and click **Send API Request**.

### With client credentials

Use this method for CI/CD pipelines, service accounts, or any context where you have a `client_id` and `client_secret` but are not signing in through the Developer Portal.

1. Open any API documentation page.
1. Click the **⋮** menu in the bottom-right corner, then click the **Bearer Token** key icon.
1. Select **Manual credentials** from the application dropdown.
1. Enter your `client_id` and `client_secret`.
1. Optionally, enter scopes.
1. Click **Generate Token**.
1. Copy the returned token.

You can request only scopes your subscription grants. If the Developer Portal rejects a scope, verify that your subscription includes the required account and profile access. For details on scope format and components, see [Scopes](https://docs.tealium.com/dev-portal-scopes/).

### Token details

| Property | Value |
|---|---|
| Format | JSON Web Token (JWT) |
| Lifetime | 7200 seconds (2 hours). |
| Grant type | `client_credentials` |
| Refresh | Not supported. Generate a new token when the current one expires. |

## Troubleshoot common errors

| Problem | Solution |
|---|---|
| Token generation fails | Verify that your application has an active subscription to the API you want to use. |
| `401 Unauthorized` | Your token has expired. Generate a new one. |
| `403 Forbidden` | Your token's scopes don't include the required account, profile, or resource. Check your subscription access. |
| Scope rejected during generation | Your application has not been granted that scope. Request access from the account owner. |
| No applications in the dropdown | Create an application and subscribe to at least one API first. |
