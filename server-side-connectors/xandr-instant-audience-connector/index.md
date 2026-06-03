---
title: Xandr Instant Audience Service Connector
description: This article describes how to set up the Xandr Instant Audience Service connector.
url: https://docs.tealium.com/server-side-connectors/xandr-instant-audience-connector/
---
The underlying integration for this connector uses Xandr Instant Audience Service functionality that is in the Alpha-Beta phase and is therefore subject to change. [Learn more](https://learn.microsoft.com/en-us/xandr/data-providers/instant-audience-service)

## How it works

The Xandr Instant Audience Service is a server-side method that uses streaming architecture to add individual or small groups of users to segments using the Xandr API. Rather than aggregating and periodically sending large batches of data using the Batch Segment Service, the Xandr Instant Audience Service associates users to segments in near real-time.

## Prerequisites

* Xandr Member ID shared with Tealium&#39;s Xandr member ID.

## Action Endpoint

```
https://streaming-data.appnexus.com/rt-segment
```

### Batching and Rate Limits

This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* 500 records
* 10 minutes
* Greater than (&amp;gt;) 1MB

## Getting Started

### Obtain Authorization

To use the Xandr Instant Audience Service and enable this integration, you need to open a ticket with Xandr to have your member shared with Tealium&#39;s Member (`9537`).

Provide the following information in a [support request to Xandr](https://help.xandr.com/):

1. Any external user IDs.
    * For example, if you use a `mapUID` to store the mapping with Xandr.
    * If you use the external user ID of another member, include their `member_id`.
1. Segments that belong to other members.
    * Provide the associated `member_ids`. Tealium&#39;s Member ID is `9537`.
1. The default expiration of your segments.
    * For example, never expire, expire 60 days from now, etc.
    * If you include `EXPIRATION` in your `seg` block, your default expiration will not be used.
1. Internal capacity planning estimates:
    * The number of unique user IDs per post.
    * The number of expected posts per day.
    * The number of unique segments per post.

Xandr typically responds to these requests within one to three  business days.

## Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 500
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Add User to Segment| ✓| ✓|
|Remove User From Segment| ✓| ✓|

## Configure Settings

Navigate to the **Connector Marketplace** and add a new connector. For general instructions on how to add a connector, see the [About Connectors]() article.

After selecting your source, click **Continue** and then **Add Connector**. Enter a name for the connector.

Click **Done** when you are finished configuring the connector.

## Action Settings - Parameters and Options

Click **Continue** to configure the connector actions. Enter in a name for the action and then select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Action - Add User to Segment

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|AAID|  &lt;ul&gt;&lt;li&gt;Android Advertising Identifier.&lt;/li&gt;&lt;li&gt;The mobile device ID for Android devices.&lt;/li&gt;&lt;li&gt;Example: `AEBE52E7-03EE-455A-B3C4-E57283966239`&lt;/li&gt;&lt;/ul&gt; |
|Xandr/AppNexus User ID|  &lt;ul&gt;&lt;li&gt;The User ID returned by the cookie match endpoint.&lt;/li&gt;&lt;li&gt;Example: `12345678900987654321`&lt;/li&gt;&lt;li&gt;In addition to configuring the connector, we recommend pairing with the Cookie Match tag. This tag performs a cookie sync to exchange device IDs, which facilitates the server-to-server actions described below. ([Learn more]()) &lt;/li&gt;&lt;/ul&gt; |
|IDFA|  &lt;ul&gt;&lt;li&gt;Identifier for Advertisers.&lt;/li&gt;&lt;li&gt;The mobile device ID for iOS devices.&lt;/li&gt;&lt;li&gt;Example: `6D92078A-8246-4BA4-AE5B-76104861E7DC`&lt;/li&gt;&lt;/ul&gt; |
|MD5 UDID|  &lt;ul&gt;&lt;li&gt;The MD5 hashed value of the User ID.&lt;/li&gt;&lt;li&gt;Example: `4a8a2b374f463b7aedbb44a066363b81`&lt;/li&gt;&lt;/ul&gt; |
|Open UDID|  &lt;ul&gt;&lt;li&gt;Deprecated, do not use.&lt;/li&gt;&lt;/ul&gt; |
|SH1 UDID|  &lt;ul&gt;&lt;li&gt;The SHA1 hashed value of the User ID.&lt;/li&gt;&lt;li&gt;Example: `F12877BFFD9C07E7224C9A6EFB7A709F4E29FDEA`&lt;/li&gt;&lt;/ul&gt; |
|SHA1 MAC|  &lt;ul&gt;&lt;li&gt;Deprecated, do not use.&lt;/li&gt;&lt;/ul&gt; |
|Tealium Visitor ID|  &lt;ul&gt;&lt;li&gt;Deprecated, do not use.&lt;/li&gt;&lt;/ul&gt; |
|Expiration|  &lt;ul&gt;&lt;li&gt;The lifetime of the user-segment association in minutes, starting from when we read it.&lt;/li&gt;&lt;li&gt;A value of zero (`0`) means that the segment never expires.&lt;/li&gt;&lt;li&gt;A value of negative one (`-1`) means that the user is to be removed from this segment.&lt;/li&gt;&lt;li&gt;Example: `1440`&lt;/li&gt;&lt;/ul&gt; |
|Member ID|  &lt;ul&gt;&lt;li&gt;The ID of the member that owns this segment or has been shared the segment by data provider Tealium.&lt;/li&gt;&lt;li&gt;Example: `9537`&lt;/li&gt;&lt;/ul&gt; |
|Segment Code|  &lt;ul&gt;&lt;li&gt;A user-defined name for the segment.&lt;/li&gt;&lt;li&gt;Example: `mysegment-003`&lt;/li&gt;&lt;/ul&gt; |
|Segment ID|  &lt;ul&gt;&lt;li&gt;The segment ID.&lt;/li&gt;&lt;li&gt;Example: `12693755`&lt;/li&gt;&lt;/ul&gt; |
|Value|  &lt;ul&gt;&lt;li&gt;A numeric value that you assign to a segment.&lt;/li&gt;&lt;li&gt;Example: &lt;/li&gt;&lt;/ul&gt; |

### Action - Remove User From Segment

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|AAID|  &lt;ul&gt;&lt;li&gt;Android Advertising Identifier.&lt;/li&gt;&lt;li&gt;The mobile device ID for Android devices.&lt;/li&gt;&lt;li&gt;Example: `AEBE52E7-03EE-455A-B3C4-E57283966239`&lt;/li&gt;&lt;/ul&gt; |
|Xandr/AppNexus User ID|  &lt;ul&gt;&lt;li&gt;The User ID returned by the cookie match endpoint.&lt;/li&gt;&lt;li&gt;Example: `12345678900987654321`&lt;/li&gt;&lt;/ul&gt; |
|IDFA|  &lt;ul&gt;&lt;li&gt;Identifier for Advertisers.&lt;/li&gt;&lt;li&gt;The mobile device ID for iOS devices.&lt;/li&gt;&lt;li&gt;Example: `6D92078A-8246-4BA4-AE5B-76104861E7DC`&lt;/li&gt;&lt;/ul&gt; |
|MD5 UDID|  &lt;ul&gt;&lt;li&gt;The MD5 hashed value of the User ID.&lt;/li&gt;&lt;li&gt;Example: `4a8a2b374f463b7aedbb44a066363b81`&lt;/li&gt;&lt;/ul&gt; |
|Open UDID|  &lt;ul&gt;&lt;li&gt;Deprecated, do not use.&lt;/li&gt;&lt;/ul&gt; |
|SH1 UDID|  &lt;ul&gt;&lt;li&gt;The SHA1 hashed value of the User ID.&lt;/li&gt;&lt;li&gt;Example: `F12877BFFD9C07E7224C9A6EFB7A709F4E29FDEA`&lt;/li&gt;&lt;/ul&gt; |
|SHA1 MAC|  &lt;ul&gt;&lt;li&gt;Deprecated, do not use.&lt;/li&gt;&lt;/ul&gt; |
|Tealium Visitor ID|  &lt;ul&gt;&lt;li&gt;Deprecated, do not use.&lt;/li&gt;&lt;/ul&gt; |
|Segment ID|  &lt;ul&gt;&lt;li&gt;The segment ID.&lt;/li&gt;&lt;li&gt;Example: `12693755`&lt;/li&gt;&lt;/ul&gt; |
|Segment Code|  &lt;ul&gt;&lt;li&gt;A user-defined name for the segment.&lt;/li&gt;&lt;li&gt;Example: `mysegment-003`&lt;/li&gt;&lt;/ul&gt; |
|Member ID|  &lt;ul&gt;&lt;li&gt;The ID of the member that owns this segment or has been shared the segment by data provider Tealium.&lt;/li&gt;&lt;li&gt;Example: `9537`&lt;/li&gt;&lt;/ul&gt; |

## Frequently Asked Questions

### What are some example use cases that this integration supports?

* **Search or time-sensitive retargeting in RTB**  
As a buyer or DMP, this service is useful if you would like to mimic search retargeting capabilities. As a user enters search keywords, you receive a server-side signal that triggers a server-side association to the segments. The user can then see ads that are relevant to their search, which enables you to capitalize on the immediate relevancy of the content for the user.
* **Page performance sensitive targeting**  
Use this service if you want to avoid page load strain, but still want to be able to conduct retargeting without increasing the pixels present on the page.
* **Alternative real-time audience targeting**  
The Instant Audience Service can also be used for transactional retargeting, in which user scores are computed based on offline data or modeling. This only requires an additional trigger to have the user added to a segment that you want to buy against in real-time.  
A concrete example is, based on Clickstream data, a buyer computes a score for a user that has browsed three products in the kitchen category of its site and pushes a segment value to based on this user score to immediately show them an ad for additional kitchen items.
* **De-targeting users who have converted**  
This service lets you use your budget as efficiently as possible by quickly de-targeting users that have already converted.

### How often do User IDs expire?

 UIDs expire on a rolling basis, so user IDs that have not been seen for the longest period of time are removed from our database to make room for new user IDs. If you upload UIDs that are very old, you may have a high percentage of invalid user IDs in your status report. Tealium keeps your cookie mapping fresh by requesting new UIDs at the start of each session.

### How quickly are updates to segments activated by Xandr?

Xandr sets its target Service Level Agreement (SLA) for adding users to segments with the Xandr Instant Audience Service to two minutes. To adhere to a maximum of two minutes activation time, the Instant Audience Service currently has some limits, which Tealium has incorporated into the batching functionality. For additional details, see the Batching and Rate Limits section above.
