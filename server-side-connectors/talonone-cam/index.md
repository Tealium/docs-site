---
title: Talon.One Campaign Audience Manager Connector Setup Guide
description: This article describes how to set up the Talon.One Campaign Audience Manager connector.
url: https://docs.tealium.com/server-side-connectors/talonone-cam/
---
## API Information

This connector uses the following vendor API:

* API Name: Third-party API
* API Version: v1
* API Endpoint: `https://integration.talon.one/cdp/`
* Documentation: [Talon.One Third-party API: Customer Data Platforms](https://docs.talon.one/third-party-api#tag/Customer-data-platforms)

## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Update Customer Profile | ✓ | ✗ |

## Configure Settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

### API Key

(Required) The API Key generated within the Campaign Manager software.

To generate an API key in the Campaign Manager:

1. Log in to the Campaign Manager and open the **Application* of your choice, or create one.
1. Navigate to **Settings > Developer settings**.
1. Click **Create API Key**.
1. Enter a title for the key.
1. Under **Do you want to use this API Key with a 3rd party service?**, select **Yes**.
1. Select the platform to integrate with.
1. Set an expiration date for the key.
1. Click **Create API Key**.

### Management API Key

(Required) The Management API key gives you access to the endpoints selected by the admin who created the key.

To generate a Management API Key:

1. Log in to the Campaign Manager.
1. Navigate to **Account > Management API keys**.
1. Click **Create Key**.
1. Enter a name for the key.
1. Set an expiration date for the key.
1. Select the **`/v1/audiences` (GET)** and **`/v1/attributes` (POST, GET)** endpoints so the key will have access to them.
1. Click **Create Key**.

### Base URL

(Required) The Base URL of your Talon.One deployment. Do not include HTTP(S) protocol in the URL. For example: `mycompany.europe-west1.talon.one`.

## Action Settings - Parameters and Options

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Action - Update Customer Profile

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Customer Profile ID | The integration ID of the customer profile. This is the unique identifier that is being applied to the visitor. It should be a visitor ID associated within Tealium. We recommend that you do not use an email address. If this field is not mapped, it will be auto-mapped to the Tealium Visitor ID. |
| Run Rule Engine | Indicates whether to run the Rule Engine.<ul><li>If `true`, the rules are run and their effects applied. Audience changes are applied.</li><li>If `false`, the rules are not executed, the response time improves, and audience changes are not applied.</li></ul> |
| Customer Profile Attributes | Set attributes of your choice to the values of your choice.<ul><li>New attributes are created automatically.</li><li>Custom and enabled build-in attributes are displayed. All other built-in attributes must be enabled first in the attribute library.</li></ul> |
| Audiences Add | The IDs of the audiences for the customer to join. |
| Audiences Remove | The audience IDs of the audiences for the customer to leave. |
| Template Variables | Provide template variables as data input for **Templates**.<ul><li>Use the dot notation for the names of nested template variables (for example, `items.name`).</li><li>Nested template variables are typically built from data layer list attributes.</li><li>For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li></ul> |
| Templates | Provide templates to be referenced in **Customer Parameters** and **Customer Profile Attributes** sections. Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`. For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/). |