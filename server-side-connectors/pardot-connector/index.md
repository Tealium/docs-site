---
title: Salesforce Pardot Connector Setup Guide for AudienceStream
description: This article describes how to set up the Salesforce Pardot Connector service in your Customer Data Hub profile.
url: https://docs.tealium.com/server-side-connectors/pardot-connector/
---
With the Salesforce Pardot Connector, you can send one-to-one emails based off of audiences.

## Requirements

* Pardot Business Unit ID
* Salesforce SSO

## Supported Actions

|**Action Name**| **Trigger on Audience**| **Trigger on Streams**|
|---| ---| ---|
|Send Email to Prospect| ✓| x|
|Create or Update Prospect| ✓| x|
|Add Prospect to List| ✓| x|
|Opt-out Prospect from List| ✓| x|
|Remove Prospect from List| ✓| x|

## Configure Settings

Go to the Connector Marketplace and add a new Pardot connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

To configure your vendor, follow these steps:

1. In the **Configuration** tab, click **Add Connector**.
1. Enter a Name for the connector and implementation Notes.
1. Under **Account Type**, select the type of account you are connecting to: **Developer**, **Sandbox**, or **Production**.
1. Enter the **Pardot Business Unit ID**.
    * You can find this value by navigating to **Setup** in Salesforce and entering **Business Unit Setup** in the **Quick Find** box.
    * The **Pardot Business Unit ID** begins with `OUv` and is 18 characters long.
1. Click **Establish Connection**.
    * A Salesforce Login window will appear. Enter your Salesforce SSO credentials and click **Log In**.
    * If MFA is enabled, you may need to verify your Salesforce login. 

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab to set up actions and their triggers.

This section describes how to set up parameters and options for each action:

### Action - Send Email to Prospect

#### Parameters

