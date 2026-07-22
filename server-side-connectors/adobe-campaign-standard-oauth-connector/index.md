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

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

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
| Update Strategy | <ul><li>(Required) Select applicable update strategy.</li><li>**Create Only**: Look up an existing profile and if not found, create a new profile.</li><li>**Update Only**: Look up an existing profile and update it.</li><li>**Create or Update**: Look up an existing profile and if found, update it, otherwise create a new profile.</li></ul> |
| Profile Data | <ul><li>Profile Field names and corresponding values.
.</li></ul> |
| Filter | <ul><li>Required when **Update Strategy** is `Create Or Update` or `Update Only`.</lil><li>We recommend choosing filters that return unique results.</li><li>For more information, see [Campaign: Calling a resource using a composite identification key](https://experienceleague.adobe.com/docs/campaign-standard/using/developing/adding-or-extending-a-resource/uc-calling-resource-id-key.html?lang=en).</li><li>If the search result returns multiple profiles, only the first one is updated.</li></ul>  |
| Is Custom Filter | <ul><li>Select this option if the chosen filter is custom.</li><li>For more information, see [Campaign: Custom filters](https://experienceleague.adobe.com/docs/campaign-standard/using/working-with-apis/global-concepts/additional-operations/filtering.html?lang=en#custom-filters).</li></ul> |
| Filter Parameters | <ul><li>Filter parameters used in search.</li></ul> |
| Template Variables | <ul><li>Provide template variables as data input. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Name nested template variables with the dot notation. For example, `items.name`.</li><li>Nested template variables are typically built from data layer list attributes.</li></ul> |
| Templates | <ul><li>Provide templates to be referenced in body data. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.</li></ul> |