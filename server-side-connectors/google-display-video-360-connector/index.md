---
title: Google Display and Video 360 Connector Setup Guide
description: This article describes how to set up the Google Display & Video 360 connector in your Customer Data Hub account.
url: https://docs.tealium.com/server-side-connectors/google-display-video-360-connector/
---
## Requirements

To grant Tealium access to create, list, and update Google audiences, link your account to Tealium in the Google DV360 interface (**Linked Accounts &gt; Link New Account &gt; External Data Partner &gt; Tealium**). For more information, see [Google: Sharing audience lists from external data management platforms or customer match uploader partners](https://support.google.com/displayvideo/answer/9649053?hl=en).

 Previously, this connector required that you request for Google to add your account to their allowlist. The latest version of the connector no longer has this requirement. 

## API Information

This connector uses the following vendor APIs:

* User List Operations (creation/listing)
  * API Name: Google Data Manager API
  * API Version: v1
  * API Endpoint: `https://datamanager.googleapis.com`
  * Documentation: [Google Data Manager API](https://developers.google.com/data-manager/api)
* User List Uploading
  * API Name: Google Authorized Buyers
  * API Version: v2
  * API Endpoint: `https://cm.g.doubleclick.net/upload`
  * Documentation: [Google Authorized Buyers API](https://developers.google.com/authorized-buyers/rtb/bulk-uploader)

It may take up to 72 hours from when the connector fires before the visitor becomes available for use. &lt;br&gt;
For more information, see [Tips for using third-party audience lists](https://support.google.com/displayvideo/answer/6212219?hl=en&amp;amp;ref_topic=2726036).

## Configuration

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

When you add this connector, you must accept the vendor&#39;s data platform policy that appears.

After adding the connector, configure the following settings:

* **Client Customer ID**
  * (Required) Your customer identifier in the selected product
* **Select the Target Product**
  * (Required) The account that establishes a connection must have access to the target product selected.
* **Google Network ID**
  * (Optional)
  * If you use the Google-hosted version of the Google Cookie Matching tag, enter your Google Network ID.
  * If you use the Tealium-hosted version of the Google Cookie Matching tag, leave this blank.

### Create a New Segment

Use the following steps to create a new segment in AudienceStream:

1. Click **Create a New Segment** from the top of the **Actions** selection drop-down list.
2. Enter the **Segment Name**, **Segment Member Lifespan**, **Integration Code**, and **Segment Description**.  
![](/images/server-side-connectors/audiencestream-create-segment.jpg)
If you use a [DataAccess]() product (EventStore, AudienceStore, EventDB, or AudienceDB), the segment name must be fewer than 128 characters in length. Otherwise, DataAccess may trim the segment name and errors may occur.
3. Click **Create Segment**.  
The Integration Code is an ID used by user list sellers to correlate IDs on their systems. If no ID is available, you can manually enter a random number between `1` and `1000`. Confirmation will appear in the form of a check mark next to the Create Segment button to verify that the segment has been created.

Allow 3 to 4 hours before using new audiences within an action when you create a new Google Display &amp;amp; Video 360 audience. When your audience list is visible inside Google Display &amp;amp; Video 360, you can then use your audience without error. For more information, see [Google Display &amp;amp; Video Help: Audience list targeting](https://support.google.com/displayvideo/answer/2949947?hl=en).

## Actions

| Action Name | AudienceStream | EventStream |
| ----------- | :------------: | :---------: |
| Add Visitor to User-List or Segment | ✓ | ✓ |
| Remove Visitor from User-List or Segment | ✓ | ✓ |

### Add Visitor to User-List or Segment

#### Parameters

 You must use one of the following ID parameters: **Partner Provided ID (already MD5 hashed)**, **Partner Provided ID (apply MD5 hash)**, **Google User ID**, **iOS Advertising ID**, **Android Advertising ID**, **RIDA**, **AFAI**, or **MSAI**. 

| Parameter | Description |
|---| ---|
| Select the Target User-list/Segment | (Required) User map identifier. Specifies the user that this operation applies to. This is the target User-list/Segment where the user will be added to. |
| Partner Provided ID (already MD5 hashed) | This parameter is sent to Google by the Tealium iQ cookie matching service tag. The default cookie match tag implementation sends the Tealium Visitor ID as an MD5 hash. If you are using this ID as the default, map this attribute to the MD5 hash option. |
| Partner Provided ID (apply MD5 hash) | This parameter is similar to **Partner Provided ID (already MD5 hashed)**, except that it will MD5 hash the value for you. |
| Google User ID | Google User ID. Provided by the ADX cookie-matching service. |
| iOS Advertising ID | iOS Advertising ID. |
| Android Advertising ID | Android Advertising ID. |
| RIDA | Roku ID. |
| AFAI | Amazon Fire TV ID. |
| MSAI | Xbox/Microsoft ID. |
| Data Source ID | (Optional) An ID indicating the data source that contributed this membership. Required to be in the range of `1` to `1,000`. Any ID greater than `1,000` results in a `BAD_DATA_SOURCE_ID` error. These IDs do not have reference or meaning for Google and are only used as labels for reporting purposes. |

##### Consent

When using the **Add Visitor to User List** action, the connector will send consent as `true`. Use audience logic to prevent non-consented visitors from being added to lists. Use the **Remove Visitor from User List** action to remove non-consented visitors from lists.

### Remove Visitor from User-List or Segment

#### Parameters

| Parameter | Description |
|---| ---|
| Select the Target User-list/Segment | (Required) This is the target User-list/Segment where the user will be removed from. |
| Google User ID | Google User ID. Provided by the ADX cookie-matching service. |
| Data Source ID | (Optional) An ID indicating the data source that contributed this membership. Required to be in the range of `1` to `1,000`. Any ID greater than `1,000` results in a `BAD_DATA_SOURCE_ID` error. These IDs do not have reference or meaning for Google and are only used as labels for reporting purposes. |
