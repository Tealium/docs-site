---
title: Visitor stitching scenarios
description: This article shows examples of a visitor using a different email address on a subsequent visit to a webiste.
url: https://docs.tealium.com/server-side/visitor-stitching/scenarios/
---
When the same user is identified by two email addresses, the result is based on the device and browser used for each.

For example, a user visits a website for the first time and provides an email address when submitting a form. The email address is hashed, it enriches the `Email Address Hash` visitor ID attribute, and a new visitor profile is created in AudienceStream.

The resulting visitor profile might look like this:

|Attribute| Value|
|---| ---|
|Anonymous ID| 01754649ad73005a6d584d2732c401078005b0700093c|
|Device| Laptop|
|Browser| Chrome 89|
|Email Address Hash| 16c18d336f0b250f0e2d907452ceb9658a74ecdae8bc94864c23122a72cc27a5|

## Scenario 1: a different email address from the same device and browser

A week later, a user visits the website using the same device and browser and submits a form with a different email address. There are two ways this can happen, as follows:

* Case A: The same user visits and submits a form with a different email address.
* Case B: Two users share a device and a different user submits a form with a different email address.

### Case A

The anonymous ID is the same, so the incoming event will match the profile that was created on the user&#39;s first visit. However, because a visitor ID attribute cannot be changed, the new email address hash value will not be used.

**Result for case A:** One visitor profile with a visitor ID attribute set to the original email address hash.

![](/images/server-side/two-emails-first.png)

### Case B

Users sharing a device and visiting the same websites using different user identifiers (an email address in this case) is referred to as visitor switching. Tealium Support or Professional Services can assist you with implementing a solution to handle visitor switching. For more information, see the following Tealium knowledge base articles:

