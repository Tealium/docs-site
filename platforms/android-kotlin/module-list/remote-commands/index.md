---
title: RemoteCommands Module
description: Enables triggering of native code blocks from events in Tealium iQ Tag Management, controlled by extensions and load rules.
url: https://docs.tealium.com/platforms/android-kotlin/module-list/remote-commands/
---
Learn more about [remote commands](/platforms/remote-commands/).

## Requirements

* If using the `webview` remote command, the [Tag Management Dispatcher module](/platforms/android-kotlin/module-list/tag-management/) is required.
* RemoteCommandDispatcher `1.4.0` and above requires `com.tealium:kotlin-core:1.6.0` as a minimum version.

## Install

Install the RemoteCommands Dispatcher module using Maven (Recommended) or manually.

### Maven

To install the module using Maven:

1. In your project&#39;s top-level `build.gradle` file, add the following Maven repository:
      ```groovy
      maven {
            url &#34;https://maven.tealiumiq.com/android/releases/&#34;
      }
      ```

2. In your project module&#39;s `build.gradle` file, add the Maven dependencies for the RemoteCommands Dispatcher. This will pull in the Tealium Kotlin library.
      ```groovy
      dependencies {
            implementation &#39;com.tealium:kotlin-core:1.6.0&#39;
            implementation &#39;com.tealium:kotlin-remotecommand-dispatcher:1.4.0&#39;
            implementation &#39;com.tealium:remotecommands:1.0.1&#39;
      }
      ```

### Manual

To install the RemoteCommands Dispatcher manually:

1. Download the Tealium [Collect Dispatcher](https://github.com/Tealium/tealium-kotlin/tree/master/collectdispatcher) module.

2. Copy the file `tealium-kotlin.remotecommand-1.4.0.aar` into your project&#39;s `&lt;PROJECT_ROOT&gt;/&lt;MODULE&gt;/libs` directory.

3. Add the Tealium library dependency to your project module’s `build.gradle` file:
      ```groovy
      dependencies {
            implementation(name:&#39;tealium-kotlin.remotecommand-1.4.0&#39;, ext:&#39;aar&#39;)
      }
      ```

## Remote Command Options

There are two configuration options for remote commands:

* **JSON File**  
A JSON file, loaded locally or hosted remotely, containing the vendor settings, data mappings, and event triggers.
* **Remote Command Tag**  
A tag in iQ Tag Management that offers configuration options for the vendor&#39;s API (for use with the Tag Management module).

See the [list of remote command vendor integrations](/platforms/remote-commands/integrations/).

### Examples

The Remote Command tag is configurable in Tealium iQ Tag Management, with a JSON file in your app, or JSON file on a remote server. Once the remote command is configured and the module is installed, add the following lines to the initialization:





```kotlin
val config = TealiumConfig(application,
        &#34;ACCOUNT&#34;,
        &#34;PROFILE&#34;,
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands));
var tealium = Tealium.create(TEALIUM_MAIN, config) {
  val remoteCommands = RemoteCommand(this);
  // register the command
  remoteCommands?.add(remoteCommands);
}
```




```kotlin
val config = TealiumConfig(application,
        &#34;ACCOUNT&#34;,
        &#34;PROFILE&#34;,
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands));
var tealium = Tealium.create(TEALIUM_MAIN, config) {
  val remoteCommands = RemoteCommand(this);
  remoteCommands?.add(remoteCommands, filename = &#34;FILENAME.json&#34;);
}
```





```kotlin
val config = TealiumConfig(application,
        &#34;ACCOUNT&#34;,
        &#34;PROFILE&#34;,
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands));
var tealium = Tealium.create(TEALIUM_MAIN, config) {
  val remoteCommands = RemoteCommand(this);
  remoteCommands?.add(remoteCommands, remoteUrl = &#34;https://tags.tiqcdn.com/dle/ACCOUNT/PROFILE/FILENAME.json&#34;);
}
```





After the JSON file has been configured and either added to your app or hosted on a server, learn about the different [JSON load options](/platforms/remote-commands/how-it-works/#load-options).


## Data Layer

No additional variables are introduced by this module.

## API Reference

### `RemoteCommand()`
Creates a new remote command object ready to be passed to the `add` command.

```kotlin
val remoteCommand = object : RemoteCommand(&#34;commandName&#34;, &#34;description&#34;) {
    override fun onInvoke(response: Response) {
        Logger.dev(BuildConfig.TAG, &#34;ResponsePayload for webView RemoteCommand ${response.requestPayload}&#34;)
    }
}
```

| Parameter     | Description                                       | Example         |
|-------------- |-------------------------------------------------- |---------------- |
| `commandName`  | Required String command name                      | `&#34;sample&#34;`     |
| `description` | Optional String description of the remote command | `&#34;testing RCs&#34;` |


### `add()`

Registers a specified remote command with Tealium for later triggering. Tealium must have been initialized before adding a new Remote Command.

```kotlin
val tealium = Tealium.create(instanceName, config) {
    remoteCommands?.add(remoteCommand)
}
```

The following is a usage example:

```kotlin
val remoteCommand = object : RemoteCommand(&#34;sample&#34;, &#34;testing RCs&#34;) {
    override fun onInvoke(response: Response) {
        Logger.dev(BuildConfig.TAG, &#34;ResponsePayload for webView RemoteCommand ${response.requestPayload}&#34;)
    }
}

val tealium = Tealium.create(instanceName, config) {
    remoteCommands?.add(remoteCommand)
}
```

### `remove()`
Removes a previously registered remote command to prevent it from being triggered again.

```kotlin
val tealium = Tealium.create(instanceName, config) {
   remoteCommands?.remove(&#34;commandName&#34;)
}
```

### `removeAll`

Removes all previously registered remote commands.

```kotlin
val tealium = Tealium.create(instanceName, config) {
    remoteCommands?.removeAll()
}
```
