---
title: Connecting Tableau
description: This article describes how to connect Tableau to Tealium DataAccess
url: https://docs.tealium.com/server-side/data-storage/data-viz-tools/connecting-tableau/
---## Prerequisites

* Basic knowledge of Tableau
* Be sure to install the appropriate drivers from the Tableau website at [http://www.tableau.com/support/drivers](http://www.tableau.com/support/drivers).
* To install, click **Amazon Redshift** and follow the directions on the screen.  
Tealium has a partnership with Tableau but is not a reseller. Ensure that you obtain the proper Tableau licensing before attempting to use the product. If you need assistance, contact your Account Manager to initiate and facilitate support.

### Connecting to Redshift

This section describes how to add a new data source and connect to Amazon Redshift.

![](/images/server-side/tableau-data-soure-example.jpg)

Use the following steps to connect to Amazon Redshift:

1. Add a new data source.
1. Enter your Redshift Credentials.  
Ensure that you require Secure Sockets Layer (SSL).
1. Select a schema.  
Select the schema that most closely resembles your account and profile.  
For example, if your account is `tealium` and your profile is `dataaccess` your schema will be `tealium__dataaccess`.
1. Select one or more tables.  
Tables and views for your account are listed in the Tables section. Select the tables that you want to analyze in Tableau.
    * At this point, you can optionally join multiple tables if you know which fields relate the tables together.
    * During this process, you will have to tell Tableau which field in the &#34;left&#34; table is related to the field in the &#34;right&#34; table and the enter the type of join that you want to create between the two tables (left, right, inner, or full outer).  
    ![](/images/server-side/tableau-join2.jpg)
1. To start using the data, create a new sheet or select an existing sheet.

#### AudienceDB example

In the following example, the keys used to join two (2) tables together are as follows:

`visits_view.&#34;visit - visitor id&#34;` = `visitors_view_normalized.&#34;visitor - id&#34;`

![](/images/server-side/tableau-join.jpg)

### Preparing data for analysis

When using a new data source, organize the fields prior to creating any reports, as described in the following suggestions:

* **Dimensions and Measures**  
By default, most (or all) fields are imported as &#34;dimensions&#34;, or fields that you want to slice your data by. If you intend to use a field as metric that you can summarize, convert these fields from &#34;dimensions&#34; to &#34;measures&#34;. This often includes fields such as Order Total, Total Units, etc.
* **Custom Measures**  
EventDB is event-level data; therefore you will often want to count how often an event (row or record) contains a field with a specific value. An example is a custom measure of &#34;Unique Visitors&#34;. This is accomplished by creating a new calculated field using calculation shown in the following example. In this instance, it will count the unique number of times that a specific visitor ID appeared in the data: `COUNTD([Event - Visitor Id])`

### Examples of custom calculations

The following list provides examples of other custom calculations you may want to use:

* Total Events (Measure)  
`COUNTD([Event - Id])`
* Mac&#43;Chrome Revenue (Measure)  
`IF FIND([Event - User Agent],&#34;Chrome&#34;) &gt; 0 AND FIND([Event - User Agent],&#34;Mac&#34;) &gt; 0 THEN [Event - Udo - Order Subtotal] END`
* Unique Orders  
`COUNTD([Event - Udo - Order Id])`
* High Value Orders  
`COUNTD(IF [Event - Udo - Order Subtotal] &gt; 500 THEN [Event - Udo - Order Id] END)`
* While there are several default fields in EventDB, most of the other fields are unique to each customer database and based on what is configured in Tealium IQ. You can create custom calculations using any combination of default or custom fields in EventDB.

## Troubleshooting

### Unable to connect to RedShift due to a password issue

Check that your password does not contain any of the following disallowed characters:

* Plus sign (`&#43;`)
* At symbol (`@`)
* Right or left curly brackets (`{`, ``}`)
* Right parenthesis (`)*`)
* Semicolon (`;`)

### An error message occurs when attempting to connect to any Tableau Server page

The Tableau server gateway port (Default = 80) is likely blocked by something outside of the Tableau Server, such as a proxy or firewall. As a result, the response from Tableau server does not reach the user.

If you receive this message, it is likely that one of the following has occurred:

* The connection was reset.
* The connection to the server was reset while the page was loading.
* The site is temporarily unavailable or too busy, try again in a few moments.
* If you cannot load any pages, check your computer&#39;s network connection.
* If your computer or network is protected by a firewall or proxy, ensure that your browser is permitted to access the web.

To resolve this issue, work with your IT team to unlock the port used as the gateway port on the Tableau server.

## Additional resources

* [Tableau Knowledge Base](https://kb.tableau.com/articles/issue/error-the-connection-was-reset-connecting-to-tableau-server)  
Contains detailed information about commonly asked questions and best practices.
* [Connecting Tableau to an Amazon RedShift Data Source](https://onlinehelp.tableau.com/current/pro/desktop/en-us/examples_amazonredshift.htm)  
This article describes how to connect Tableau to an Amazon Redshift database and set up the data source.
