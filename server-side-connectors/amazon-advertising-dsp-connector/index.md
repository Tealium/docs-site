---
title: Amazon Advertising DSP Connector Setup Guide
description: This article describes how to set up the Amazon Advertising DSP connector.
url: https://docs.tealium.com/server-side-connectors/amazon-advertising-dsp-connector/
---

<blockquote>
This connector is now deprecated. For the current connector, see [Amazon Ads Audience Management connector](https://docs.tealium.com/amazon-ads-audience-management-connector/).
</blockquote>


The Amazon Ads API enables Amazon advertisers and members of the Amazon Advertising Partner Network to programmatically manage advertising operations. Tealium’s integration with Amazon Ads Data Provider API allows clients to add and remove visitors from audiences within Amazon Ads DSP.

## Connector actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Add Hashed Record| ✓| ✗|
|Add to Audience| ✓| ✗|
|Remove from Audience| ✓| ✗|

## Configure settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors](https://docs.tealium.com/about-connectors/) article.


<blockquote>
When you add this connector, you will be prompted to accept the vendor's data platform policy.
</blockquote>


After adding the connector, configure the following settings:

* **API Base URLs**  
Select your API Base URL.

* **Amazon Advertiser ID**  
Enter your Amazon Advertising account ID.

You must also establish a connection to Amazon. Click **Establish Connection** and follow the directions on the page to connect the Tealium Connector App to your Amazon Advertising account.

Click **Done** when you are finished configuring the connector.

## Action settings — parameters and options

Click **Continue** to configure the connector actions. Enter a name for the action and then select the action type from the drop-down menu.

The Amazon Advertising DSP connector supports the following actions:

* Add Hashed Record

* Add to Audience

* Remove from Audience

The following section describes how to set up parameters and options for each action.

### Action — Add Hashed Record

This action is used to send hashed PII and an external identifier (for example, customer ID) to Amazon DSP to match Amazon shoppers with their hashed customer records, including name, email, mobile, address, and zip code. Advertisers can then use the data provider API to add customers to audiences using the previously sent external identifier.

For example, configure a **Known Customer** audience that visitors join when both their email and customer ID are present in their profile. Then configure an Amazon DSP connector with the **Add Hashed Record** action that triggers when a visitor joins the **Known Customer** audience. The connector's action sends the hashed email and the customer ID to Amazon. That customer ID can then be used later to add that visitor to an audience with the **Add to Audience** Amazon DSP connector action.

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 5000
* Max time since oldest request: 10 minutes
* Max size of requests: 5 MB

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|External ID|  <ul><li>The external identifier for this record.</li><li>This can be any ID unique to the record in the caller's own identity space.</li><li>This identifier will be matched to hashed records in Amazon Ads and can then be used to add users to audiences.</li></ul> |
|Email Address (already SHA256 hashed)|  <ul><li>Email address. </li><li>Must be SHA256 Hashed. </li><li>If already hashed, use **Already SHA256 Hashed** option. Provide a value which has been whitespace trimmed, lowercased and hashed using SHA256 hash. </li></ul> |
|Email Address (apply SHA256 hash)|  <ul><li>Email address. </li><li>Must be SHA256 Hashed. </li><li>Use **Apply SHA256 Hash** option with plain text value, the connector will whitespace trim, lowercase and hash this value using SHA256 hash. </li></ul> |
|First Name (already SHA256 hashed)|  <ul><li>First Name. </li><li>Must be SHA256 Hashed. </li><li>If already hashed, use **Already SHA256 Hashed** option. Provide a value which has been whitespace trimmed, lowercased and hashed using SHA256 hash. </li></ul> |
|First Name (apply SHA256 hash)|  <ul><li>First Name. </li><li>Must be SHA256 Hashed. </li><li>Use **Apply SHA256 Hash** option with plain text value, the connector will whitespace trim, lowercase and hash this value using SHA256 hash.</li></ul> |
|Last Name (already SHA256 hashed)|  <ul><li>Last Name. </li><li>Must be SHA256 Hashed. </li><li>If already hashed, use **Already SHA256 Hashed** option. Provide a value which has been whitespace trimmed, lowercased and hashed using SHA256 hash. </li></ul> |
|Last Name (apply SHA256 hash)|  <ul><li>Last Name. </li><li>Must be SHA256 Hashed. </li><li>Use **Apply SHA256 Hash** option with plain text value, the connector will whitespace trim, lowercase and hash this value using SHA256 hash.</li></ul> |
|Street Address (already SHA256 hashed)|  <ul><li>Street Address. </li><li>Must be SHA256 Hashed. </li><li>If already hashed, use **Already SHA256 Hashed** option. Provide a value which has been whitespace trimmed, lowercased and hashed using SHA256 hash. </li></ul> |
|Street Address (apply SHA256 hash)|  <ul><li>Street Address. </li><li>Must be SHA256 Hashed. </li><li>Use **Apply SHA256 Hash** option with plain text value, the connector will whitespace trim, lowercase and hash this value using SHA256 hash.</li></ul> |
|Phone Number (already SHA256 hashed)|  <ul><li>Phone Number. </li><li>Must be SHA256 Hashed. </li><li>If already hashed, use **Already SHA256 Hashed** option. Provide a value which has been whitespace trimmed and hashed using SHA256 hash. </li></ul> |
|Phone Number (apply SHA256 hash)|  <ul><li>Phone Number. </li><li>Must be SHA256 Hashed. </li><li>Use **Apply SHA256 Hash** option with plain text value, the connector will whitespace trim and hash this value using SHA256 hash.</li></ul> |
|City (already SHA256 hashed)|  <ul><li>City. </li><li>Must be SHA256 Hashed. </li><li>If already hashed, use **Already SHA256 Hashed** option. Provide a value which has been whitespace trimmed, lowercased and hashed using SHA256 hash. </li></ul> |
|City (apply SHA256 hash)|  <ul><li>City. </li><li>Must be SHA256 Hashed. </li><li>Use **Apply SHA256 Hash** option with plain text value, the connector will whitespace trim, lowercase and hash this value using SHA256 hash.</li></ul> |
|Postal Code (already SHA256 hashed)|  <ul><li>Postal Code. </li><li>Must be SHA256 Hashed. </li><li>If already hashed, use **Already SHA256 Hashed** option. Provide a value which has been whitespace trimmed, lowercased and hashed using SHA256 hash. </li></ul> |
|Postal Code (apply SHA256 hash)|  <ul><li>Postal Code. </li><li>Must be SHA256 Hashed. </li><li>Use **Apply SHA256 Hash** option with plain text value, the connector will whitespace trim, lowercase and hash this value using SHA256 hash.</li></ul> |
|State (already SHA256 hashed)|  <ul><li>State. </li><li>Must be SHA256 Hashed. </li><li>If already hashed, use **Already SHA256 Hashed** option. Provide a value which has been whitespace trimmed, lowercased and hashed using SHA256 hash. </li></ul> |
|State (apply SHA256 hash)|  <ul><li>State. </li><li>Must be SHA256 Hashed. </li><li>Use **Apply SHA256 Hash** option with plain text value, the connector will whitespace trim, lowercase and hash this value using SHA256 hash.</li></ul> |

#### Hashed attibutes

Mapped values need to be normalized and hashed according to Amazon's [Hashed Audience documentation](https://advertising.amazon.com/dsp/help/ss/en/audiences/advertiser-audiences/advertiser-hashed-audience/#GA6BC9BW52YFXBNE).

### Action — Add to Audience

This action is used to add a visitor to an audience within Amazon DSP. For exaqmple, you can to add a visitor to a specific Amazon DSP audience for retargeting when they reach a certain lifetime spending threshold.

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 2000
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Audience ID|  To use an existing Tealium-created Amazon audience, enter the Tealium audience ID located in an existing Tealium connector action configuration.<br> To create a new audience in Amazon DSP, click **Create Audience** and enter the following information: <ul><li>The name for the new Amazon DSP audience</li><li>A description</li><li>A unique external audience ID</li><li>A comma-separated list of two-letter country codes. This is a DMA-related field that represents the source of the user audience data. The default value is `UNKNOWN`.</li></ul>After you select or create an audience, click **Verify Audience ID** to verify that the audience is correct. |
|External ID| An External ID previously sent to Amazon through hashed matching.|
|MAID| Mobile advertising identifier.|
|Amazon Cookie| Cookie obtained through a cookie sync.|

#### Consent

When using the **Add to Audience** action, the connector sends `GRANTED` for all `amazonConsent` values. To prevent non-consented visitors from being added to audiences, create an audience with rules that check visitor profile consent status. Then use the **Remove from Audience** action to remove visitors that have not given consent.

### Action — Remove from Audience

This action is used to remove a visitor from an audience within Amazon DSP. For example, you can remove a visitor from a specific Amazon DSP audience when they leave an AudienceStream audience so they are not retargeted.

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 2000
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Audience ID| To use an existing Tealium-created Amazon audience, enter its ID and click **Verify Audience ID** to verify that the audience is correct.<br> You can copy the audience ID created in the "Add to Audience" action configuration. Be sure to copy-paste this name from an existing Tealium connector action configuration and not from the ID displayed in the Amazon interface.|
|External ID| An External ID previously sent to Amazon through hashed matching.|
|MAID| Mobile advertising identifier.|
|Amazon Cookie| Cookie obtained through a cookie sync.|

## Integration strategies

There are three options for user identification when adding a visitor to an Amazon DSP audience:

* Cookie ID
* External ID
* MAID

Your integration strategy will differ depending on the user identifier used.

### Cookie ID

The Cookie ID identifier is a first party identifier matched to a third party cookie within the Amazon system, and this Cookie ID identifier can be used to target anonymous visitors on a browser level. The Amazon Advertising Cookie Matching Service TiQ tag provides an easy integration, passing the first party `tealium_visitor_id` to Amazon for matching.

A visit or visitor level attribute can be created to hold this `tealium_visitor_id` value. The attribute is mapped in the Amazon DSP connector to Cookie ID.

### External ID

The External ID is a unique identifier for a visitor, which has first been matched in the Amazon DSP system with hashed PII. This ID can be a client-owned identifier, such as customer ID, or it can be a Tealium-generated identifier, such as `tealium_visitor_id`. The identifier should persist for the lifetime of the visitor and should not change per device.

Prior to using the External ID in an **Add to Audience** action, customers first need to send the ID and hashed PII to Amazon using the **Add Hashed Record** action.

The following two example implementations assume that email is used as the hashed PII and the email address is captured in a visitor-scoped attribute:

#### Customer ID example

The following example assumes `Customer ID` is a visitor-scoped attribute populated by the client’s system:

1. Configure a **Known Customer** audience that visitors join when both `Customer Email` and `Customer ID` are present in their profile.
1. Configure an Amazon DSP connector with the **Add Hashed Record** action that triggers when a visitor joins the **Known Customer** audience.
1. In this action, map `Customer ID` as `External ID` and `Customer Email` as a hashed identifier.
1. The connector's action then sends the hashed email and the customer ID to Amazon.
1. The `Customer ID` value can then be used later to add that visitor to an audience with the **Add to Audience** connector action.

#### Tealium Visitor ID example

1. Configure a visitor-scoped attribute `First Tealium VID`, which captures the `tealium_visitor_id` event attribute if the visitor-scoped attribute is not populated. 
1. Create an audience **Amazon DSP** that visitors join when `First Tealium VID` and `Customer Email` are populated. 
1. Configure up an **Add Hashed Record** action in the Amazon DSP connector to trigger when a visitor joins the **Amazon DSP** audience. 
In this action, map `First Tealium VID` as `External ID` and `Customer Email` as a hashed identifier. 
1. The `First Tealium VID` value can then be used to add visitors to Amazon audiences using the **Add to Audience** connector action.

### MAID

A Mobile Advertising Identifier (MAID) is a unique pseudo-anonymous identifier tied to a mobile phone. Like the Cookie ID, this identifier is device-based and not dependent on PII. Create a visitor-level attribute to persist the MAID identifier, which is then used in the **Add to Audience** connector action as the user identifier.
