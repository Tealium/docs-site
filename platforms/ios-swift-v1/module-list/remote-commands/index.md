---
title: RemoteCommands Module
description: Enables triggering of native code blocks from events in Tealium iQ Tag Management, controlled by extensions and load rules.
url: https://docs.tealium.com/platforms/ios-swift-v1/module-list/remote-commands/
---
[Learn more](https://docs.tealium.com/platforms/remote-commands/) about remote commands.

## Requirements

* Tealium iQ Tag Management module. Not a compile-time dependency, but Remote Commands are triggered from the module.

## Supported Platforms

* iOS

## Install

Install the RemoteCommands module with CocoaPods or Carthage.

### CocoaPods

To install the RemoteCommands module with CocoaPods, add the following pod to your Podfile:  
```ruby
pod 'tealium-swift/TealiumRemoteCommands'
```

The framework is auto-instantiated. It has a dependency on the `TealiumCore` pod. [Learn more](https://docs.tealium.com/platforms/ios-swift-v1/install/#cocoapods) about CocoaPods installation for iOS.

### Carthage

To install the RemoteCommands module with Carthage, following these steps:

1. Go to the app target's General configuration page in Xcode.

2. Add the following framework to the **Embedded Binaries** section:  
      ```ruby
      TealiumRemoteCommands.framework
      ```
3. If you need to interact with the RemoteCommands API, add the following required import statement to your project:  
      ```swift
      import TealiumRemoteCommands
      ```

The framework is auto-instantiated. It has a dependency on `TealiumCore`. No additional import statements are necessary. [Learn more](https://docs.tealium.com/platforms/ios-swift-v1/install/#carthage) about Carthage installation for iOS.

## Example

Once the Remote Command Tag is configured in Tealium IQ and the module is installed in your app, add the following lines to the initialization as shown in the following example:

```swift
class TealiumHelper {
	var tealium: Tealium?
	// ...
	private func initTealium() {
		let config = TealiumConfig(account: "ACCOUNT",
 	       		                 profile: "PROFILE",
        	   	                 environment: "ENVIRONMENT",
           		                 datasource: "DATASOURCE")
    	guard let remoteCommands = self?.tealium?.remoteCommands() else {
          return
        }
        let brazeCommand = BrazeCommand(brazeTracker: BrazeTracker())
        let brazeRemoteCommand = brazeCommand.remoteCommand()
        remoteCommands.add(brazeRemoteCommand)

		// ...
	}
}
```

## Data Layer
No additional variables are introduced by this module.

## API Reference


### `init()`
Creates a new remote command object ready to be passed to the `add` command.

| Parameter   | Description                                       | Example       |
|-------------|---------------------------------------------------|--------------------|
| `commandId`   | Required String identifier for the remote command | `"logger" `       |
| `description` | Optional String description of the remote command | `"Log Response object to console"` |
| `queue`       | Queue on which to trigger the code block          | `DispatchQueue.main` |
| `completion`  | The block of code to trigger                      |                   |

The following is a usage example:

```swift
let customCommand = TealiumRemoteCommand(commandId: "logger",
                                        description: "Log Response object to console",
                                        queue: DispatchQueue.main)
                                        { (response) in
                                            // code to execute
                                            print("Custom command response: (response)")
                                        })
```

### `add()`


<blockquote>
As of 1.6.5, we recommend adding Remote Commands using the `TealiumConfig` [`addRemoteCommand()`](https://docs.tealium.com/platforms/ios-swift-v1/api/tealium-config/#addremotecommand) method
</blockquote>


Registers a specified remote command with Tealium for later triggering. Tealium must have been initialized before adding a new Remote Command.

```swift
add(remoteCommand: TealiumRemoteCommand)
```

The following is a usage example:

```swift
var tealium: Tealium?
let customCommand = TealiumRemoteCommand(commandId: "logger",
    description: nil,
    queue: DispatchQueue.main)
    { response in
        // code to execute
        print("Custom command response: (response)")
    })
if let remoteCommands = self.tealium?.remoteCommands() {
        remoteCommands.add(customCommand)
} else {
print("Remote commands not available")
}
```

### `remove()`
Removes a previously registered remote command to prevent it being triggered again.

```swift
remove(commandWithId: String)
```

```swift
// assumes "tealium" previously instantiated
tealium?.remoteCommands()?.remove(commandWithId: "logger")
```

### `disableRemoteCommands()`

Disables the remote commands module.

```swift
disableRemoteCommands()
```

The following is a usage example:

```swift
// assumes "tealium" previously instantiated
tealium?.remoteCommands()?.disableRemoteCommands()
```

### `enableRemoteCommands()`

Enables the remote commands module (only required if previously disabled; default is enabled).

```TealiumSwift
enabledRemoteCommands()
```

The following is a usage example:

```swift
// assumes "tealium" previously instantiated
tealium?.remoteCommands()?.enableRemoteCommands()
```

### `disableRemoteHTTPCommand()`
Disables the built-in remote HTTP command, but leaves the remote commands module enabled for other commands.

```swift
disableRemoteHTTPCommand()
```

The following is a usage example:

```swift
// assumes "tealium" previously instantiated
tealium?.remoteCommands()?.disableRemoteHTTPCommand()
```

### `enableRemoteHTTPCommand()`
Enables the built-in remote HTTP command (only required if previously disabled; default is enabled).

```swift
enableRemoteHTTPCommand()`
```

The following is a usage example:

```swift
// assumes "tealium" previously instantiated
tealium?.remoteCommands()?.enableRemoteHTTPCommand()
```


## Remote HTTP Command

This is a reserved internal command with identifier `_http` which triggers an HTTP request from native code, and passes the response back to the Tealium iQ web view. This is used in some cases to bypass CORS restrictions that may be encountered in a web browser. To use this command, there are specific mapping names you must use:

| Mapping Name | Description |
| --- | --- |
| `url` | (Required) The URL of the request you want to trigger. |
|`method`| (Required) The HTTP method you want to call. PUT, GET and POST are currently the only supported methods.v
|`headers` |(Optional) A JavaScript object (JSON) containing the header key-value pairs to pass along with the request. For example, `{"Content-Type": "application/json"}`).|
|`callback_function`| (Optional) A JavaScript function to be invoked when the command has completed. The callback function is passed 2 parameters: `code` is the HTTP response code such as 404 or 200, and `body`, which is the response body from the request. |

Here's a sample callback function:

```swift
var my_callback = function(code, body) {
   // assuming the response body was a JSON object, this logs a variable called my_response_variable to the console in the web view
	console.log(body.my_response_variable);
}
```