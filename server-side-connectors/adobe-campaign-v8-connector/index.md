---
title: Adobe Campaign v8 Connector Setup Guide
description: This article describes how to set up the Adobe Campaign v8 connector.
url: https://docs.tealium.com/server-side-connectors/adobe-campaign-v8-connector/
---
## Configuration

To configure the Adobe Campaign v8 connector in Tealium, you first need to generate the OAuth server-to-server credentials for the connection in Adobe. For more information, see [Adobe: Add API to project using OAuth Server-to-Server credential](https://developer.adobe.com/developer-console/docs/guides/services/services-add-api-oauth-s2s/).

Complete the following steps to generate Adobe credentials and configure the connector:

1. Create a new Adobe Developer Console project or use an existing project. For more information, see [Adobe: Projects Overview](https://developer.adobe.com/developer-console/docs/guides/projects/).
1. Add the Adobe services to the project that you want associated with the project credentials. For more information, see [Adobe: Services Overview](https://developer.adobe.com/developer-console/docs/guides/services/). This connector requires the following services:
    * Adobe Campaign API
    * I/O Management API
1. Select the Adobe Campaign API product profiles you want to manage with these credentials.
1. After you add the services to the project, you can access the project credentials. For more information, see [Adobe: Credentials](https://developer.adobe.com/developer-console/docs/guides/credentials/).  
Go to your project overview and select **OAuth Server-to-Server** in the **Credentials** section. The following credentials are required for this connector:
    * Client ID (API Key)
    * Client secret
    * Technical Account Email
1. Note your credentials and return to Tealium to complete the connector configuration.
1. In Tealium, go to the Connector Marketplace and add a new Adobe Campaign v8 connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).
1. After adding the connector, configure the following settings:
    * **Client ID**  
        * (Required) The Client ID (API Key).
    * **Client Secret**  
        * (Required) The Client Secret.
    * **Server Host**  
        * (Required) Provide server host.  
        For example, the host is `example.campaign.adobe.com` for the API URL `https://example.campaign.adobe.com/nl/jsp/soaprouter.jsp`.
1. In Adobe, go to the **Developers** section in the **Adobe Admin** console. For more information, see [Adobe: Manage developers](https://helpx.adobe.com/enterprise/using/manage-developers.html#add-developers).
1. Add a new developer with the Technical Account Email from the Adobe project credentials.
1. Grant access to Adobe Campaign v8 for the developer you just added. 
    1. From the **Adobe Admin** console, add a user. 
    1. Add the email of the developer you just added.
    1. Add the Adobe Campaign Managed Cloud service and include your selected product profiles while creating the credentials.
    For more information, see [Adobe: Manage user permissions](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/admin/permissions/manage-permissions).
1. Update the newly created technical operator in the Adobe Campaign client console. For more information, see [Adobe: Update the technical account operator within the Campaign client console](https://experienceleague.adobe.com/en/docs/campaign/technotes-ac/tn-new/ims-migration#ims-migration-step-9). 

## Migration

Migrate existing Adobe Campaign Classic connectors to Adobe Campaign V8 connectors using the Adobe Campaign Classic to v8 Migrator tool.

Complete the following steps to migrate your Adobe Analytics tag using Tealium Tools:

1. Add the Adobe Campaign Classic to v8 Migrator to your Tealium Tools using the JSON definition at the following URL: `https://solutions.tealium.net/hosted/tealiumTools/acc_to_v8/acc_to_v8.json`. For more information about adding custom tools, see [Manage Custom Tools](https://docs.tealium.com/tealium-tools-browser-extension/#add-a-custom-tool).
1. Go to either **Event Connectors** or **Audience Connectors** and launch the Adobe Campaign Classic to v8 Migrator tool from Tealium Tools.
1. Select how actions should be migrated. To disable your existing Adobe Campaign Classic actions as part of the migration, select **Disable existing action**. To migrate only active actions, select **Migrate only active actions.**
1. Select the scope for the migration from the drop-down list:
    * All Adobe Campaign Classic actions
    * Specific Adobe Campaign Classic action
    * Specific Adobe Campaign Classic connector
1. Enter the Adobe Campaign Client ID and Client secret for the project. The server host is automatically extracted from the existing Adobe Campaign Classic configuration.
1. Click **Start**.  
The Migrator tool automatically migrates existing Adobe Campaign Classic connectors to new Adobe Campaign v8 connectors. The name of the connector will be the same, with the suffix  `V8 (Migrated)`.
1. Verify the new connector configurations and actions.
1. Save and publish your profile.

## IP addresses to allow

You will need to add the [Tealium IP addresses](https://docs.tealium.com/ip-allow-list/) to your [Adobe Campaign allow list](https://experience.adobe.com/#/controlpanel/instances) (**Adobe Experience Platform** > **Control Panel** > **Instances**).

For more information, see [Adobe Campaign: Allowlist IP addresses](https://experienceleague.adobe.com/en/docs/control-panel-learn/tutorials/instance-settings/allowlist-ip-adresses).

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Custom SOAP Request (Batched) | ✓ | ✓ |
| Send Custom SOAP Request | ✓ | ✓ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Send Custom SOAP Request (Batched)

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. Requests are queued until one of the following thresholds is met:

* Max number of requests: 200
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| SOAP Action Header Value | `SOAP` Action, for example: `nms:rtEvent#PushEvent`.<br>This value will be assigned to `SOAPAction` `HTTP` header. |
| SOAP Request Body Prefix | Provide a template of the opening portion of `SOAP` Request, for example: <br>`<?xml version="`1`.0" encoding="utf-`8`"?><soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:urn="urn:nms:rtEvent"><soapenv:Header/><soapenv:Body><urn:PushEvent><urn:domEvent>`.<br>You can use template variables in the `SOAP` Request Body Prefix. For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/). |
| SOAP Request Body Data | Provide a template for the `SOAP` Request batch item to be sent.<br>You can use template variables in the `SOAP` Request Body Data. |
| SOAP Request Body Suffix | Provide a template for the closing portion of `SOAP` Request, for example: <br>`</urn:domEvent></urn:PushEvent></soapenv:Body></soapenv:Envelope>`.<br>You can use template variables in the `SOAP` Request Body Suffix. |
| SOAP Request Body Joiner | A character or string to use between body items when batching. If not specified, an empty string is used. |
| SOAP Request Template Variables | Provide template variables as data input for `SOAP Request Body Prefix`, `SOAP Request Body Data` and `SOAP Request Body Suffix`. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).<br>Name nested template variables with the dot notation. For example, `items.name`. Nested template variables are typically built from data layer list attributes. |
| SOAP Response Error Identifier | If the response contains an error string, it is marked as a failure. By default, an `HTTP` response status outside `200`-`299` range is also marked as a failure. |

### Send Custom SOAP Request

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| SOAP Action Header Value | `SOAP` Action, for example: `nms:rtEvent#PushEvent`.<br>This value will be assigned to `SOAPAction` `HTTP` header. |
| SOAP Request Body Template | Provide `SOAP` Request Body Template to be sent. For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/). Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`. |
| SOAP Request Body Template Variables | Provide template variables as data input for `SOAP Request Body Template`. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/). Name nested template variables with the dot notation, for example `items.name`. Nested template variables are typically built from data layer list attributes. |
| SOAP Response Error Identifier | If the response contains an error string, it is marked as a failure. By default, an `HTTP` response status outside `200`-`299` range is also marked as a failure. |