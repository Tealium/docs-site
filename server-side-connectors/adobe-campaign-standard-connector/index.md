---
title: Adobe Campaign Standard Connector Setup Guide
description: This article describes how to set up the Adobe Campaign Standard connector in your Customer Data Hub account.
url: https://docs.tealium.com/server-side-connectors/adobe-campaign-standard-connector/
---
## Connector actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Send Transactional Event| ✓| ✗|
|Trigger Signal Activity| ✓| ✗|
|Create or Update Profile| ✓| ✗|

## Configure settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors](https://docs.tealium.com/about-connectors/) article.

After adding the connector, configure the following settings:

* **Technical Account ID**
  * The Technical Account ID can be found in the [Adobe I/O Console](https://console.adobe.io/).
  * For more information see [Authenticating and accessing Adobe Experience Platform APIs](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/authenticate_to_acp_tutorial/authenticate_to_acp_tutorial.md#login-to-adobe-io-console).

* **Organization ID**
  * The Organization ID can be found in the [Adobe I/O Console](https://console.adobe.io/).

* **Tenant ID**
  * The Tenant ID can be found in your Adobe Marketing Cloud URL.
  * Example: <https://yourtenantid.experiencecloud.adobe.com/campaign.html>

* **API Key**
  * The API Key (Client ID) can be found in the [Adobe I/O Console](https://console.adobe.io/).

* **Secret Key**
  * The Client Secret can be found in the [Adobe I/O Console](https://console.adobe.io/).

* **Private Key**
  * The Private Key is generated as part of creating an integration in the Adobe Console.
  * For more information see: [Authenticating and accessing Adobe Experience Platform APIs](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/authenticate_to_acp_tutorial/authenticate_to_acp_tutorial.md#create-integration) .

## Action settings - parameters and options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Send Transactional Event

To send a transactional event, you must first create and configure an event. For more information, see [Configuring a transactional event](https://experienceleague.adobe.com/docs/campaign-standard/using/communication-channels/transactional-messaging/event-configuration/configuring-transactional-event.html) and [Managing transactional messages](https://experienceleague.adobe.com/docs/campaign-standard/using/working-with-apis/managing-transactional-messages.html).

The API endpoint used to send a transactional event varies depending on your configuration.

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Email|  <ul><li>(Required) The email address of the recipient.</li></ul> |
|Event ID|  <ul><li>(Required) The type of event you want to send.</li><li>This ID is generated when creating the event definition.</li><li>For additional information, see the [Adobe Campaign Documentation](https://helpx.adobe.com/campaign/standard/administration/using/configuring-transactional-messaging.html).</li></ul> |
|Expiration Date|  <ul><li>(Optional) The sending of the transactional event will be cancelled after this date.</li></ul> |
|Scheduled Send Date|  <ul><li>(Optional) The transactional event will be processed and the transactional message will be sent at this date.</li></ul> |
|Template Name|  <ul><li>If using a template to pass data, input with "Transactional Message Content Template" and enter name of main template.</li><li>Do not include double curly braces in name, for example, use `SomeTemplateName` not `{{SomeTemplateName}}`.</li></ul> |
|Template Variables|  <ul><li>Provide template variables as data input for "Transactional Message Content Template".</li><li>For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Name nested template variables with the dot notation.</li><li>Example: `items.name`</li><li>Nested template variables are typically built from data layer list attributes.</li></ul> |
|Transactional Message Content Template|  <ul><li>Template describing enriched transactional message content.</li><li>Templates are injected by name with double curly braces into supported fields.</li><li>For example, `{{SomeTemplateName}}`.</li><li>For additional information about using enriched message content, see Adobe's [Campaign Documentation.](https://helpx.adobe.com/campaign/standard/administration/using/configuring-transactional-messaging.html)</li></ul> |
| Transactional API Endpoint |  <ul><li>(Optional) Specify to override default value of " `mc`" followed by Tenant ID from connector configuration.</li><li>This is typically applicable when working in your stage instance.</li><li>Example: If stage Tenant ID is "`geometrixx-mkt-stage3`", then override Transactional API Endpoint to "`geometrixx`".</li></ul> |

### Action - Trigger Signal Activity

For more information, see [Triggering a signal activity](https://experienceleague.adobe.com/docs/campaign-standard/using/working-with-apis/managing-workflows/triggering-a-signal-activity.html) in the Adobe documentation.

To trigger signal activity, the REST workflow/execution API is used.

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Workflow ID|  <ul><li>The ID of the workflow configured in your Adobe console.</li></ul> |
|Source|  <ul><li>Used to indicate the triggering request source.</li></ul> |
|Parameter Map|  <ul><li>It is possible to call a workflow with parameters.</li><li>Map a parameter's value to it's name.</li><li>String, Number, Boolean, and Date/Time types are supported.</li></ul> |

### Action - Create or Update Profile

To retrieve, create, or update a profile, requests are sent to the Adobe ProfileAndServices API

For more information, see [Creating Profiles with APIs,](https://experienceleague.adobe.com/docs/campaign-standard/using/working-with-apis/managing-profiles/creating-profiles-api.html) [Updating Profiles with APIs](https://experienceleague.adobe.com/docs/campaign-standard/using/working-with-apis/managing-profiles/updating-profiles.html), and [Retrieving profile with APIs](https://experienceleague.adobe.com/docs/campaign-standard/using/working-with-apis/managing-profiles/retrieving-profiles.html?lang=en).

##### Parameters

|**Parameter**| **Description**|
|---| ---|
|Update Strategy|  <ul><li>(Required) Select applicable update strategy.  <ul><li>**Create Only** — Look up an existing profile and if not found, create a new profile.</li><li>**Update Only** — Look up an existing profile and update it.</li><li>**Create or Update** — Look up an existing profile and if found, update it, otherwise create a new profile.</li></ul> </li></ul> |
|Filter|  <ul><li>Required when Update Strategy is **Create Or Update** or **Update Only**.</li><li>It is strongly recommended to select filters that return unique results.</li><li>For additional information, see: [Composite Identification Key](https://experienceleague.adobe.com/docs/campaign-standard/using/developing/adding-or-extending-a-resource/uc-calling-resource-id-key.html?lang=en).</li><li>If the search result returns multiple profiles, only the first one is updated.</li></ul> |
|Is Custom Filter|  <ul><li>See [about custom filters.](https://experienceleague.adobe.com/docs/campaign-standard/using/working-with-apis/global-concepts/additional-operations/filtering.html?lang=en#custom-filters)</li></ul> |
|Template Variables|  <ul><li>Provide template variables as data input.</li><li>For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Name nested template variables with the dot notation.</li><li>Example: `items.name`</li><li>Nested template variables are typically built from data layer list attributes.</li></ul> |
|Templates|  <ul><li>Provide templates to be referenced in Body Data.</li><li>For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).</li><li>Templates are injected by name with double curly braces into supported fields.</li><li>For example, `{{SomeTemplateName}}`.</li></ul> |