---
title: Data Connect recipe best practices
description: This article describes best practices for Data Connect.
url: https://docs.tealium.com/server-side/data-connect/manage-data-connect-integrations/best-practices/
---
The following best practices will help you create Workato recipes that leverage the Tealium Events app to send data to Tealium:


* **Data Cleanliness**   
Before importing data to Tealium, examine the data that will be sent for quality and cleanliness.
* **Regional Tealium API domain**   
When configuring your Tealium Events app, use your regional Tealium API domain. You can find your regional Tealium API domain in your [Tealium Connect data source](https://docs.tealium.com/tealium-connect-data-source/). 
* **Connections per app**  
Use one connection per app in your Workato account. For example, if you have two recipes that need to use the Salesforce app, create the Salesforce connection in the first recipe and select the existing connection from the list of active connections in the second recipe.
* **Reduce tasks**  
To reduce task costs and increase processing efficiency, maximize the file batches and minimize the number of Workato tasks you need to accomplish your business goal. 
  * To see the number of tasks used in a recipe, navigate to **Integrations > Jobs** and select a job. In the **Job Details** section, **Tasks Used** lists the number of tasks used by that specific job.
  * When using batch triggers, set the **Batch size** to the maximum size. 
  * While the default setting in Workato is to retrieve all fields from your source data, ensure that you retrieve only the fields sent to Tealium. 
    To select specific fields to send to Tealium:
    * In the **Setup** step of your app configuration, click **Show optional fields** and ensure **Fields to retrieve** is selected.
    * Under **Fields to retrieve**, select the specific fields to send to Tealium.
* **Customize the poll interval for your trigger**   
The default value is 5 minutes. This default interval is too short for most use cases, especially for low volume data import cases. Using a poll interval that is too short will result in using more tasks than needed. We recommend setting the polling interval to be the longest value that your use case can tolerate.  
To customize the poll interval for your trigger, complete the following steps:  
  * In the **Setup** step of your app configuration, click **Show optional fields** and ensure **Trigger poll interval** is selected.
  * Under **Trigger poll interval**, select a custom poll interval for your use case.
* **Tealium Visitor ID**  
For each record in Data Connect, the value used for the `tealium_visitor_id` must be populated. If this value is not set, the Data Connect Tealium Events app will fail to import the records that are missing the ID. Other data in the same Tealium Connect API call will also be affected.  
To ensure the `tealium_visitor_id` is populated correctly, choose one of the following solutions:
  * **WHERE clause** - Many Workato apps have a **WHERE clause** in their polling triggers that allow you to filter out, at source, records that won't have a value for `tealium_visitor_id.`
  * **Custom step** - In cases where it is not possible to use a WHERE clause, use a JavaScript or Ruby step in the Workato recipe to filter out records with a missing identifier. For more information, see the [JavaScript article](https://docs.workato.com/connectors/javascript.html) in the Workato documentation.

