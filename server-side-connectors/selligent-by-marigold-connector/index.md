---
title: Selligent by Marigold Connector Setup Guide
description: This article describes how to set up the Selligentby Marigold connector.
url: https://docs.tealium.com/server-side-connectors/selligent-by-marigold-connector/
---
For more information about the Selligent APIs, see the [Selligent Marketing Cloud API Explorer.](https://partners.slgnt.eu/Portal/Api/swagger/ui/index#!/)

## Batch limits

This connector uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 2500
* Max time since oldest request: 10 minutes
* Max size of requests: 20 MB

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors](https://docs.tealium.com/about-connectors/) article.

After adding the connector, configure the following settings:

* **Server URL**  
Your Selligent base URL. Include the `https` value in your server URL.  For example, `https://example.sIgnt.eu`.
* **Organization**  
Your organization. Must match the organization in the upper-right corner of the **Selligent Admin Configuration** screen.
* **API Key**  
Generated from **Selligent Admin Configuration**.
* **API Secret**  
Generated from **Selligent Admin Configuration**.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Upsert To List| ✓| ✓|
|Delete From List| ✓| ✓|
|Add to Segment| ✓| ✓|
|Delete from Segment| ✓| ✓|
|Trigger Custom Journey| ✓| ✓|
|Trigger Transactional Message| ✓| ✓|

### Upsert To List

API Endpoint: `https://partners.slgnt.eu/Portal/Api/swagger/ui/index#!/Data/Data_LoadData`

This endpoint loads user data into the list with the given API name in the given organization, similar to subscribing or updating a user within a specific list. Lists are comparable to audiences. The list is retrieved based on your credentials and organization inputted in the Configuration screen.

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|List| Select a Selligent list. The list retrieves specific fields that are required for data mapping in the Data Configuration section. |
|Data| The data to be mapped is dependent on the data required from the list retrieved and selected from the list selection. The list fields that are retrieved must specify the expected data type of the field or column within the list table. For additional questions about mapping, contact your Selligent and Tealium Account Managers.|

### Delete From List

API Endpoint: `https://partners.slgnt.eu/Portal/Api/swagger/ui/index#!/Data/Data_DeleteData`

This endpoint deletes data from the list with the given API name in the given organization. Use this action to remove a user and subsequently unsubscribe them from a given list. For example, when someone leaves an audience.

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|List| Select a Selligent list. The list retrieves specific fields that are required for data mapping in the Data Configuration section. |
|Data| The data to be mapped is dependent on the data required from the list retrieved and selected from the list selection. The list fields that are retrieved must specify the expected data type of the field or column within the list table. If updating a customer record, use the Upsert action.|

### Add to Segment

API Endpoint: `https://partners.slgnt.eu/Portal/Api/swagger/ui/index#!/Data/Data_LoadSegmentData`

This endpoint loads data into the segment with the given Segment API name in the list with the given API name in the given organization. Use this action to subset user data into a segment within a list. This action can be used to add users to targeted static segments within lists within the Selligent Platform.

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|List| Select a Selligent list. The list retrieves specific fields that are required for data mapping in the Data Configuration section. |
|Segment| Select a segment. Provides only static segments that can be used to subscribe a user to that segment.|
|Data| The data to be mapped is dependent on the data required from the list retrieved and selected from the list selection. The list fields that are retrieved must specify the expected data type of the field or column within the list table.|

### Delete from Segment

API Endpoint: ` https://partners.slgnt.eu/Portal/Api/swagger/ui/index#!/Data/Data_DeleteSegmentData`

This endpoint deletes data through JSON from the segment with the given Segment API name in the list with the given API name in the given organization. Use this action to unsubscribe a user from a segment. The delete action does not delete the segment, but instead deletes the user from the supported segment.

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|List| Select a Selligent list. The list retrieves specific fields that are required for data mapping in the Data Configuration section. |
|Segment| Provides only static segments created within Selligent Marketing Cloud list and deletes the user from the segment.|
|Data| The data to be mapped is dependent on the data required from the list retrieved and selected from the list selection. The list fields that are retrieved must specify the expected data type of the field or column within the list table.|

### Trigger Custom Journey

API Endpoint: `https://partners.slgnt.eu/Portal/Api/swagger/ui/index#!/Custom/Custom_TriggerEntryPoint`

This action triggers a specific start component in the custom journey. Use this action to add a user to a custom Customer Journey and select an entry point step for the user to be inserted into.

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Journey| Select a Selligent custom journey. This journey is retrieved based on the created customer journeys within your Selligent Platform. `Journey` returns only the `custom` types of customer journeys created.|
|Journey Entry Point| Select a journey entry point to add the user to. |
|User ID| The ID of the user for whom the campaign is triggered.|

### Trigger Transactional Message

API Endpoint: `https://partners.slgnt.eu/Portal/Api/swagger/ui/index#!/Transactional/Transactional_Send`

This endpoint can be used to trigger the transactional message with the given API name in the given organization. Use this action to send a transactional email to a designated recipient and with a specific language designation. You can also use this action to kick off a particular journey. For example, if you want to send an email directly from Tealium. The action sends a message through the transactional journeys created within the Selligent platform. This action can be used in scenarios where a transactional customer journey is already created and for sending a message to the user for the transactional journey.

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Transactional Journey| Select a Selligent transactional journey. Transactional customer journeys will be retrieved and populated in this field.|
|Recipient| (Required) The recipient to whom the content should be sent.|
|Language| (Required) The language in which the email should be sent.|
| Lookup | Determines which profile field Selligent uses to find the recipient. If left unmapped, the `lookup` field is omitted from the request and Selligent applies its server-side default `MASTER.MAIL` (the main audience email field). Map a value in the form `SCOPE.FIELD` only when your transactional setup identifies contacts by another field or related profile scope. |
| External ID | Optional external ID for this message send. Used to track requests. |
