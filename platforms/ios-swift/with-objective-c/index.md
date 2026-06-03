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
2. Give this file a temporary name, such as &#34;placeholder.m&#34;, as you are going to remove it later.
3. Click &#34;Finish&#34; and XCode prompts you to create a Bridging Header (if it doesn&#39;t, you probably already have a Bridging Header in your project). Press &#34;Create Bridging Header&#34; to continue, and Xcode automatically creates the new header file for you.
4. Delete the `placeholder.m` file from the project and notice a new file called `&lt;ProjectName&gt;-Bridging-Header.h`
5. Add the following import statement to the new Bridging Header:  
      ```objc
      @import TealiumIOS;
      ```

      Next, to call the Objective-C code from Swift:

      ```objc
      class TealiumHelper {
          func somefunc () {
              let tealConfig = TEALConfiguration.init(account: &#34;ACCOUNT&#34;, profile: &#34;PROFILE&#34;, environment: &#34;ENVIRONMENT&#34;)
              let teal = Tealium.newInstance(forKey: &#34;KEY&#34;, configuration: tealConfig)
              teal.trackView(withTitle: &#34;SCREEN_NAME&#34;, dataSources: [&#34;DATA&#34;:&#34;VALUE&#34;])
          }
      }
      ```
## Call Swift from Objective-C

The Swift library cannot be directly called from Objective-C, since it is missing the required annotations in the code, and in many cases, modules do not inherit from NSObject, rather they use the native Swift data types.
However, by using an intermediate helper class, it is possible to call the Swift library from Objective-C.

### Helper Class

1. In your Objective-C project, create a new Swift file. You are prompted to add a bridging header if you don&#39;t already have one. Accept this prompt. Name the new Swift file &#34;TealiumHelper.swift&#34;.
2. Import the new Swift header (`&lt;ProjectName&gt;-Swift.h`) into files that need to call the new helper.  
      ```objc
      #import &#34;ProjectName-Swift.h&#34;
      ```

The methods in the helper file are now be available to use in your Objective-C code. We recommend making the helper a singleton.

```objc
#import &#34;TestSwiftBridge-Swift.h&#34;

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
	// instantiate the helper singleton
    TealiumHelper * help = [TealiumHelper sharedInstance];
    // call the start method, which initializes the Tealium library
    [help start];
    // trigger a new event tracking call from objective-c
    [help track:@&#34;this is from objective-c!&#34; data:@{@&#34;mydata&#34;:@&#34;hello from obj-c&#34;}];
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
    static let account = &#34;tealiummobile&#34;
    static let profile = &#34;demo&#34;
    static let environment = &#34;dev&#34;
    static let dataSourceKey = &#34;abc123&#34;
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
//        config.hostedDataLayerKeys = [&#34;hdl-test&#34;: &#34;product_id&#34;]
// Optional - Only required if using Timed Events
//        config.timedEventTriggers = [TimedEventTrigger(start: &#34;product_view&#34;, end: &#34;order_complete&#34;),
//                                     TimedEventTrigger(start: &#34;start_game&#34;, end: &#34;buy_coins&#34;)]

        #if os(iOS)
        // Add dispatchers
        config.dispatchers = [Dispatchers.TagManagement, Dispatchers.RemoteCommands, Dispatchers.Collect]
        #else
        config.dispatchers = [Dispatchers.Collect]
        #endif

        // Add collectors
        #if os(iOS) &amp;&amp; targetEnvironment(macCatalyst)
        // Optional - Only required if using Visitor Service
        config.collectors = [Collectors.VisitorService]
        #elseif os(iOS) &amp;&amp; !targetEnvironment(macCatalyst)
        config.collectors = [Collectors.Attribution, Collectors.VisitorService, Collectors.Location]

         // Batching:
         config.batchingEnabled = false // true to enable

        // Location - Geofence Monitoring:
//        config.geofenceUrl = &#34;https://tags.tiqcdn.com/dle/tealiummobile/location/geofences.json&#34;
//        config.useHighAccuracy = true
//        config.updateDistance = 200.0
        
        // SKAdNetwork event handling
        config.searchAdsEnabled = true
        config.skAdAttributionEnabled = true
        config.skAdConversionKeys = [&#34;conversion_event&#34;: &#34;conversion_value&#34;]

        // Remote Commands:
        let remoteCommand = RemoteCommand(commandId: &#34;hello&#34;, description: &#34;world&#34;) { response in
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
            self.tealium?.dataLayer.add(data: [&#34;somekey&#34;: &#34;someval&#34;], expiry: .afterCustom((.months, 1)))
            self.tealium?.dataLayer.add(key: &#34;someotherkey&#34;, value: &#34;someotherval&#34;, expiry: .forever)
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
