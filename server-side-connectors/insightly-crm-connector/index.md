---
title: Insightly CRM Connector Setup Guide
description: This article describes how to set up the Insightly CRM connector.
url: https://docs.tealium.com/server-side-connectors/insightly-crm-connector/
---
## Supported Actions

|**Action Name**| **Trigger on Audience**| **Trigger on Streams**|
|---| ---| ---|
|Add a Contact| ✓| ✓|
|Update a Contact| ✓| ✓|
|Add a Lead| ✓| ✓|
|Update a Lead| ✓| ✓|

### API Information

This connector uses the following vendor API:

* API Name: Insightly API
* API Version: v3.1
* API Endpoint: `https://api..insightly.com/`
* Documentation: [Insightly API](https://api.insightly.com/v3.1/Help)

## Configure Settings

Go to the Connector Marketplace and add a new Insightly Connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

To configure the connector, follow these steps:

1. In the **Configure** tab, provide the API Pod and the API Key for your Insightly account.  
To obtain this information, log in to your Insightly account and select the **User Settings** section.
1. In the API sub-section, find the API Key and the API URL.
  * The API URL has the following format: `https://api.{pod}.insightly.com/v3.1/`
  * Example: If your API URL is `https://api.na1.insightly.com`, the API Pod is `na1`.
  * For more information, see: [Insightly: Finding Your API key or URL and resetting your key](https://support.insight.ly/hc/en-us/articles/204864594-Finding-your-Insightly-API-key).

## Action Settings: Parameters and Options

Click **Next** or go to the **Actions** tab. It&#39;s where you&#39;ll set up actions to trigger.

This section describes how to set up parameters and options for each action.

### Action: Add a Contact

This action lets you create a new contact in the Insightly CRM.

#### Parameters

* **Attributes**
  * Required
  * Contact attributes.
  * First Name is required, other attributes are optional.

* **Custom Fields**
  * Optional
  * If provided, these fields are sent as a list of `CUSTOMFIELDS` objects.

* **Tags**
  * Optional
  * If provided, these fields are sent as a list of `TAGS` objects.

### Action: Update a Contact

This action lets you update an existing contact in the Insightly CRM.

#### Parameters

* **Attributes**
  * Required
  * Contact attributes.
  * Contact ID is required, other attributes are optional.

* **Custom Fields**
  * Optional
  * If provided, these fields are sent as a list of `CUSTOMFIELDS` objects.

* **Tags**
  * Optional
  * If provided, these fields are sent as a list of `TAGS` objects.

### Action: Add a Lead

This action lets you create a new lead in the Insightly CRM.

#### Parameters

* **Attributes**
  * Required
  * Lead attributes.
  * Last Name is required, other attributes are optional.

* **Custom Fields**
  * Optional
  * If provided, these fields are sent as a list of `CUSTOMFIELDS` objects.

* **Tags**
  * Optional
  * If provided, these fields are sent as a list of `TAGS` objects.

### Action: Update a Lead

This action allows to update an existing lead in the Insightly CRM.

#### Parameters

* **Attributes**
  * Required
  * Lead attributes.
  * Lead ID is required, other attributes are optional.

* **Custom Fields**
  * Optional
  * If provided, these fields are sent as a list of `CUSTOMFIELDS` objects.

* **Tags**
  * Optional
  * If provided, these fields are sent as a list of `TAGS` objects.

## Vendor Documentation

* [Insightly Homepage](https://www.insightly.com/)
* [Insightly API Documentation](https://api.insightly.com/v3.1/Help#!)
