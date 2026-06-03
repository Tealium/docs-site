---
title: RemoteCommands Module
description: Enables triggering of native code blocks from events in Tealium iQ Tag Management, controlled by extensions and load rules.
url: https://docs.tealium.com/platforms/ios-swift/module-list/remote-commands/
---
Learn more about [remote commands](/platforms/remote-commands/).

## Requirements

* If using the `webview` remote command, the [TagManagement module](/platforms/ios-swift/module-list/tag-management/) is required.

Not a compile-time dependency, but remote commands are triggered from the module.

## Supported Platforms

* iOS
* macOS (JSON only)
* tvOS (JSON only)
* watchOS (JSON only)

## Install

Install the RemoteCommands module with Swift Package Manager, CocoaPods or Carthage.

### Swift Package Manager (Recommended)

Supported in version 1.9.0&#43;, the Swift Package Manager (SMP) is the recommended and simplest way to install the Tealium Swift library:

1. In your Xcode project, select **File &gt; Add Package Dependencies**.
2. Enter the repository URL: `https://github.com/tealium/tealium-swift`
3. Configure the version rules. Typically, `&#34;Up to next major&#34;` is recommended. If the current Tealium Swift library version does not appears in the list, then reset your Swift package cache.
4. Select the RemoteCommands module from the list of modules to install and add it each of your app targets in your Xcode project, under **Frameworks and Libraries**

