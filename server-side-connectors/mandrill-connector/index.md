---
title: Mandrill Connector Setup Guide
description: This article describes how to set up the Mandrill by MailChimp connector in your Customer Data Hub account.
url: https://docs.tealium.com/server-side-connectors/mandrill-connector/
---## Connector actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Send Transactional Email using a Template| ✓| ✗|

## Configure settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors]() article.

After adding the connector, configure the following settings:

* **Mandrill API Key**: This parameter is Required

## Action settings - parameters and options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Send Transactional Email using a Template

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Target Template|  &lt;ul&gt;&lt;li&gt;(Required) Target Template.&lt;/li&gt;&lt;/ul&gt; |
|Subaccount|  &lt;ul&gt;&lt;li&gt;(Optional) Subaccount for this message&lt;/li&gt;&lt;li&gt;Must already exist or will fail with an error&lt;/li&gt;&lt;/ul&gt; |
|Tag List|  &lt;ul&gt;&lt;li&gt;(Optional) String(s) to tag the message with.&lt;/li&gt;&lt;li&gt;Stats are accumulated using tags, though Mandrill only stores the first 100 we see, so this should not be unique or change frequently.&lt;/li&gt;&lt;li&gt;Tags should be 50 characters or less.&lt;/li&gt;&lt;li&gt;Any tags starting with an underscore are reserved for internal use and will cause errors.&lt;/li&gt;&lt;/ul&gt; |
|message.subject| Message subject line|
|message.from_email| Email address of sender |
|message.from_name| Name of sender|
|message.to.email|  &lt;ul&gt;&lt;li&gt;(Required) Email address of recipient&lt;/li&gt;&lt;/ul&gt; |
|message.to.name| Name of recipient|
|message.important| Values are true or false|
|message.track_opens|  &lt;ul&gt;&lt;li&gt;Track file opens&lt;/li&gt;&lt;li&gt;Values are yes or no&lt;/li&gt;&lt;/ul&gt; |
|message.track_clicks|  &lt;ul&gt;&lt;li&gt;Track clicks&lt;/li&gt;&lt;li&gt;Values are yes or no&lt;/li&gt;&lt;/ul&gt; |
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
|Google Analytics Domains to Set|  &lt;ul&gt;&lt;li&gt;(Optional) An array of strings indicating for which any matching URLs will automatically automatically append Google Analytics parameters to their query string.&lt;/li&gt;&lt;/ul&gt; |
|Google Analytics Campaign to Set|  &lt;ul&gt;&lt;li&gt;(Optional) Optional string indicating the value to set for the `utm_campaign` tracking parameter.&lt;/li&gt;&lt;li&gt;If not provide, the from address for the email is used instead.&lt;/li&gt;&lt;/ul&gt; |
|Recipient Header Type|  &lt;ul&gt;&lt;li&gt;(Optional) The header type to use for the recipient, defaults to &#34;to&#34; if not provided one of the following: `to`, `cc`, `bcc`&lt;/li&gt;&lt;li&gt;`to.type:`&lt;/li&gt;&lt;/ul&gt; |
|Header Data (Map Value to Key)|  &lt;ul&gt;&lt;li&gt;Optional extra headers to add to the message (most headers are allowed)&lt;/li&gt;&lt;/ul&gt; |
|Template Content To Set (Map Content to Name)|  &lt;ul&gt;&lt;li&gt;An array of template content to send.&lt;/li&gt;&lt;li&gt;Each item in the array should be a struct with two keys:  &lt;ul&gt;&lt;li&gt;name the name of the content block to set the content&lt;/li&gt;&lt;li&gt;content The actual content to put into the block&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|Global Merge Vars To Set (Map Content to Name)|  &lt;ul&gt;&lt;li&gt;(Optional) Global merge variables to use for recipient.&lt;/li&gt; &lt;ul&gt;&lt;li&gt;name (string) The global merge variable&#34;s name. Merge variable names are case-insensitive and may not start with an underscore (`_`) character&lt;/li&gt;&lt;li&gt;content (mixed) The content of the global merge variable&lt;/li&gt;&lt;/ul&gt; &lt;/ul&gt; |
|Metadata To Set (Map Value to Key)|  &lt;ul&gt;&lt;li&gt;(Optional) Metadata an associative array of user metadata.&lt;/li&gt;&lt;li&gt;Mandrill will store this metadata and make it available for retrieval.&lt;/li&gt;&lt;li&gt;In addition, you can select up to 10 metadata fields to index and make searchable using the Mandrill search api.&lt;/li&gt;&lt;/ul&gt; |
