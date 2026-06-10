---
title: Visitor ID Discovery
description: This is a critical step to ensure that our identity resolution strategy is accurate and that the attribute we've chosen, Email Address, is unique across our customer base.
url: https://docs.tealium.com/server-side/getting-started/audiencestream-cdp/visitor-id-discovery/
---
We will use Audience Discovery to sample our active customers using our new Email Address attribute. The Audience Discovery chart will display a distribution of the unique values of that attribute. If everything is working as expected, each Email Address value will only have one visitor associated with it.

## Verify with audience discovery

Remember, for this to work you will need to let some time pass since the creation of the email address attribute so that AudienceStream can collect enough data to provide a decent sample set. Follow these steps to validate the email address attribute.

1. Navigate to **Activate &gt; Discover** (Audience Discovery).
1. Click **Perspective** and select the visitor string attribute **Email Address**.
1. You should examine not just the **Live** view, but the **Historic** view.

The chart will list each unique value of the Email Address attribute across the x-axis, along with a bar indicating how many visitor profiles currently contain that value.

If we configured our attribute correctly, and the data is suitable for visitor stitching, each bar with a value should have a reasonable number of visitor profiles.

The number is the number of different visitor profiles from which we have seen this candidate stitching key. So if, for example, an email address had been seen in 3 visitor profiles, it would be expected that a user with this email address had logged in from 3 different devices during the time period for the report.

What you are looking out for here is any out of place bar heights or a suspicious distribution. For example, if most email addresses had been seen from 1, 2 or 3 visitor profiles, but some email addresses had been seen from 50 or more visitor profiles, then this requires further investigation at this point. If all email addresses on the first page of the report had been seen from a suspiciously high number of devices, then this too requires further investigation.

The first bar shows the number of visitors with **no value &#34;(none)&#34;**, which represents the unknown visitors that have not provided an email address yet.

![](/images/server-side/as-getting-started-discovery-sample-data.jpg)

The example above confirms that Email Address is being collected uniquely and accurately, so now it&#39;s time to complete our identity resolution strategy with the Visitor ID attribute.

Click **Next** to create a Visitor ID attribute and start taking advantage of visitor stitching.
