---
title: Custom Commands
description: Learn about custom commands.
url: https://docs.tealium.com/platforms/remote-commands/custom-commands/
---
When using iQ Tag Management in your app, custom remote commands provide the ability to trigger native code blocks from the non-rendered webview. This is used in cases where data held inside the non-rendered webview needs to be passed back to the native code for further processing.

Remote commands use custom URL schemes as a way for JavaScript tags to trigger methods in your app. A tag in the non-rendered webview sends the app requests which are processed by a remote command handler that triggers custom code or a vendor SDK.

### Components

A remote command has a command name and a payload of data.

- **Command**  
The name of the command, or command ID, registered with native code in your app.
- **Payload**  
The data passed to the native app and received as an object named `requestPayload` in the response callback of the handler.

Define remote commands in your native app at build time. The Custom Remote Command tag only executes pre-defined code on the device.

### Native Code

In the native code, the `add()` function registers a remote command handler. The callback function `response` has  access to the payload with `response.payload`. In the following example, the referenced payload variables have a matching data layer variable configured in iQ Tag Management.



```swift
tealium = Tealium(config: config) { [weak self] _ in
	let remoteCommand = RemoteCommand(commandId: &#34;myRemoteCommand&#34;, description: &#34;&#34;) { response in
		guard let payload = response.payload,
	    let myVariable = payload[&#34;myVariable&#34;] as? String else {
			return
		}
		print(myVariable)
	}
	self.tealium?.remoteCommands?.add(remoteCommand)
}
```


```kotlin
val remoteCommand = object : RemoteCommand(&#34;sample&#34;, &#34;testing RCs&#34;) {
    override fun onInvoke(response: Response) {
        Logger.dev(BuildConfig.TAG, &#34;ResponsePayload for webView RemoteCommand ${response.requestPayload}&#34;)
    }
}
val tealium = Tealium.create(instanceName, config) {
    remoteCommands?.add(webViewRemoteCommand)
}
```



Add a module for the vendor integration to the build script for your platform. Modules are named in the format of `TealiumVendorXYZ`, for example `TealiumBraze`.

To install, replace the vendor&#39;s dependency with the Tealium remote command dependency. For example, remove the following line:  
```bash
pod &#34;VendorXYZ-iOS-SDK&#34;
```
Then add the following line:
```bash
pod &#34;TealiumVendorXYZ&#34;
```


### Use Case: Purchase Survey

The following steps demonstrate how to use a remote command to trigger a survey in your app after a user completes a purchase.

1. Create native code that prompts the user to take a survey, passing the message and URL as method parameters (from the non-rendered webview).
2. Register the block of code as a remote command with the Tealium API.
3. Add the Custom Remote Command tag in iQ Tag Management and set the command ID to the same command registered in the native code.
4. Set data mappings to pass specific variables back to the app, such as `survey_title` or `survey_url`.
5. In the native code, use the variables passed back in the response payload to display the survey to the user.

After completing these steps, you are able to configure the survey title, URL, and logic using extensions in iQ Tag Management without re-deploying your app.


### Remote Command Tag

Use iQ Tag Management where a remote command is set up as an instance of the custom Remote Command tag with the following settings:

* **Command ID**  
The name of the command (the same name used in the native method `addRemoteCommandID`).
* **Load rule**  
A rule to determine when to trigger the remote command.
* **Mapped variables**  
The data to include in the remote command. Mapped data layer variables are available in the `response.requestPayload` object in the native code callback.

### Example Remote Command Tag

The following is an example of a tracked event in Swift.

```swift
tealium?.track(
    title: &#34;My Screen&#34;,
    data: [&#34;tealium_event&#34;: &#34;my_event&#34;, &#34;my_variable&#34;: &#34;my_value&#34;]
);
```

The tag setup is defined as follows:

* **Command ID**  
`myRemoteCommand`
* **Load rule**  
`IF tealium_event EQUALS my_event`
* **Mapped variable**  
`my_variable -&gt; myVariable`

The following screenshots show the example configured in iQ Tag Management.

![](/images/platforms/remote-commands/tag-example.png)

