---
title: Changelog
url: https://docs.tealium.com/server-side/connectors/webhook-connectors/changelog/
---
### 2024-07-10

Added the following actions to all HTTP-based webhook connectors:
  * **Send Event Data via HTTP Request**
  * **Send Visitor Data via HTTP Request**
  * **Send Batched Visitor Data via HTTP Request**

### 2021-11-30

* Added configuration option for Webhook connectors to support 302 responses when configured.

### 2021-07-20

* In the Connector Actions table, added links to each action.

### 2021-06-07

* Added Action - Send Batched Customized Data via HTTP Request (Advanced) action and Batch Limitations section

### 2020-11-05

* Added batch support for the Webhook 2-Legged OAuth2 and 3-Legged OAuth2 connectors.

### 2018-12-18

* Disabled Apache cookie management for Webhook connector to prevent domain-level cookies from being shared.

### 2017-08-24

* Added two new actions: Send Event Data via HTTP Request and Send Visitor Data via HTTP Request.
* Removed the following two Actions: POST-visitor and PUT-visitor. Though the actions are no longer displayed in the Actions drop-down list, Tealium continues to support them if the actions are currently installed in your profile.

### 2017-03-02

* Added new Webhook OAuth2 Connector for supporting OAuth service. This service is separate from the Webhook (BasicAuth) Connector.

### 2016-11-13

* Added new Send Custom Request Action to support complex JSON and XML payloads. Supports a built-in template utility for translating nested JSON.
* Moved GET, POST, and PUT methods under the new Action. They are no longer treated as separate Actions

### 2016-06-14

* The AudienceDirect Connector has been retired in favor of Webhook.
* The POST-visitor and PUT-Visitor Actions are now integrated in the new Webhook (BasicAuth) Connector.
* If your profile contains any deprecated/non-functional AudienceDirect Actions, you must reconfigure them in a new Webhook instance.
