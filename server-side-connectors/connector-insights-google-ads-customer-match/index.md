---
title: Connector Insights: Google Ads Customer Match
description: Insights brings additional connector data from the vendor into your Tealium account to help you evaluate its performance.
url: https://docs.tealium.com/server-side-connectors/connector-insights-google-ads-customer-match/
---
The Google Ads Customer Match Connector insight integrates with the Google Ads Customer Match connector, bringing user list data from Google into your account. This article shows you how to access the feature and explore the data.

## Overview of Connector Insights

The insight for the Google Ads Customer Match connector summarizes the user list data received by Google. These insights are presented in a summary of the user list names and their sizes.

## Custom Audience Parameters

The Google Ads Customer Match insight offers the following information about the Google Ads list set up in the connector action:

* **Size for Display** estimates the number of users in this list on the Google Display Network.
* **Size for Search** estimates the number of users in this list on the Google domain, available for targeting in Google Ads search campaigns.
* **Match Rate Percentage** displays the percentage of users in this list that match Google users.

If the number of users is yet to be determined, these values are null.

![](/images/server-side-connectors/connector-insights-google-ads-customer-match.png)

## Using Connector Insights

To access Connector Insights, go to **Connect &gt; Audience Connectors**, search for the **Google Ads Customer Match (Tealium-Provided Credentials) Connector** connector, and click **Insights**.

![](/images/server-side-connectors/connector-insights-btn.png)

## Understanding Google Ads Custom Audiences Insights

The Google Ads Customer Match insight performs a [Google Ads API user_list query](https://developers.google.com/google-ads/api/fields/v14/user_list) to provide information about your configured audience.

|**Parameter**| **Description**|
|----|----|
| List Name | Name of the user list. | 
| Description | Description of the user list. | 
| Membership Status | Indicates whether a user list is open or active. Only open user lists can accumulate more users and be targeted. | 
| Size For Display | Estimated number of users in this user list on the Google Display Network. This value is null if the number of users has not yet been determined. | 
| Size For Search | Estimated number of users in this user list in the `google.com` domain. These are the users available for targeting in Search campaigns. This value is null if the number of users has not yet been determined. | 

## Offline User Data Jobs

The Job ID summary shows the processing status of your records in the Google Ads platform:

![](/images/server-side-connectors/connector-insights-google-ads-customer-match-offline-user-data-jobs.png)

## Additional Resources

* [About Customer Match - Google Ads Help](https://support.google.com/google-ads/answer/6379332?hl=en)
* [Customer Match Audience - Display &amp; Video 360 Help](https://support.google.com/displayvideo/answer/9539301)
* [Google Ads API: user_list](https://developers.google.com/google-ads/api/fields/v14/user_list)
* [Google Ads Customer Match (Tealium-Provided Credentials) Connector Setup Guide]()