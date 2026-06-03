---
title: Google Vertex AI Search for Commerce Connector Setup Guide
description: Set up this connector to send Tealium event data to Google Vertex AI Search for personalized and intuitive shopping experiences.
url: https://docs.tealium.com/server-side-connectors/google-vertex-commerce-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Google API
* API Version: v2
* API Endpoint: `https://retail.googleapis.com`
* Documentation: [Vertex AI Search for commerce](https://cloud.google.com/solutions/vertex-ai-search-commerce)


## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **Google Cloud Platform Project ID**: (Required) Your Google Cloud project ID. The project must have Vertex Search AI enabled.
* **Private key JSON file**: (Required) Paste the JSON key generated for your service account. The service account requires access to `retail.userEvents.import`. Google recommends using the Retail Editor role.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Write User Event | ✗ | ✓ |

Enter a name for the action and select the action type.

The following section describes how to set up parameters and options for each action.

### Write User Event

#### Parameters

| Parameter | Description |
| --- | --- |
| Catalog | Select the Vertex AI Search for Commerce catalog where user events are recorded. |
| Event Type | Choose the type of user event to send to Vertex AI Search for Commerce. This determines how the event is interpreted and which fields are required in the payload.&lt;ul&gt;&lt;li&gt;`add-to-cart`&lt;/li&gt;&lt;li&gt;`remove-from-cart`&lt;/li&gt;&lt;li&gt;`category-page-view`&lt;/li&gt;&lt;li&gt;`detail-page-view`&lt;/li&gt;&lt;li&gt;`home-page-view`&lt;/li&gt;&lt;li&gt;`purchase-complete`&lt;/li&gt;&lt;li&gt;`search`&lt;/li&gt;&lt;li&gt;`shopping-cart-page-view`&lt;/li&gt;&lt;/ul&gt;|

#### Event Data

| Parameter | Description |
| --- | --- |
| Attributes | Map extra user event features to include in the recommendation model |
| Template Variables    | &lt;ul&gt;&lt;li&gt;(Optional) Provide template variables as data input for templates. For more information, see .&lt;/li&gt;&lt;li&gt;Name nested template variables with the dot notation. For example: `items.name`&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes.&lt;/li&gt;&lt;/ul&gt;   |
| Templates             | &lt;ul&gt;&lt;li&gt;(Optional) Provide templates to be referenced in either URL, URL Parameter, Header, or Body Data. For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.&lt;/li&gt;&lt;li&gt;When using OAuth, the template variable `{{webhook_access_token}}` refers to the token returned by the authentication request.&lt;/li&gt;&lt;/ul&gt; |