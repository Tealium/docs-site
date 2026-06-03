---
title: LinkedIn Matched Audiences Connector Setup Guide
description: This article describes how to set up the LinkedIn Matched Audiences connector.
url: https://docs.tealium.com/server-side-connectors/linkedin-matched-audiences-connector/
---
## How it works

LinkedIn offers a centralized Data Management Platform (DMP) platform that aggregates LinkedIn advertiser data. DMP Segments act as staging entities, which can take in user information from a third-party provider, map them to LinkedIn member profiles, and output Ad Segments, which can then be used with other LinkedIn Ads APIs. This integration lets you map between user information from LinkedIn advertisers and LinkedIn member profiles. The LinkedIn Matched Audiences connector provides the ability to manage users and companies for insertion into DMP Segments.

Users can be matched with hashed email addresses to their LinkedIn account for targeting. The Email Address parameter supports non-hashed email addresses with hashing that can be applied when the connector action fires, as well as SHA-256 or SHA-512 already-hashed addresses.

Additional identifiers, such as the Android Ad ID (GAIDs) and First name &#43; Last name, can be used to match a user in a DMP segment. If no valid user ID is provided, the First Name and Last Name parameters **must** be provided.

Companies can be matched on company name, company domain, company website, or their LinkedIn organization URN.

### Considerations

