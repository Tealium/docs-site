---
title: Amazon EventBridge Connector Setup Guide
description: This article describes how to set up the Amazon EventBridge connector.
url: https://docs.tealium.com/server-side-connectors/amazon-eventbridge-connector/
---
## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Send Event Data to Event Source| ✗| ✓|
|Send Visitor Data to Event Source| ✓| ✗|
|Send Customized Data to Event Source (Advanced)| ✓| ✓|

## Configure Settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors](https://docs.tealium.com/about-connectors/) article.

After adding the connector, configure the following settings:

* **Account ID**  
Enter your Account ID.
* **Region**  
(Required) select region.

Click **Done** when you are finished configuring the connector.

## Action Settings — Parameters and Options

Click **Continue** to configure the connector actions. Enter in a name for the action and then select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Action — Send Event Data to Event Source

#### Parameters

| **Parameter**         | **Description**                                                                                                                                                                                                                                                           |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Event Source          | Select partner event source to send data to.                                                                                                                                                                                                                              |
| Detail Type           | A free-form string used to decide what fields to expect in the event detail. For more information about Detail Type, read [Amazon EventBridge API PutPartnerEvents documentation](https://docs.aws.amazon.com/eventbridge/latest/APIReference/API_PutPartnerEvents.html). |
| Resources             | AWS resources, identified by Amazon Resource Name (ARN), which the event primarily concerns.<br> Any number, including zero, may be present.                                                                                                                              |
| Print Attribute Names | If attribute names get updated, the names in the payload will reflect the update.                                                                                                                                                                                         |
|                       |                                                                                                                                                                                                                                                                           |
### Action — Send Visitor Data to Event Source

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Event Source| Select partner event source to send data to.|
|Detail Type| A free-form string used to decide what fields to expect in the event detail.|
|Resources| AWS resources, identified by Amazon Resource Name (ARN), which the event primarily concerns.<br> Any number, including zero, may be present.|
| Include Current Visit Data With Visitor Data | Add the current visit data to the payload. This includes event visit data if Exclude Current Visit Event Data isn't selected. |
| Exclude Current Visit Event Data | Exclude event data from the current visit data. |
|Print Attribute Names| If attribute names get updated, the names in the payload will reflect the update.|

### Action — Send Customized Data to Event Source (Advanced)

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Event Source| Select partner event source to send data to.|
|Detail Type| A free-form string used to decide what fields to expect in the event detail.|
|Resources| AWS resources, identified by Amazon Resource Name (ARN), which the event primarily concerns.<br> Any number, including zero, may be present.|
|Custom Message Definition|
|Message Template Variables| (Optional) Provide template variables as data input for templates. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).<br> Name nested template variables with the dot notation (Example: `items.name`).<br> Nested template variables are typically built from data layer list attributes.|
|Message Templates| (Optional) Provide templates to be referenced in either URL, URL Parameter, Header or Body Data. For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).<br> Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.|