---
title: Visitor Stitching
description: Now that you've seen how to build rich customer profiles using attributes and enrichments, it's time to review how to identify your customers through identity resolution and visitor stitching.
url: https://docs.tealium.com/server-side/getting-started/audiencestream-cdp/visitor-stitching/
---
The data we&#39;re collecting so far is anonymous and could be fragmented across the customer&#39;s different browsers and devices. Let&#39;s see how we can pull this data together to create a complete profile of the customer.

## Identity resolution

![](/images/server-side/as-getting-started-identity-resolution.jpg)

Identity resolution refers to the various ways that customers can engage with your brand anonymously, then associating that behavior back to a known customer. Most sites and apps attempt to keep track of unknown users, such as with using cookies, until the user identifies themselves, by logging in or completing a purchase (for example).

AudienceStream provides a special attribute called **visitor ID** that is used to store unique identifiers for each customer. Setting a visitor ID in a user profile resolves the identity from an unknown user (anonymous) to a known user.

## Visitor stitching

As customer data flows into AudienceStream from various data sources (mobile phones, tablets, laptops, desktop computers, etc.), separate visitor profiles are maintained for each channel. However, once the customer&#39;s identity is resolved in two or more of those channels, a process called visitor stitching automatically combines the attributes from each profile into a new master profile that replaces the others. This powerful feature creates a cross-channel profile of your known customers.

Click **Next** to learn about the visitor ID attribute and what to consider in your configuration.