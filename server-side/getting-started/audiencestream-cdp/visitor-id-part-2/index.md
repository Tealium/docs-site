---
title: Visitor ID Part 2
description: In this step we will complete the identity resolution plan by creating the visitor ID attribute for Email Address and populate it with the values we are already collecting in the corresponding string attribute.
url: https://docs.tealium.com/server-side/getting-started/audiencestream-cdp/visitor-id-part-2/
---
## Visitor ID: Email Address

Since we now that the string attribute, **Email Address**, is working as expected, we can use the same rule from that attribute to configure this visitor ID attribute.

To create a visitor ID attribute:

1. Navigate to **AudienceStream &gt; Visitor/Visit Attributes** and click **&#43; Add Attribute**.
1. Select the scope of **Visitor** and click **Continue**.
1. Select the data type **Visitor ID** and click **Continue**.
1. Enter the name of the attribute, `Email Address`.
1. Click **Add Enrichment**.
1. In the drop-down-list, select the **Email Address** string attribute.
1. In the **Rule** drop-down list, select the previously created rule for user registration events.
1. Click **Finish**.

Now you can save and publish your account.

## Enable visitor stitching

The last and easiest step is to turn on visitor stitching. This feature is not enabled by default. It&#39;s only after you&#39;ve carefully identified, configured, and validated your identity resolution strategy that visitor stitching should be turned on. Contact your account manager to enable this feature in your account.

Click **Next** to move on to audiences and learn how to activate your customer data with your preferred vendors.
