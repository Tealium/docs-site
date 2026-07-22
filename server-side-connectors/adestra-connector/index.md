---
title: Adestra Connector Setup Guide
description: This article describes how to set up the Adestra connector in your Customer Data Hub account.
url: https://docs.tealium.com/server-side-connectors/adestra-connector/
---
## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Create or Update Contact| ✓| ✓|
|Add Contact To List| ✓| ✓|
|Remove Contact From List| ✓| ✓|
|Send Email| ✓| ✓|

## Configure Settings

Go to the **Connector Marketplace** and add a new connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **API Key**: (Required) Adestra account API key, see: [Create API Token](https://app.adestra.com/doc/page/current/index/integration/zapier/initial-config#Step3:CreateAPITokeninMessageFocus "Create API Token")

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Create or Update Contact

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Update Strategy|  <ul><li>(Required) Select applicable update strategy.  <ul><li>**Create Only** Look up an existing contact and if not found, create a new contact.</li><li>**Update Only** Look up an existing contact and update it.</li><li>**Create or Update** Look up an existing contact and if found, update it, otherwise create a new contact.</li></ul> </li></ul> |
|Core Table|  <ul><li>(Required) Select the core table to create or update the contact in.</li></ul> |
|Contact Lookup Email Address|  <ul><li>(Required) Email address to lookup contact.</li></ul> |

### Action - Add Contact To List

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Core Table|  <ul><li>(Required) Select the core table the contact belongs to.</li></ul> |
|Contact Lookup Email Address|  <ul><li>(Required) Email address to lookup contact.</li></ul> |
|List|  <ul><li>(Required) List to add the contact to.</li></ul> |

### Action - Remove Contact From List

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Core Table|  <ul><li>(Required) Core tables store contacts in Adestra.</li><li>Select the core table the contact belongs to.</li></ul> |
|Contact Email Address|  <ul><li>(Required) Email address to lookup contact.</li></ul> |
|List|  <ul><li>(Required) List to remove the contact from.</li></ul> |

### Action - Send Email

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Email Campaign|  <ul><li>(Required) Select the campaign to be launched.</li></ul> |
|Contact Email Address|  <ul><li>(Required) Email address to send email to.</li></ul> |
|Transaction Data|  <ul><li>(Required) Template data to set within the email campaign.</li></ul> |
