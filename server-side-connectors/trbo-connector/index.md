---
title: trbo Connector Setup Guide
description: This article describes how to set up the trbo connector. Use trbo’s onsite personalization platform to address customers individually and personally in real time!
url: https://docs.tealium.com/server-side-connectors/trbo-connector/
---
## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Send Visitor Profile| ✓| ✗|

## Configure Settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors](https://docs.tealium.com/about-connectors/) article.

After adding the connector, configure the following settings:

* **Shop ID**  
The Shop ID of your trbo shop, which appears in the trbo interface.
* **Client ID**  
The Client ID of your trbo connection.
* **App Secret**  
The Secret key of your trbo connection.

Click **Done** when you are finished configuring the connector.

## Action Settings — Parameters and Options

Click **Continue** to configure the connector actions. Enter in a name for the action and then select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Action — Send Visitor Profile

#### Parameters

No parameters or options required.

This connector sends the entire visitor JSON object. For more information, read [the AudienceStore Data Guide](https://docs.tealium.com/audiencestore-data-guide/).
