---
title: Mandrill Connector Setup Guide
description: This article describes how to set up the Mandrill by MailChimp connector in your Customer Data Hub account.
url: https://docs.tealium.com/server-side-connectors/mandrill-connector/
---## Connector actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Send Transactional Email using a Template| ✓| ✗|

## Configure settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors](https://docs.tealium.com/about-connectors/) article.

After adding the connector, configure the following settings:

* **Mandrill API Key**: This parameter is Required

## Action settings - parameters and options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Send Transactional Email using a Template

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Target Template|  <ul><li>(Required) Target Template.</li></ul> |
|Subaccount|  <ul><li>(Optional) Subaccount for this message</li><li>Must already exist or will fail with an error</li></ul> |
|Tag List|  <ul><li>(Optional) String(s) to tag the message with.</li><li>Stats are accumulated using tags, though Mandrill only stores the first 100 we see, so this should not be unique or change frequently.</li><li>Tags should be 50 characters or less.</li><li>Any tags starting with an underscore are reserved for internal use and will cause errors.</li></ul> |
|message.subject| Message subject line|
|message.from_email| Email address of sender |
|message.from_name| Name of sender|
|message.to.email|  <ul><li>(Required) Email address of recipient</li></ul> |
|message.to.name| Name of recipient|
|message.important| Values are true or false|
|message.track_opens|  <ul><li>Track file opens</li><li>Values are yes or no</li></ul> |
|message.track_clicks|  <ul><li>Track clicks</li><li>Values are yes or no</li></ul> |
|message.auto_text| Optional|
|message.auto_html| Optional|
|message.inline_css| Optional|
|message.url_strip_qs| Optional|
|message.preserve_recipients| Optional|
|message.view_content_link| Optional|
|message.bcc_address| Optional|
|message.tracking_domain| Optional|
|message.signing_domain| Optional|
|message.return_path_domain| Optional|
|message.merge| Optional|
|message.merge_language| Optional|
|async| Optional|
|ip_pool| Optional|
|send_at| Optional|
|Google Analytics Domains to Set|  <ul><li>(Optional) An array of strings indicating for which any matching URLs will automatically automatically append Google Analytics parameters to their query string.</li></ul> |
|Google Analytics Campaign to Set|  <ul><li>(Optional) Optional string indicating the value to set for the `utm_campaign` tracking parameter.</li><li>If not provide, the from address for the email is used instead.</li></ul> |
|Recipient Header Type|  <ul><li>(Optional) The header type to use for the recipient, defaults to "to" if not provided one of the following: `to`, `cc`, `bcc`</li><li>`to.type:`</li></ul> |
|Header Data (Map Value to Key)|  <ul><li>Optional extra headers to add to the message (most headers are allowed)</li></ul> |
|Template Content To Set (Map Content to Name)|  <ul><li>An array of template content to send.</li><li>Each item in the array should be a struct with two keys:  <ul><li>name the name of the content block to set the content</li><li>content The actual content to put into the block</li></ul> </li></ul> |
|Global Merge Vars To Set (Map Content to Name)|  <ul><li>(Optional) Global merge variables to use for recipient.</li> <ul><li>name (string) The global merge variable"s name. Merge variable names are case-insensitive and may not start with an underscore (`_`) character</li><li>content (mixed) The content of the global merge variable</li></ul> </ul> |
|Metadata To Set (Map Value to Key)|  <ul><li>(Optional) Metadata an associative array of user metadata.</li><li>Mandrill will store this metadata and make it available for retrieval.</li><li>In addition, you can select up to 10 metadata fields to index and make searchable using the Mandrill search api.</li></ul> |
