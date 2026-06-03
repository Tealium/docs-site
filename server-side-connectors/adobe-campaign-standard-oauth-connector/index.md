---
title: Adobe Campaign Standard (OAuth) Connector Setup Guide
description: This article describes how to set up the Adobe Campaign Standard (OAuth) connector.
url: https://docs.tealium.com/server-side-connectors/adobe-campaign-standard-oauth-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Adobe Campaign Standard (OAuth)
* API Version: v1.0
* API Endpoint: `https://mc.adobe.io/`

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:
* **Tenant ID**  
    * The Tenant ID can be found in your Adobe Marketing Cloud URL.
    * For example, `https://_yourtenantid_.experiencecloud.adobe.com/campaign.html`.
* **API Key**  
    * The API Key (Client ID) can be found in the [Adobe I/O Console](https://console.adobe.io/).
* **Secret Key**  
    * The client secret can be found in the [Adobe I/O Console](https://console.adobe.io/).

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Create or Update Profile | ✓ | ✗ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Create or Update Profile

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Update Strategy | &lt;ul&gt;&lt;li&gt;(Required) Select applicable update strategy.&lt;/li&gt;&lt;li&gt;**Create Only**: Look up an existing profile and if not found, create a new profile.&lt;/li&gt;&lt;li&gt;**Update Only**: Look up an existing profile and update it.&lt;/li&gt;&lt;li&gt;**Create or Update**: Look up an existing profile and if found, update it, otherwise create a new profile.&lt;/li&gt;&lt;/ul&gt; |
| Profile Data | &lt;ul&gt;&lt;li&gt;Profile Field names and corresponding values.
.&lt;/li&gt;&lt;/ul&gt; |
| Filter | &lt;ul&gt;&lt;li&gt;Required when **Update Strategy** is `Create Or Update` or `Update Only`.&lt;/lil&gt;&lt;li&gt;We recommend choosing filters that return unique results.&lt;/li&gt;&lt;li&gt;For more information, see [Campaign: Calling a resource using a composite identification key](https://experienceleague.adobe.com/docs/campaign-standard/using/developing/adding-or-extending-a-resource/uc-calling-resource-id-key.html?lang=en).&lt;/li&gt;&lt;li&gt;If the search result returns multiple profiles, only the first one is updated.&lt;/li&gt;&lt;/ul&gt;  |
| Is Custom Filter | &lt;ul&gt;&lt;li&gt;Select this option if the chosen filter is custom.&lt;/li&gt;&lt;li&gt;For more information, see [Campaign: Custom filters](https://experienceleague.adobe.com/docs/campaign-standard/using/working-with-apis/global-concepts/additional-operations/filtering.html?lang=en#custom-filters).&lt;/li&gt;&lt;/ul&gt; |
| Filter Parameters | &lt;ul&gt;&lt;li&gt;Filter parameters used in search.&lt;/li&gt;&lt;/ul&gt; |
| Template Variables | &lt;ul&gt;&lt;li&gt;Provide template variables as data input. For more information, see .&lt;/li&gt;&lt;li&gt;Name nested template variables with the dot notation. For example, `items.name`.&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes.&lt;/li&gt;&lt;/ul&gt; |
| Templates | &lt;ul&gt;&lt;li&gt;Provide templates to be referenced in body data. For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.&lt;/li&gt;&lt;/ul&gt; |