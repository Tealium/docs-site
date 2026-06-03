---
title: Qualtrics XM Directory Connector Setup Guide
description: This article describes how to set up the Qualtrics XM Directory connector.
url: https://docs.tealium.com/server-side-connectors/qualtrics-xm-directory-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Qualtrics XM Directory API
* API Version: v3
* API Endpoint: `https://ca1.qualtrics.com`
* Documentation: [Qualtrics XM Directory API](https://api.qualtrics.com/api-reference/docs/api-reference.md)

## Connector actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Create or Update Directory Contact| ✓| ✓|
|Create Contact Transaction| ✓| ✓|

## Configure settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors]() article.

After adding the connector, configure the following settings:

* **Data Center ID**
  * Your Data Center ID can be found by going to **Account Settings** &amp;gt; **Qualtrics IDs**&amp;gt; **IDs** &amp;gt; **Box User**.
* **Client ID**
  * Provide your web application Client ID that has access to the Qualtrics XM Directory API.
  * Your Client ID can be found by going to **Account Settings** **&amp;gt; Qualtrics IDs &amp;gt;** **OAuth Client Manager**.
  * Your Qualtrics XM Directory API OAuth Client Manager Page must contain the following **Grant Type**:
    * `client_credentials` and **Scopes** must be: `manage:contact_transactions`, `manage:directory_contacts`, `read:directories`, and `read:mailing_lists`.
  * For additional information, see [OAuth authentication (client credentials)](https://api.qualtrics.com/api-reference/docs/Instructions/oauth-authentication.md) and [OAuth 2.0 Scopes](https://api.qualtrics.com/api-reference/docs/Instructions/oauthscopes.md).
* **Client Secret**
  * Provide your web application client secret.

 When creating your application within Qualtrics, configure the redirect URLs to match your Tealium environment. For example: [https://sso.tealiumiq.com/oauth/qualtrics/callback.html](https://sso.tealiumiq.com/oauth/qualtrics/callback.html) for SSO enabled customers and [https://my.tealiumiq.com/oauth/qualtrics/callback.html](https://my.tealiumiq.com/oauth/qualtrics/callback.html) for standard customers. 

## Action settings - parameters and options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - create or update directory contact

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Update Strategy|  &lt;ul&gt;&lt;li&gt;(Required) Select applicable update strategy.  &lt;ul&gt;&lt;li&gt;**Create Only**: Look up an existing contact and if not found, create a new contact.&lt;/li&gt;&lt;li&gt;**Update Only**: Look up an existing contact and update it.&lt;/li&gt;&lt;li&gt;**Create or Update**: Look up an existing contact and if found, update it, otherwise create a new contact.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|Directory|  &lt;ul&gt;&lt;li&gt;(Required) Select the directory to create or update the contact in.&lt;/li&gt;&lt;/ul&gt; |
|FirstName|
|LastName|
|Email|
|Phone|
|ExtRef|
|Language|
|Unsubscribed|
|FirstName|
|LastName|
|Email|
|Phone|
|ExtRef|
|Language|
|Unsubscribed|
|Embedded Data|  &lt;ul&gt;&lt;li&gt;The embedded data object contains extra metadata that you want to associate with contacts.&lt;/li&gt;&lt;li&gt;This user-defined data could include such data as birthplace, gender, employment status, etc.&lt;/li&gt;&lt;/ul&gt; |
|ContactId|
|FirstName|
|LastName|
|Email|
|Phone|
|ExtRef|
|Language|
|Unsubscribed|

### Action - Create contact transaction

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Directory|  &lt;ul&gt;&lt;li&gt;(Required) Select the directory to create or update the contact in.&lt;/li&gt;&lt;/ul&gt; |
|Mailing List|  &lt;ul&gt;&lt;li&gt;(Required) Select the mailing list to create the contact transaction in.&lt;/li&gt;&lt;/ul&gt; |
|ContactId|
|FirstName|
|LastName|
|Email|
|Phone|
|ExtRef|
|Language|
|Unsubscribed|
|Transaction Date|
