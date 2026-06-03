---
title: Remote Command: SKAdNetwork
description: Tealium remote command integration for Apple's SKAdNetwork for Swift.
url: https://docs.tealium.com/platforms/remote-commands/integrations/skadnetwork/
---
[SKAdNetwork](https://developer.apple.com/documentation/storekit/skadnetwork) is Apple&#39;s SDK to help advertisers measure the success of ad campaigns while maintaining user privacy. 

## Requirements

* [Tealium for iOS-Swift](/platforms/ios-swift/) (2.9.0&#43;)
* [SKAdNetwork Remote Command JSON File](/platforms/remote-commands/integrations/skadnetwork/#json-template)

## How It Works

The SKAdNetwork integration uses two items:

1. The remote commands module that sends the SKAdNetwork conversion value
2. Either the JSON configuration file or Remote Command tag that translates event tracking into the conversion value

A JSON configuration file is the recommended option for this integration, hosted either remotely or locally within your app. If you are using iQ Tag Management, add the Remote Command tag for the vendor integration. Learn more about [vendor integrations](/platforms/remote-commands/how-it-works/#vendor-integrations).

## Install

### Dependency Manager




1. In your Xcode project, select **File &gt; Add Packages... &gt; Add Package Dependency**.
2. Enter the repository URL: `https://github.com/tealium/tealium-ios-skadnetwork-remote-command`.
3. Configure the version rules. Typically, `Up to next major` is recommended. If the current `TealiumSKAdNetwork` version does not appear in the list, then reset your Swift package cache.
4. Select the `TealiumSKAdNetwork` module to install, and select the app target you want the module to be installed in.
5. If you are using any additional modules from the Tealium Swift library, follow [the Swift Package Manager instructions](/platforms/ios-swift/install/#swift-package-manager-recommended) to add them.

If your project has more than one app target and needs `TealiumSKAdNetwork` module in more app targets, you must manually add them in the **Frameworks, Libraries, and Embedded Content** section.

To install `TealiumSKAdNetwork` in additional app targets:

1. Select your Xcode project in the **Project Navigator**.
2. In your Xcode project, select the app target under the **TARGETS** section.
3. Navigate to **General &gt; Frameworks, Libraries &amp; Embedded Content** and select the `TealiumSKAdNetwork` module to add it to your app target.




1. Remove `pod &#34;tealium-swift&#34;` and `pod &#34;SKAdNetwork&#34;`, if they exist in your Podfile. The dependency for `tealium-swift` is already included in the `TealiumSKAdNetwork` framework.

2. Add the following dependency to your Podfile:  
      ```ruby
      pod &#34;TealiumSKAdNetwork&#34;
      ```  
      The `TealiumSKAdNetwork` pod includes the following `TealiumSwift` dependencies:  
      ```bash
      &#34;tealium-swift/Core&#34;
      &#34;tealium-swift/RemoteCommands&#34;
      ```

3. Include a dispatcher pod in your installation, either `tealium-swift/Collect` or `tealium-swift/TagManagement`, and include any other individual sub modules in your podfile. For example:   
      ```ruby
      pod &#34;TealiumSKAdNetwork&#34;
      pod &#34;tealium-swift/Collect&#34;
      pod &#34;tealium-swift/Lifecycle&#34;
      pod &#34;tealium-swift/Attribution&#34;
      ```

4. Import the modules `TealiumSwift` and `TealiumSKAdNetwork` in your `TealiumHelper` file, and any other files that access the `Tealium` class, or the Adjust remote command.




1. Remove `tealium-swift` from your Cartfile. The dependency for `tealium-swift` is already included in the `TealiumSKAdNetwork` framework.

2. Remove the following line if it exists in your Cartfile:  
      ```bash
      github &#34;skadnetwork/ios_sdk&#34;
      ```

3.  Add the following dependency to your Cartfile:  
      ```bash
      github &#34;tealium/tealium-ios-skadnetwork-remote-command&#34;
      ```




### Manual Installation

The manual installation for SKAdNetwork remote commands requires the [Tealium for Swift](/platforms/ios-swift/) library to be installed. To install the SKAdNetwork remote commands for your iOS project:

1. Install the [SKAdNetwork SDK](https://github.com/skadnetwork/ios_sdk), if you haven&#39;t already done so.

2. Clone the [Tealium iOS SKAdNetwork remote command](https://github.com/tealium/tealium-ios-skadnetwork-remote-command) repo and drag the files within the `Sources` folder into your project.

3. Set the [`remoteAPIEnabled`](/platforms/ios-swift/api/tealium-config/#remoteapienabled) configuration flag to `true`.

## Initialize

Initialize remote commands with a JSON configuration file or the Remote Command tag for Tealium&#39;s iOS (Swift) library.

The following code is designed for use with the JSON Remote Command feature, using the local file option:  
```swift
var tealium : Tealium?
let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                           profile: &#34;PROFILE&#34;,
                           environment: &#34;ENVIRONMENT&#34;,
                           dataSource: &#34;DATASOURCE&#34;,
                           optionalData: nil)

config.remoteAPIEnabled = true // Required to use Remote Commands
config.dispatchers = [Dispatchers.RemoteCommands, Dispatchers.Collect]

tealium = Tealium(config: config) { _ in
    guard let remoteCommands = self.tealium?.remoteCommands else {
        return
    }

    // Webview Tag
    let skadnetwork = SKAdNetworkRemoteCommand(delegate: self)

    // Local JSON
    //let skadnetwork = SKAdNetworkRemoteCommand(type: .local(file: &#34;skadnetwork&#34;), delegate: self)

    // Remote JSON
    //let skadnetwork = SKAdNetworkRemoteCommand(type: .remote(url: &#34;https://some.domain.com/skadnetwork.json&#34;), delegate: self)

	remoteCommands.add(skadnetwork)
}
```

### Delegate

The delegate is an optional parameter to receive conversion updates and completion calls to potentially debug and handle errors and potentially track this too.

```swift
    /// When we detect that a new conversion value needs to be sent
    func onConversionUpdate(conversionData: ConversionData, lockWindow: Bool)
    /// When the new conversion value was sent and completed, optionally with an error
    func onConversionUpdateCompleted(error: Error?)
}
```

### JSON Template

If you are configuring remote commands using a [JSON configuration file](/platforms/remote-commands/how-it-works/#json-configuration-file), refer to the following templates to get started. Edit the mappings as needed.




The template includes common mappings for a simple value attribution strategy. We are mapping the fine and coarse values that you send in some events.

```json
{
    &#34;config&#34;: {
      &#34;send_higher_value&#34;: true
    },
    &#34;mappings&#34;: {
        &#34;fine_value&#34;:&#34;fine_value&#34;,
        &#34;coarse_value&#34;:&#34;coarse_value&#34;
    },
    &#34;commands&#34;: {
        &#34;launch&#34;: &#34;initialize,registerappforattribution,setconversionvalue&#34;,
        &#34;register&#34;: &#34;setconversionvalue&#34;,
        &#34;login&#34;: &#34;setconversionvalue&#34;,
        &#34;tutorial&#34;: &#34;setconversionvalue&#34;,
        &#34;addtocart&#34;: &#34;setconversionvalue&#34;,
        &#34;purchase&#34;: &#34;setconversionvalue&#34;,
        &#34;user_type:premium,subscribe&#34;: &#34;setconversionvalue&#34;
    },
    &#34;statics&#34;: {
        &#34;launch&#34;: {
            &#34;fine_value&#34;: 0,
            &#34;coarse_value&#34;: &#34;low&#34;
        }
}
```




The template includes common mappings for a standard events based attribution strategy. Each event maps to one of the 6 bits in the conversion value.

```json
{
    &#34;config&#34;: {
      &#34;send_higher_value&#34;: true
    },
    &#34;mappings&#34;: {
        &#34;bit_number&#34;:&#34;bit_number&#34;,
        &#34;fine_value&#34;:&#34;fine_value&#34;,
        &#34;coarse_value&#34;:&#34;coarse_value&#34;
    },
    &#34;commands&#34;: {
        &#34;launch&#34;: &#34;initialize,registerappforattribution,setconversionvalue&#34;,
        &#34;register&#34;: &#34;setconversionbit&#34;,
        &#34;login&#34;: &#34;setconversionbit&#34;,
        &#34;tutorial&#34;: &#34;setconversionbit&#34;,
        &#34;addtocart&#34;: &#34;setconversionbit&#34;,
        &#34;purchase&#34;: &#34;setconversionbit&#34;,
        &#34;user_type:premium,subscribe&#34;: &#34;setconversionbit&#34;
    },
    &#34;statics&#34;: {
        &#34;launch&#34;: {
            &#34;fine_value&#34;: 0,
            &#34;coarse_value&#34;: &#34;low&#34;
        },
        &#34;register&#34;: {
            &#34;bit_number&#34;: 0,
            &#34;coarse_value&#34;: &#34;low&#34;
        },
        &#34;login&#34;: {
            &#34;bit_number&#34;: 1,
            &#34;coarse_value&#34;: &#34;low&#34;
        },
        &#34;tutorial&#34;: {
            &#34;bit_number&#34;: 2,
            &#34;coarse_value&#34;: &#34;low&#34;
        },
        &#34;addtocart&#34;: {
            &#34;bit_number&#34;: 3,
            &#34;coarse_value&#34;: &#34;medium&#34;
        },
        &#34;purchase&#34;: {
            &#34;bit_number&#34;: 4,
            &#34;coarse_value&#34;: &#34;high&#34;
        },
        &#34;user_type:premium,subscribe&#34;: {
            &#34;bit_number&#34;: 5,
            &#34;coarse_value&#34;: &#34;high&#34;
        },
    }
}
```





The template includes common mappings for a mixed attribution strategy. Two of the 6 bits will be used to store some value, and 4 bits will be used to encode some events.

```json
{
    &#34;config&#34;: {
      &#34;send_higher_value&#34;: true
    },
    &#34;mappings&#34;: {
        &#34;bit_number&#34;:&#34;bit_number&#34;,
        &#34;fine_value&#34;:&#34;fine_value&#34;,
        &#34;coarse_value&#34;:&#34;coarse_value&#34;,
        &#34;limit_to_highest_n_bits&#34;: &#34;limit_to_highest_n_bits&#34;,
        &#34;limit_to_lowest_n_bits&#34;: &#34;limit_to_lowest_n_bits&#34;
    },
    &#34;commands&#34;: {
        &#34;launch&#34;: &#34;initialize,registerappforattribution,setconversionvalue&#34;,
        &#34;register&#34;: &#34;setconversionbit&#34;,
        &#34;login&#34;: &#34;setconversionbit&#34;,
        &#34;tutorial&#34;: &#34;setconversionbit&#34;,
        &#34;addtocart&#34;: &#34;setconversionbit&#34;,
        &#34;purchase&#34;: &#34;setconversionbit&#34;,
        &#34;subscribe&#34;: &#34;setconversionvalue&#34;
    },
    &#34;statics&#34;: {
        &#34;launch&#34;: {
            &#34;fine_value&#34;: 0,
            &#34;coarse_value&#34;: &#34;low&#34;
        },
        &#34;register&#34;: {
            &#34;bit_number&#34;: 0,
            &#34;coarse_value&#34;: &#34;low&#34;
        },
        &#34;login&#34;: {
            &#34;bit_number&#34;: 1,
            &#34;coarse_value&#34;: &#34;low&#34;
        },
        &#34;tutorial&#34;: {
            &#34;bit_number&#34;: 2,
            &#34;coarse_value&#34;: &#34;low&#34;
        },
        &#34;addtocart&#34;: {
            &#34;bit_number&#34;: 3,
            &#34;coarse_value&#34;: &#34;medium&#34;
        },
        &#34;purchase&#34;: {
            &#34;bit_number&#34;: 4,
            &#34;coarse_value&#34;: &#34;high&#34;
        },
        &#34;user_type:common,subscribe&#34;: {
            &#34;limit_to_highest_n_bits&#34;: 2,
            &#34;fine_value&#34;: 1,
            &#34;coarse_value&#34;: &#34;low&#34;
        },
        &#34;user_type:premium,subscribe&#34;: {
            &#34;limit_to_highest_n_bits&#34;: 2,
            &#34;fine_value&#34;: 2,
            &#34;coarse_value&#34;: &#34;medium&#34;
        },
        &#34;user_type:premium_plus,subscribe&#34;: {
            &#34;limit_to_highest_n_bits&#34;: 2,
            &#34;fine_value&#34;: 3,
            &#34;coarse_value&#34;: &#34;high&#34;
        }
    }
}
```





## Supported Methods

We map a command to each SKAdNetwork method. To trigger a SKAdNetwork method, pass the corresponding command in the specified format.

| Remote Command | SKAdNetwork Method |
| :-- | :-- |
| `initialize` | `configure()` |
| `registerappforattribution` | `registerAppForAdNetworkAttribution()` |
| `setconversionbit` | `setConversionBit()` |
| `resetconversionbit` | `resetConversionBit()` |
| `setconversionvalue` | `setConversionValue()` |
| `resetconversionvalue` | `resetConversionValue()` |

All these methods affect the conversion value and will cause an update to the conversion value in the SKAdNetwork API.

### Initialize

You can set the `send_higher_value` flag to true to filter out lower values and only send higher values.

| Remote Command | SKAdNetwork Method |
|---|---|
| `initialize`  | `configure()` |

|  Parameter | Type |
|---|---|
|  `send_higher_value` | `Bool` |

### Register App For Attribution

This is an old method used for iOS &lt; 14. If you support older iOS versions than 14, you can&#39;t report any conversion value but can still use this method to report that an install occurred.
This method should probably be sent at launch if you support older OS versions.

| Remote Command | SKAdNetwork Method |
|---|---|
| `registerappforattribution` | `registerAppForAdNetworkAttribution()` |

### Set Conversion Bit

You can specify a bit to raise in the conversion value. Note that if the bit was already raised, the fine value won&#39;t change.

| Remote Command | SKAdNetwork Method |
|---|---|
| `setconversionbit` | `setConversionBit()` |

|  Parameter | Type | Description |
|---|---|---|
| `bit_number` | `Int` | A number from 0 to 5 |
| `coarse_value` | `String` | The coarse value of this installation (low-medium-high) |
| `lock_window` | `Bool` | True if you don&#39;t want to update the conversion value again in the current window |

### Reset Conversion Bit

You can specify a bit to reset in the conversion value. Note that this only happens when the `send_higher_value` is set to false, as resetting a bit would also lower the conversion value automatically.

| Remote Command | SKAdNetwork Method |
|---|---|
| `resetconversionbit` | `resetConversionBit()` |

|  Parameter | Type | Description |
|---|---|---|
| `bit_number` | `Int` | A number from 0 to 5 |
| `coarse_value` | `String` | The coarse value of this installation (low-medium-high) |
| `lock_window` | `Bool` | True if you don&#39;t want to update the conversion value again in the current window |

### Set Conversion Value

You can specify a conversion value. Only higher values will be taken when `send_higher_value` is true.

| Remote Command | SKAdNetwork Method |
|---|---|
| `setconversionvalue` | `setConversionValue()` |

|  Parameter | Type | Description |
|---|---|---|
| `fine_value` | `Int` | A number from 0 to 63. |
| `coarse_value` | `String` | The coarse value of this installation (low-medium-high). |
| `lock_window` | `Bool` | True if you don&#39;t want to update the conversion value again in the current window. |
| `limit_to_highest_n_bits` | `Int` | A number from 1 to 5, specifying how many bits should be used to represent this value, starting from the highest. Default is 6. |
| `limit_to_lowest_n_bits` | `Int` | A number from 1 to 5, specifying how many bits should be used to represent this value, starting from the lowest. Default is 6. |

Note that you can only specify the limit starting from the highest or the lowest bit, not both.

### Reset Conversion Value

Ignores the `send_higher_value` flag in the configuration and resets the conversion value to the starting state (fine value = 0 and coarse value = nil).

| Remote Command | SKAdNetwork Method |
|---|---|
| `resetconversionvalue` | `resetConversionValue()` |