* [Anonymous User Tracking under ITP with Visitor Switching in AudienceStream](https://support.tealiumiq.com/en/support/solutions/articles/36000441645-anonymous-user-tracking-under-itp-with-visitor-switching-in-audiencestream)
* [Visitor Switching in iQ](https://support.tealiumiq.com/en/support/solutions/articles/36000419055-visitor-switching-in-iq)
* [Visitor Switching in Tealium Mobile SDKs](https://support.tealiumiq.com/en/support/solutions/articles/36000493080-visitor-switching-in-tealium-mobile-sdks)

## Scenario 2: a different email from a different device or browser

A week later, the same user visits the website using a different device or browser and submits a form with a different email address. The anonymous ID is different, so the incoming event does not match the profile that was created on the user&#39;s first visit. A new profile is created and there are two profiles for this user after the second visit. No visitor stitching occurs, because the visitor ID attribute does not match (the email addresses are different). These two profiles could be stitched together later, if they matched on a second visitor ID attribute.

**Result:** Two visitor profiles, with each visitor ID attribute set to the corresponding email address hash.

![](/images/server-side/two-emails-both.png)

## Example of two visitor profiles matching on a second visitor ID attribute

In this example, a user visits a web site from two different devices and is assigned a customer ID for each visit. The anonymous IDs do not match, and two separate profiles are created. The customer ID is configured to enrich visitor ID attribute #1, and the visitor ID attribute is enriched in each profile, as shown below.

This scenario could only happen if the anonymous ID (`tealium_visitor_id`) is not known, or is different in the two profiles. If the anonymous IDs match, no user IDs or visitor ID attributes would be evaluated, and the second profile would not be created.

![](/images/server-side/match-2nd-visid-first.png)

The user visits the website again from the first device and provides an email address when submitting a form. The customer_email address attribute is configured to enrich visitor ID attribute #2. Visitor ID attribute #2 in Profile A is enriched with the email address, as shown below.

![](/images/server-side/match-2nd-visid-second.png)

When the user visits the website from the second device and provides the same email address when submitting a form, the email address matches visitor ID attribute #2 in Profile A, and the two profiles are stitched together to create Profile C, as shown below.

![](/images/server-side/match-2nd-visid-third.png)

Profile C contains a new `replaces` array, which holds values that are no longer stored in visitor ID attributes, but can still be used for visitor stitching in the future. Profile A and Profile B had different values for the anonymous ID and Visitor ID Attribute #1 (Customer ID). Because only one value can be set per visitor ID attribute, two values had to move to the `replaces` array. Profile B was the newer profile and had fewer events than Profile A, so the Profile B identifiers were moved to the `replaces` array.

### HTTP API and file import data sources

For web or HTTP API data sources, this scenario would happen only if the attribute ID value of Visitor ID Attribute #1 (Customer ID) is lower than Visitor ID Attribute #2 (Hashed Email).

With file import, visitor ID mappings can be customized and user identifier enrichment occurs in the order mapped, this scenario could be achieved in a few different ways depending on the setup.

For more information, see [Tealium Collect HTTP API](), [About incoming webhooks](), or [About file import]().

#### Stateless events

Both HTTP API and file import send stateless events because the `tealium_visitor_id` value is not automatically assigned. For HTTP API requests, each event generates a new visitor profile unless `tealium_visitor_id` is set. In these cases, we recommend generating your own anonymous value for `tealium_visitor_id`.

File import data sources typically include a user identifier that maps to a visitor ID attribute.

If a `tealium_visitor_id` value is not included in an HTTP API request or in a file import mapping, AudienceStream assigns a random value to the anonymous ID and creates a new visitor profile prior to visitor stitching.

## Additional scenarios

### What happens when there are two different visitor ID attribute values during a stitch event?

Two visitor ID attributes are defined. One visitor ID attribute captures the email address and the other captures the X handle.

A user visits a site from a computer and signs up for a newsletter using the `marketer@xyzcorp.com` email address. Within the same session, the user sees a product and tweets about it using the `marketerxyz` X handle. The user uses a tablet later on and submits an order with the email address `name@xyzcorp.com`. The user then tweets about the order using the `marketerxyz` X handle.

A visitor stitching match occurs on the X handle. The X handles are the same, but the email addresses are not. What happens now?

#### Answer
The two profiles from the two devices are stitched together based on the X handle.

When the primary stitched profile is created, two secondary IDs are created, one for the X handle and one for the email address. The X handle secondary ID is set to `marketerxyz` because the handle is the same on both devices.

During visitor stitching, all past events for the profiles are chronologically ordered and reprocessed. The email secondary ID is set to the first email address encountered during reprocessing, in this case `marketer@xyzcorp.com`.

In the future, either email address can be used to stitch to the visitor profile. This only applies because there were two separate devices, with different email addresses and profiles, which were later stitched together based on the X handle.

### What happens when two visitor profiles are stitched with different attribute values?

What happens when two visitor profiles are stitched and an attribute exists in each profile but with different values? 

For example:

* On the desktop device, &#34;Opt-In Status&#34; flag is &#34;True&#34;
* On the mobile device, &#34;Opt-In Status&#34; flag is &#34;False&#34;

#### Answer

First, it’s important to note a few important system functionalities.

* As events feed into AudienceStream, these events are used to create a visitor profile.
* When a visitor’s visit expires, both the visitor and all of the events of their visit are stored in two different DB collections (separate from EventStore logs).
* Over the lifetime of a visitor there can be hundreds or even thousands of events, and a majority of the time these persisted events are never used and will expire when the visitor profile expires.

With that foundation set we can now discuss what occurs upon a stitching event. When matching profiles are found, AudienceStream will load up all past events for all of the visitors being stitched, sort each event chronologically, and replay all events to create a primary stitched profile.

So back to the question, whether the `Opt-In Status` flag will be set to `True` or `False`. The answer is that it depends on the outcome of all of the enrichments that are reprocessed when AudienceStream replays all of these visitors&#39; past events.

#### More notes and possible questions

You may be curious about more advanced attributes such as `list` and `tally`. Even though `tally` and `list` attributes look like they are merged, it&#39;s because they are setup using additive enrichments (add to list, increment tally, etc.). These have typically been correctly stitched in the past.

Depending on how many events there are, stitching can take awhile to execute as it&#39;s an extremely complex and CPU heavy task to execute. However, over the past couple of years Engineering has made numerous optimizations to make this stitching process more efficient. Typically, it is a very quick process.

Does this mean stitching is backwards compatible? Imagine this scenario of events:

* Customer registers on a website on their desktop

  * customer_type is passed to AS
  * customer_email is passed to AS

* Within AudienceStream

  * Visitor ID is assigned using customer_email
  * customer_type is ignored

* 1 week later a Trait is created that stores the `customer_type`
* 2 weeks later the visitor authenticates on Mobile with the same `customer_email` value (but no `customer_type` is passed)
* We stitch the desktop and mobile profiles together

The Trait capturing `customer_type` will not have existed in either device&#39;s visitor profile. However, when AS reprocesses all the events, AudienceStream will use the latest AudienceStream profile definition and re-evaluate the Trait&#39;s enrichment. This means the primary visitor profile will now have the Trait storing the `customer_type`.

#### How does this affect Omnichannel data?

Omnichannel data is considered event data and it will behave in the same manner, meaning the event data will persist in the Event Database and chronologically be a part of the online event data.

#### How does this affect timeline timestamps and audiences joined/left dates in AudienceStore?

The timestamps represent when the singular event occurred, not when the stitching event occurred.
