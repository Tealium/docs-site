---
title: DoubleClick Ad Exchange Connector Setup Guide
description: This article describes how to set up the DoubleClick for Ad Exchange connector in your Customer Data Hub account.
url: https://docs.tealium.com/server-side-connectors/doubleclick-ad-exchange-connector/
---

## Connector actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Add Visitor to User-List or Segment| ✓| ✓|
|Remove Visitor from User-List or Segment| ✓| ✓|

## API information

This connector uses the following vendor API:

* API Name: Google Audience Partner API DmpUserListService
* API Version: v201809
* API Endpoint: `&lt;https://ddp.googleapis.com/&gt;`
* Documentation: [Authorized Buyer (formerly DoubleClick Ad Exchange) API](https://developers.google.com/authorized-buyers/)

## Configure settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors]() article.

When you add this connector you are prompted to accept the vendor&#39;s data platform policy.

After adding the connector, configure the following settings:

* **Client Customer ID (Required)**
  * Your (DoubleClick Customer) Identifier in the selected product.

* **Select the Target Product (Required)**
  * The target product, either **DoubleClick AdExhchange - Buyer** or **DoubleClick AdExchange - Publisher**.

## Create a new segment

Use the following steps to create a new segment in AudienceStream:

1. Click **Create a New Segment** from the top of the Actions selection drop-down screen.
2. Enter the **Segment Name**, **Segment Member Lifespan**, **Integration Code**, and **Segment Description**.  If you use a [DataAccess]() product (EventStore, AudienceStore, EventDB, or AudienceDB), the segment name must be fewer than 128 characters in length. Otherwise, DataAccess may trim the segment name and errors may occur.
![](/images/server-side-connectors/audiencestream-create-segment.jpg)
3. Click **Create Segment**.  
The Integration Code is an ID used by user list sellers to correlate IDs on their systems. If no ID is available, you can manually enter a random number between 1 and 1,000. Confirmation displays in the form of a check mark next to the Create Segment button to verify that the segment has been created.

## Action settings - parameters and options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Add Visitor to User-List or Segment

#### Parameters

|**Parameter**|  * **Description** |
|---| ---|
|Select the Target User-list/Segment|  &lt;ul&gt;&lt;li&gt;(Required) User map identifier.&lt;/li&gt;&lt;li&gt;Specifies the user that this operation applies to.&lt;/li&gt;&lt;li&gt;This is the target User-list/Segment where the user will be added to.&lt;/li&gt;&lt;/ul&gt; |
|Google User ID|  &lt;ul&gt;&lt;li&gt;Google User ID&lt;/li&gt;&lt;li&gt;Provided by the ADX cookie-matching service.&lt;/li&gt;&lt;/ul&gt; |
|iOS Advertising ID|  &lt;ul&gt;&lt;li&gt;iOS Advertising ID&lt;/li&gt;&lt;/ul&gt; |
|Android Advertising ID|  &lt;ul&gt;&lt;li&gt;Android Advertising ID&lt;/li&gt;&lt;/ul&gt; |
|RIDA|  &lt;ul&gt;&lt;li&gt;Roku ID&lt;/li&gt;&lt;/ul&gt; |
|AFAI|  &lt;ul&gt;&lt;li&gt;Amazon Fire TV ID&lt;/li&gt;&lt;/ul&gt; |
|MSAI|  &lt;ul&gt;&lt;li&gt;Xbox/Microsoft ID&lt;/li&gt;&lt;/ul&gt; |
|Data Source ID|  &lt;ul&gt;&lt;li&gt;(Optional) An ID indicating the data source that contributed this membership.&lt;/li&gt;&lt;li&gt;Required to be in the range of 1 to 1,000.&lt;/li&gt;&lt;li&gt;Any ID greater than 1,000 results in a BAD_DATA_SOURCE_ID error.&lt;/li&gt;&lt;li&gt;These IDs do not have reference or meaning for Google and are only used as labels for reporting purposes.&lt;/li&gt;&lt;/ul&gt; |

### Action - Remove Visitor from User-List or Segment

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Select the Target User-list/Segment|  &lt;ul&gt;&lt;li&gt;Required, this is the target User-list/Segment where the user will be removed from.&lt;/li&gt;&lt;/ul&gt; |
|Google User ID|  &lt;ul&gt;&lt;li&gt;Google User ID&lt;/li&gt;&lt;li&gt;Provided by the ADX cookie-matching service.&lt;/li&gt;&lt;/ul&gt; |
|iOS Advertising ID|  &lt;ul&gt;&lt;li&gt;iOS Advertising ID&lt;/li&gt;&lt;/ul&gt; |
|Android Advertising ID|  &lt;ul&gt;&lt;li&gt;Android Advertising ID&lt;/li&gt;&lt;/ul&gt; |
|RIDA|  &lt;ul&gt;&lt;li&gt;Roku ID&lt;/li&gt;&lt;/ul&gt; |
|AFAI|  &lt;ul&gt;&lt;li&gt;Amazon Fire TV ID&lt;/li&gt;&lt;/ul&gt; |
|MSAI|  &lt;ul&gt;&lt;li&gt;Xbox/Microsoft ID&lt;/li&gt;&lt;/ul&gt; |
|Data Source ID|  &lt;ul&gt;&lt;li&gt;(Optional) An ID indicating the data source that contributed this membership.&lt;/li&gt;&lt;li&gt;Required to be in the range of 1 to 1,000.&lt;/li&gt;&lt;li&gt;Any ID greater than 1,000 results in a BAD_DATA_SOURCE_ID error.&lt;/li&gt;&lt;li&gt;These IDs do not have reference or meaning for Google and are only used as labels for reporting purposes.&lt;/li&gt;&lt;/ul&gt; |
