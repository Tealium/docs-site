---
title: Visitor ID Part 1
description: In this step, we will show how to safely create a visitor ID attribute and introduce Audience Discovery, which allows us to validate the identity resolution strategy before finalizing it.
url: https://docs.tealium.com/server-side/getting-started/audiencestream-cdp/visitor-id-part-1/
---
In this example, we will capture email addresses during user registration events based on the requirements from the previous step.

## Capture email address

This step assumes you already have an event attribute for `email_address` and an event named `user_register` that sends it. From here, we will create a string visitor attribute for email address, test it in Audience Discovery, then create the final visitor ID attribute.

1. Go to **AudienceStream &gt; Visitor/Visit Attributes** and click **&#43; Add Attribute**.
1. Select the scope of **Visitor** and click **Continue**.
1. Select the data type **String** and click **Continue**.
1. Enter the attribute name `Email Address`.
1. Click **Add Enrichment**, select **Set String**, and set the **Visitor String** to the event variable `email_address`
1. Leave the **WHEN** set to **Any Event**, then click **Create a New Rule**.
1. Create a rule that identifies the qualifying event, for example:

[
  [
    {
      &#34;input&#34;: &#34;tealium_event&#34;,
      &#34;operator&#34;: &#34;equals&#34;,
      &#34;filter&#34;: &#34;user_register&#34;
    }
  ]
]

1. Click **Finish**, then **Save**.

Now, you have a visitor attribute to capture the email address of customers during qualifying events. You can easily extend this logic to include other qualifying events (such as purchases or lead forms) as you encounter them.

At this point you&#39;ll want to save and publish your account and wait a few days for AudienceStream to start collecting this data. Once we have enough sample data we&#39;ll use Audience Discovery to validate our identity resolution strategy before finalizing it with the visitor ID attribute.

Click **Visitor ID Discovery** to learn how to use Audience Discovery for data validation.
