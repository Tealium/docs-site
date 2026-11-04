---
title: Google AI Commerce Search Connector Setup Guide
description: AI Commerce Search, formerly known as Vertex AI Search for Commerce, provides Google-quality search, browse, and recommendations for ecommerce experiences.
url: https://docs.tealium.com/server-side-connectors/google-ai-commerce-search-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Google API
* API Version: v2
* API Endpoint: `https://retail.googleapis.com`
* Documentation: [AI Commerce Search](https://docs.cloud.google.com/gemini-enterprise-cx/ai-commerce-search/reference/rest)


## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **Google Cloud Platform Project ID**: (Required) Your Google Cloud project ID with AI Commerce Search enabled.
* **Private key JSON file**: (Required) Paste the JSON key generated for your service account. The service account requires the `retail.userEvents.create` and `retail.catalogs.list` permissions. Google recommends using the Retail Editor role, which includes both permissions.

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
| Catalog | Select the AI Commerce Search catalog where user events will be recorded. |
| Event Type | Choose the type of user event to send to AI Commerce Search. This determines how the event is interpreted and which fields are required in the payload.<ul><li>`add-to-cart`</li><li>`remove-from-cart`</li><li>`category-page-view`</li><li>`detail-page-view`</li><li>`home-page-view`</li><li>`purchase-complete`</li><li>`search`</li><li>`shopping-cart-page-view`</li></ul>|

#### Event Data

| Parameter | Description |
| --- | --- |
| Attributes | Map extra user event features to include in the recommendation model |
| Template Variables    | <ul><li>(Optional) Provide template variables as data input for templates. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Name nested template variables with the dot notation. For example: `items.name`</li><li>Nested template variables are typically built from data layer list attributes.</li></ul>   |
| Templates             | <ul><li>(Optional) Provide templates to be referenced in either URL, URL Parameter, Header, or Body Data. For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).</li><li>Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.</li><li>When using OAuth, the template variable `{{webhook_access_token}}` refers to the token returned by the authentication request.</li></ul> |