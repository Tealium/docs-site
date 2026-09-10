---
title: Salesforce Data 360 Connector Setup Guide
description: This article describes how to set up the Salesforce Data 360 connector.
url: https://docs.tealium.com/server-side-connectors/salesforce-data-360-connector/
---
## API information

This connector uses the following vendor API:

* API Name: Salesforce Data 360 Ingestion API
* API Version: v1
* API Endpoint: [Salesforce Data Cloud Ingestion API](https://developer.salesforce.com/docs/data/data-cloud-int/references/data-cloud-ingestionapi-ref/c360-a-api-get-started.html)

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **Salesforce Domain**
  * (Required) The My Domain URL for your Salesforce organization, for example, `https://company.my.salesforce.com`. The client credentials flow requires a My Domain URL. Other Salesforce hosts return a `request not supported on this domain` error.
* **Client ID**
  * (Required) The Consumer Key from your Salesforce Connected App or External Client App.
  * The app must have the client credentials flow enabled, a Run As user configured, and the `cdp_ingest_api` and `api` OAuth scopes.
  * If Salesforce returns `no client credentials user enabled`, verify that a Run As user is configured. This error doesn't indicate that the Client Secret is incorrect.
* **Client Secret**
  * (Required) The Consumer Secret from your Salesforce Connected App or External Client App.
* **Source API Name**
  * (Required) The Source API Name of the Ingestion API source in Salesforce Data 360.

## Actions

| Action Name | AudienceStream | EventStream |
| ----------- | :------------: | :---------: |
| Send Ingestion API Records | ✓ | ✓ |

### Send Ingestion API Records

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. With parallel processing, events can reach the vendor out of sequence. If event order is important, add a sequence value to the events. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/).

Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 200
* Max time since oldest request: 10 minutes

#### Parameters

| Parameter | Description |
| --- | --- |
| Object API Name | (Required) The Salesforce Data 360 object to send records to. The available objects are retrieved from the selected Ingestion API source. If the object isn't listed, enter its Object API Name, and then press Enter. Names are case-sensitive and must match the Salesforce schema exactly. |
| Record Data | (Required) Map Tealium attributes to the destination fields in the Salesforce Data 360 object schema. See [Record Data](#record-data) for mapping requirements. |

#### Record Data

Map Tealium attributes to the destination fields for the selected Salesforce Data 360 object. Follow these requirements when configuring mappings:

* If a field requires a nested object or array, define a template on the **Templates** tab and enter the template name as the mapped value.
* Include the Data Stream's primary key and any other fields marked as required in the Salesforce ingestion schema.
* For partial updates, include the configured **Record Modified** field. For Engagement objects, also include the configured **Event Time** field.
* Ensure that mapped values match the data types and formats expected by Salesforce, such as ISO 8601 timestamps, numbers, and boolean values.
* If a source contains multiple objects, such as `SalesCustomer` and `Order`, create a separate action for each Object API Name so that each **Record Data** mapping corresponds to a single object schema.


<blockquote>
Salesforce processes ingestion requests asynchronously. A successful response confirms that Salesforce accepted the request for processing, but doesn't confirm that every record was ingested. Missing required values, invalid data types, or other schema mismatches can cause records to fail during downstream processing without returning an error to Tealium.
</blockquote>


#### Templates

| Parameter | Description |
| --- | --- |
| Templates | (Optional) Create a template for fields that require nested objects or arrays, conditional fields, formatted timestamps, derived or static values, or schema-specific transformations. Enter a template name on the left and a template that renders valid JSON on the right. To use the template, map its name to the destination field under **Record Data**. Templates are sent only when referenced by a mapped field. Don't include the top-level `data` wrapper. Tealium adds it automatically. |
| Template Variables | (Optional) Map Tealium attributes to the variable names used in your templates. |
