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

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a connector.

## Actions

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

#### Batch limits

This connector uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of records: 10,000
* Max time since oldest request: 60 minutes
* Max size of requests: 2 MB

### Add or Update Row

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Row Operation|  <ul><li>Use the drop-down list to select the type of row operation to perform:  <ul><li>**Add Only** - Add a new row without lookup.</li><li>**Update Only** - Look up an existing row and update it.</li><li>**Add or Update** - Look up an existing row and, if found, update it. Otherwise add a new row.</li></ul> </li></ul> |
|Spreadsheet ID|  <ul><li>Enter an existing spreadsheet ID.</li><li>This is the ID of the spreadsheet you want to write to.</li></ul> |
|Worksheet Name|  <ul><li>Select an existing worksheet name.</li><li>Your spreadsheet may contain multiple worksheets.</li><li>Enter the title of the worksheet you want to target.</li><li>The worksheet must already contain column names in first header row</li></ul> |
|Row Data|  <ul><li>Column names must already exist in the first header row of the worksheet.</li><li>Empty row values are skipped and not included.</li><li>You must have an attribute and the spreadsheet column name where you want to look for the value of the attribute.</li><li>To map row values to column names: <ul><li>Select your Attribute from the **Map** drop-down list and enter the column name (Custom Value) in the **To** field. When the action fires, it will search for the Attribute value in the specified column.</li><li>If the value exists, the matching row will have its cells updated as specified in Row Data.</li><li>If the value does not exist, a new row is created with Row ID value and Attributes specified in Row Data.</li></ul> </li></ul> |
|Lookup (Optional)|  <ul><li>Required for **Update Only** and **Add or Update** row operations.</li><li>Maps a value to a header by which to look for an existing row.</li><li>The Google Sheets API does not offer native support to look up rows by value. Lookups must therefore be explicitly enabled using the **Enable Lookup** button at the top left of the screen.</li><li>Lookups are enabled once per spreadsheet (using each individual Spreadsheet ID).</li></ul> |

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
