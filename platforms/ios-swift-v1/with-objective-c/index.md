---
title: Working with Objective-C
description: Learn about creating a bridging header to work between Objective-C and Swift.
url: https://docs.tealium.com/platforms/ios-swift-v1/with-objective-c/
---
<blockquote>
This is the previous version (1.x) of Tealium for iOS (Swift). For the latest version, see [Tealium for iOS (Swift) 2.x](https://docs.tealium.com/platforms/ios-swift/).
</blockquote>


We recommend using our native Swift library, even for Objective-C projects, but if you still need to use the Objective-C library, this document helps.

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

### Links

- [TealiumHelper File (Objective-C compatible)](https://raw.githubusercontent.com/Tealium/tealium-swift/master/samples/TealiumHelper.swift)
