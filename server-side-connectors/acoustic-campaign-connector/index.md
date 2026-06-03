---
title: Acoustic Campaign Connector Setup Guide
description: This article describes how to set up the Acoustic Campaign connector.
url: https://docs.tealium.com/server-side-connectors/acoustic-campaign-connector/
---
## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Upsert Contact in Database| ✓| ✗|
|Insert Contact into Contact List| ✓| ✗|
|Upsert Contact in Database and Add to Program| ✓| ✗|
|Send Email using Custom Triggered Autoresponder| ✓| ✗|
|Upsert Contact in Relational Table| ✓| ✗|

## Configure Settings

Navigate to the **Connector Marketplace** and add a new connector. For general instructions on how to add a connector, see the [About Connectors]() article.

After adding the connector, configure the following settings:

* **OAuth2 Client ID**  
(Required) OAuth2 Client ID. Please, contact Acoustic for assistance.
* **OAuth2 Client Secret**  
(Required) OAuth2 Client Secret. Please, contact Acoustic for assistance.
* **OAuth2 Refresh Token**  
(Required) OAuth2 Refresh Token. Please, contact Acoustic for assistance.
* **Server Host**  
Please provide your host.  
Hint: `api-campaign-ZZ-X.goacoustic.com`. Replace `X` with your pod number and replace `ZZ` with your region.  
Do not include HTTP(S) protocol. Example: `api-campaign-us-5.goacoustic.com`.

Click **Done** when you are finished configuring the connector.

## Action Settings — Parameters and Options

Click **Continue** to configure the connector actions. Enter in a name for the action and then select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Action — Upsert Contact in Database

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Database Name| Select the database name to upsert the contact in.&lt;br&gt; It can be found by logging into your Acoustic account and navigating to **Data &amp;gt; Databases**.|
|Database Type| The type of database.|
|Enable Auto Reply (If AutoResponder is defined for database)|
|Contact Identifier(s)| If your database has a key other than Email, you must include all unique key columns with their corresponding name/value pairs. If adding and/or updating contacts in a flexible database, one or more Sync Fields must be specified to look up the contact.|
|Enable Contact Database Column Update Criteria|

### Action — Insert Contact into Contact List

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Contact List Name| Select the contact list name to add the contact to.&lt;br&gt; It can be found by logging into your Acoustic account and&lt;br&gt; navigating to **Data &amp;gt; Contact Lists**.| 
|Contact List&#39;s Corresponding Database| Select the corresponding contact list&#39;s database name to add the contact to.&lt;br&gt; It can be found by logging into your Acoustic account and navigating to **Data &amp;gt; Databases**.|

### Action — Upsert Contact in Database and Add to Program

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Database Name| Select the database name to upsert contact in.&lt;br&gt; It can be found by logging into your Acoustic account and navigating to **Data &amp;gt; Databases**.|
|Database Type| The type of database.|
|Enable Auto Reply (If AutoResponder is defined for database)|
|Contact Identifier(s)| If your database has a key other than Email, you must include all unique key columns with their corresponding name/value pairs. If adding and/or updating contacts in a flexible database, one or more Sync Fields must be specified to look up the contact.|
|Program ID| Unique ID of the Program.|
|Enable Contact Database Column Update Criteria|

### Action — Send Email using Custom Triggered Autoresponder

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Autoresponder Mailing Send ID| For this operation to work, the autoresponder has to be custom triggered. Choose &#34;Custom&#34; option when creating the Automated Mailing Send and use a Database as its &#34;Contact Source&#34;.&lt;br&gt; You can find the **Autoresponder ID** by logging into your Acoustic Campaign account Autoresponder listing page and hovering your mouse over the mailing name.|
|Autoresponder&#39;s Corresponding Database| Provide the database name that was used when creating the selected Autoresponder.|

### Action — Upsert Contact in Relational Table

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Target Relational Table| Select the relational table name to upsert contact in.|