* AudienceStream will display the DMP Segment status in the dropdown population when a segment is retrieved. For more information about the meaning of Audience segment status messages, see [DMP Segment State Transition flow for a DMP Segment](https://docs.microsoft.com/en-us/linkedin/marketing/integrations/matched-audiences/matched-audiences?view=li-lms-2022-08).
* AudienceStream will only display Tealium-created Audience segments.
* The minimum audience size that can be used in a campaign is 300 members.
* After you create a DMP segment, you must wait 5 seconds for the segment to be available to add users or companies.
* While you may be able to subscribe a user or a company to a DMP Audience that is not in `READY` status, Segments with `EXPIRED`, `FAILED`, or `ERROR` status are not allowed to be included in or excluded from a campaign&#39;s targeting.
* Authentication access is valid for 365 days. Once authentication access expires, the user will be required to re-authenticate.

### Match rates and audience size

* It is important to understand the subtle difference between `audienceSize` and `matchedCount` values. If any change occurs on the segment, matched count and input count are calculated based on data collected from the past 7 days, in a rolling 7-day window.
* Audience size is based on all input data. Audience volumes sent by the Connector action may not align with the matched count returned in the Audience insights.
* If your match rate is high, but your audience size is 0, it is likely the targeted members have opted out of third-party targeting on LinkedIn. In some cases this may bring your lists below the 300 member threshold.
* In addition, audience count takes opt-out instances into account, while match count doesn&#39;t. For more information regarding summary differences between the `audienceSize` and `matchedCount` values, see [Differences Between Audience Size and Matched Count Fields](https://docs.microsoft.com/en-us/linkedin/marketing/integrations/matched-audiences/create-and-manage-segment-destinations?view=li-lms-2022-08&amp;amp;tabs=http#differences-between-audience-size-and-matched-count-fields).
* Lookalike segment creation will require a DMP Segment must be in READY status with at least 200 audience count to be used as a seed segment.

## API information

This connector uses the following vendor API:

* API Name: LinkedIn API
* API Version: 202601
* API Endpoint: `https://api.linkedin.com/rest`
* Documentation: [LinkedIn Marketing API](https://docs.microsoft.com/en-us/linkedin/marketing/)

## Batch limits

This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 5000.
* Rate Limit: 500 requests per user for user actions, 200 requests per user for company actions.
* Max time since oldest request: 60 minutes.
* Max size of requests: 100 MB.

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

## Create DMP segment

DMP Segments act as staging entities, which can take in user information from Tealium, map them to LinkedIn member profiles, and output Ad Segments, which can then be used with other LinkedIn Ads APIs. A DMP segment is tied to a sponsored account.

DMP Segment Users is a sub-resource of DMP segments and lets you add users to a DMP Segment.

### Parameters

|Parameter| Description|
|---| ---|
|Segment Name| (Required) The name of the DMP Segment to appear in the LinkedIn Ads account.|
|Segment Type|  (Required) Select the source platform from where users profiles are being imported. Supports: &lt;ul&gt;&lt;li&gt;**Standard** - Populates as a Tealium-supplied list in your Ads account.&lt;/li&gt;&lt;li&gt;**LookAlike** - Based on an existing audience segment, advertisers can expand the group of audience.&lt;/li&gt;&lt;/ul&gt; |
|Segment Description|  (Optional) A description for the DMP segment |
|Source Segment ID|  (Optional) &lt;ul&gt;&lt;li&gt;This field is only applicable for LookAlike Segment Types.&lt;/li&gt;&lt;li&gt;The foreign key on the source platform. This is an optional field that will be indexed and can be used by the source platform to find their segments.&lt;/li&gt;&lt;/ul&gt; |
|Segment Content Type|  The content type of the profiles being imported into the DMP segment. &lt;ul&gt;&lt;li&gt;Default content type: `USER`.&lt;/li&gt;&lt;li&gt;Supports User and Company lists.&lt;/li&gt;&lt;/ul&gt; |

## Create Lookalike Seed Segment

DMP Segment lookalike is typically useful for advertisers who want to increase their reach. Based on an existing audience segment, advertisers can expand the group of an audience by leveraging a DMP Segment lookalike. DMP Segment lookalike takes in an existing Ad Segment as a seed and constructs an audience similar to the seed audience. The process may take up to 48 hours.

You will need a DMP Segment (or an adSegment for website retargeting cases) in `READY` status with at least a 300 audience count to use as a seed.

### Parameters

|Parameter| Description|
|---| ---|
|Lookalike Segment| (Required) The Lookalike segment name you want to create.|
|Seed DMP Segment|  (Required) Select a seed DMP segment to use as the seed segment to create an audience similar to the seed audience. &lt;ul&gt;&lt;li&gt;The DMP Segment must be in `READY` status with at least a 200 audience count to use as a seed.&lt;/li&gt;&lt;/ul&gt; |

## Configuration

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors]() article.

After adding the connector, configure the following settings:

* **Ad Account**  
(Required) Select an Ad Account ID that aligns with your sponsored account.

Click **Done** when you are finished configuring the connector.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Add User to DMP Segment| ✓| ✗|
|Remove User from DMP Segment| ✓| ✗|
|Add Company to DMP Segment| ✓| ✗|
|Remove Company from DMP Segment| ✓| ✗|

Click **Continue** to configure the connector actions. Enter in a name for the action and then select the action type.

The following section describes how to set up parameters and options for each action.

### Add User to DMP Segment

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|DMP Segment| Select DMP Segment to add user to.|
|Email Address (already SHA256 hashed)| An cleartext email address (must include an `@`) that has already been SHA256 hashed.|
|Email Address (apply SHA256 hash)| A plain text email address which the connector will whitespace trim, lowercase, and hash using SHA256 hash.|
|Email Address (already SHA512 hashed)| An cleartext email address (must include an `@`) that has already been SHA512 hashed.|
|Email Address (apply SHA512 hash)| A plain text email address which the connector will whitespace trim, lowercase, and hash using SHA512 hash.|
|Android Ad ID| A plain text Android Ad ID.|
|First Name| A plain text string that represents the first name of the contact to match, in 35 characters or less.|
|Last Name| A plain text string that represents the last name of the contact to match, in 35 characters or less.|
|Title| A plain text string that represents the contact&#39;s title, in 50 characters or less.|
|Company| A plain text string that represents the contact&#39;s company name, in 50 characters or less.|
|Country| An ISO standardized two-letter country code.|

### Remove User from DMP Segment

#### Parameters

You must provide a valid Android ID or provide a valid first name or last name to match.

|**Parameter**| **Description**|
|---| ---|
|DMP Segment| Select the DMP Segment to remove the user from.|
|Email Address (already SHA256 hashed)| An cleartext email address (must include an `@`) that has already been SHA256 hashed.|
|Email Address (apply SHA256 hash)| A plain text email address which the connector will whitespace trim, lowercase, and hash using SHA256 hash.|
|Email Address (already SHA512 hashed)| An cleartext email address (must include an `@`) that has already been SHA512 hashed.|
|Email Address (apply SHA512 hash)| A plain text email address which the connector will whitespace trim, lowercase, and hash using SHA512 hash.|
|Android Ad ID| A plain text Android Ad ID.|
|First Name| A plain text string that represents the first name of the contact to match, in 35 characters or less.|
|Last Name| A plain text string that represents the last name of the contact to match, in 35 characters or less.|
|Title| A plain text string that represents the contact&#39;s title, in 50 characters or less.|
|Company| A plain text string that represents the contact&#39;s company name, in 50 characters or less.|
|Country| An ISO standardized two-letter country code.|

### Add Company to DMP Segment

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|DMP Segment| Select the DMP Segment to add the company to.|
|Company Name| A string that represents the company name.|
|Company Website Domain| A URL-encoded string that represents the company website&#39;s domain.|
|Company Email Domain| A URL-encoded string that represents the company email&#39;s domain.|
|Organization URN| The LinkedIn company page URN of this particular company. The connector will append `urn:li:organization:` if the value is provided without a `urn` prefix.|
|Company Page Url| The LinkedIn company page URL of this company, in 100 characters or less.|
|Stock Symbol| The company&#39;s stock symbol, in 5 characters or less.|
|Industries| A single or array attribute of up to three industry names that this company belongs to, each in 50 characters or less.|
|City| The company&#39;s city, in 50 characters or less.|
|State| The company&#39;s state or province, in 50 characters or less.|
|Country| The company&#39;s ISO standardized two-letter country code.|
|Postal Code| The company&#39;s postal code, in 20 characters or less.|

### Remove Company from DMP Segment

#### Parameters

|Parameter| Description|
|---| ---|
|DMP Segment| Select DMP Segment to remove company from.|
|Company Name| A string that represents the company name.|
|Company Website Domain| A URL-encoded string that represents the company website&#39;s domain.|
|Company Email Domain| A URL-encoded string that represents the company email&#39;s domain.|
|Organization URN| The LinkedIn company page URN of this particular company. The connector will append `urn:li:organization:` if the value is provided without a `urn` prefix.|
|Company Page Url| The LinkedIn company page URL of this company, in 100 characters or less.|
|Stock Symbol| The company&#39;s stock symbol, in 5 characters or less.|
|Industries| A single or array attribute of up to three industry names that this company belongs to, each in 50 characters or less. |
|City| The company&#39;s city, in 50 characters or less.|
|State| The company&#39;s state or province, in 50 characters or less.|
|Country| The company&#39;s ISO standardized two-letter country code.|
|Postal Code| The company&#39;s postal code, in 20 characters or less.|
