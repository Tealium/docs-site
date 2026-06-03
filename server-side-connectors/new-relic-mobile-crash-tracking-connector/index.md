---
title: New Relic Mobile Crash Tracking Connector Setup Guide
description: Apps crash. You want to know why. With the New Relic Mobile Crash connector, you can find out all the reasons your apps crashed, and how you can solve and prevent those crashes quickly and easily. This article describes how to configure the New Relic Mobile Crash connector in your Customer Data Hub account.
url: https://docs.tealium.com/server-side-connectors/new-relic-mobile-crash-tracking-connector/
---
## How it works

In the event of a system crash, incoming data from live events is captured. Crash tracking connectors in the UDH can then utilize cloud delivery methods to forward crash data to vendors and customize the display of relevant data in live events.

### Requirements

* New Relic Account
* API Key

#### Recommended SDK modules:

* [Tealium for Android Crash Reporter Module](/platforms/android-java/module-list/crash-reporter/)

### Supported Actions

| **Action Name**          | **Trigger on Audiences** | **Trigger on Events** |
|:-------------------------|:-------------------------|:----------------------|
| Send Android Crash Event | ✗                        | ✓                     |

## Configure Settings

Go to the Connector Marketplace and add a new New Relic Mobile Crash connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

To configure your vendor, follow these steps:

1. In the **Configure** tab, provide a title for the connector instance.

1. Enter the API key that you received from New Relic for your account.

1. Provide additional notes about your implementation.

## Action Settings: Parameters and Options

Click **Next** or go to the **Actions** tab. It&#39;s where you&#39;ll set up actions and trigger them.

This section describes how to set up parameters and options for each action.

### Action: Send Android Crash Event

The connector automatically maps event attributes to the requisite fields before being sent over to New Relic.

#### Parameters

1. **Crash Event Attributes**: These parameters allow for you to override the default mappings.

#### Options: Crash Event Attributes

| **Option**                   | **Description**                                                                                | **Example**                                                                                                                                                                                                                               |
|:-----------------------------|:-----------------------------------------------------------------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| App Name                     | User-readable app name                                                                         | `My App`                                                                                                                                                                                                                                  |
| App Build                    | App build ID                                                                                   | `1`                                                                                                                                                                                                                                       |
| App RDNS                     | Bundle ID                                                                                      | `com.tealium.example`                                                                                                                                                                                                                     |
| App UUID                     | Install ID                                                                                     | `a4cc5192-cde5-4788-bb0a-fc7c06ac07eb`                                                                                                                                                                                                    |
| App Version                  | Version                                                                                        | `1.0.1`                                                                                                                                                                                                                                   |
| Connection Type              | Internet connection                                                                            | `WIFI`                                                                                                                                                                                                                                    |
| Crash Build ID               | Build ID                                                                                       | `c0319246-ff40-4fdc-877f-7341ad48f52c`                                                                                                                                                                                                    |
| Crash Cause                  | Human readable cause                                                                           | `Index out of bounds`                                                                                                                                                                                                                     |
| Crash Name                   | App-generated name                                                                             | `java.lang.RuntimeException`                                                                                                                                                                                                              |
| Crash Process ID             | `Low-level process ID`                                                                         |                                                                                                                                                                                                                                           |
| Crash Threads                | Array of stringified JSON                                                                      | `[&#34;{&#34;crashed&#34;:true, &#34;state&#34;:&#34;RUNNABLE&#34;, &#34;threadNumber&#34;:1, &#34;threadId&#34;:&#34;main&#34;, &#34;priority&#34;:5,&#34;stack&#34;: [{&#34;className&#34;: &#34;com.tealium.example.fragment.ControlFragment&#34;, &#34;methodName&#34;:&#34;onClick&#34;, &#34;lineNumber&#34;:89}]}&#34;]` |
| Crash UUID                   | Unique crash identifier                                                                        | `c0319246-ff40-4fdc-877f-7341ad48f52c`                                                                                                                                                                                                    |
| Device                       | Device name                                                                                    | `motorola`                                                                                                                                                                                                                                |
| Device CPU Type              | Architecture                                                                                   | `armv7l`                                                                                                                                                                                                                                  |
| Device Free System Storage   | Space available in bytes                                                                       | `48189440`                                                                                                                                                                                                                                |
| Device Free External Storage | Space available in bytes                                                                       | `2208235520`                                                                                                                                                                                                                              |
| Device Memory Usage          | RAM usage percentage                                                                           | `62`                                                                                                                                                                                                                                      |
| Device Model                 | Technical model number                                                                         | `XT1028`                                                                                                                                                                                                                                  |
| Device Orientation           | 0-3 according to the [docs](https://developer.android.com/reference/android/view/Surface.html) | `1` (90 degree rotation)                                                                                                                                                                                                                    |
| Device OS Version            | Major OS version                                                                               | `5.1`                                                                                                                                                                                                                                     |
| Device OS Build              | OS Build version                                                                               | `2`                                                                                                                                                                                                                                       |
| Device Resolution            | Screen resolution                                                                              | `1024x768` or `normal`                                                                                                                                                                                                                    |
| Device Runtime               | Runtime version                                                                                | `2.1.0`                                                                                                                                                                                                                                   |
| Platform                     | Platform name                                                                                  | `Android`                                                                                                                                                                                                                                 |
| Timestamp Epoch              | ms since epoch                                                                                 | `1497563845000`                                                                                                                                                                                                                           |
