---
title: Salesforce Standard Objects Connector Setup Guide
description: This article describes how to set up the Salesforce Standard Objects connector.
url: https://docs.tealium.com/server-side-connectors/salesforce-standard-objects-connector/
---
## Connector Actions

| Action name | Visitor profile | Event data |
| --- | :---: | :---: |
|Create or Update Standard Object| ✓| ✓|
|Delete Standard Object| ✓| ✓|

## Configure Settings

Go to the connector marketplace and add a new connector. For more information, see [about-connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

## Action Settings - Parameters and Options

Click **Continue** to configure the connector actions. Enter a name for the action and select the action type from the list.

### Action - Create or Update Standard Object

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Update Strategy|  <ul><li>(Required) Select applicable update strategy.</li><li>Create Only  <ul><li>Create new Standard Object without lookup.</li></ul> </li><li>Update Only  <ul><li>Look up an existing Standard Object and update it.</li></ul> </li><li>Create or Update  <ul><li>Look up an existing Standard Object and if found, update it, otherwise create a new item.</li></ul> </li></ul> |
|Standard Object|  <ul><li>Select the applicable Standard Object to create or update.</li></ul> |

### Action - Delete Standard Object

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Standard Object|  <ul><li>Type of Standard Object instance to delete.</li></ul> |