Learn more about the [SPM installation for iOS](/platforms/ios-swift/install/#swift-package-manager-recommended).

### CocoaPods

To install the RemoteCommands module with CocoaPods, add the following pod to your Podfile:  
```perl
pod &#39;tealium-swift/RemoteCommands&#39;
```

Learn more about the [CocoaPods installation for iOS](/platforms/ios-swift/install/#cocoapods).

### Carthage

To install the RemoteCommands module with Carthage, following these steps:

1. Go to the app target&#39;s General configuration page in Xcode.

2. Add the following framework to the **Embedded Binaries** section:  
      ```perl
      TealiumRemoteCommands.framework
      ```
3. If you need to interact with the RemoteCommands API, add the following required import statement to your project:  

      ```swift
      import TealiumRemoteCommands
      ```

Learn more about the [Carthage installation for iOS](/platforms/ios-swift/install/#carthage).

## Remote Command Options

There are two configuration options for remote commands:

* **JSON File**  
A JSON file, loaded locally or hosted remotely, containing the vendor settings, data mappings, and event triggers.
* **Remote Command Tag**  
A tag in iQ Tag Management that offers configuration options for the vendor&#39;s API (for use with the Tag Management module).

See the [list of remote command vendor integrations](/platforms/remote-commands/integrations/).

### Examples

Configure the Remote Command tag in Tealium iQ Tag Management. You can also use a JSON file in your app or on a remote server. After configuration, register the remote command by using [`addRemoteCommand()`](/platforms/ios-swift/api/tealium-config/#addremotecommand) on `TealiumConfig`. Complete registration before you initialize `Tealium`:





```swift
var tealium: Tealium?

let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                           profile: &#34;PROFILE&#34;,
                           environment: &#34;ENVIRONMENT&#34;,
                           dataSource: &#34;DATASOURCE&#34;)

let remoteCommand = RemoteCommand(commandId: &#34;display&#34;, description: &#34;Display Prompt&#34;) { response in
    guard let payload = response.payload else {
        return
    }
    print(&#34;Use response payload: \(payload)&#34;)
}
config.addRemoteCommand(remoteCommand)

tealium = Tealium(config: config)
```




```swift
var tealium: Tealium?

let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                           profile: &#34;PROFILE&#34;,
                           environment: &#34;ENVIRONMENT&#34;,
                           dataSource: &#34;DATASOURCE&#34;)

let remoteCommand = RemoteCommand(commandId: &#34;display&#34;, description: &#34;Display Prompt&#34;, type: .local(file: &#34;FILENAME&#34;)) { response in
    guard let payload = response.payload else {
        return
    }
    print(&#34;Use response payload: \(payload)&#34;)
}
config.addRemoteCommand(remoteCommand)

tealium = Tealium(config: config)
```





```swift
var tealium: Tealium?

let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                           profile: &#34;PROFILE&#34;,
                           environment: &#34;ENVIRONMENT&#34;,
                           dataSource: &#34;DATASOURCE&#34;)

let remoteCommand = RemoteCommand(commandId: &#34;display&#34;, description: &#34;Display Prompt&#34;, type: .remote(url: &#34;https://tags.tiqcdn.com/dle/ACCOUNT/PROFILE/FILENAME.json&#34;)) { response in
    guard let payload = response.payload else {
        return
    }
    print(&#34;Use response payload: \(payload)&#34;)
}
config.addRemoteCommand(remoteCommand)

tealium = Tealium(config: config)
```





### Add a remote command after initialization

Add remote commands after you initialize `Tealium` by using the `tealium.remoteCommands` manager. When possible, add remote commands in `TealiumConfig` to ensure they receive all events. By default, `webview` commands initialize on load, so adding them later via `tealium.remoteCommands` may cause them to miss initialization.

If you need to add a remote command after `Tealium` is initialized, use this pattern:

```swift
tealium = Tealium(config: config)

let remoteCommand = RemoteCommand(
    commandId: &#34;display&#34;,
    description: &#34;Display Prompt&#34;,
    type: .remote(url: &#34;https://tags.tiqcdn.com/dle/ACCOUNT/PROFILE/FILENAME.json&#34;)) { response in
    guard let payload = response.payload else {
        return
    }
    print(&#34;Use response payload: \(payload)&#34;)
}
tealium?.remoteCommands.add(remoteCommand)
```

## Data Layer

No additional variables are introduced by this module.

## API Reference

### `init()`
Creates a new remote command object ready to be passed to the `add` command.

| Parameter   | Description                                       | Example       |
|-------------|---------------------------------------------------|--------------------|
| `commandId`   | Required String identifier for the remote command | `&#34;logger&#34; `       |
| `description` | Optional String description of the remote command | `&#34;Log Response object to console&#34;` |
| `type`       | Type of remote command (webview (default), local or remote JSON)     | `.local(file: &#34;logger&#34;)` |
| `completion`  | The block of code to trigger                      |                   |

The following is a usage example:

```swift
let customCommand = TealiumRemoteCommand(commandId: &#34;logger&#34;,
                                        description: &#34;Log Response object to console&#34;,
                                        type: .local(file: &#34;logger&#34;))
                                        { (response) in
                                            // code to execute
                                            print(&#34;Custom command response: \(response)&#34;)
                                        })
```

### `add()`

As of 1.6.5, we recommend adding Remote Commands using the `TealiumConfig` [`addRemoteCommand()`](/platforms/ios-swift/api/tealium-config/#addremotecommand) method 

Registers a specified remote command with Tealium for later triggering. Tealium must have been initialized before adding a new Remote Command.

```swift
add(_ remoteCommand: TealiumRemoteCommandProtocol)
```

The following is a usage example:

```swift
var tealium: Tealium?
let customCommand = RemoteCommand(commandId: &#34;logger&#34;,
    description: nil)
    { response in
        // code to execute
        print(&#34;Custom command response: \(response)&#34;)
    }
if let remoteCommands = self.tealium?.remoteCommands {
        remoteCommands.add(customCommand)
} else {
		print(&#34;Remote commands not available&#34;)
}
```

### `remove()`
Removes a previously-registered remote command to prevent it being triggered again.

```swift
remove(commandWithId: String)
```

```swift
remove(jsonCommand: String)
```

```swift
// assumes &#34;tealium&#34; previously instantiated
tealium?.remoteCommands?.remove(commandWithId: &#34;logger&#34;)

tealium?.remoteCommands?.remove(jsonCommand: &#34;logger&#34;)
```

### `remoteHTTPCommandDisabled`
When `true`, disables the built-in remote HTTP command, but leaves the remote commands module enabled for other commands. Default is `false` - or [Remote HTTP Command](#remote-http-command) enabled

```swift
remoteHTTPCommandDisabled
```

The following is a usage example:

```swift
// assumes &#34;config&#34; previously instantiated (`TealiumConfig()`)
config.remoteHTTPCommandDisabled = false
```

## Remote HTTP Command

This is a reserved internal command with identifier `_http` which triggers an HTTP request from native code, and passes the response back to the Tealium iQ web view. This is used in some cases to bypass CORS restrictions that may be encountered in a web browser. To use this command, there are specific mapping names you must use:

| Mapping Name | Description |
| --- | --- |
| `url` | (Required) The URL of the request you want to trigger. |
|`method`| (Required) The HTTP method you want to call. PUT, GET and POST are currently the only supported methods.v
|`headers` |(Optional) A JavaScript object (JSON) containing the header key-value pairs to pass along with the request. For example, `{&#34;Content-Type&#34;: &#34;application/json&#34;}`).|
|`callback_function`| (Optional) A JavaScript function to be invoked when the command has completed. The callback function is passed 2 parameters: `code` is the HTTP response code such as 404 or 200, and `body`, which is the response body from the request. |

The following is an example callback function:

```swift
var my_callback = function(code, body) {
   // assuming the response body was a JSON object, this logs a variable called my_response_variable to the console in the web view
	console.log(body.my_response_variable);
}
```
