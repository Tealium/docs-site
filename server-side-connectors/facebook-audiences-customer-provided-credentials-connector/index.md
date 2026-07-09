---
title: Facebook Audiences Customer-Provided Credentials Connector Setup Guide
description: This article describes how to set up the Facebook Audiences Customer-Provided Credentials connector in your Customer Data Hub account.
url: https://docs.tealium.com/server-side-connectors/facebook-audiences-customer-provided-credentials-connector/
---
This article describes how to set up the Facebook Audiences Customer-Provided Credentials connector.

## Prerequisites 

For more information about creating a Facebook app, see [Facebook: App Development](https://developers.facebook.com/docs/apps/).

Before you configure your connector, complete the following steps:

1. Agree to the [Facebook Custom Audience Terms](https://www.facebook.com/ads/manage/customaudiences/tos.php).
1. Add the following redirect URI to your Facebook account: `https://my.tealiumiq.com/oauth/facebook/callback.html`. From the Facebook App Dashboard, navigate to **Facebook Login &gt; Settings** and enter the URI under **Valid OAuth Redirect URIs of your Facebook App**.
1. Request `ads_management` permission in your Facebook app. The `ads_management` permission allows your app to both read and manage the Ads account it owns, or has been granted access to, by the Ad account owner. For more information, see [Facebook: Permission Reference](https://developers.facebook.com/docs/facebook-login/permissions/#reference-ads_management).

To get more app resources, such as a better rate limit, request Ads Management **Standard Access**. For more information, see [Facebook: Access and Authentication](https://developers.facebook.com/docs/marketing-api/access/).

## API information

This connector uses the following vendor API:

* API Name: Facebook Graph API - Marketing API
* API Version: v25.0
* API Endpoint: `https://graph.facebook.com`

## Batch limits
  
This connector uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 10000
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **App ID**: (Required) The Facebook App ID you want to connect. 
* **App Secret**: (Required) The App Secret of the Facebook App you want to connect.
* **Ad Account ID**: (Required) The Facebook Ads Account ID you want to manage. For more information about your Facebook ad account ID, see [Facebook: Find your Facebook ad account ID number](https://www.facebook.com/help/1492627900875762)

This connection will generally expire within 60 days, causing unpredictable results for all Facebook Ad actions.

Reestablish the connection at any point by clicking **Establish Connection/Connected**.  

Before clicking the **Establish Connection** button, ensure that you are signed into Facebook with the account that is linked with the Ad Account ID that is being used. If this is not the case issues, can arise with the token that is generated.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Add User to Custom Audience | ✓ | ✗ |
| Remove User from Custom Audience | ✓ | ✗ |
| Opt Out User from All Custom Audiences | ✓ | ✗ |

Enter a name for the action and select the action type.

The following section describes how to set up parameters and options for each action.

### Add User to Custom Audience

Four types of identifiers are supported: emails, phone numbers, user or app IDs, and secondary IDs. Multiple secondary identifiers are supported. If you specify a **Facebook User ID**, you must also provide a **Facebook App ID**. Only one email or phone number is supported. If multiple identifiers are specified, they are selected in the order listed above. For example, if both email and phone number are specified, the email will be chosen unless it has no value.

#### Parameters

| Parameter | Description|
| --- | --- |
|Custom Audience to Add User To|  &lt;ul&gt;&lt;li&gt;(Required) Select your Target Custom Audience.&lt;/li&gt;&lt;li&gt;Audiences created from customer files are not displayed.&lt;/li&gt;&lt;li&gt;Before you can use this connector and build a custom audience in Facebook, you must agree to the [Facebook Custom Audience Terms](https://www.facebook.com/ads/manage/customaudiences/tos.php).&lt;/li&gt;&lt;/ul&gt; |
|Email Address|  &lt;ul&gt;&lt;li&gt;Identify a user based on their email address.&lt;/li&gt;&lt;/ul&gt; |
|Phone Number|  &lt;ul&gt;&lt;li&gt;Identify a user based on their phone number.&lt;/li&gt;&lt;li&gt;Include only digits with country code, area code, and number. For example, `16505551212`.&lt;/li&gt;&lt;/ul&gt; |
|Facebook User ID|  &lt;ul&gt;&lt;li&gt;Identify a user based on their Facebook ID.&lt;/li&gt;&lt;li&gt;You must provide the &#34;Facebook App ID&#34; corresponding to the Facebook User ID (UID) when using this identifier type.&lt;/li&gt;&lt;/ul&gt; |
|Facebook App ID|  &lt;ul&gt;&lt;li&gt;Required if the &#34;Facebook User ID&#34; is used as the user identifier.&lt;/li&gt;&lt;li&gt;See &#34;Facebook User ID&#34;.&lt;/li&gt;&lt;/ul&gt; |
|Mobile Advertiser ID|  &lt;ul&gt;&lt;li&gt;Use this to target a user based on the app user ID, Apple&#39;s Advertising Identifier (IDFA), or Android&#39;s advertising ID.&lt;/li&gt;&lt;/ul&gt; |
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
| Custom Audience Override | (Optional) Provide a Custom Audience ID to override the value in the Required Section. This field lets you use AudienceStream variables to populate the Audience ID. |
| User Identifier Already Hashed | Check this box if the Target User Identifier is already hashed. Facebook only accepts the SHA256 hashing method.  |

### Remove User from Custom Audience

Four types of identifiers are supported: emails, phone numbers, user or app IDs, and secondary IDs. Multiple secondary identifiers are supported. If you specify a **Facebook User ID**, you must also provide a **Facebook App ID**. Only one email or phone number is supported. If multiple identifiers are specified, they are selected in the order listed above. For example, if both email and phone number are specified, the email will be chosen unless it has no value.

#### Parameters

| Parameter | Description|
| --- | --- |
|Custom Audience to Remove User From|  &lt;ul&gt;&lt;li&gt;(Required) Select your Target Custom Audience.&lt;/li&gt;&lt;li&gt;Before you can use this connector and build a custom audience in Facebook, you must agree to the [Facebook Custom Audience Terms](https://www.facebook.com/ads/manage/customaudiences/tos.php).&lt;/li&gt;&lt;/ul&gt; |
|Email Address|  &lt;ul&gt;&lt;li&gt;Identify a user based on their email address.&lt;/li&gt;&lt;/ul&gt; |
|Phone Number|  &lt;ul&gt;&lt;li&gt;Identify a user based on their phone number.&lt;/li&gt;&lt;li&gt;Include only digits with country code, area code, and number. For example, `16505551212`.&lt;/li&gt;&lt;/ul&gt; |
|Facebook User ID|  &lt;ul&gt;&lt;li&gt;Identify a user based on their Facebook ID.&lt;/li&gt;&lt;li&gt;You must provide the &#34;Facebook App ID&#34; corresponding to the Facebook User ID (UID) when using this identifier type.&lt;/li&gt;&lt;/ul&gt; |
|Facebook App ID|  &lt;ul&gt;&lt;li&gt;Required if the &#34;Facebook User ID&#34; is used as the user identifier.&lt;/li&gt;&lt;li&gt;See &#34;Facebook User ID&#34;.&lt;/li&gt;&lt;/ul&gt; |
|Mobile Advertiser ID|  &lt;ul&gt;&lt;li&gt;Use this to target a user based on the app user ID, Apple&#39;s Advertising Identifier (IDFA), or Android&#39;s advertising ID.&lt;/li&gt;&lt;/ul&gt; |
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
| Custom Audience Override | (Optional) Provide a Custom Audience ID to override the value in the Required Section. This field lets you use AudienceStream variables to populate the Audience ID. |
| User Identifier Already Hashed | Check this box if the Target User Identifier is already hashed. Facebook only accepts the SHA256 hashing method.   |

### Opt Out User from All Custom Audiences

#### Parameters

| Parameter | Description|
| --- | --- |
Email Address|  &lt;ul&gt;&lt;li&gt;Identify a user based on their email address.&lt;/li&gt;&lt;/ul&gt; |
|Phone Number|  &lt;ul&gt;&lt;li&gt;Identify a user based on their phone number.&lt;/li&gt;&lt;li&gt;Include only digits with country code, area code, and number. For example, `16505551212`.&lt;/li&gt;&lt;/ul&gt; |
|Facebook User ID|  &lt;ul&gt;&lt;li&gt;Identify a user based on their Facebook ID.&lt;/li&gt;&lt;li&gt;You must provide the &#34;Facebook App ID&#34; corresponding to the Facebook User ID (UID) when using this identifier type.&lt;/li&gt;&lt;/ul&gt; |
|Facebook App Id|  &lt;ul&gt;&lt;li&gt;Required if the &#34;Facebook User ID&#34; is used as the user identifier&lt;/li&gt;&lt;li&gt;See &#34;Facebook User ID&#34;.&lt;/li&gt;&lt;/ul&gt; |
|Mobile Advertiser ID|  &lt;ul&gt;&lt;li&gt;Use this to target a user based on the app user ID, Apple&#39;s Advertising Identifier (IDFA), or Android&#39;s advertising ID.&lt;/li&gt;&lt;/ul&gt; |
|Zip Code|  &lt;ul&gt;&lt;li&gt;Postal code.&lt;/li&gt;&lt;li&gt;Exact format depends on country.&lt;/li&gt;&lt;/ul&gt; |
|City|  &lt;ul&gt;&lt;li&gt;User City.&lt;/li&gt;&lt;li&gt;Lowercase.&lt;/li&gt;&lt;li&gt;No punctuation or spaces.&lt;/li&gt;&lt;/ul&gt; |
|Country|  &lt;ul&gt;&lt;li&gt;User Country.&lt;/li&gt;&lt;li&gt;2-letter country code.&lt;/li&gt;&lt;li&gt;ISO 3166-1 Alpha-2 format.&lt;/li&gt;&lt;/ul&gt; |
|US State|  &lt;ul&gt;&lt;li&gt;User State in the United States.&lt;/li&gt;&lt;li&gt;Lowercase.&lt;/li&gt;&lt;li&gt;2-character ANSI abbreviation code.&lt;/li&gt;&lt;/ul&gt; |
|First Name|  &lt;ul&gt;&lt;li&gt;User first name.&lt;/li&gt;&lt;li&gt;Lowercase.&lt;/li&gt;&lt;li&gt;No punctuation or special characters.&lt;/li&gt;&lt;li&gt;UTF-8 format.&lt;/li&gt;&lt;/ul&gt; |
|Last Name|  &lt;ul&gt;&lt;li&gt;User last name.&lt;/li&gt;&lt;li&gt;Lowercase.&lt;/li&gt;&lt;li&gt;No punctuation or special characters.&lt;/li&gt;&lt;li&gt;UTF-8 format.&lt;/li&gt;&lt;/ul&gt; |
|First Initial|  &lt;ul&gt;&lt;li&gt;First initial of user.&lt;/li&gt;&lt;li&gt;Lowercase.&lt;/li&gt;&lt;li&gt;No punctuation or special characters.&lt;/li&gt;&lt;li&gt;UTF-8 format.&lt;/li&gt;&lt;/ul&gt; |
|Year of birth|  &lt;ul&gt;&lt;li&gt;Year of birth for user.&lt;/li&gt;&lt;li&gt;`YYYY` format.&lt;/li&gt;&lt;li&gt;Values from `1900` to current year.&lt;/li&gt;&lt;/ul&gt; |
|Day of birth|  &lt;ul&gt;&lt;li&gt;Day of birth for user.&lt;/li&gt;&lt;li&gt;`DD` format.&lt;/li&gt;&lt;li&gt;Values from `01` to `31`.&lt;/li&gt;&lt;/ul&gt; |
|Month of Birth|  &lt;ul&gt;&lt;li&gt;Birth month for user.&lt;/li&gt;&lt;li&gt;`MM` format.&lt;/li&gt;&lt;li&gt;Values from `01` to `12`.&lt;/li&gt;&lt;/ul&gt; |
|Gender|  &lt;ul&gt;&lt;li&gt;Gender of user.&lt;/li&gt;&lt;li&gt;`M` for male, `F` for female&lt;/li&gt;&lt;/ul&gt; |
|Lookalike Value|  &lt;ul&gt;&lt;li&gt;An arbitrary, numeric value for each user set when you create a seed custom audience from CRM data.&lt;/li&gt;&lt;li&gt;Facebook uses this to determine which users in audience are worth the most to you, in a quantifiable way.&lt;/li&gt;&lt;/ul&gt; |
| User Identifier Already Hashed | Check this box if the Target User Identifier is already hashed. Facebook only accepts the SHA256 hashing method.   |


## Using the Facebook Audiences Customer-Provided Credentials connector

### Create a visitor ID attribute

The Facebook Audiences Customer-Provided Credentials connector requires at least one visitor ID attribute with the ability to be passed through to Facebook Audiences.

Use the following resources to set up a Visitor ID attribute:

* [Setting up a Visitor ID attribute]()
* [Facebook Marketing API](https://developers.facebook.com/docs/marketing-api/audiences-api)

### Define an audience

Your account may have several visitor ID attributes defined. In this case, it is important to create a visitor-scoped attribute of the boolean data type and named `Known Visitor` to check for the existence of any of the visitor IDs. Using this attribute ensures that the audience only contains visitors with an assigned visitor ID that can be passed to Facebook. You cannot target an unknown visitor.

This connector also has required ID parameters, such as email, phone, app, or user IDs. At least one of these IDs is required. Including these IDs in your audience filter helps avoid connector errors.

Use the following example to [create an audience filter]() of visitors that have a &#34;Known Visitor&#34; boolean data type set to `true`. You can add the badge and boolean attributes in advance or add them when creating the filter.

![](/images/server-side-connectors/edit-audience-shoe-fan.png)

### Connect Tealium to your Facebook Audiences account

You will need the account ID to configure the connector with your Facebook Audiences account.

Use the following steps to get your Facebook Audiences account ID:

1. Log in to your Facebook Audiences account.
1. Click an ad account, campaign, ad set, or ad in [Ads Manager](https://www.facebook.com/ads/manage).
1. Copy the `account_id` parameter value from the URL in your browser then return to the connector in AudienceStream.  
![](/images/server-side-connectors/facebook-account-id.png)

1. In the **Configure** window, add your title and any relevant notes and your Ad Account ID (copied from above).
1. Click **Establish Connection** to verify the connection.

### Create custom audience

Now that you are connected to your Facebook Audiences account, it&#39;s time to create a Custom Audience. You will need to create your first Custom Audience on the Facebook site to accept the terms and conditions before you are able to create a Custom Audience with the connector.

Use the following steps to create a custom audience:

1. In the connector configuration, click the **Create** tab.
1. Configure the following fields:
   * **Audience Name** (Required): The name of the custom audience. Use the audience or segment name from your CRM (for example, `Qualified Leads - US - Q3 2026` or `High Value Customers - EMEA`). Meta uses this name to identify your audience segment.
   * **Audience Metadata (JSON)** (Optional): A JSON object describing the audience criteria, mapped to the `description` parameter in the Meta API. Use key-value pairs with aggregated or categorical attributes. Do not include PII. For example: `{&#34;lifecycle_stage&#34;:&#34;churned&#34;,&#34;region&#34;:&#34;EMEA&#34;,&#34;tier&#34;:&#34;high_value&#34;}`. Meta uses this metadata with Audience Labels and optimization features. Label assignment occurs in Meta Ads Manager. The value must be valid JSON for Meta to parse the metadata.
1. Click **Create**.  
The `customer_file_source` parameter supports the following values:
    * `USER_PROVIDED_ONLY`
    * `PARTNER_PROVIDED_ONLY`
    * `BOTH_USER_AND_PARTNER_PROVIDED`

On the Facebook Audiences site, you have the option to create audiences based on a customer list, website traffic, or app activity. For this example, create your audience based on a customer list.

To use your custom audience, it must contain a minimum of 20 entries. If your audience has been created successfully, a small check icon displays beside the button.

### Specify connector actions

You must now specify the actions you want the connector to take.

Use the following steps to specify actions for the connector:

1. Click the **Actions** tab.
1. Select **Add User to Custom Audience**.  
![](/images/server-side-connectors/facebook-ads-connector-action-add-user-to-custom-audience.jpg)
1. Click **&#43; Create Action**.

### Configure connector actions

Use the following steps to configure actions for the connector:

1. From the **Audience** menu, select the **Shoe-Fans** audience you created earlier.  
The **Custom Audience to Add User To** menu displays audiences that exist in your Facebook Audiences account.
1. From the **Custom Audience to Add User To** drop-down list, select the audience you want to add visitors to.
1. In the **Target User Identifier** drop-down list, map the visitor email attribute to the matching visitor identifier in your Facebook Audiences account.
1. Leave the **WHEN** set to **Joined Audience**.
1. Click **Save**.

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

