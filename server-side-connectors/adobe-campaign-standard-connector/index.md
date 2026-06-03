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

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors]() article.

After adding the connector, configure the following settings:

* **Technical Account ID**
  * The Technical Account ID can be found in the [Adobe I/O Console](https://console.adobe.io/).
  * For more information see [Authenticating and accessing Adobe Experience Platform APIs](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/authenticate_to_acp_tutorial/authenticate_to_acp_tutorial.md#login-to-adobe-io-console).

* **Organization ID**
  * The Organization ID can be found in the [Adobe I/O Console](https://console.adobe.io/).

* **Tenant ID**
  * The Tenant ID can be found in your Adobe Marketing Cloud URL.
  * Example: &lt;https://yourtenantid.experiencecloud.adobe.com/campaign.html&gt;

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
|Email|  &lt;ul&gt;&lt;li&gt;(Required) The email address of the recipient.&lt;/li&gt;&lt;/ul&gt; |
|Event ID|  &lt;ul&gt;&lt;li&gt;(Required) The type of event you want to send.&lt;/li&gt;&lt;li&gt;This ID is generated when creating the event definition.&lt;/li&gt;&lt;li&gt;For additional information, see the [Adobe Campaign Documentation](https://helpx.adobe.com/campaign/standard/administration/using/configuring-transactional-messaging.html).&lt;/li&gt;&lt;/ul&gt; |
|Expiration Date|  &lt;ul&gt;&lt;li&gt;(Optional) The sending of the transactional event will be cancelled after this date.&lt;/li&gt;&lt;/ul&gt; |
|Scheduled Send Date|  &lt;ul&gt;&lt;li&gt;(Optional) The transactional event will be processed and the transactional message will be sent at this date.&lt;/li&gt;&lt;/ul&gt; |
|Template Name|  &lt;ul&gt;&lt;li&gt;If using a template to pass data, input with &#34;Transactional Message Content Template&#34; and enter name of main template.&lt;/li&gt;&lt;li&gt;Do not include double curly braces in name, for example, use `SomeTemplateName` not `{{SomeTemplateName}}`.&lt;/li&gt;&lt;/ul&gt; |
|Template Variables|  &lt;ul&gt;&lt;li&gt;Provide template variables as data input for &#34;Transactional Message Content Template&#34;.&lt;/li&gt;&lt;li&gt;For more information, see .&lt;/li&gt;&lt;li&gt;Name nested template variables with the dot notation.&lt;/li&gt;&lt;li&gt;Example: `items.name`&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes.&lt;/li&gt;&lt;/ul&gt; |
|Transactional Message Content Template|  &lt;ul&gt;&lt;li&gt;Template describing enriched transactional message content.&lt;/li&gt;&lt;li&gt;Templates are injected by name with double curly braces into supported fields.&lt;/li&gt;&lt;li&gt;For example, `{{SomeTemplateName}}`.&lt;/li&gt;&lt;li&gt;For additional information about using enriched message content, see Adobe&#39;s [Campaign Documentation.](https://helpx.adobe.com/campaign/standard/administration/using/configuring-transactional-messaging.html)&lt;/li&gt;&lt;/ul&gt; |
| Transactional API Endpoint |  &lt;ul&gt;&lt;li&gt;(Optional) Specify to override default value of &#34; `mc`&#34; followed by Tenant ID from connector configuration.&lt;/li&gt;&lt;li&gt;This is typically applicable when working in your stage instance.&lt;/li&gt;&lt;li&gt;Example: If stage Tenant ID is &#34;`geometrixx-mkt-stage3`&#34;, then override Transactional API Endpoint to &#34;`geometrixx`&#34;.&lt;/li&gt;&lt;/ul&gt; |

### Action - Trigger Signal Activity

For more information, see [Triggering a signal activity](https://experienceleague.adobe.com/docs/campaign-standard/using/working-with-apis/managing-workflows/triggering-a-signal-activity.html) in the Adobe documentation.

To trigger signal activity, the REST workflow/execution API is used.

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Workflow ID|  &lt;ul&gt;&lt;li&gt;The ID of the workflow configured in your Adobe console.&lt;/li&gt;&lt;/ul&gt; |
|Source|  &lt;ul&gt;&lt;li&gt;Used to indicate the triggering request source.&lt;/li&gt;&lt;/ul&gt; |
|Parameter Map|  &lt;ul&gt;&lt;li&gt;It is possible to call a workflow with parameters.&lt;/li&gt;&lt;li&gt;Map a parameter&#39;s value to it&#39;s name.&lt;/li&gt;&lt;li&gt;String, Number, Boolean, and Date/Time types are supported.&lt;/li&gt;&lt;/ul&gt; |

### Action - Create or Update Profile

To retrieve, create, or update a profile, requests are sent to the Adobe ProfileAndServices API

For more information, see [Creating Profiles with APIs,](https://experienceleague.adobe.com/docs/campaign-standard/using/working-with-apis/managing-profiles/creating-profiles-api.html) [Updating Profiles with APIs](https://experienceleague.adobe.com/docs/campaign-standard/using/working-with-apis/managing-profiles/updating-profiles.html), and [Retrieving profile with APIs](https://experienceleague.adobe.com/docs/campaign-standard/using/working-with-apis/managing-profiles/retrieving-profiles.html?lang=en).

##### Parameters

|**Parameter**| **Description**|
|---| ---|
|Update Strategy|  &lt;ul&gt;&lt;li&gt;(Required) Select applicable update strategy.  &lt;ul&gt;&lt;li&gt;**Create Only** — Look up an existing profile and if not found, create a new profile.&lt;/li&gt;&lt;li&gt;**Update Only** — Look up an existing profile and update it.&lt;/li&gt;&lt;li&gt;**Create or Update** — Look up an existing profile and if found, update it, otherwise create a new profile.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|Filter|  &lt;ul&gt;&lt;li&gt;Required when Update Strategy is **Create Or Update** or **Update Only**.&lt;/li&gt;&lt;li&gt;It is strongly recommended to select filters that return unique results.&lt;/li&gt;&lt;li&gt;For additional information, see: [Composite Identification Key](https://experienceleague.adobe.com/docs/campaign-standard/using/developing/adding-or-extending-a-resource/uc-calling-resource-id-key.html?lang=en).&lt;/li&gt;&lt;li&gt;If the search result returns multiple profiles, only the first one is updated.&lt;/li&gt;&lt;/ul&gt; |
|Is Custom Filter|  &lt;ul&gt;&lt;li&gt;See [about custom filters.](https://experienceleague.adobe.com/docs/campaign-standard/using/working-with-apis/global-concepts/additional-operations/filtering.html?lang=en#custom-filters)&lt;/li&gt;&lt;/ul&gt; |
|Template Variables|  &lt;ul&gt;&lt;li&gt;Provide template variables as data input.&lt;/li&gt;&lt;li&gt;For more information, see .&lt;/li&gt;&lt;li&gt;Name nested template variables with the dot notation.&lt;/li&gt;&lt;li&gt;Example: `items.name`&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes.&lt;/li&gt;&lt;/ul&gt; |
|Templates|  &lt;ul&gt;&lt;li&gt;Provide templates to be referenced in Body Data.&lt;/li&gt;&lt;li&gt;For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected by name with double curly braces into supported fields.&lt;/li&gt;&lt;li&gt;For example, `{{SomeTemplateName}}`.&lt;/li&gt;&lt;/ul&gt; |