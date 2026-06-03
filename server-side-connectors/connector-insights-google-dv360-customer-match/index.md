---
title: Connector Insights: Google DV360 Customer Match Connector
description: This article describes how to access connector insights and explore insights data for the Google DV360 Customer Match connector.
url: https://docs.tealium.com/server-side-connectors/connector-insights-google-dv360-customer-match/
---
The Google DV360 Customer Match Connector insight integrates with the Google DV360 Customer Match connector, bringing user list data from Google into your account. The insight for the Google DV360 Customer Match connector summarizes the user list data received by Google. These insights are presented in a summary of the user list names and sizes.

## Access Connector Insights

To access Connector Insights, go to **AudienceStream &gt; Audience Connectors**, search for the **Google DV360 Customer Match connector**, and click **Insights**.

![](/images/server-side-connectors/insights/using-connector-insights-google-dv360-customer-match.png)

## Customer Match insights

The Google DV360 Customer Match Insights provides information about the Google DV360 list configured in the connector action.

* **Size for Display**: The estimated number of users in this user list on the Google Display Network. 
* **Size for Search**: The estimated number of users in this user list in the Google domain, which are available for targeting in Google DV360 search campaigns. These values are null if the number of users has not yet been determined.
* **Match rate percentage**: Indicates match rate for Customer Match lists. If the number of users is yet to be determined, these values will be null.

![](/images/server-side-connectors/insights/values-connector-insights-google-dv360-customer-match.png)

## Audience information

The Google DV360 Customer Match insight uses the [Google Ads API searchStream](https://developers.google.com/google-ads/api/fields/v14/user_list) to provide information about your configured audience.

| Column |  Description |
| ----- |----- |
| List Name |  Name of the user list| 
| Description| Description of the user list| 
| Membership Status| Indicates whether a user list is open or active. Only open user lists can accumulate more users and be targeted.| 
| Size For Display| Estimated number of users in this user list, on the Google Display Network. This value is null if the number of users has not yet been determined.| 
| Size For Search|  Estimated number of users in this user list in the Google domain. These are the users available for targeting in search campaigns. This value is null if the number of users has not yet been determined.| 

 Tealium retrieves list statistics directly from Google DV 360, which may cause a difference between matches and the total volume of connector requests in this insight and the [Google DV 360 Customer Match connector](). 

## Offline user data jobs

The **Job ID** summary shows the processing status of your records in the Google DV360 platform.

![](/images/server-side-connectors/insights/connector-insights-google-dv360-customer-match-offline-user-data-jobs.png)

## Additional resources

* [Google Ads: About Customer Match](https://support.google.com/google-ads/answer/6379332?hl=en)
* [Google Display &amp; Video 360: Customer Match audience](https://support.google.com/displayvideo/answer/9539301)
* [Google Ads API: user_list](https://developers.google.com/google-ads/api/fields/v14/user_list)
* 