---
title: Remote Command: Branch
description: Tealium remote command integration for Branch on Android and Swift/iOS.
url: https://docs.tealium.com/platforms/remote-commands/integrations/branch/
---
## Requirements

* [Branch Key from Dashboard](https://dashboard.branch.io/settings/link)
* One of these mobile libraries:
  * [Tealium for Android (Kotlin)](https://docs.tealium.com/platforms/android-kotlin/) (1.0.0+)
  * [Tealium for Android (Java)](https://docs.tealium.com/platforms/android-java/) (5.9.0+)
  * [Tealium for iOS (Swift)](https://docs.tealium.com/platforms/ios-swift/) (2.1.0+)
* One of these remote command integrations:
  * [Branch Remote Command JSON File](https://docs.tealium.com/platforms/remote-commands/integrations/branch/#json-template)
  * [Branch Remote Command tag](https://docs.tealium.com/branch-mobile-remote-command-tag/) in Tealium iQ Tag Management

## How It Works

The Branch integration uses three items:

1. The Branch native SDK
2. The remote commands module that wraps the Branch methods
3. Either the JSON configuration file or Remote Command tag that translates event tracking into native Branch calls

Adding the Branch remote command module to your app automatically installs and builds the required Branch libraries, without having to add vendor-specific code to your app. If you are using a dependency manager installation, there is no need to install the Branch SDK separately.

There are two remote command options: A JSON configuration file, or using iQ Tag Management to configure the mappings. A JSON configuration file is the recommended option for your vendor integration, hosted either remotely or locally within your app. If using iQ Tag Management, add the Remote Command tag for the vendor integration. Learn more about [vendor integrations](https://docs.tealium.com/platforms/remote-commands/how-it-works/#vendor-integrations).

## Install

### Dependency Manager




1. In your Xcode project, select **File > Add Packages... > Add Package Dependency**.
2. Enter the repository URL: `https://github.com/tealium/tealium-ios-branch-remote-command`.
3. Configure the version rules. Typically, `Up to next major` is recommended. If the current `TealiumBranch` version does not appear in the list, then reset your Swift package cache.
4. Select the `TealiumBranch` module to install, and select the app target you want the module to be installed in.

If your project has more than one app target and needs `TealiumBranch` module in more app targets, you have to manually add them in the **Frameworks, Libraries, and Embedded Content** section.

To install `TealiumBranch` in additional app targets:

1. Select your Xcode project in the **Project Navigator**.
2. In your Xcode project, select the app target under the **TARGETS** section.
3. Navigate to **General > Frameworks, Libraries & Embedded Content** and  select the `TealiumBranch` module to add it to your app target.

To add additional modules from the Tealium Swift library, follow the [Swift Package Manager](https://docs.tealium.com/platforms/ios-swift/install/#swift-package-manager-recommended) instructions.




1. Remove `tealium-swift` and `pod "Branch"` if they already exist your Podfile. The dependency for `tealium-swift` is already included in the `TealiumBranch` framework.

2. Add the following dependency to your Podfile:
      ```ruby
      pod "TealiumBranch"
      ```
      The `TealiumBranch` pod includes the following `TealiumSwift` dependencies:  
      ```bash
      'tealium-swift/Core'
      'tealium-swift/RemoteCommands'
      'tealium-swift/TagManagement'
      ```

3. Import the modules `TealiumSwift` and `TealiumBranch` in your `TealiumHelper` file, and any other files that access the `Tealium` class, or the Branch Remote Command.




1. Remove `tealium-swift` from your Cartfile. The dependency for `tealium-swift` is already included in the `TealiumBranch` framework.

2.  Add the following dependency to your Cartfile:  
      ```bash
      github "tealium/tealium-ios-branch-remote-command"
      ```


<blockquote>
Tealium for Swift SDK (version 1.6.5+) requires the `TealiumDelegate` module to be included with your installation.
</blockquote>





1. Install [Tealium for Android (Kotlin)](https://docs.tealium.com/platforms/android-kotlin/install/) or [Tealium for Android (Java)](https://docs.tealium.com/platforms/android-java/install/), if you haven't done so already.

2. Add the Tealium Maven URL to your project’s top-level `build.gradle` file:

      ```groovy
      allprojects {
        repositories {
          mavenCentral()
          maven {
            url "https://maven.tealiumiq.com/android/releases/"
          }
        }
      }
      ```

3. Import both the Branch SDK and Tealium-Branch remote commands by adding the following dependencies in your app project's `build.gradle` file:  
      ```groovy
      dependencies {
            implementation 'com.tealium.remotecommands:branch:1.0.0'
      }
      ```





### Manual Installation




The manual installation for Branch remote commands requires the [Tealium for Swift](https://docs.tealium.com/platforms/ios-swift/) library to be installed. To install the Branch remote commands for your iOS project:

1. Install the [Branch SDK](https://help.branch.io/developers-hub/docs/ios-basic-integration#via-manual-framework), if you haven't already done so.

2. Clone the Tealium iOS Branch remote command repo and drag the files within the `Sources` folder into your project.  
GitHub repo: [https://github.com/tealium/tealium-ios-branch-remote-command](https://github.com/tealium/tealium-ios-branch-remote-command)

3. Set the [`remoteAPIEnabled`](https://docs.tealium.com/platforms/ios-swift/api/tealium-config/#remoteapienabled) configuration flag to `true`.




The manual installation for Branch remote commands requires [Tealium for Android (Kotlin)](https://docs.tealium.com/platforms/android-kotlin/install/) or [Tealium for Android (Java)](https://docs.tealium.com/platforms/android-java/install/) to be installed.

To install the Branch remote commands for your Android project:

1. Add `flatDir` to your project root `build.gradle` file:

      ```groovy
      allprojects {
            repositories {
              mavenCentral()
              flatDir {
                  dirs 'libs'
              }
            }
      }
      ```

2. Add `tealium-branch.aar` to `<PROJECT_ROOT>/<MODULE>/libs`.

3. Add the Tealium library dependency to your `build.gradle` file:

      ```groovy
      dependencies {
            implementation(name:'tealium-branch', ext:'aar')
      }
      ```




## Initialize

For all Tealium libraries, register the Branch mobile remote commands when you initialize.




Initialize remote commands with a JSON configuration file or the Remote Command tag for Tealium's iOS (Swift) library:
```swift
var tealium : Tealium?
let config = TealiumConfig(account: "ACCOUNT",
                           profile: "PROFILE",
                           environment: "ENVIRONMENT",
                           dataSource: "DATASOURCE")
config.dispatchers = [Dispatchers.TagManagement, Dispatchers.RemoteCommands]
config.remoteAPIEnabled = true // Required to use Remote Commands

tealium = Tealium(config: config) { _ in
    guard let remoteCommands = self.tealium?.remoteCommands else {
        return
    }

    // Webview Tag
    let branch = BranchRemoteCommand() 

    // Local JSON
    //let branch = BranchRemoteCommand(type: .local(file: "branch")) 

    // Remote JSON
    //let branch = BranchRemoteCommand(type: .remote(url: "https://some.domain.com/branch.json")) 

    remoteCommands.add(branch)
}
```




Initialize remote commands with a JSON configuration file or the Remote Command tag for Tealium's Kotlin library:
```kotlin
val config = TealiumConfig(application,
        "ACCOUNT",
        "PROFILE",
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands, Dispatchers.TagManagement));
val branch = BranchRemoteCommand(application);

var tealium = Tealium.create(TEALIUM_MAIN, config) {

    // Webview Tag
    remoteCommands?.add(branch); 

    // Local JSON
    //remoteCommands?.add(branch, filename = "branch.json"); 

    // Remote JSON
    //remoteCommands?.add(branch, remoteUrl = "https://some.domain.com/branch.json"); 
}
```




Initialize remote commands with the Remote Command tag for Tealium's Android (Java) library:

```java
RemoteCommand branch = new BranchRemoteCommand(application);
teal.addRemoteCommand(branch);
```



## JSON Template

If you are configuring remote commands using a [JSON configuration file](https://docs.tealium.com/platforms/remote-commands/how-it-works/#json-configuration-file), refer to the following template to get started. The template includes common mappings used in a standard installation. Edit the mappings as needed.


```json
{
  "config": {
    "settings": {
      "enable_logging": true,
      "branch_dev_key": "branch_key",
      "collect_device_id": true
    }
  },
  "mappings": {
    "tealium_event": "event.description",
    "description": "buo.description",
    "item_id": "buo.canonical_identifier",
    "title": "buo.title",
    "feature": "link.feature",
    "channel": "link.channel",
    "campaign": "link.campaign",
    "latitude": "metadata.latitude",
    "longitude": "metadata.longitude",
    "currency_code": "metadata.currency_type",
    "customer_id": "event.user_id",
    "coupon": "metadata.coupon",
    "product_brand": "metadata.product_brand",
    "product_category": "metadata.product_category",
    "product_id": "metadata.sku",
    "product_name": "metadata.product_name",
    "product_variant": "metadata.product_variant",
    "product_unit_price": "metadata.price",
    "product_quantity": "event.quantity",
    "currency_type": "event.currency",
    "order_tax": "event.tax"
  },
  "commands": {
    "launch": "initialize",
    "user_login": "login,setuserid",
    "user_register": "completeregistration",
    "show_offers": "clickad",
    "cart_add": "addtocart",
    "wishlist_add": "addtowishlist",
    "payment": "addpaymentinfo",
    "level_up": "achievelevel",
    "email_signup": "subscribe",
    "product": "viewitem",
    "share": "share",
    "rate": "rate",
    "search": "search",
    "invite": "invite",
    "order": "initiatepurchase",
    "record_score": "record_score",
    "teal_custom_event": "teal_custom_event"
  }
}
```

## Supported Methods

We map a command to each Branch method. To trigger a Branch method, pass the corresponding command in the specified format.

#### iOS Remote Commands

| iOS Remote Command | Branch Method |
| :-- | :-- |
| `initialize` | `initSession()` |
| `setuserid` | `setIdentity()` |
| `logout` | `logout()` |
| Any other | `logEvent()` |

#### Android Remote Commands

| Android Remote Command | Branch Method |
| :-- | :-- |
| `initialize` | `initSession()` |
| `setuserid` | `setIdentity()` |
| `logout` | `logout()` |
| `createdeeplink` | `generateShortUrl()` |
| Any other | `logEvent()` |

### Standard Event Names

The following standard event command names are supported with the `logEvent` method. When a command is sent, and all required variables are mapped and defined for the event, then the command is automatically triggered in the Branch SDK.

| Remote Command | Branch Event Name (iOS)| Branch Event Name (Andriod)
| :-- | :-- | :-- |
|`achievelevel`| `BranchStandardEvent.achieveLevel`| `BRANCH_STANDARD_EVENT.ACHIEVE_LEVEL` |
|`addpaymentinfo`| `BranchStandardEvent.addPaymentInfo`| `BRANCH_STANDARD_EVENT.ADD_PAYMENT_INFO`|
|`addtocart`| `BranchStandardEvent.addToCart`| `BRANCH_STANDARD_EVENT.ADD_TO_CART` |
|`addtowishlist`| `BranchStandardEvent.addToWishlist`| `BRANCH_STANDARD_EVENT.ADD_TO_WISHLIST` |
|`clickad`| `BranchStandardEvent.clickAd`| `BRANCH_STANDARD_EVENT.CLICK_AD` |
|`completetutorial`| `BranchStandardEvent.completeTutorial`| `BRANCH_STANDARD_EVENT.COMPLETE_TUTORIAL`|
|`completeregistration`| `BranchStandardEvent.completeRegistration`| `BRANCH_STANDARD_EVENT.COMPLETE_REGISTRATION` |
|`completestream`| Custom event `BranchEvent(eventName)`| `BRANCH_STANDARD_EVENT.COMPLETE_STREAM` |
|`initiatepurchase`| `BranchStandardEvent.initiatePurchase`| `BRANCH_STANDARD_EVENT.INITIATE_PURCHASE` |
|`initiatestream`| Custom event `BranchEvent(eventName)`| `BRANCH_STANDARD_EVENT.INITIATE_STREAM` |
|`invite`| `BranchStandardEvent.invite`| `BRANCH_STANDARD_EVENT.INVITE` |
|`login`| `BranchStandardEvent.login`| `BRANCH_STANDARD_EVENT.LOGIN` |
|`purchase`| `BranchStandardEvent.purchase`| `BRANCH_STANDARD_EVENT.PURCHASE` |
|`rate`| `BranchStandardEvent.rate`| `BRANCH_STANDARD_EVENT.RATE` |
|`reserve`| `BranchStandardEvent.reserve`| `BRANCH_STANDARD_EVENT.RESERVE` |
|`search`| `BranchStandardEvent.search`| `BRANCH_STANDARD_EVENT.SEARCH` |
|`share`| `BranchStandardEvent.share`| `BRANCH_STANDARD_EVENT.SHARE` |
|`spendcredits`| `BranchStandardEvent.spendCredits`| `BRANCH_STANDARD_EVENT.SPEND_CREDITS` |
|`starttrial`| `BranchStandardEvent.startTrial`| `BRANCH_STANDARD_EVENT.START_TRIAL` |
|`subscribe`| `BranchStandardEvent.subscribe`| `BRANCH_STANDARD_EVENT.SUBSCRIBE` |
|`unlockachievement`| `BranchStandardEvent.unlockAchievement`| `BRANCH_STANDARD_EVENT.UNLOCK_ACHIEVEMENT` |
|`viewad`| `BranchStandardEvent.viewAd`| `BRANCH_STANDARD_EVENT.VIEW_AD` |
|`viewcart`| `BranchStandardEvent.viewCart`| `BRANCH_STANDARD_EVENT.VIEW_CART` |
|`viewitem`| `BranchStandardEvent.viewItem`| `BRANCH_STANDARD_EVENT.VIEW_ITEM` |
|`viewitems`| `BranchStandardEvent.viewItems`| `BRANCH_STANDARD_EVENT.VIEW_ITEMS` |
|`custom`| `BranchEvent(eventString)` | `BranchEvent(eventString)` |


### SDK Setup

Learn more about the Branch SDK Setup:

  - [Branch iOS SDK](https://help.branch.io/developers-hub/docs/ios-basic-integration)
  - [Branch Android SDK](https://help.branch.io/developers-hub/docs/android-basic-integration)

#### Initialize

The Branch SDK is initialized automatically upon launch. The Branch Key is set in the Info.plist or the `branch_dev_key` inside the JSON configuration file.

| Remote Command | Branch Method |
|---|---|
| `initialize`  | `initSession()` |

There are a few configuration options available for the Branch Remote Command tag. If any of the below are set on launch, they are sent during the `configure()` method.

##### Configuration Options

| Name | TiQ Variable Mapping | Description | Type |
|---|---|---|---|
| Enable Logging  | `enable_logging` | Log Branch events to the console | `Bool` |
| Branch Key | `branch_dev_key`  | The key for your branch application. | `String` |


#### Send Identity Link

|  Remote Command | Branch Method |
|---|---|
| `setIdentity`  | `setIdentity()` |

|  Parameter | Type |
|---|---|
|  `id` (required) | String |
