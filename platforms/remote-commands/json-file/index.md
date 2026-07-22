---
title: JSON File
description: Use a JSON file to configure remote commands.
url: https://docs.tealium.com/platforms/remote-commands/json-file/
---
## Requirements

* [Tealium for Android-Kotlin](https://docs.tealium.com/platforms/android-kotlin/) (1.0.0+)
* [Tealium for Android-Java](https://docs.tealium.com/platforms/android-java/) (5.9.0+)
* [Tealium for iOS-Swift](https://docs.tealium.com/platforms/ios-swift/) (2.0.0+)

Static Mappings and Compound Command Keys require a higher version of the libraries 

* [Tealium Remote Commands for Android-Kotlin](https://docs.tealium.com/platforms/android-kotlin/module-list/remote-commands) (1.3.0+)
* [Tealium for iOS-Swift](https://docs.tealium.com/platforms/ios-swift/) (2.9.0+)

## JSON File

Configure a vendor integration using a JSON file. 

Load this file locally in the app or from a remotely hosted URL. 
When loading a file locally it needs to be bundled with the application and its name needs to be passed to the remote command in the code. 

A [JSON template file](https://docs.tealium.com/platforms/remote-commands/how-it-works/#vendor-templates) is available for each vendor integration. Each JSON template file has three main sections: `config`, `mappings`, and `commands` plus an optional section `statics`.


<blockquote>
In cross-platform frameworks, place the JSON file in each platform-specific directory. For Android, place the file in `<project>/app/src/main/assets`. For iOS, place file at the top level.
</blockquote>


### Configuration Mapping

The `config` section sets vendor SDK initialization options such as client ID, API key, or the log level. For example, the following sets the application ID:  
```json
{
    "config": {
        "applicationid": "appid123"
    }
}
```

### Data Mapping

The `mappings` section defines your data mappings. The following mapping assigns the data layer variable `product_id` to the vendor parameter `param_item_id`.

```json
{
    "mappings": {
        "product_id": "param_item_id"
    }
}
``` 

The vendor parameter may use a prefix with dot notation to scope a mapping to a specific object in the payload. The prefix defines the object and the value to the right of the `.` becomes a property of the object. For example, the following mapping assigns `product_id` to the `param_item_id` variable of the `event` object. The remote commands parser creates an `event` object with `param_item_id` as one of its properties.

```json
{
    "mappings": {
        "product_id": "event.param_item_id"
    }
}
```


<blockquote>
The object prefix is typically `event.`, `product.`, or `purchase.`, but may be any custom object name. Refer to the [JSON template files](https://docs.tealium.com/platforms/remote-commands/how-it-works/#vendor-templates) to see the object prefixes used for your vendor integration.
</blockquote>



### Commands

The `commands` section maps Tealium event names to the vendor's events. In the basic implementation, the key is the Tealium event name and the right value is the Tealium wrapper for the vendor's method. In the following example, the Tealium event `cart_add` is mapped to the vendor method `logevent`:

```json
{
    "commands": {
        "cart_add": "logevent"
    }
}
```

#### All Events - All Views

In case you want all events and/or all views to be mapped to a specific command, specify either `all_events` or `all_views` as commands key:


```json
{
    "commands": {
        "all_events": "logevent",
        "all_views": "logevent"
    }
}
```

### Compound Keys

Starting from version 2.9.0 of the Swift library and version 1.3.0 of the Kotlin remote command module, commands can also be triggered when other DataLayer variables match specific values.

To do this, you have to create a compound key that contains the data layer key and a data layer value, separated by a `:`.

For example:

```json
{
    "commands": {
        "screen_view:cart_view": "logevent"
    }
}
```

In this case, the remote command looks in the data layer for `screen_view`, and if it's found, its value is compared to the string `cart_view`. 
If they are the identical, then the remote command triggers the `logevent` command.

For retro-compatibility and for ease of use, in cases where the data layer key is not specified, `tealium_event` is implied. Therefore these two commands are exactly identical:

```json
{
    "commands": {
        "cart_add": "logevent",
        "tealium_event:cart_add": "logevent"
    }
}
```

In some cases, you might want to have more than just one condition to trigger a command, so create a list of `dataLayerKey:dataLayerValue` by separating them with a comma.

For example:

```json
{
    "commands": {
        "screen_view:cart_view,cart_is_empty:false": "logevent"
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
    "config": {
        "keys_equality_delimiter": "==",
        "keys_separation_delimiter": "&&"
        ...
    },
    "commands": {
        "screen_view==cart_view&&cart_is_empty==false": "logevent"
    }
}
```

### Static Mappings

Another feature that makes use of Compound Keys is Static Mappings. This also requires Swift 2.9.0+ and Kotlin 1.3.0+.

Static Mappings allow you to add static values into the data layer for the remote command to use.

Other mappings and commands can make use of those values to trigger other commands or to add parameters.

For example: 

```json
{
    "statics": {
        "screen_view:cart_view,cart_is_empty:false": {
            "possible_buyer": true,
            "apply_discount_percentage":  20.0
        }
    }
}
```

This adds the two keys `possible_buyer` and `apply_discount_percentage` with their respective values (true and 20.0) in the payload of the command. It is assumed that both conditions in the compound key are matched.

### Example

The following is an example JSON configuration:  
```json
{
    "config": {
        "analytics_enabled": "true",
        "session_timeout_seconds": "30",
        "log_level": "max",
        "minimum_seconds": "100",
        ...
    },
    "mappings": {
        "event_title": "event_name",
        "product_brand": "event.param_item_brand",
        "product_category": "event.param_item_category",
        "product_id": "event.param_item_id",
        "product_list": "event.param_item_list",
        "product_location_id": "event.param_item_location_id",
        "product_name": "event.param_item_name",
        "product_variant": "event.param_item_variant",
        "purchase_type": "event.purchase_type",
        ...
    },
    "commands": {
        "launch": "config",
        "cart_add": "logevent",
        "screen_view:homepage": "logview"
        ...
    },
    "statics": {
        "screen_view:homepage,tealium_event:cart_add": {
            "purchase_type": "fast"
        },
        "screen_view:product_detail,tealium_event:cart_add": {
            "purchase_type": "slow"
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
let config = TealiumConfig(account: "ACCOUNT",
        profile: "PROFILE",
        environment: "ENVIRONMENT")
config.dispatchers = [Dispatchers.TagManagement, Dispatchers.RemoteCommands]
config.remoteAPIEnabled = true

tealium = Tealium(config: config) { _ in
    guard let remoteCommands = self.tealium?.remoteCommands else {
        return
    }
  	let facebook = FacebookRemoteCommand(type: .local(file: "facebook")) // or equivalently "facebook.json" on TealiumSwift 2.13.0+
	remoteCommands.add(facebook)
}
```




To use a local configuration file stored in your Android (Kotlin) app:    
```kotlin
val config = TealiumConfig(application,
        "ACCOUNT", "PROFILE",
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands));
var tealium = Tealium.create(TEALIUM_MAIN, config) {
  val facebook = FacebookRemoteCommand(this);
  remoteCommands?.add(facebook, filename = "facebook.json"); // or equivalently "facebook" on TealiumKotlin RemoteCommandDispatcher 1.4.0+
}
```





#### Remote URL Commands

Host the configuration file, accessible as a URL, using the [hosted data layer](https://docs.tealium.com/use-case-supplementing-product-data/).

Starting from TealiumSwift 2.13.0 and TealiumKotlin RemoteCommandDispatcher 1.4.0 for URL RemoteCommands, you can also provide a backup local remote command that will be used in case the JSON configuration can't be downloaded (or while it's downloading) and is not already cached.

To do so, bundle the JSON file for the local commands. As a backup, Android and iOS platforms will look for a settings file named in the `commandId` of the Remote Command you add. Optionally, if you are on Android and the filename is available, pass the filename along with the bundle so the filename will be used instead of the `commandId`.




To use the hosted configuration file in your iOS (Swift) app:  
```swift
let config = TealiumConfig(account: "ACCOUNT",
        profile: "PROFILE",
        environment: "ENVIRONMENT")
config.dispatchers = [Dispatchers.TagManagement, Dispatchers.RemoteCommands]
config.remoteAPIEnabled = true

tealium = Tealium(config: config) { _ in
    guard let remoteCommands = self.tealium?.remoteCommands else {
        return
    }
  	let facebook = FacebookRemoteCommand(type: .remote(url: "https://tags.tiqcdn.com/dle/ACCOUNT/PROFILE/facebook.json"))
	remoteCommands.add(facebook)
}
```



To use the hosted configuration file in your Android (Kotlin) app:    
```kotlin
val config = TealiumConfig(application,
        "ACCOUNT", "PROFILE",
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands));
var tealium = Tealium.create(TEALIUM_MAIN, config) {
  val facebook = FacebookRemoteCommand(this);
  remoteCommands?.add(facebook, remoteUrl = "https://tags.tiqcdn.com/dle/ACCOUNT/PROFILE/facebook.json");
}
```


