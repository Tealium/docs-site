---
title: JSON File
description: Use a JSON file to configure remote commands.
url: https://docs.tealium.com/platforms/remote-commands/json-file/
---
## Requirements

* [Tealium for Android-Kotlin](/platforms/android-kotlin/) (1.0.0&#43;)
* [Tealium for Android-Java](/platforms/android-java/) (5.9.0&#43;)
* [Tealium for iOS-Swift](/platforms/ios-swift/) (2.0.0&#43;)

Static Mappings and Compound Command Keys require a higher version of the libraries 

* [Tealium Remote Commands for Android-Kotlin](/platforms/android-kotlin/module-list/remote-commands) (1.3.0&#43;)
* [Tealium for iOS-Swift](/platforms/ios-swift/) (2.9.0&#43;)

## JSON File

Configure a vendor integration using a JSON file. 

Load this file locally in the app or from a remotely hosted URL. 
When loading a file locally it needs to be bundled with the application and its name needs to be passed to the remote command in the code. 

A [JSON template file](/platforms/remote-commands/how-it-works/#vendor-templates) is available for each vendor integration. Each JSON template file has three main sections: `config`, `mappings`, and `commands` plus an optional section `statics`.

In cross-platform frameworks, place the JSON file in each platform-specific directory. For Android, place the file in `&lt;project&gt;/app/src/main/assets`. For iOS, place file at the top level.

### Configuration Mapping

The `config` section sets vendor SDK initialization options such as client ID, API key, or the log level. For example, the following sets the application ID:  
```json
{
    &#34;config&#34;: {
        &#34;applicationid&#34;: &#34;appid123&#34;
    }
}
```

### Data Mapping

The `mappings` section defines your data mappings. The following mapping assigns the data layer variable `product_id` to the vendor parameter `param_item_id`.

```json
{
    &#34;mappings&#34;: {
        &#34;product_id&#34;: &#34;param_item_id&#34;
    }
}
``` 

The vendor parameter may use a prefix with dot notation to scope a mapping to a specific object in the payload. The prefix defines the object and the value to the right of the `.` becomes a property of the object. For example, the following mapping assigns `product_id` to the `param_item_id` variable of the `event` object. The remote commands parser creates an `event` object with `param_item_id` as one of its properties.

```json
{
    &#34;mappings&#34;: {
        &#34;product_id&#34;: &#34;event.param_item_id&#34;
    }
}
```

The object prefix is typically `event.`, `product.`, or `purchase.`, but may be any custom object name. Refer to the [JSON template files](/platforms/remote-commands/how-it-works/#vendor-templates) to see the object prefixes used for your vendor integration.


### Commands

The `commands` section maps Tealium event names to the vendor&#39;s events. In the basic implementation, the key is the Tealium event name and the right value is the Tealium wrapper for the vendor&#39;s method. In the following example, the Tealium event `cart_add` is mapped to the vendor method `logevent`:

```json
{
    &#34;commands&#34;: {
        &#34;cart_add&#34;: &#34;logevent&#34;
    }
}
```

#### All Events - All Views

In case you want all events and/or all views to be mapped to a specific command, specify either `all_events` or `all_views` as commands key:


```json
{
    &#34;commands&#34;: {
        &#34;all_events&#34;: &#34;logevent&#34;,
        &#34;all_views&#34;: &#34;logevent&#34;
    }
}
```

### Compound Keys

Starting from version 2.9.0 of the Swift library and version 1.3.0 of the Kotlin remote command module, commands can also be triggered when other DataLayer variables match specific values.

To do this, you have to create a compound key that contains the data layer key and a data layer value, separated by a `:`.

For example:

```json
{
    &#34;commands&#34;: {
        &#34;screen_view:cart_view&#34;: &#34;logevent&#34;
    }
}
```

In this case, the remote command looks in the data layer for `screen_view`, and if it&#39;s found, its value is compared to the string `cart_view`. 
If they are the identical, then the remote command triggers the `logevent` command.

For retro-compatibility and for ease of use, in cases where the data layer key is not specified, `tealium_event` is implied. Therefore these two commands are exactly identical:

```json
{
    &#34;commands&#34;: {
        &#34;cart_add&#34;: &#34;logevent&#34;,
        &#34;tealium_event:cart_add&#34;: &#34;logevent&#34;
    }
}
```

In some cases, you might want to have more than just one condition to trigger a command, so create a list of `dataLayerKey:dataLayerValue` by separating them with a comma.

For example:

```json
{
    &#34;commands&#34;: {
        &#34;screen_view:cart_view,cart_is_empty:false&#34;: &#34;logevent&#34;
    }
}
```

In this case, the `logevent` command is only triggered if both `screen_view==cart_view` and `cart_is_empty==false`.

#### Delimiters override

Starting from version 2.9.1 of the Swift SDK, the default delimiters can be overwritten to use your own delimiters, in case you have commas and colons in your data layer values. 

To override the `:` and `,` delimiters with your preferred strings, add the keys `keys_equality_delimiter` and `keys_separation_delimiter` in the configuration part of the JSON.

Of course, if you override the delimiters you then have to use them in your compound keys.

```json
{
    &#34;config&#34;: {
        &#34;keys_equality_delimiter&#34;: &#34;==&#34;,
        &#34;keys_separation_delimiter&#34;: &#34;&amp;&amp;&#34;
        ...
    },
    &#34;commands&#34;: {
        &#34;screen_view==cart_view&amp;&amp;cart_is_empty==false&#34;: &#34;logevent&#34;
    }
}
```

### Static Mappings

Another feature that makes use of Compound Keys is Static Mappings. This also requires Swift 2.9.0&#43; and Kotlin 1.3.0&#43;.

Static Mappings allow you to add static values into the data layer for the remote command to use.

Other mappings and commands can make use of those values to trigger other commands or to add parameters.

For example: 

```json
{
    &#34;statics&#34;: {
        &#34;screen_view:cart_view,cart_is_empty:false&#34;: {
            &#34;possible_buyer&#34;: true,
            &#34;apply_discount_percentage&#34;:  20.0
        }
    }
}
```

This adds the two keys `possible_buyer` and `apply_discount_percentage` with their respective values (true and 20.0) in the payload of the command. It is assumed that both conditions in the compound key are matched.

### Example

The following is an example JSON configuration:  
```json
{
    &#34;config&#34;: {
        &#34;analytics_enabled&#34;: &#34;true&#34;,
        &#34;session_timeout_seconds&#34;: &#34;30&#34;,
        &#34;log_level&#34;: &#34;max&#34;,
        &#34;minimum_seconds&#34;: &#34;100&#34;,
        ...
    },
    &#34;mappings&#34;: {
        &#34;event_title&#34;: &#34;event_name&#34;,
        &#34;product_brand&#34;: &#34;event.param_item_brand&#34;,
        &#34;product_category&#34;: &#34;event.param_item_category&#34;,
        &#34;product_id&#34;: &#34;event.param_item_id&#34;,
        &#34;product_list&#34;: &#34;event.param_item_list&#34;,
        &#34;product_location_id&#34;: &#34;event.param_item_location_id&#34;,
        &#34;product_name&#34;: &#34;event.param_item_name&#34;,
        &#34;product_variant&#34;: &#34;event.param_item_variant&#34;,
        &#34;purchase_type&#34;: &#34;event.purchase_type&#34;,
        ...
    },
    &#34;commands&#34;: {
        &#34;launch&#34;: &#34;config&#34;,
        &#34;cart_add&#34;: &#34;logevent&#34;,
        &#34;screen_view:homepage&#34;: &#34;logview&#34;
        ...
    },
    &#34;statics&#34;: {
        &#34;screen_view:homepage,tealium_event:cart_add&#34;: {
            &#34;purchase_type&#34;: &#34;fast&#34;
        },
        &#34;screen_view:product_detail,tealium_event:cart_add&#34;: {
            &#34;purchase_type&#34;: &#34;slow&#34;
        }
        ...
    }
}
```

### Load Options

There are two options for loading the JSON configuration file: as a local file or from a hosted URL.

#### Local File Commands

Bundle the remote command configuration JSON within the application and then pass its name to the RemoteCommand initialization method.

Starting from TealiumSwift 2.13.0 and TealiumKotlin RemoteCommandDispatcher 1.4.0 for local RemoteCommands, both libraries accept a name with and without the extension. 

If you are using an earlier version of those libraries then you need to pass the name without the extension on iOS and the name with the extension on Kotlin. 

This situation is also true for all cross-platform libraries, depending on the specific native Tealium library you are targeting.





To use a local configuration file stored in your iOS (Swift) app:  
```swift
let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
        profile: &#34;PROFILE&#34;,
        environment: &#34;ENVIRONMENT&#34;)
config.dispatchers = [Dispatchers.TagManagement, Dispatchers.RemoteCommands]
config.remoteAPIEnabled = true

tealium = Tealium(config: config) { _ in
    guard let remoteCommands = self.tealium?.remoteCommands else {
        return
    }
  	let facebook = FacebookRemoteCommand(type: .local(file: &#34;facebook&#34;)) // or equivalently &#34;facebook.json&#34; on TealiumSwift 2.13.0&#43;
	remoteCommands.add(facebook)
}
```




To use a local configuration file stored in your Android (Kotlin) app:    
```kotlin
val config = TealiumConfig(application,
        &#34;ACCOUNT&#34;, &#34;PROFILE&#34;,
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands));
var tealium = Tealium.create(TEALIUM_MAIN, config) {
  val facebook = FacebookRemoteCommand(this);
  remoteCommands?.add(facebook, filename = &#34;facebook.json&#34;); // or equivalently &#34;facebook&#34; on TealiumKotlin RemoteCommandDispatcher 1.4.0&#43;
}
```





#### Remote URL Commands

Host the configuration file, accessible as a URL, using the [hosted data layer]().

Starting from TealiumSwift 2.13.0 and TealiumKotlin RemoteCommandDispatcher 1.4.0 for URL RemoteCommands, you can also provide a backup local remote command that will be used in case the JSON configuration can&#39;t be downloaded (or while it&#39;s downloading) and is not already cached.

To do so, bundle the JSON file for the local commands. As a backup, Android and iOS platforms will look for a settings file named in the `commandId` of the Remote Command you add. Optionally, if you are on Android and the filename is available, pass the filename along with the bundle so the filename will be used instead of the `commandId`.




To use the hosted configuration file in your iOS (Swift) app:  
```swift
let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
        profile: &#34;PROFILE&#34;,
        environment: &#34;ENVIRONMENT&#34;)
config.dispatchers = [Dispatchers.TagManagement, Dispatchers.RemoteCommands]
config.remoteAPIEnabled = true

tealium = Tealium(config: config) { _ in
    guard let remoteCommands = self.tealium?.remoteCommands else {
        return
    }
  	let facebook = FacebookRemoteCommand(type: .remote(url: &#34;https://tags.tiqcdn.com/dle/ACCOUNT/PROFILE/facebook.json&#34;))
	remoteCommands.add(facebook)
}
```



To use the hosted configuration file in your Android (Kotlin) app:    
```kotlin
val config = TealiumConfig(application,
        &#34;ACCOUNT&#34;, &#34;PROFILE&#34;,
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands));
var tealium = Tealium.create(TEALIUM_MAIN, config) {
  val facebook = FacebookRemoteCommand(this);
  remoteCommands?.add(facebook, remoteUrl = &#34;https://tags.tiqcdn.com/dle/ACCOUNT/PROFILE/facebook.json&#34;);
}
```


