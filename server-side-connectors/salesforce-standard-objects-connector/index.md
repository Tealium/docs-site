---
title: Salesforce Standard Objects Connector Setup Guide
description: This article describes how to set up the Salesforce Standard Objects connector.
url: https://docs.tealium.com/server-side-connectors/salesforce-standard-objects-connector/
---
## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Create or Update Standard Object| ✓| ✓|
|Delete Standard Object| ✓| ✓|

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

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
