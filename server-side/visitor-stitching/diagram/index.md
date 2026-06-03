---
title: Visitor stitching example
description: This article provides an example of the visitor stitching process that occurs when a visitor uses different devices during a series of visits to a website.
url: https://docs.tealium.com/server-side/visitor-stitching/diagram/
---
## First visit

A new visitor visits your website from their laptop.
1. An anonymous ID is assigned to the visitor and profile A is created. The anonymous ID allows one profile to be maintained for multiple visits.
1. When the visitor authenticates with a never before seen email address, user@example.com, the email address is assigned to a user identifier.
1. A visitor ID attribute in profile A is enriched with the value of the user identifier (the email address).
![](/images/server-side/visitor-stitching-example-first-visit.png)

## Second visit

The next day, the same person visits your website from their tablet.
1. An anonymous ID is assigned to the visitor and profile B is created.
1. The visitor logs in to the website using the same email address stored in profile A, user@example.com.
![](/images/server-side/visitor-stitching-example-second-visit.png)  
    A visitor ID attribute in profile B is set to the email address, user@example.com.
1. AudienceStream performs a visitor ID lookup on the email address. Profile A and profile B have a visitor ID attribute set to the same email address and the profiles are determined to be associated.
1. AudienceStream stitches profiles A and B together and creates profile C.  
![](/images/server-side/visitor-stitching-profile-c-created.png)
    * Profile C is now used for both the desktop and tablet and contains the following:
        * All the events and historical data from profiles A and B.
        * A `replaces` array that contains links to profile A and profile B.
    * The `replaced by` attribute in profiles A and B contains a link to profile C.
    * Lookup can still be performed on the anonymous IDs in profiles A and B.

## Third visit

A few days later, a nurture campaign sends an email to `user@example.com`.
1. The user opens the email on their phone and taps the link to your website.
1. The email address is passed in a query string parameter in the URL, allowing AudienceStream to identify the user upon page load.
1. Profile D is created with a user identifier set to the email address.  
![](/images/server-side/visitor-stitching-third-visit-profile-d-created.png)  
    The email address in profile D matches the email address in the visitor ID attribute in profile C and the two profiles are stitched together, creating profile E.
![](/images/server-side/visitor-stitching-profile-e-created.png)
    * Profile E is now used for the desktop, tablet, and phone and contains the following:
        * All the events and historical data from profiles C and D.
        * A `replaces` array that contains links to profile C and profile D.
    * The `replaced by` attribute in profiles C and D contains a link to profile E.
    * Lookup can still be performed on the anonymous IDs in profiles A, B, C, and D.