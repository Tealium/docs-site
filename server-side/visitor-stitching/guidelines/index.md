---
title: Visitor stitching guidelines
description: This article provides guidelines for visitor stitching.
url: https://docs.tealium.com/server-side/visitor-stitching/guidelines/
---
The following are important guidelines for visitor ID attributes and visitor stitching:

* **Uniqueness**  
A visitor ID attribute must have at least 3 unique characters and be at least 6 characters long.  
Learn more about [visitor ID attribute requirements]().
* **Case sensitive**&lt;br&gt;
Visitor ID attribute values are case sensitive so, `UserName@example.com` is different from `username@example.com`. If the attribute values contain these variations, use the [lower-case enrichment]() to normalize them.
* **Multiple IDs**  
Multiple visitor ID attributes are evaluated as an OR condition in order of attribute ID from lowest to highest (oldest to newest).
* **Robustness**  
Only [user identifiers]() that are guaranteed to match the visitor across devices should be used for visitor ID attributes.
* **Stitched visitor profile**  
When multiple visitor profiles are stitched, the original profiles remain and a new visitor profile is created to store the stitched profiles.
* **Avoid test data**  
Be careful not to capture default or test values in your user identifiers, such as, `undefined`, `unknown`, or `not set`.
* **Shared IDs**  
Before stitching is enabled, determine how to handle shared IDs, such as those used at libraries or universities, so that multiple visitors are not stitched inadvertently.
* **Size limit**  
The maximum size of a visitor profile after encryption and compression is 400 KB.
* **Shared devices**  
When two users share a device, both users have the same anonymous ID. If they visit the same websites, but use different user identifiers (such as an email address or a customer ID), this is referred to as visitor switching. Tealium Support or Professional Services can assist you with implementing a solution to handle visitor switching. For more information, see the following Tealium knowledge base articles:  
    * [Anonymous User Tracking under ITP with Visitor Switching in AudienceStream](https://support.tealiumiq.com/en/support/solutions/articles/36000441645-anonymous-user-tracking-under-itp-with-visitor-switching-in-audiencestream)
    * [Visitor Switching in iQ](https://support.tealiumiq.com/en/support/solutions/articles/36000419055-visitor-switching-in-iq)
    * [Visitor Switching in Tealium Mobile SDKs](https://support.tealiumiq.com/en/support/solutions/articles/36000493080-visitor-switching-in-tealium-mobile-sdks)