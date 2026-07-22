---
title: View-Through Tracking Extension
description: Use the View-Through Tracking extension to configure a cross-domain view-through tracking pixel for use in your ad creative. This feature includes a complimentary tier of 120 million impressions with overage charges incurred beyond that. Contact your account manager for information about pricing and usage.
url: https://docs.tealium.com/iq-tag-management/extensions/extensions-list/view-through-tracking-extension/
---
## Requirements

* utag v4.38 or later. For more information about updating the `utag.js` template, see our knowledge base article [Best Practices for Updating to the Latest Version of utag.js](https://support.tealiumiq.com/en/support/solutions/articles/36000363470).
* iQ Tag Management account
* Manage Account permissions

**Optional**:

* Tealium Collect tag (for EventStream tracking)
* Manage JavaScript Code permission (for customized data handling)

## How it works

Using this extension, measure the impact of display ads on your customers' behavior by tracking which ads are seen by your visitors on other websites within a certain time frame, regardless of whether or not an ad click was generated. This requires information to be captured when the ad is displayed and for that information to be available when they come to your site.

### Use case

A user is reading an article on a news site. An ad appears for a certain watch, but the user does not click on the ad as they are busy reading an article. Later in the day, or the following day, the user looks up the watch from the display ad to find out more. The user is then converted.

By the end of the customer's session, more is known about the customer and what they are looking for, such as watch type or feature preferences, potential price range, and whether or not the customer visited blogs or knowledge bases to learn more about a specific model.

The View-Through Tracking solution uses the following two simple components to allow the sharing of data between your display ads and your iQ Tag Management account.

* **Display Ad Image Pixel**  
Used to send the relevant data to the Tealium View-Through tracking service. This is a standard URL containing query string parameters for the ad data to collect.
* **Custom JavaScript Code Extension**  
An extension is created in your iQ Tag Management account to extract the view-through data collected during the visitor's journey to your site.

### Workflow

The following list summarizes the basic workflow for the extension:

* The tracking URL placed in ad creative.  
As a result, the user browsing **siteA.com** is served the **Client's** ad.
* The ad loads and calls the DataBridge endpoint (the tracking URL).  
As a result, the ad server dynamically populates tracking parameters and any other hard-coded parameters.
* The tracking URL endpoint writes the data passed in the query parameters to a new third-party cookie, along with a third party Tealium ID.  
As a result, depending on the operators used, data is incremented, decremented, or overwritten on each subsequent impression served to the user
* User leaves **siteA.com** and goes to **client.com** where Tealium is installed.  
As a result, the extension reads the new third-party cookie and enriches the visitor profile with the data.
* The client is now able to create attributes and audiences based on the ad impression data and that data is leveraged in Tealium DataAccess.

## Using the extension

Before you begin, familiarize yourself with [how extensions work]().


<blockquote>
Multiple profiles may have this extension, but it is only allowed to be added once per profile.
</blockquote>


Once the extension is added, the following configuration options are available:

### Tracking Pixel URL

* **DataBridge Key**: (Automatically generated)
* **Base URL**: (Automatically generated)

### Tracking Pixel parameters

Create the parameters to use in the tracking pixel. These parameters capture the values you set, either here or dynamically in your ad creative. They are available as variables in your data layer.

* **Variable**: Select a variable from the drop-down list or click the plus sign (**+**) to add a variable.
* **Description**: (Optional) Enter a description of the variable.
* **Method**: Select from the drop-down menu one of the following operators for the variable.
    * **Increment**: A whole number to increment. For example, increase total impressions by 1.
    * **Decrement**: A whole number to decrement. For example, decrease total impressions by 1.
    * **Append**: Sets a string into an array every time the requested endpoint is called. The end result is similar to the breadcrumb affect as it leaves "crumbs" on a trail.
    * **Set**: The last value seen for the created call.
    * **Clear**: Clears the current setting.

* **Value**: Type in the value for your variable.
* **Full View-Through Tracking Pixel URL**: The URL below is generated from the settings above. Click **Copy** to copy the URL to include it within your ad creative. When it fires on the ad server, it tracks the data directly to the cookie.
    ![](https://docs.tealium.com/images/iq-tag-management/view-through-extension-full-tracking-pixel.jpg)

<blockquote>
The parameters you add in this step captures the values you set and any variables you add become available in your data layer.
</blockquote>


![](https://docs.tealium.com/images/iq-tag-management/view-through-extension-full-tracking-pixel-url.jpg)

### Data processing

This code processes the view-through tracking data and sets the corresponding variables in the data layer. To customize this code you need the **Manage JavaScript Code** permission.

This section provides guidance on how you want the data to be processed once the client comes back to your site. On the same screen, edit the code to customize how your view-through tracking data is processed and how the corresponding values are set in the data layer.

After you add the URL to your ad server, click **Customize Code** and an editor window displays the current JavaScript code.

![](https://docs.tealium.com/images/iq-tag-management/view-through-tracking-configuration-data-processing.jpg)

By default, extension looks for the cookie in the code, reads and processes the data, and then adds it to the data layer. Once the data is in the data layer, use it as you see fit.

For example, in the code sample above, Line 12 is commented out by default. If you remove the comment characters to uncomment this line, the Tealium Collect tag is triggered with the new data, which automatically fires into the Customer Data Hub.

```
// utag.view(utag.data,null,[##UTDBCOLLECTTAGID##]);
```


<blockquote>
This is considered a third-party cookie and occurs once per session, per user.
</blockquote>


If you want to fire additional tags, such as Google Analytics, or send the data to Optimizely, fire this tag and include this data.

### Usage Reporting

You can View usage reports in tabular format directly in the extension configuration screen or view a graphical representation of your usage.

* **Start**: Click the text field, and use the calendar popup to select the start date of the usage report.
* **End**: Click the text field, and use the calendare popup to select the end date of the usage report.

Click **Update** to see the usage report, which displays the total number of reads, total number of writes, and total number of track impressions by Account and Profile. To view a different report, simply adjust the date range and click **Update** again.

![](https://docs.tealium.com/images/iq-tag-management/view-through-extension-usage-reporting-calendar-popup.jpg)

### Graphical format from the data supply chain view

Use the following steps to view Usage Reports in graphical format from the Data Supply Chain view:

1. To view usage reports in a graphical format, go to **Analyze > Usage**.
1. View the following graphical representations of your track impressions:  
    ![](https://docs.tealium.com/images/iq-tag-management/view-through-usage-reporting-graphical-in-data-supply-chain.jpg)  
    * Total View-Through Tracking Writes
    * Total View-Through Tracking Reads

## Compliance Considerations

The following sections contain additional considerations that are helpful when forming your strategies while ensuring compliance.

### Ad Exchanges and Ad Networks

The DataBridge endpoint is certified for use on Google AdExchange. The majority of other ad exchanges do not require certification for third-party tracking, clients place the tracking pixel with no issue. OATH and Yahoo do require approval from the client's account manager prior to use of the tracking pixel.

### GDPR

No inherent risks have been identified with the current application. In the advertising ecosystem in general, individual ad exchanges today have many restrictions in place to prevent PII extraction for a user. When a user returns to your site, you have new data points but the data is now considered first party data, to which your overall GDPR policies apply.

### Intelligent Tracking Prevention (ITP)

Because this product relies on the use of [third-party cookies](https://en.wikipedia.org/wiki/HTTP_cookie#Third-party_cookie), ITP and other browser level restrictions on third party cookies may limit the ability to track.

## FAQ

#### What problems does this extension solve?

Companies looking for ways to better measure how display influences the customer journey. In the past, it has been difficult to translate data into information meaningful to a business. Using the View-Through extension, tie data back to customer profiles for attribution and utilize the data in real-time.

| Ad Server Only | With Impression Tracking |
|:---------------|:-------------------------|
| <ul><li>Campaign, creative, and impression data siloed.</li><li>Difficult to understand insights at the customer level and unable to quickly personalize the customer experience based on campaigns viewed.</li><li>Difficult to relate campaign experience to a customer profile.</li></ul> | <ul><li>Enables companies to bring impression, campaign, and creative insights out of the ad server and into the data layer to more efficiently analyze campaign or creative effectiveness.</li><li>The ability to act on trusted data in real time.</li><li>The ability to personalize data.</li><li>Enables users to track impression data and act on it immediately when the customer returns to the site, regardless of whether or not the customer clicks on an ad.</li><li>Track customer insights and act in real time. For example, total impressions served to a customer, a list of campaigns the customer has been exposed to, domains a user viewed the ads on, and specific creatives that they have viewed. This is done in real time and with your own data, resulting in reduced ad spending as you better understand which campaigns and creatives are most effective and which to suppress.</li><li>Does not need to be used specifically for conversions, though it may be used to measure View-Through conversions.</li><li>Build more complete customer profile attributes and audiences in your Customer Data Platform (CDP).</li><li>Provides the ability to send data to EventStream and AudienceStream.</li></ul> |

#### What is a DataBridge?

A DataBridge is a component that works as a third-party cookie service to share data across domains. This allows customers to share data from one domain to another using a single, shared endpoint. The View-Through extension is an application of the DataBridge component. A unique DataBridge Key is used to access and configure the View-Through extension.

#### What kind of data and what data points are tracked?

Track any information that your ad server produces using macros. [DFP example](https://support.google.com/admanager/answer/2376981?visit_id=636960437187397170-4165199539&amp;rd=1)

#### Where do I use the View-Through tracking pixel?

The View-Through tracking pixel is approved on all major ad networks. OATH and Yahoo require prior approval from your Account Manager.

#### Are Facebook Ads trackable?

No. Tealium is not a Facebook Measurement partner.

#### Does this extension work with the existing Channels extension?

Yes, they both work at the same time.. This method is particularly helpful when developing an attribution strategy.

#### How are usage and billing tracked?

This feature is free for up to 120 million track impressions per year, after which overage charges are incurred. Usage and billing is tracked in iQ Tag Management. Your Account Manager applies automation to monitor your usage and notify you when you are approaching the 120M mark.

* To monitor overall usage, check the Customer Data Hub usage reports.
* To monitor usage of the free tier, use the reporting widget in the View-Through extension.
