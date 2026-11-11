---
title: Heap Connector Setup Guide
description: This article describes how to set up the Heap connector.
url: https://docs.tealium.com/server-side-connectors/heap-connector/
---
## Connector Actions

| Action name | Visitor profile | Event data |
| --- | :---: | :---: |
|Add User Properties| ✓| ✗|
|Track| ✗| ✓|

## Configure Settings

Go to the connector marketplace and add a new connector. For more information, see [about-connectors](https://docs.tealium.com/about-connectors/).

## Action Settings - Parameters and Options

Click **Continue** to configure the connector actions. Enter a name for the action and select the action type from the list.

### Action - Add User Properties

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|App ID|  <ul><li>The `app_id` corresponding to one of your projects.</li></ul> |
|Identity|  <ul><li>An identity, typically corresponding to an existing user.</li><li>If no such identity exists, a new user is created with that identity.</li><li>Limited to 255 characters.</li><li>For more information, see: [Heap: Add User Properties](https://developers.heap.io/docs/using-identify)</li></ul> |
|User Properties|  <ul><li>An object with key-value properties you want associated with the user.</li><li>Each key and property must either be a number or string with fewer than 1024 characters.</li><li>For more information, see: [Heap: Add User Properties](https://developers.heap.io/docs/using-identify)</li></ul> |

### Action - Track

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|App ID|  <ul><li>The `app_id` corresponding to one of your projects.</li></ul> |
|Identity|  <ul><li>An identity, typically corresponding to an existing user.</li><li>If no such identity exists, then a new user will be created with that identity.</li><li>Limited to 255 characters.</li><li>For more information, see the [Heap documentation](https://developers.heap.io/reference#track).</li></ul> |
|Event|  <ul><li>The name of the server-side event.</li><li>Limited to 1024 characters.</li><li>For more information, see the [Heap documentation](https://developers.heap.io/reference#track).</li></ul> |
|Properties|  <ul><li>An object with key-value properties you want associated with the user.</li><li>Each key and property must either be a number or string with fewer than 1024 characters.</li><li>For more information, see the [Heap documentation](https://developers.heap.io/reference#track).</li></ul> |
|Timestamp|  <ul><li>ISO 8601 or Unix epoch milliseconds.</li><li>Example: `2017-03-10T22:21:56+00:00`</li><li>For more information, see the [Heap documentation](https://developers.heap.io/reference#track).</li></ul> |
