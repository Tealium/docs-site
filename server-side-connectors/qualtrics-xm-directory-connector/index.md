---
title: Qualtrics XM Directory Connector Setup Guide
description: This article describes how to set up the Qualtrics XM Directory connector.
url: https://docs.tealium.com/server-side-connectors/qualtrics-xm-directory-connector/
---
## API information

This connector uses the following vendor API:

* API Name: Qualtrics XM Directory API
* API Version: v3
* API Endpoint: `https://ca1.qualtrics.com`
* Documentation: [Qualtrics XM Directory API](https://api.qualtrics.com/api-reference/docs/api-reference.md)

## Connector actions

| Action name | Visitor profile | Event data |
| --- | :---: | :---: |
|Create or Update Directory Contact| ✓| ✓|
|Create Contact Transaction| ✓| ✓|

## Configure settings

Go to the connector marketplace and add a new connector. For more information, see [about-connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **Data Center ID**
  * Your Data Center ID can be found by going to **Account Settings** &gt; **Qualtrics IDs**&gt; **IDs** &gt; **Box User**.
* **Client ID**
  * Provide your web application Client ID that has access to the Qualtrics XM Directory API.
  * Your Client ID can be found by going to **Account Settings** **&gt; Qualtrics IDs &gt;** **OAuth Client Manager**.
  * Your Qualtrics XM Directory API OAuth Client Manager Page must contain the following **Grant Type**:
    * `client_credentials` and **Scopes** must be: `manage:contact_transactions`, `manage:directory_contacts`, `read:directories`, and `read:mailing_lists`.
  * For additional information, see [OAuth authentication (client credentials)](https://api.qualtrics.com/api-reference/docs/Instructions/oauth-authentication.md) and [OAuth 2.0 Scopes](https://api.qualtrics.com/api-reference/docs/Instructions/oauthscopes.md).
* **Client Secret**
  * Provide your web application client secret.

 
<blockquote>
When creating your application within Qualtrics, configure the redirect URLs to match your Tealium environment. For example: [https://sso.tealiumiq.com/oauth/qualtrics/callback.html](https://sso.tealiumiq.com/oauth/qualtrics/callback.html) for SSO enabled customers and [https://my.tealiumiq.com/oauth/qualtrics/callback.html](https://my.tealiumiq.com/oauth/qualtrics/callback.html) for standard customers.
</blockquote>
 

## Action settings - parameters and options

Click **Continue** to configure the connector actions. Enter a name for the action and select the action type from the list.

### Action - create or update directory contact

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Update Strategy|  <ul><li>(Required) Select applicable update strategy.  <ul><li>**Create Only**: Look up an existing contact and if not found, create a new contact.</li><li>**Update Only**: Look up an existing contact and update it.</li><li>**Create or Update**: Look up an existing contact and if found, update it, otherwise create a new contact.</li></ul> </li></ul> |
|Directory|  <ul><li>(Required) Select the directory to create or update the contact in.</li></ul> |
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
|Embedded Data|  <ul><li>The embedded data object contains extra metadata that you want to associate with contacts.</li><li>This user-defined data could include such data as birthplace, gender, employment status, etc.</li></ul> |
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
|Directory|  <ul><li>(Required) Select the directory to create or update the contact in.</li></ul> |
|Mailing List|  <ul><li>(Required) Select the mailing list to create the contact transaction in.</li></ul> |
|ContactId|
|FirstName|
|LastName|
|Email|
|Phone|
|ExtRef|
|Language|
|Unsubscribed|
|Transaction Date|
