---
title: Working with Objective-C
description: Learn about creating a bridging header to work between Objective-C and Swift.
url: https://docs.tealium.com/platforms/ios-swift/with-objective-c/
---We recommend using our native Swift library, even for Objective-C projects, but if you still need to use the Objective-C library, this document helps.

## Call Objective-C from Swift
Call the Objective-C library from Swift code by simply adding a bridging header to your project, and importing the appropriate headers.

### Bridging Header
To create a bridging header:

1. In your Swift project, create a new file. When prompted to select a file type, select Objective-C File.
2. Give this file a temporary name, such as "placeholder.m", as you are going to remove it later.
3. Click "Finish" and XCode prompts you to create a Bridging Header (if it doesn't, you probably already have a Bridging Header in your project). Press "Create Bridging Header" to continue, and Xcode automatically creates the new header file for you.
4. Delete the `placeholder.m` file from the project and notice a new file called `<ProjectName>-Bridging-Header.h`
5. Add the following import statement to the new Bridging Header:  
      ```objc
      @import TealiumIOS;
      ```

      Next, to call the Objective-C code from Swift:

      ```objc
      class TealiumHelper {
          func somefunc () {
              let tealConfig = TEALConfiguration.init(account: "ACCOUNT", profile: "PROFILE", environment: "ENVIRONMENT")
              let teal = Tealium.newInstance(forKey: "KEY", configuration: tealConfig)
              teal.trackView(withTitle: "SCREEN_NAME", dataSources: ["DATA":"VALUE"])
          }
      }
      ```
## Call Swift from Objective-C

The Swift library cannot be directly called from Objective-C, since it is missing the required annotations in the code, and in many cases, modules do not inherit from NSObject, rather they use the native Swift data types.
However, by using an intermediate helper class, it is possible to call the Swift library from Objective-C.

### Helper Class

1. In your Objective-C project, create a new Swift file. You are prompted to add a bridging header if you don't already have one. Accept this prompt. Name the new Swift file "TealiumHelper.swift".
2. Import the new Swift header (`<ProjectName>-Swift.h`) into files that need to call the new helper.  
      ```objc
      #import "ProjectName-Swift.h"
      ```

The methods in the helper file are now be available to use in your Objective-C code. We recommend making the helper a singleton.

```objc
#import "TestSwiftBridge-Swift.h"

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
	// instantiate the helper singleton
    TealiumHelper * help = [TealiumHelper sharedInstance];
    // call the start method, which initializes the Tealium library
    [help start];
    // trigger a new event tracking call from objective-c
    [help track:@"this is from objective-c!" data:@{@"mydata":@"hello from obj-c"}];
    return YES;
}
```

### Sample TealiumHelper file

```swift
// 
// TealiumHelper.swift
//
//  Copyright © 2021 Tealium, Inc. All rights reserved.
//

import TealiumCollect
import TealiumCore
import TealiumLifecycle
import TealiumVisitorService
#if os(iOS)
import TealiumAttribution
import TealiumLocation
import TealiumRemoteCommands
import TealiumTagManagement
#endif

enum TealiumConfiguration {
    static let account = "tealiummobile"
    static let profile = "demo"
    static let environment = "dev"
    static let dataSourceKey = "abc123"
}

// Change this to false to disable all the Tealium logs
let enableHelperLogs = true

@objc
class TealiumHelper: NSObject {
    
    @objc
    static let shared = TealiumHelper()

    let config = TealiumConfig(account: TealiumConfiguration.account,
                               profile: TealiumConfiguration.profile,
                               environment: TealiumConfiguration.environment,
                               dataSource: TealiumConfiguration.dataSourceKey)

    var tealium: Tealium?

    // MARK: Tealium Initilization
    private override init() {
        super.init()
        // Optional Config Settings
        if enableHelperLogs { config.logLevel = .info }

// Optional - Only required if using Visitor Service
//        config.visitorServiceDelegate = self

// Optional - Only required if using Consent Manager
//        config.consentLoggingEnabled = true
//        config.consentPolicy = .ccpa

// Optional - Only required if using Hosted Data Layer
//        config.hostedDataLayerKeys = ["hdl-test": "product_id"]
// Optional - Only required if using Timed Events
//        config.timedEventTriggers = [TimedEventTrigger(start: "product_view", end: "order_complete"),
//                                     TimedEventTrigger(start: "start_game", end: "buy_coins")]

        #if os(iOS)
        // Add dispatchers
        config.dispatchers = [Dispatchers.TagManagement, Dispatchers.RemoteCommands, Dispatchers.Collect]
        #else
        config.dispatchers = [Dispatchers.Collect]
        #endif

        // Add collectors
        #if os(iOS) && targetEnvironment(macCatalyst)
        // Optional - Only required if using Visitor Service
        config.collectors = [Collectors.VisitorService]
        #elseif os(iOS) && !targetEnvironment(macCatalyst)
        config.collectors = [Collectors.Attribution, Collectors.VisitorService, Collectors.Location]

         // Batching:
         config.batchingEnabled = false // true to enable

        // Location - Geofence Monitoring:
//        config.geofenceUrl = "https://tags.tiqcdn.com/dle/tealiummobile/location/geofences.json"
//        config.useHighAccuracy = true
//        config.updateDistance = 200.0
        
        // SKAdNetwork event handling
        config.searchAdsEnabled = true
        config.skAdAttributionEnabled = true
        config.skAdConversionKeys = ["conversion_event": "conversion_value"]

        // Remote Commands:
        let remoteCommand = RemoteCommand(commandId: "hello", description: "world") { response in
            guard let payload = response.payload else {
                return
            }
            // Do something w/remote command payload
            if enableHelperLogs {
                print(payload)
            }
        }
        config.addRemoteCommand(remoteCommand)
        #endif

        tealium = Tealium(config: config) { _ in
            // Optional post init processing
            self.tealium?.dataLayer.add(data: ["somekey": "someval"], expiry: .afterCustom((.months, 1)))
            self.tealium?.dataLayer.add(key: "someotherkey", value: "someotherval", expiry: .forever)
        }
    }
    
    @objc
    public func start() {
        _ = TealiumHelper.shared
    }
    
    @objc
    func resetConsentPreferences() {
        tealium?.consentManager?.resetUserConsentPreferences()
    }
    
    @objc
    func track(title: String, data: [String: Any]?) {
        let dispatch = TealiumEvent(title, dataLayer: data)
        tealium?.track(dispatch)
    }

    @objc
    func trackView(title: String, data: [String: Any]?) {
        let dispatch = TealiumView(title, dataLayer: data)
        tealium?.track(dispatch)
    }

    @objc
    func joinTrace(_ traceID: String) {
        tealium?.joinTrace(id: traceID)
    }

    @objc
    func leaveTrace() {
        tealium?.leaveTrace()
    }
}
```
