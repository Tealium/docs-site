---
title: Facebook Audiences Connector Setup Guide
description: This article describes how to set up the Facebook Audiences connector in your Customer Data Hub account.
url: https://docs.tealium.com/server-side-connectors/facebook-audiences-connector/
---
## API information

This connector uses the following vendor API:

* API Name: Facebook Graph API - Marketing API
* API Version: v25.0
* API Endpoint: `https://graph.facebook.com`
* Documentation: [Facebook Marketing API](https://developers.facebook.com/docs/marketing-api/)

## Batch limits

This connector uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 10000
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

## Configuration

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **Authentication type**: Select the authentication type to use to connect to Facebook. This option is not available in the legacy connectors interface.
    * **SUAT (System User Authentication Token)**: (Recommended) Select this option for a more stable and persistent authentication method. For more information, see [Facebook: Get a System User Access Token](https://developers.facebook.com/docs/news-indexing/guides/access-tokens/).
    * **OAuth2**: This connection generally expires within 60 days, causing unpredictable results for all Facebook Ad actions. You must re-authenticate the connection before it expires to avoid issues. If you select this option, click **Establish Connection** to authenticate with Facebook.  
    Before clicking the **Establish Connection** button, ensure that you are signed into Facebook with the account that is linked with the Ad Account ID that is being used. If this is not the case, issues can arise with the token that is generated.
* **Ad Account ID**: (Required) The Facebook Audiences Account ID you want to manage. For more information, see [Facebook: Find your Facebook ad account ID number](https://www.facebook.com/business/help/1492627900875762).

 Before you can use this connector and build a custom audience in Facebook, you must agree to the [Facebook Custom Audience Terms](https://www.facebook.com/ads/manage/customaudiences/tos.php).

### Create custom audience

You must create your first custom audience on the Facebook site to accept the terms and conditions before you are able to create a custom audience through the connector.

To use your custom audience, it must contain a minimum of 20 entries. If your audience has been created successfully, a small check icon is displayed beside the button.

Click **Create Custom Audience**, then configure the following settings:

* **New Custom Audience Name**: (Required) The name of the custom audience.
* **New Custom Audience Description**: The description of the custom audience.
* **Customer File Source**:
  * `USER_PROVIDED_ONLY`: Use advertiser-collected information directly from customers.
  * `PARTNER_PROVIDED_ONLY`: Use advertiser-sourced information directly from partners, such as agencies or data providers.
  * `BOTH_USER_AND_PARTNER_PROVIDED`: Use advertiser-collected information directly from customers and partner-sourced information, such as agencies.
* **Audience Type**:
  * `VALUE_BASED_AUDIENCE`: Identify customers that share similar behaviors with your highest-value customers.
  * `CUSTOMER_FILE_AUDIENCE`: (Default) Identify customers based on information from the customer file, such as their email address, phone number, or other identifiers.

On the Facebook Audiences site, you have the option to create audiences based on a customer list, website traffic, or app activity. For this example, create your audience based on a customer list.

For more information, see [Meta Business Help Center: Create a customer list custom audience](https://www.facebook.com/business/help/170456843145568?id=2469097953376494).

## Actions

| Action Name | AudienceStream | EventStream |
|---| ---| ---|
|Add User to Custom Audience| ✓| ✗|
|Remove User from Custom Audience| ✓| ✗|
|Opt Out User from All Custom Audiences| ✓| ✗|

Enter a name for the action and select the action type.

The following section describes how to set up parameters and options for each action.

### Add User to Custom Audience

#### Parameters

|Parameter| Description|
|---| ---|
|Custom Audience to Add User To|  &lt;ul&gt;&lt;li&gt;(Required) Select your Target Custom Audience.&lt;/li&gt;&lt;li&gt;Audiences created from customer files are not displayed.&lt;/li&gt;&lt;li&gt;Before you can use this connector and build a custom audience in Facebook, you must agree to the [Facebook Custom Audience Terms](https://www.facebook.com/ads/manage/customaudiences/tos.php).&lt;/li&gt;&lt;/ul&gt; |
|Email Address|  &lt;ul&gt;&lt;li&gt;Identify a user based on their email address.&lt;/li&gt;&lt;/ul&gt; |
|Phone Number|  &lt;ul&gt;&lt;li&gt;Identify a user based on their phone number. Include only digits with country code, area code, and number. For example, `16505551212`.&lt;/li&gt;&lt;/ul&gt; |
|Facebook User ID|  &lt;ul&gt;&lt;li&gt;Identify a user based on their Facebook ID.&lt;/li&gt;&lt;li&gt;You must provide the &#34;Facebook App ID&#34; corresponding to the Facebook User ID (UID) when using this identifier type.&lt;/li&gt;&lt;/ul&gt; |
|Facebook App ID|  &lt;ul&gt;&lt;li&gt;Required if the &#34;Facebook User ID&#34; is used as the user identifier.&lt;/li&gt;&lt;li&gt;See &#34;Facebook User ID&#34;.&lt;/li&gt;&lt;/ul&gt; |
|Mobile Advertiser ID|  &lt;ul&gt;&lt;li&gt;Use this to target a user based on the app user ID, Apple&#39;s Advertising Identifier (IDFA), or Android&#39;s advertising ID.&lt;/li&gt;&lt;/ul&gt; |
|External ID|  &lt;ul&gt;&lt;li&gt;Do not hash.&lt;/li&gt;&lt;li&gt;Any unique ID from the advertiser, such as loyalty membership IDs, user IDs, and external cookie IDs.&lt;/li&gt;&lt;/ul&gt; |
|Zip Code|  &lt;ul&gt;&lt;li&gt;Postal code.&lt;/li&gt;&lt;li&gt;Exact format depends on country.&lt;/li&gt;&lt;/ul&gt; |
|City|  &lt;ul&gt;&lt;li&gt;User City.&lt;/li&gt;&lt;li&gt;Lowercase.&lt;/li&gt;&lt;li&gt;No punctuation or spaces.&lt;/li&gt;&lt;/ul&gt; |
|Country|  &lt;ul&gt;&lt;li&gt;User Country.&lt;/li&gt;&lt;li&gt;2-letter country code.&lt;/li&gt;&lt;li&gt;ISO 3166-1 Alpha-2 format.&lt;/li&gt;&lt;/ul&gt; |
|US State|  &lt;ul&gt;&lt;li&gt;User State in the United States.&lt;/li&gt;&lt;li&gt;Lowercase.&lt;/li&gt;&lt;li&gt;2-character ANSI abbreviation code.&lt;/li&gt;&lt;/ul&gt; |
|First Name|  &lt;ul&gt;&lt;li&gt;User first name.&lt;/li&gt;&lt;li&gt;Lowercase.&lt;/li&gt;&lt;li&gt;No punctuation or special characters.&lt;/li&gt;&lt;li&gt;UTF-8 format.&lt;/li&gt;&lt;/ul&gt; |
|Last Name|  &lt;ul&gt;&lt;li&gt;User last name.&lt;/li&gt;&lt;li&gt;Lowercase.&lt;/li&gt;&lt;li&gt;No punctuation or special characters.&lt;/li&gt;&lt;li&gt;UTF-8 format.&lt;/li&gt;&lt;/ul&gt; |
|Year of Birth|  &lt;ul&gt;&lt;li&gt;Year of birth for user.&lt;/li&gt;&lt;li&gt;&lt;code&gt;YYYY&lt;/code&gt; format.&lt;/li&gt;&lt;li&gt;Values from &lt;code&gt;1900&lt;/code&gt; to current year.&lt;/li&gt;&lt;li&gt;No punctuation or special characters.&lt;/li&gt;&lt;li&gt;UTF-8 format.&lt;/li&gt;&lt;/ul&gt; |
|Day of Birth|  &lt;ul&gt;&lt;li&gt;Day of birth for user.&lt;/li&gt;&lt;li&gt;`DD` format.&lt;/li&gt;&lt;li&gt;Values from `01` to `31`.&lt;/li&gt;&lt;/ul&gt; |
|Month of Birth|  &lt;ul&gt;&lt;li&gt;Birth month for user.&lt;/li&gt;&lt;li&gt;`MM` format.&lt;/li&gt;&lt;li&gt;Values from `01` to `12`.&lt;/li&gt;&lt;/ul&gt; |
|Custom Audience Override|  &lt;ul&gt;&lt;li&gt;(Optional) Provide a **Custom Audience ID** to override the value in the required section. This field lets you use AudienceStream variables to populate the Audience ID.&lt;/li&gt;&lt;/ul&gt; |
|User Identifier Already Hashed|  &lt;ul&gt;&lt;li&gt;Select this option if the target user identifier is already hashed. Only values hashed with SHA256 are supported by Facebook.&lt;/li&gt;&lt;/ul&gt;

### Remove User from Custom Audience

#### Parameters

|Parameter| Description|
|---| ---|
|Custom Audience to Remove User From|  &lt;ul&gt;&lt;li&gt;(Required) Select your Target Custom Audience.&lt;/li&gt;&lt;li&gt;Before you can use this connector and build a custom audience in Facebook, you must agree to the [Facebook Custom Audience Terms](https://www.facebook.com/ads/manage/customaudiences/tos.php).&lt;/li&gt;&lt;/ul&gt; |
|Email Address|  &lt;ul&gt;&lt;li&gt;Identify a user based on their email address.&lt;/li&gt;&lt;/ul&gt; |
|Phone Number|  &lt;ul&gt;&lt;li&gt;Identify a user based on their phone number. Include only digits with country code, area code, and number. For example, `16505551212`.&lt;/li&gt;&lt;/ul&gt; |
|Facebook User ID|  &lt;ul&gt;&lt;li&gt;Identify a user based on their Facebook ID.&lt;/li&gt;&lt;li&gt;You must provide the &#34;Facebook App ID&#34; corresponding to the Facebook User ID (UID) when using this identifier type.&lt;/li&gt;&lt;/ul&gt; |
|Facebook App ID|  &lt;ul&gt;&lt;li&gt;Required if the &#34;Facebook User ID&#34; is used as the user identifier.&lt;/li&gt;&lt;li&gt;See &#34;Facebook User ID&#34;.&lt;/li&gt;&lt;/ul&gt; |
|Mobile Advertiser ID|  &lt;ul&gt;&lt;li&gt;Use this to target a user based on the app user ID, Apple&#39;s Advertising Identifier (IDFA), or Android&#39;s advertising ID.&lt;/li&gt;&lt;/ul&gt; |
|External ID|  &lt;ul&gt;&lt;li&gt;Do not hash.&lt;/li&gt;&lt;li&gt;Any unique ID from the advertiser, such as loyalty membership IDs, user IDs, and external cookie IDs.&lt;/li&gt;&lt;/ul&gt; |
|Zip Code|  &lt;ul&gt;&lt;li&gt;Postal code.&lt;/li&gt;&lt;li&gt;Exact format depends on country.&lt;/li&gt;&lt;/ul&gt; |
|City|  &lt;ul&gt;&lt;li&gt;User City.&lt;/li&gt;&lt;li&gt;Lowercase.&lt;/li&gt;&lt;li&gt;No punctuation or spaces.&lt;/li&gt;&lt;/ul&gt; |
|Country|  &lt;ul&gt;&lt;li&gt;User Country.&lt;/li&gt;&lt;li&gt;2-letter country code.&lt;/li&gt;&lt;li&gt;ISO 3166-1 Alpha-2 format.&lt;/li&gt;&lt;/ul&gt; |
|US State|  &lt;ul&gt;&lt;li&gt;User State in the United States.&lt;/li&gt;&lt;li&gt;Lowercase.&lt;/li&gt;&lt;li&gt;2-character ANSI abbreviation code.&lt;/li&gt;&lt;/ul&gt; |
|First Name|  &lt;ul&gt;&lt;li&gt;User first name.&lt;/li&gt;&lt;li&gt;Lowercase.&lt;/li&gt;&lt;li&gt;No punctuation or special characters.&lt;/li&gt;&lt;li&gt;UTF-8 format.&lt;/li&gt;&lt;/ul&gt; |
|Last Name|  &lt;ul&gt;&lt;li&gt;User last name.&lt;/li&gt;&lt;li&gt;Lowercase.&lt;/li&gt;&lt;li&gt;No punctuation or special characters.&lt;/li&gt;&lt;li&gt;UTF-8 format.&lt;/li&gt;&lt;/ul&gt; |
|First Initial|  &lt;ul&gt;&lt;li&gt;First initial of user.&lt;/li&gt;&lt;li&gt;Lowercase.&lt;/li&gt;&lt;li&gt;No punctuation or special characters.&lt;/li&gt;&lt;li&gt;UTF-8 format.&lt;/li&gt;&lt;/ul&gt; |
|Year of Birth|  &lt;ul&gt;&lt;li&gt;Year of birth for user.&lt;/li&gt;&lt;li&gt;`YYYY` format.&lt;/li&gt;&lt;li&gt;Values from `1900` to current year.&lt;/li&gt;&lt;/ul&gt; |
|Day of Birth|  &lt;ul&gt;&lt;li&gt;Day of birth for user.&lt;/li&gt;&lt;li&gt;`DD` format.&lt;/li&gt;&lt;li&gt;Values from `01` to `31`.&lt;/li&gt;&lt;/ul&gt; |
|Month of Birth|  &lt;ul&gt;&lt;li&gt;Birth month for user.&lt;/li&gt;&lt;li&gt;`MM` format.&lt;/li&gt;&lt;li&gt;Values from `01` to `12`.&lt;/li&gt;&lt;/ul&gt; |
|Gender|  &lt;ul&gt;&lt;li&gt;Gender of user.&lt;/li&gt;&lt;li&gt;`M` for male, `F` for female&lt;/li&gt;&lt;/ul&gt; |
|Lookalike Value|  &lt;ul&gt;&lt;li&gt;An arbitrary, numeric value for each user set when you create a seed custom audience from CRM data.&lt;/li&gt;&lt;li&gt;Facebook uses this to determine which users in audience are worth the most to you, in a quantifiable way.&lt;/li&gt;&lt;/ul&gt; |
|Custom Audience Override|  &lt;ul&gt;&lt;li&gt;(Optional) Provide a **Custom Audience ID** to override the value in the required section. This field lets you use AudienceStream variables to populate the Audience ID.&lt;/li&gt;&lt;/ul&gt; |
|User Identifier Already Hashed|  &lt;ul&gt;&lt;li&gt;Select this option if the target user identifier is already hashed. Only values hashed with SHA256 are supported by Facebook.&lt;/li&gt;&lt;/ul&gt; |

### Opt Out User from All Custom Audiences

#### Parameters

|Parameter| Description|
|---| ---|
|Email Address|  &lt;ul&gt;&lt;li&gt;Identify a user based on their email address.&lt;/li&gt;&lt;/ul&gt; |
|Phone Number|  &lt;ul&gt;&lt;li&gt;Identify a user based on their phone number. Include only digits with country code, area code, and number. For example, `16505551212`.&lt;/li&gt;&lt;/ul&gt; |
|Facebook User ID|  &lt;ul&gt;&lt;li&gt;Identify a user based on their Facebook ID.&lt;/li&gt;&lt;li&gt;You must provide the &#34;Facebook App ID&#34; corresponding to the Facebook User ID (UID) when using this identifier type.&lt;/li&gt;&lt;/ul&gt; |
|Facebook App ID|  &lt;ul&gt;&lt;li&gt;Required if the &#34;Facebook User ID&#34; is used as the user identifier.&lt;/li&gt;&lt;li&gt;See &#34;Facebook User ID&#34;.&lt;/li&gt;&lt;/ul&gt; |
|Mobile Advertiser ID|  &lt;ul&gt;&lt;li&gt;Use this to target a user based on the app user ID, Apple&#39;s Advertising Identifier (IDFA), or Android&#39;s advertising ID.&lt;/li&gt;&lt;/ul&gt; |
|External ID|  &lt;ul&gt;&lt;li&gt;Do not hash.&lt;/li&gt;&lt;li&gt;Any unique ID from the advertiser, such as loyalty membership IDs, user IDs, and external cookie IDs.&lt;/li&gt;&lt;/ul&gt; |
|Zip Code|  &lt;ul&gt;&lt;li&gt;Postal code.&lt;/li&gt;&lt;li&gt;Exact format depends on country.&lt;/li&gt;&lt;/ul&gt; |
|City|  &lt;ul&gt;&lt;li&gt;User City.&lt;/li&gt;&lt;li&gt;Lowercase.&lt;/li&gt;&lt;li&gt;No punctuation or spaces.&lt;/li&gt;&lt;/ul&gt; |
|Country|  &lt;ul&gt;&lt;li&gt;User Country.&lt;/li&gt;&lt;li&gt;2-letter country code.&lt;/li&gt;&lt;li&gt;ISO 3166-1 Alpha-2 format.&lt;/li&gt;&lt;/ul&gt; |
|US State|  &lt;ul&gt;&lt;li&gt;User State in the United States.&lt;/li&gt;&lt;li&gt;Lowercase.&lt;/li&gt;&lt;li&gt;2-character ANSI abbreviation code.&lt;/li&gt;&lt;/ul&gt; |
|Year of Birth|  &lt;ul&gt;&lt;li&gt;Year of birth for user.&lt;/li&gt;&lt;li&gt;`YYYY` format.&lt;/li&gt;&lt;li&gt;Values from `1900` to current year.&lt;/li&gt;&lt;/ul&gt; |
|Day of Birth|  &lt;ul&gt;&lt;li&gt;Day of birth for user.&lt;/li&gt;&lt;li&gt;`DD` format.&lt;/li&gt;&lt;li&gt;Values from `01` to `31`.&lt;/li&gt;&lt;/ul&gt; |
|Month of Birth|  &lt;ul&gt;&lt;li&gt;Birth month for user.&lt;/li&gt;&lt;li&gt;`MM` format.&lt;/li&gt;&lt;li&gt;Values from `01` to `12`.&lt;/li&gt;&lt;/ul&gt; |
|User Identifier Already Hashed|  &lt;ul&gt;&lt;li&gt;Select this option if the target user identifier is already hashed. Only values hashed with SHA256 are supported by Facebook.&lt;/li&gt;&lt;/ul&gt; |
|Last Name|  &lt;ul&gt;&lt;li&gt;User last name.&lt;/li&gt;&lt;li&gt;Lowercase.&lt;/li&gt;&lt;li&gt;No punctuation or special characters.&lt;/li&gt;&lt;li&gt;UTF-8 format.&lt;/li&gt;&lt;/ul&gt; |
|First Initial|  &lt;ul&gt;&lt;li&gt;First initial of user.&lt;/li&gt;&lt;li&gt;Lowercase.&lt;/li&gt;&lt;li&gt;No punctuation or special characters.&lt;/li&gt;&lt;li&gt;UTF-8 format.&lt;/li&gt;&lt;/ul&gt; |
|Gender|  &lt;ul&gt;&lt;li&gt;Gender of user.&lt;/li&gt;&lt;li&gt;`M` for male, `F` for female&lt;/li&gt;&lt;/ul&gt; |
|Lookalike Value|  &lt;ul&gt;&lt;li&gt;An arbitrary, numeric value for each user that is set when you create a seed custom audience from CRM data.&lt;/li&gt;&lt;li&gt;Facebook uses this value to determine which users in audience are worth the most to you, in a quantifiable way.&lt;/li&gt;&lt;/ul&gt; |

## Using the Facebook Audiences connector

### Create a visitor ID

The Facebook Audiences connector requires at least one visitor ID attribute with the ability to be passed through to Facebook Audiences.

Use the following resources to set up a visitor ID attribute:

* [Setting up a Visitor ID attribute]()
* [Facebook Marketing API](https://developers.facebook.com/docs/marketing-api/audiences-api)

### Define an audience

Your account may have several visitor ID attributes defined. In this case, it is important to create a [visitor badge named `Known Visitor`]() to check for the existence of any of the visitor IDs. Using this attribute ensures that the audience only contains visitors with an assigned visitor ID that can be passed to Facebook. You cannot target an unknown visitor.

Combine the `Known Visitor` badge with other conditions to create an audience for the connector.

This connector also has required ID parameters, such as email, phone, app, or user IDs. At least one of these IDs is required. Including these IDs in your audience filter helps avoid connector errors.

### Testing

The most effective testing method is to run a [Trace]() to ensure that your events are handled properly and to check your Facebook dashboard to verify that your Custom Audience was created and populated.

## FAQ

### Why can&#39;t I see my audiences in the AudienceStream drop-down list?

If you have more than 2,000 audiences in Facebook, they are not all selectable in the drop-down list from an AudienceStream connector.

Use the following steps in Facebook to view all audiences and select the identifier for a specific audience:

1. Log in to Facebook as the user that has access to the Facebook Audiences account.
1. Go to &lt;https://www.facebook.com/adsmanager/audiences&gt;.
1. Find the audience you are looking for and copy the Audience ID.  
    If the Audience ID does not display, you can modify your table column view to include it.  

    ![](/images/server-side-connectors/facebook-ads-find-audience-id.png)
1. Return to AudienceStream and enter the Audience ID as custom value for your AudienceStream connector.
