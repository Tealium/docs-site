---
title: Google Universal Analytics Tag Advanced Mapping
description: Learn how to properly configure a data mappings between Tealium and Google Universal Analytics (GUA) for events, campaign tracking, social interactions, e-commerce, content groups, custom variables, and mobile.
url: https://docs.tealium.com/client-side-tags/google-universal-analytics-tag-advanced-mapping/
---

<blockquote>
As of July 1, 2023, Google Universal Analytics properties stopped processing hits. This tag has been deprecated and no longer available in the tag marketplace. For the current tag, see [Google Analytics 4](https://docs.tealium.com/google-analytics-4-ga4-tag/).
</blockquote>


## Requirements

Before you begin make sure you add the [E-Commerce extension](https://docs.tealium.com/e-commerce-extension/). This extension automatically maps e-commerce data to Google Universal Analytics. See the E-Commerce section below to see which destinations the E-Commerce variables map to.

## Standard mapping

Tealium provides Standard mappings that allow you to override the default setting or dynamically set standard configuration values. Where possible we will identify what Google uses for the default value to help you determine if you should utilize a mapping to alter the default value. The Standard mappings include:

* **Tracking ID**
The Tracking ID is the identifier Google assigns for your account. This is typically a string of characters beginning with ‘UA-’. This mapping lets you override or dynamically set the Tracking ID available through the Marketplace tag interface.
Note that, since the Google Universal Analytics tag supports multiple tracking IDs configured through one tag, any mappings you do should retain a quantitative match between the ‘tracking ID’ and ‘tracker name’. For example, if there are 5 separate tracking IDs listed then there should be the same number of tracker names listed. Undesirable behavior would result should only 4 of the 5 tracker names be listed.
* **Tracker Name**
This mapping lets you override or dynamically set the Tracker Name or Names available through the Marketplace tag interface. This is needed only for multiple account tracking.
Note that since the Google Universal Analytics tag supports multiple tracking IDs configured through one tag, any mappings you do should retain a quantitative match between the ‘tracking ID’ and ‘tracker name’. For example, if there are 5 separate tracking IDs listed then there should be the same number of tracker names listed. Undesirable behavior would result should only 4 of the 5 tracker names be listed.
* **Page**
By default, Page is the path name portion of the page URL and is primarily used to specify virtual page paths, such as for modal windows. This parameter is what Google uses as the page identifier since it is unique for any given web page.
* **Title**
Identifies the title of the page or document. By default Google returns the JavaScript title property.
```js
document.title
```
* **Location**
Identifies the url the visitor is viewing. By default Google returns the full URL (excluding anchor) of the page.
* **UID**
Identifies the visitor or customer. Map to this destination to manually specify the user’s ID. This value is unique and persistent, and if used with an authentication system, lets you track a single user across sessions and devices.
* **Cookie Domain**
The Cookie Domain parameter specifies the domain used to store the analytics cookie. Setting this to "none" sets the cookie without specifying a domain. See the "Domain" in the "Tag Configuration" section of the [Google Universal Analytics: Basic Configuration](https://docs.tealium.com/google-universal-analytics-analyticsjs-tag/) article for more information.
* **Cookie Expires**
By default, cookies created by the Google Universal Analytics tag are set to expire after 2 years. This expiration is refreshed every time a hit is sent. Passing this parameter with a value of 0 turns it into a session-based cookie, otherwise the value is measured in seconds.
* **Legacy Cookie Domain**
The Legacy Cookie Domain parameter overrides the domain used to store the analytics cookie. Google will auto-detect this value if you leave it blank. Setting this to "none" creates the cookie without specifying a domain. Read "Domain" in the "Tag Configuration" section of the [Google Universal Analytics: Basic Configuration](https://docs.tealium.com/google-universal-analytics-analyticsjs-tag/) article for more information.
* **Legacy History Import**
Determines whether or not to import history data from `ga.js` cookies. Make sure the Variable you are mapping to this destination contains Boolean value "true" or "false".
* **nonInteraction**
Allows you specify whether or not the event will impact your bounce rate. By default, Google identifies an event as an Interaction. See the section describing Non-Interaction Events within Google's [About Events](https://support.google.com/analytics/answer/1033068#NonInteractionEvents) article.
* **Enhanced Link Attribution**
Lets you turn enhanced link attribution on or off and will override the configuration. Default is **Off**. Enhanced Link Attribution improves the accuracy of your In-Page Analytics report by automatically differentiating between multiple links to the same URL on a single page by using link element IDs. For more information see Google's [Enhanced Link Attribution](https://support.google.com/analytics/answer/2558867?hl=en) article.
* **setAllowLinker (allowLinker)**
Lets you turn cross-domain tracking on or off. By default this is **Off**. For more information see Google's [Linker](https://developers.google.com/analytics/devguides/collection/analyticsjs/linker) article.
* **Auto Linking Domain (crossDomainTrack)**
Used to provide the list of domains you want to track activity across. If there is more than one domain then each must be comma-separated in the list.
* **Site Speed Sample Rate (siteSpeedSampleRate)**
Used to specify the size of the user sample from which Google determines page timing metrics. By default Google sets this to 1%.
* **Sample Rate (sampleRate)**
Indicates the percentage of visitors that should be tracked. The default value is 100, meaning 100% of users are sampled in. See the Google developers section [Sample Rate](https://developers.google.com/analytics/devguides/collection/analyticsjs/field-reference#sampleRate) for additional details.
* **Autofill E-Commerce Params (autofill\_params)**
Lets you turn ON/OFF the "Autofill E-Commerce values" and override the toggle in the Tag settings.
* **Optimizely Integration (optimizely)**
Lets you turn ON/OFF the "Optimizely Integration" and override the toggle in the Tag settings.
* **Initialize tracker before Extensions (init\_before\_extensions)**
Lets you turn ON/OFF the "Enable create before Extensions" and override the toggle in the Tag settings.
* **Session Control (sessionControl)**
Lets you set the session duration either to "start" or "end". See the Google developers reference [Session Control](https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters?hl=en#sc) for additional details.
* **Anonymize IP (anonymizeip)**
Lets you turn ON/OFF the "Anonymize IP" and override the toggle in the Tag settings. See the Google developers reference [Anonymize IP](https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters?hl=en#aip) for additional details.
* **Data Source (dataSource)**
This is the variable value of the hit. Examples include web, mobile, crm, etc. See the Google developers reference [Data Source](https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters?hl=en#ds) for additional details.
* **Clear Vars**  
Recommended for single page applications only. Mapping to destination overrides the [Clear Vars Tag setting](https://docs.tealium.com/google-universal-analytics-analyticsjs-tag/).
* **Client ID**  
Randomly generated ID for the browser instance. [Learn more](https://developers.google.com/analytics/devguides/collection/analyticsjs/field-reference#clientId).
* **Custom Set Command (set.###)**
Lets you pass custom parameters to the "set" command. For example, `ga(‘set’, ‘dataSource’, ‘web’)`.

## Event mapping


<blockquote>
Events are only sent if both the Event Category and Event Action are defined.
</blockquote>


The other two parameters, Event Label and Event Value, are optional. These are often used to mark specific conversions, like if someone played a video on a web page or added an item to their shopping cart.

* **eventCategory** (Required)  
Lets you map a variable that identifies the type of interaction, for example ‘click’.
* **eventAction** (Required)  
Lets you map a variable that identifies the object that was interacted with, like ‘button’.
* **eventLabel**  
Lets you map a variable that categorizes events, like ‘nav buttons’.
* **eventValue**  
Lets you map a variable that identifies the count of events. For example: 4 times. The value for this parameter must be a number and non-negative.
* **ga\_events**  
Lets you map a variable that contains an array of event hits.
* **Global View Callback and Standard Event Callback**  
These destinations correspond to [Google's hitCallback function](https://developers.google.com/analytics/devguides/collection/analyticsjs/field-reference#hitCallback). Map to the Global View Callback destination to call the function for all hit types, including page views. Map to the Standard Event Callback destination to call the function only when Event Category and Event Action destinations are populated. You must first set the value of your data layer variable (the one you are mapping) to the callback function.  
Use the following steps map the variable to your callback destination:
  1. [Add a new Set Data Value Extension](https://docs.tealium.com/set-data-values-extension/) and scope it to Google Universal Analytics Tag
  1. Under Configuration, select your Variable from the Set drop-down list.
  1. Set the **To** drop-down selection to **JS Code** and write your callback function in the text field.
  1. Go back to the Data Mappings tab for the tag and map the same variable to your preferred callback destination.
  1. Save and publish.
  
For additional information, see [Event Tracking Guide for Google Universal Analytics](https://docs.tealium.com/google-universal-analytics-event-tracking/).


## Campaign mapping

Campaign values are automatically pulled from the URL of the page through query string parameters. GUA lets you set these values manually. All the values listed below are optional.

* **Campaign ID**
Unique identifier of the campaign assigned by Google.
* **Campaign Name**
Name of your campaign.
* **Campaign Source**
Origin of the campaign, such as a website name or a company name.
* **Campaign Medium**
Type of the campaign, such as a banner ad, email campaign, or click ad.
* **Campaign Content**
Description for the campaign ad.
* **Campaign Keyword**
Keyword terms for the campaign ad.

## Social mapping

This feature set lets you measure the clicks on social buttons, such as a Facebook Like or an X post. This is similar to event tracking, but allows separate reporting with consistent variables. All three variables must be set for the social interaction event to be sent.

* **Social Network**
The network on which the action occurs (for example, Facebook, X).
* **Social Action**
The type of action that happens (for example, Like, Send, Post). Requires all Social Network, Social Action and Social Target.
* **Social Target**
Specifies the target of a social interaction. This value is typically a URL but can be any text.

## E-Commerce mapping

These variables are related to E-Commerce and will automatically pick up values from the corresponding E-Commerce extension variables. Note that these values are only sent on a ‘transaction’ page. They do not get used on any other type of E-commerce page (for example, ‘product’ or ‘cart’). If you've added and configured the E-Commerce extension, any mappings you configure here will override the E-Commerce extension's mappings.

* **Order ID (Transaction ID)**
When mapped, this variable will overwrite the value in `_corder`, representing the order ID of a completed purchase.
* **Affiliation (Store Name/ID)**
When mapped, this variable will overwrite the value in `_cstore`, representing the store or affiliation from which this transaction occurred.
* **Revenue (Grand Total)**
When mapped, this variable will overwrite the value in `_ctotal`, representing the total revenue / grand total associated with the transaction. This value should include any shipping or tax costs.
* **Shipping**
When mapped, this variable will overwrite the value in `_cship`, representing the order shipping amount.
* **Tax**
When mapped, this variable will overwrite the value in `_ctax`, representing the order tax amount.

## App/Screen tracking

These tag destinations can track various configurations of the app (short for ‘application’) used by visitors primarily for viewing content.

* **Track Screen Views (screenView)**
Identifies the type of hit as screenView.
* **Application Name (appName)**
Identifies the name of the app rendering the screen.
* **Application ID (appId)**
Identifies the unique identifier to the app.
* **Application Version (appVersion)**
Identifies the version of the app.
* **Application Installer ID (appInstallerId)**
Identifies the installer identifier of the app.
* **Screen Name (screenName)**
Identifies the name of the screen viewed by the visitor.
* **Exception Description (exception\_reason)**
This parameter describes the exception. See the section within [Exception Description](https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters?hl=en#exd) for more information.

## Content groups

Content groups let you organize your site or app's content into collections that reflect the way you think about your content. You can place similar content into the same group, then view content by group name.

**Event Type** lets you map a custom metric based on event types:

![](https://docs.tealium.com/images/client-side-tags/dimeventtypes-1.png)

Choose the event type you want to categorize your content group.


<blockquote>
Google currently lets you define up to 10 content groups, **contentGroup1** through **contentGroup10**. For more information see the Google [Content Group](https://developers.google.com/analytics/devguides/collection/analyticsjs/field-reference#contentGroup) article.
</blockquote>


## Dimensions

Dimensions correspond to the rows in a report and allow you to break down a metric by a particular value, like screen views by screen name.

![](https://docs.tealium.com/images/client-side-tags/dimensions-1.png)

This parameter lets you map a custom dimension based on event types. Selecting an option other than "All Page Hits (set)" will cause the mapping to only be applied for the selected event type.

If the mapping applies to a specific event type the type will appear in the mapping name in the format of: `{{event_type}}-dimension#`.

For example, a mapping for dimension 9 for transaction events would look like this: `transaction-dimension9`.

![](https://docs.tealium.com/images/client-side-tags/dimeventtypes-1.png)


<blockquote>
There is a maximum of 20 custom dimensions, **dimension1** through **dimension20**, for standard accounts. For Premium accounts, you may utilize **dimension21** through **dimension200**.<br>
To set a dimension in this range, select **dimension21** **-****dimension200** in the Dimension drop-down list and then click in the field that displays at the top of the window and edit the number to the dimension you want.
</blockquote>


## Metrics

A custom metric is a count of some data type, like page views. A standard metric value is an integer. If set to a currency in the GUA configuration, this value can be a fixed decimal value instead.

![](https://docs.tealium.com/images/client-side-tags/metrics-1.png)

This parameter lets you map a custom metric based on event types. Selecting an option other than "All Page Hits (set)" will cause the mapping to only be applied for the selected event type.

If the mapping applies to a specific event type the type will appear in the mapping name in the format of: `{{event_type}}-metric#`.

For example, a mapping for metric 12 for only pageview events would look like this: `pageview-metric12`.


There is a maximum of 20 custom metrics, **metric1** through **metric20**, for standard accounts. For Premium accounts, you may utilize **metric21** through **metric200**. To set a metric in this range, select **metric21 - metric200** from the Metric drop-down list and then click in the field that appears at the top of the window and alter the number to the metric you want.

## Enhanced E-Commerce

The destinations in this tab correspond to the E-commerce actions supported by GUA's Enhanced E-commerce functionality. You must map to these destinations if you have turned ON the functionality in the GUA Tag settings. Mapping to the destination is automatically accomplished when you configure Tealium's [E-Commerce Extension](https://docs.tealium.com/e-commerce-extension/).

If you want to override the mappings in the extension or add mappings not supported in the extension, you must manually map them.

More details on mapping enhanced E-Commerce actions can be found in the [GUA: Enhanced E-Commerce](https://docs.tealium.com/google-universal-analytics-tag-enhanced-e-commerce/) article. Use this reference if interested in the following E-commerce actions:

* Enhanced E-Commerce: Impressions/Promo
* Enh E-Comm: Events
