---
title: Modules
description: A list of the available modules.
url: https://docs.tealium.com/platforms/ios-swift/modules/
---The Tealium Swift library is designed around a modular architecture. Required modules must be specified when the library is initialized in the `TealiumConfig` instance.

All modules have a dependency on `TealiumCore`. Modules are separated into `Collectors` and `Dispatchers` depending on their purpose.

## Collectors

Collectors are modules that gather supplemental information from the device and append it to the data layer before it&#39;s transmitted to the Tealium Customer Data Hub. Some collectors are included in the core library, while others are optional and installed as separate modules.

The following table lists the available collectors.

| Collector Name | TealiumConfig Reference |
| --- | --- |
| `AppData`* | `Collectors.AppData`|
| `Attribution` | `Collectors.Attribution`|
| `Connectivity`* | `Collectors.Connectivity`|
| `Device`* | `Collectors.Device`|
| `Crash` | `Collectors.Crash`|
| `AutoTracking` | `Collectors.AutoTracking `|
| `Lifecycle` | `Collectors.Lifecycle`|
| `Location` | `Collectors.Location`|
| `VisitorService` | `Collectors.VisitorService`|

Modules marked with an asterisk (`*`) are included with the core library. They are enabled by default, but can be disabled using the `TealiumConfig` `collectors` property as described below. 

### Usage

To add a `Collector`, specify it in the `collectors` property of the `TealiumConfig` instance:

```swift
import TealiumCore
import TealiumLifecycle

let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                               profile: &#34;PROFILE&#34;,
                               environment: &#34;ENVIRONMENT&#34;,
                               datasource: &#34;DATASOURCE&#34;)

// Adds the Collectors you want. If omitted, default Collectors are added.
config.collectors = [Collectors.AppData, Collectors.Device, Collectors.Connectivity, Collectors.Lifecycle]                               
```

To only use the default collectors, omit or comment out the `config.collectors` line from your initialization code. 

When adding new collectors, be sure to also include `Collectors.Device` and `Collectors.Connectivity` in the array, otherwise these collectors will be disabled.

The AppData collector can&#39;t be disabled, because it collects critical information, such as the Tealium Visitor ID.

### Custom Collectors

Although custom collectors are generally not required, it is possible to build a custom collector by creating your own class conforming to the `Collector` protocol. The following example shows a simple collector that gathers the current weekday and appends it to the data layer for each tracking call.

```swift
class MyDateCollector: Collector {
    var id = &#34;MyDateCollector&#34;

    var data: [String : Any]? {
        [&#34;day_of_week&#34;: dayOfWeek]
    }

    var context: TealiumContext

    required init(context: TealiumContext,
                  delegate: ModuleDelegate?,
                  diskStorage: TealiumDiskStorageProtocol?,
                  completion: (ModuleResult) -&gt; Void) {
        self.context = context
    }

    var dayOfWeek: String {
        return &#34;\(Calendar.current.dateComponents([.weekday], from: Date()).weekday ?? -1)&#34;
    }
}

// Add collector to your config instance prior to Tealium initialization

class TealiumHelper {
	// ...
	func startTracking() {
		let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                               profile: &#34;PROFILE&#34;,
                               environment: &#34;ENVIRONMENT&#34;,
                               datasource: &#34;DATASOURCE&#34;)

// Add the Collectors you want. If omitted, default Collectors are added.
config.collectors = [Collectors.AppData,
					  Collectors.Lifecycle,
					  MyDateCollector.self]   
					  self.tealium = Tealium(config: config) { _ in }
	}
}
```

## Dispatchers

Dispatchers are modules that send the data from your data layer and send it to a Tealium endpoint. The following dispatchers are currently available:

| Dispatcher Name | TealiumConfig Reference |
| --- | --- |
| `Collect` | `Dispatchers.Collect`|
| `RemoteCommands` | `Dispatchers.RemoteCommands`|
| `TagManagement` | `Dispatchers.TagManagement`|

At least one dispatcher is required. If no dispatchers are specified, your data is not sent anywhere.

### Usage

To add a `Dispatcher`, specify it in the `dispatchers` property of the `TealiumConfig` object:

```swift
import TealiumCore
import TealiumLifecycle

let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                               profile: &#34;PROFILE&#34;,
                               environment: &#34;ENVIRONMENT&#34;,
                               datasource: &#34;DATASOURCE&#34;)

// Add the Collectors. you want Do not include if you want to use compiled Collectors
config.dispatchers = [Dispatchers.Collect]                               
```

### Custom Dispatchers

Although custom dispatchers are generally not required, it is possible to build a custom `Dispatcher` by creating your own class conforming to the `Dispatcher` protocol. The following example shows a simple dispatcher that prints the event name for each track request. A custom `Dispatcher` may be useful if you want to send data to your own custom endpoint in addition to the Tealium endpoints.

```swift
class MyCustomDispatcher: Dispatcher {
    var isReady: Bool
    var id = &#34;MyCustomDispatcher&#34;
    var config: TealiumConfig

    required init(config: TealiumConfig, delegate: ModuleDelegate, completion: ModuleCompletion?) {
        self.config = config
        self.isReady = true
    }

    func dynamicTrack(_ request: TealiumRequest, completion: ModuleCompletion?) {
        switch request {
        case let request as TealiumTrackRequest:
            print(&#34;Track received: \(request.event ?? &#34;no event name&#34;)&#34;)
            // perform track action. For example, send to custom endpoint
        case _ as TealiumBatchTrackRequest:
            print(&#34;Batch track received&#34;)
            // perform batch track action. For example, send to custom endpoint
        default:
            return
        }
    }
}

// Add dispatcher to your config instance prior to Tealium initialization
class TealiumHelper {
	// ...
	func startTracking() {
		let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                               profile: &#34;PROFILE&#34;,
                               environment: &#34;ENVIRONMENT&#34;,
                               datasource: &#34;DATASOURCE&#34;)

   // add the Dispatchers you want
   config.dispatchers = [Dispatchers.Collect, MyCustomDispatcher.self]      
					  self.tealium = Tealium(config: config) { _ in }
}
```

## Recommended Modules

### Base Implementation

For a base implementation, the following list of modules is recommended. At least one `Dispatcher` needs to be enabled, depending on which Tealium products you plan to use.

* AppData Collector
* Device Collector
* Lifecycle Collector

### Client-side

In addition to the base modules, these modules enable the Tealium library to process data client-side using Tealium iQ.

* TagManagement Dispatcher - Required to use Tealium iQ
* RemoteCommands Dispatcher - Only required if you need Remote Commands functionality


### Server-side

In addition to the base modules, these modules enable the library to send data to Tealium&#39;s server-side products (EventStream, AudienceStream, Event Data Framework).

* Collect Dispatcher - Required to use any server-side products
* Visitor Service Collector - Only required to retrieve Visitor Profiles from Tealium AudienceStream.

## Install Modules

Install the modules with CocoaPods or Carthage.

### CocoaPods

See [Install with CocoaPods](/platforms/ios-swift/install/#cocoapods) for instructions on including and excluding specific modules.

### Carthage

When you install with Carthage, you must explicitly import the modules you require. You may import all modules if you prefer, and use the module list, as described earlier, but your app is lighter if you only import the modules you need. See [Install with Carthage](/platforms/ios-swift/install/#carthage) for instructions on including/excluding specific modules.

### Swift Package Manager

See [Install with Swift Package Manager](/platforms/ios-swift/install#swift-package-manager-recommended) for instructions on including and excluding specific modules.
