---
title: Heap Connector Setup Guide
description: This article describes how to set up the Heap connector.
url: https://docs.tealium.com/server-side-connectors/heap-connector/
---
## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Add User Properties| ✓| ✗|
|Track| ✗| ✓|

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a connector.

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

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
