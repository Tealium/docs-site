---
title: Acoustic Exchange Connector Setup Guide
url: https://docs.tealium.com/server-side-connectors/acoustic-exchange-connector/
---## Requirements

* Acoustic Exchange Account
* Tealium Events Endpoint Authentication Key

## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Publish Cart Abandonment Events| ✓| ✗|
|Publish Cart Purchase Events| ✓| ✓|
|Publish Event| ✓| ✓|

## Configure Settings

Go to the **Connector Marketplace** and add a new connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **Endpoint Authentication Key**
  * Required
  * Enter endpoint authentication key.
  * For more information, see: [Endpoints Overview](https://help.goacoustic.com/hc/en-us/articles/360043302213-Endpoints-overview).

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action: Publish Cart Abandonment Events

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Channel|  <ul><li>(Required) Select channel where the event was observed.</li><li>For more information, see: [Event Catalog](https://developer.goacoustic.com/acoustic-exchange/docs/acoustic-exchange-event-catalog).</li></ul> |
|Sub Channel|  <ul>(Recommended) Select sub channel to classify further where the event was observed.</li><li>If selected channel does not have a fitting predefined sub channel to choose from, enter one manually as a custom value or leave blank.</li></ul> |

### Action: Publish Cart Purchase Events

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Channel|  <ul><li>(Required) Select channel where the event was observed.</li><li>For more information, see: [Event Catalog](https://developer.goacoustic.com/acoustic-exchange/docs/acoustic-exchange-event-catalog).</li></ul> |
|Sub Channel|  <ul><li>(Recommended) Select sub channel to classify further where the event was observed.</li><li>If selected channel does not have a fitting predefined sub channel to choose from, enter one manually as a custom value or leave blank.</li></ul> |

### Action: Publish Event

##### Parameters

|**Parameter**| **Description**|
|---| ---|
|Event Type|  <ul><li>(Required) Select event type.</li><li>For more information and a list of available events, see [Dynamic Event Library](https://exchange-us-1.goacoustic.com/#/taxonomy).</li></ul> |
|Channel|  <ul><li>(Required) Select channel where the event was observed.</li><li>For more information, see: [Event Catalog](https://developer.goacoustic.com/acoustic-exchange/docs/acoustic-exchange-event-catalog).</li></ul> |
|Sub Channel|  <ul><li>( Recommended) Select sub channel to classify further where the event was observed.</li><li>If selected channel does not have a fitting predefined sub channel to choose from, enter one manually as a custom value or leave blank.</li></ul> |
