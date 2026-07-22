---
title: Connectivity Module
description: Gathers information about the device's network connection and adds it to the data layer for each event.
url: https://docs.tealium.com/platforms/ios-swift/module-list/connectivity/
---
## Usage
Usage of this module is recommended.

The following platforms are supported:

* iOS
* tvOS
* macOS
* watchOS

## Install

This module is included as part of the Core library, and does not require separate installation.

## Initialize

To initialize the module, verify that it's specified on the `TealiumConfig` [`collectors`](https://docs.tealium.com/platforms/ios-swift/api/tealium-config/#collectors) property

`config.collectors = [Collectors.Connectivity]`


<blockquote>
Review the [Collectors](https://docs.tealium.com/platforms/ios-swift/modules/#collectors) documentation to understand how to correctly specify the collectors you require.
</blockquote>


## Data Layer
The following variables are transmitted with each tracking call while the module is enabled:

| Variable   | Description                                                                                                                      | Example  |
|------------|----------------------------------------------------------------------------------------------------------------------------------|---------------|
| `connection_type`   | Current connection type                                                               | [`"wifi"`, `"cellular"`]             |
