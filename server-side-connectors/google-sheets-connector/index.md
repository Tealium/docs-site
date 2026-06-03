---
title: Google Sheets Connector Setup Guide
description: This article describes how to set up the Google Sheets connector.
url: https://docs.tealium.com/server-side-connectors/google-sheets-connector/
---
## Usage limits

The Google Sheets connector is for testing purposes only and is intended for low volume usage.

This connector has a daily rate limit of 100 total requests for all actions in your account. Exceeding the rate limit will likely result in failed updates to the spreadsheet. The rate limit cannot be changed.

## Requirements

* Google account
* Google spreadsheet - The spreadsheet must be in your Google Drive and have column names in the first row.

## Supported actions

|Action Name| AudienceStream| EventStream|
|---| ---| ---|
|Add or Update Row| ✓| ✓|

## Configuration

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

## Actions

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

#### Batch limits

This connector uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of records: 10,000
* Max time since oldest request: 60 minutes
* Max size of requests: 2 MB

### Add or Update Row

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Row Operation|  &lt;ul&gt;&lt;li&gt;Use the drop-down list to select the type of row operation to perform:  &lt;ul&gt;&lt;li&gt;**Add Only** - Add a new row without lookup.&lt;/li&gt;&lt;li&gt;**Update Only** - Look up an existing row and update it.&lt;/li&gt;&lt;li&gt;**Add or Update** - Look up an existing row and, if found, update it. Otherwise add a new row.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|Spreadsheet ID|  &lt;ul&gt;&lt;li&gt;Enter an existing spreadsheet ID.&lt;/li&gt;&lt;li&gt;This is the ID of the spreadsheet you want to write to.&lt;/li&gt;&lt;/ul&gt; |
|Worksheet Name|  &lt;ul&gt;&lt;li&gt;Select an existing worksheet name.&lt;/li&gt;&lt;li&gt;Your spreadsheet may contain multiple worksheets.&lt;/li&gt;&lt;li&gt;Enter the title of the worksheet you want to target.&lt;/li&gt;&lt;li&gt;The worksheet must already contain column names in first header row&lt;/li&gt;&lt;/ul&gt; |
|Row Data|  &lt;ul&gt;&lt;li&gt;Column names must already exist in the first header row of the worksheet.&lt;/li&gt;&lt;li&gt;Empty row values are skipped and not included.&lt;/li&gt;&lt;li&gt;You must have an attribute and the spreadsheet column name where you want to look for the value of the attribute.&lt;/li&gt;&lt;li&gt;To map row values to column names: &lt;ul&gt;&lt;li&gt;Select your Attribute from the **Map** drop-down list and enter the column name (Custom Value) in the **To** field. When the action fires, it will search for the Attribute value in the specified column.&lt;/li&gt;&lt;li&gt;If the value exists, the matching row will have its cells updated as specified in Row Data.&lt;/li&gt;&lt;li&gt;If the value does not exist, a new row is created with Row ID value and Attributes specified in Row Data.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|Lookup (Optional)|  &lt;ul&gt;&lt;li&gt;Required for **Update Only** and **Add or Update** row operations.&lt;/li&gt;&lt;li&gt;Maps a value to a header by which to look for an existing row.&lt;/li&gt;&lt;li&gt;The Google Sheets API does not offer native support to look up rows by value. Lookups must therefore be explicitly enabled using the **Enable Lookup** button at the top left of the screen.&lt;/li&gt;&lt;li&gt;Lookups are enabled once per spreadsheet (using each individual Spreadsheet ID).&lt;/li&gt;&lt;/ul&gt; |

## FAQ

### How do I find my Spreadsheet ID to enable Lookup?

In the following URL, the Spreadsheet ID is 12345: `https://docs.google.com/spreadsheets/d/**12345**/edit#gid=0`.

### Tracking is not available to show which Google Sheets are enabled for Lookup

There is no tracking available to show which Google sheets are enabled for lookup. Once lookup is enabled, there is no method to determine that Lookup enabled for a particular sheet if you log into the account another time.

### Action Dynamic Drop-Down lists do not display in real-time

Updates to the action dynamic drop-down lists are not live and do not display in real time. For example, if you are adding a new column in Google Sheets, modifications to the sheet do not automatically inherit the changes and reflect in the drop-down list.

To view the most recent data, you can click the **Refresh** icon on the connectors page or deselect the spreadsheet and select it again. Using either of these methods refreshes the drop-down lists to reflect your most recent updates.

## Vendor Documentation

* [Google Sheets API](https://developers.google.com/sheets/api/)