* **Campaign**: (Required) Select the campaign you want to use. If you don&#39;t see the campaign you&#39;re looking for, you may enter the campaign ID as a custom value.
To find the campaign ID, open up the target campaign in Pardot and look for the numeric value at the end of the URL. For example, in this URL: `https://pi.pardot.com/campaign/read/id/123`, the ID is `123`. For more details about campaign IDs, refer to the articles [Sending One To One Emails](http://developer.pardot.com/kb/api-version-4/emails/#sending-one-to-one-emails) and [Supported Parameters](http://developer.pardot.com/kb/api-version-4/emails/#supported-parameters_1).
* **Email Template**: (Required) Select the email template you want to use. If you don&#39;t see the email template you&#39;re looking for in this list, you may enter your template ID as a custom value.

Like campaign ID, your email template ID is the numeric value at the end of the email template URL in Pardot. A template url will look something like this: `https://pi.pardot.com/emailTemplate/read/id/XXXX`, where `XXXX` is the numeric ID.

* **Prospect Identifier**: (Required) Select an identifier to find a prospect by.
  * **prospect_email:** an email address associated with a prospect
  * **id:** A Pardot ID associated with a prospect

#### Options (Optional)

##### Additional Email Options

Configure this section to override the &#34;Email Template&#34; attributes. Template Support: `subject`, `text_content`, and `html_content` options support templating. For these, reference the template name to generate message data from template.

|Option| Description|
|---| ---|
|`subject`| The subject of the email. If configured, the value should be the template key from the **Templates** section|
|`text_content`| The text body of the email. If configured, the value should be the template key from the **Templates** section. The template must contain either `%%unsubscribe%%` or `%%email_preference_center%%`|
|`html_content`| The HTML body of the email. If configured, the value should be the template key from the **Templates** section. The template must contain either `%%unsubscribe%%` or `%%email_preference_center%%`|
|`tags[]`| Configure an &#34;array/set&#34; attribute type for one or multiple tags. This is the name of the tag you&#39;d like to create or associate with this email|
|`list_ids[]`| Configure an &#34;array/set&#34; attribute type for one or multiple lists. This is the ID of the list you&#39;d like to mail to|
|`suppression_list_ids[]`| Configure an &#34;array/set&#34; attribute type for one or multiple lists. This is the ID of the list you&#39;d like to suppress mailing to|

* If no `email_template_id` is provided then either `(from_email &amp; from_name)` or `from_user_id` is required
* If the **Email Template** section is not configured, the `name`, `subject`, and either the `text_content` or `html_content` is required
* If the **Email Template** section is configured, the email template will be used first. `name`, `replyto_email`, `subject`, `text_content`, and `html_content` will override the template contents if they&#39;re provided

##### Template Variables

* Provide template variables as data input for templates. For more information, see .
* Name nested template variables with dot notation. Example: `items.name`
* Nested template variables are typically built from data layer list attributes

##### Templates

* Provide templates to be referenced in message data. For more information, see .
* Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.

### Action - Create or Update Prospect

#### Parameters

* **Prospect Lookup Identifier:** (Required) Select an identifier to find a prospect by.
  * For more information, see: [Creating and Updating Prospects](http://developer.pardot.com/kb/api-version-4/prospects/)
  * Please select from one of the following options to lookup prospects by:
    * Prospect Email (email): Email address
    * Prospect ID (id): This is the prospect&#39;s unique ID
    * Prospect FID (fid): This is the prospects CRM ID

*. **Campaign:** (Required) Select the campaign you want to use. If you don&#39;t see the campaign you&#39;re looking for, you may enter the campaign ID as a custom value.
To find the Campaign ID, open up the target campaign in Pardot and look for the numeric value at the end of the URL. For example, in this URL: `https://pi.pardot.com/campaign/read/id/123`, the ID is `123`.

* **Create If Not Exists:** (Optional) Check if you want to allow prospect creation.

* **Create Prospect Data**
  * (Required) Email Address
  * When a prospect is being created, field configurations from this section are used

* **Update Prospect Data**
  * (Required) When a prospect is being updated, field configurations from this section are used

### Action - Add Prospect to List

#### Parameters

* **Target List:** (Required) List to add the prospect to.
See: [&#34;create&#34; option under Supported Parameters](http://developer.pardot.com/kb/api-version-4/list-memberships/#supported-operations_1)
  
If you need to add a list that you don&#39;t see in the dropdown, you can find the list ID at the URL: `https://pi.pardot.com/list/read/id/XXXX`

* **Prospect Identifier:** (Required) Select an identifier to find a prospect by.
  * **prospect\_email:** An email address associated with a prospect
  * **id:** A Pardot ID that the prospect is known by

### Action - Opt out Prospect from List

#### Parameters

* **Target List:** (Required) List to add the prospect to.
See: [&#34;create&#34; option under Supported Parameters](http://developer.pardot.com/kb/api-version-4/list-memberships/#supported-operations_1)
  
If you need to add a list that you don&#39;t see in the dropdown, you can find the list ID at the URL: `https://pi.pardot.com/list/read/id/XXXX`

* **Prospect Identifier:** (Required) Select an identifier to find a prospect by.
  * **prospect_email:** An email address associated with a prospect
  * **id:** A Pardot ID that the prospect is known by

### Action - Remove Prospect from List

#### Parameters

* **Target List** (Required) List to add the prospect to.
See: [&#34;delete&#34; option under Supported Parameters](http://developer.pardot.com/kb/api-version-4/list-memberships/#supported-operations_1)
  
If you need to add a list that you don&#39;t see in the dropdown, you can find the list ID at the URL: `https://pi.pardot.com/list/read/id/XXXX`

* **Prospect Lookup Identifier:** (Required) Select an identifier to find a prospect by.
  * **prospect_email:** An email address associated with a prospect
  * **id:** A Pardot ID that the prospect is known by

## Vendor Documentation

* [How are prospects associated with campaigns?](http://help.pardot.com/customer/en/portal/articles/2128387-how-are-prospects-associated-with-campaigns-#setting-campaigns-with-the-api)
* [Sending one-to-one emails](http://developer.pardot.com/kb/api-version-4/emails/#sending-one-to-one-emails)
* [Supported Parameters](http://developer.pardot.com/kb/api-version-4/emails/#supported-parameters_1)