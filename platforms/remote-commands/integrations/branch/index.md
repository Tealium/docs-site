---
title: Remote Command: Branch
description: Tealium remote command integration for Branch on Android and Swift/iOS.
url: https://docs.tealium.com/platforms/remote-commands/integrations/branch/
---
## Requirements

* [Branch Key from Dashboard](https://dashboard.branch.io/settings/link)
* One of these mobile libraries:
  * [Tealium for Android (Kotlin)](/platforms/android-kotlin/) (1.0.0&#43;)
  * [Tealium for Android (Java)](/platforms/android-java/) (5.9.0&#43;)
  * [Tealium for iOS (Swift)](/platforms/ios-swift/) (2.1.0&#43;)
* One of these remote command integrations:
  * [Branch Remote Command JSON File](/platforms/remote-commands/integrations/branch/#json-template)
  * [Branch Remote Command tag]() in Tealium iQ Tag Management

## How It Works

The Branch integration uses three items:

1. The Branch native SDK
2. The remote commands module that wraps the Branch methods
3. Either the JSON configuration file or Remote Command tag that translates event tracking into native Branch calls

Adding the Branch remote command module to your app automatically installs and builds the required Branch libraries, without having to add vendor-specific code to your app. If you are using a dependency manager installation, there is no need to install the Branch SDK separately.

There are two remote command options: A JSON configuration file, or using iQ Tag Management to configure the mappings. A JSON configuration file is the recommended option for your vendor integration, hosted either remotely or locally within your app. If using iQ Tag Management, add the Remote Command tag for the vendor integration. Learn more about [vendor integrations](/platforms/remote-commands/how-it-works/#vendor-integrations).

## Install

### Dependency Manager




1. In your Xcode project, select **File &gt; Add Packages... &gt; Add Package Dependency**.
2. Enter the repository URL: `https://github.com/tealium/tealium-ios-branch-remote-command`.
3. Configure the version rules. Typically, `Up to next major` is recommended. If the current `TealiumBranch` version does not appear in the list, then reset your Swift package cache.
4. Select the `TealiumBranch` module to install, and select the app target you want the module to be installed in.

If your project has more than one app target and needs `TealiumBranch` module in more app targets, you have to manually add them in the **Frameworks, Libraries, and Embedded Content** section.

To install `TealiumBranch` in additional app targets:

1. Select your Xcode project in the **Project Navigator**.
2. In your Xcode project, select the app target under the **TARGETS** section.
3. Navigate to **General &gt; Frameworks, Libraries &amp; Embedded Content** and  select the `TealiumBranch` module to add it to your app target.

To add additional modules from the Tealium Swift library, follow the [Swift Package Manager](/platforms/ios-swift/install/#swift-package-manager-recommended) instructions.




1. Remove `tealium-swift` and `pod &#34;Branch&#34;` if they already exist your Podfile. The dependency for `tealium-swift` is already included in the `TealiumBranch` framework.

2. Add the following dependency to your Podfile:
      ```ruby
      pod &#34;TealiumBranch&#34;
      ```
      The `TealiumBranch` pod includes the following `TealiumSwift` dependencies:  
      ```bash
      &#39;tealium-swift/Core&#39;
      &#39;tealium-swift/RemoteCommands&#39;
      &#39;tealium-swift/TagManagement&#39;
      ```

3. Import the modules `TealiumSwift` and `TealiumBranch` in your `TealiumHelper` file, and any other files that access the `Tealium` class, or the Branch Remote Command.




1. Remove `tealium-swift` from your Cartfile. The dependency for `tealium-swift` is already included in the `TealiumBranch` framework.

2.  Add the following dependency to your Cartfile:  
      ```bash
      github &#34;tealium/tealium-ios-branch-remote-command&#34;
      ```

Tealium for Swift SDK (version 1.6.5&#43;) requires the `TealiumDelegate` module to be included with your installation.




1. Install [Tealium for Android (Kotlin)](/platforms/android-kotlin/install/) or [Tealium for Android (Java)](/platforms/android-java/install/), if you haven&#39;t done so already.

2. Add the Tealium Maven URL to your project’s top-level `build.gradle` file:

      ```groovy
      allprojects {
        repositories {
          mavenCentral()
          maven {
            url &#34;https://maven.tealiumiq.com/android/releases/&#34;
          }
        }
      }
      ```

3. Import both the Branch SDK and Tealium-Branch remote commands by adding the following dependencies in your app project&#39;s `build.gradle` file:  
      ```groovy
      dependencies {
            implementation &#39;com.tealium.remotecommands:branch:1.0.0&#39;
      }
      ```





### Manual Installation




The manual installation for Branch remote commands requires the [Tealium for Swift](/platforms/ios-swift/) library to be installed. To install the Branch remote commands for your iOS project:

1. Install the [Branch SDK](https://help.branch.io/developers-hub/docs/ios-basic-integration#via-manual-framework), if you haven&#39;t already done so.

2. Clone the Tealium iOS Branch remote command repo and drag the files within the `Sources` folder into your project.  
GitHub repo: [https://github.com/tealium/tealium-ios-branch-remote-command](https://github.com/tealium/tealium-ios-branch-remote-command)

3. Set the [`remoteAPIEnabled`](/platforms/ios-swift/api/tealium-config/#remoteapienabled) configuration flag to `true`.




The manual installation for Branch remote commands requires [Tealium for Android (Kotlin)](/platforms/android-kotlin/install/) or [Tealium for Android (Java)](/platforms/android-java/install/) to be installed.

To install the Branch remote commands for your Android project:

1. Add `flatDir` to your project root `build.gradle` file:

      ```groovy
      allprojects {
            repositories {
              mavenCentral()
              flatDir {
                  dirs &#39;libs&#39;
              }
            }
      }
      ```

2. Add `tealium-branch.aar` to `&lt;PROJECT_ROOT&gt;/&lt;MODULE&gt;/libs`.

3. Add the Tealium library dependency to your `build.gradle` file:

      ```groovy
      dependencies {
            implementation(name:&#39;tealium-branch&#39;, ext:&#39;aar&#39;)
      }
      ```




## Initialize

For all Tealium libraries, register the Branch mobile remote commands when you initialize.




Initialize remote commands with a JSON configuration file or the Remote Command tag for Tealium&#39;s iOS (Swift) library:
```swift
var tealium : Tealium?
let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                           profile: &#34;PROFILE&#34;,
                           environment: &#34;ENVIRONMENT&#34;,
                           dataSource: &#34;DATASOURCE&#34;)
config.dispatchers = [Dispatchers.TagManagement, Dispatchers.RemoteCommands]
config.remoteAPIEnabled = true // Required to use Remote Commands

tealium = Tealium(config: config) { _ in
    guard let remoteCommands = self.tealium?.remoteCommands else {
        return
    }

    // Webview Tag
    let branch = BranchRemoteCommand() 

    // Local JSON
    //let branch = BranchRemoteCommand(type: .local(file: &#34;branch&#34;)) 

    // Remote JSON
    //let branch = BranchRemoteCommand(type: .remote(url: &#34;https://some.domain.com/branch.json&#34;)) 

    remoteCommands.add(branch)
}
```




Initialize remote commands with a JSON configuration file or the Remote Command tag for Tealium&#39;s Kotlin library:
```kotlin
val config = TealiumConfig(application,
        &#34;ACCOUNT&#34;,
        &#34;PROFILE&#34;,
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands, Dispatchers.TagManagement));
val branch = BranchRemoteCommand(application);

var tealium = Tealium.create(TEALIUM_MAIN, config) {

    // Webview Tag
    remoteCommands?.add(branch); 

    // Local JSON
    //remoteCommands?.add(branch, filename = &#34;branch.json&#34;); 

    // Remote JSON
    //remoteCommands?.add(branch, remoteUrl = &#34;https://some.domain.com/branch.json&#34;); 
}
```




Initialize remote commands with the Remote Command tag for Tealium&#39;s Android (Java) library:

```java
RemoteCommand branch = new BranchRemoteCommand(application);
teal.addRemoteCommand(branch);
```



## JSON Template

If you are configuring remote commands using a [JSON configuration file](/platforms/remote-commands/how-it-works/#json-configuration-file), refer to the following template to get started. The template includes common mappings used in a standard installation. Edit the mappings as needed.


```json
{
  &#34;config&#34;: {
    &#34;settings&#34;: {
      &#34;enable_logging&#34;: true,
      &#34;branch_dev_key&#34;: &#34;branch_key&#34;,
      &#34;collect_device_id&#34;: true
    }
  },
  &#34;mappings&#34;: {
    &#34;tealium_event&#34;: &#34;event.description&#34;,
    &#34;description&#34;: &#34;buo.description&#34;,
    &#34;item_id&#34;: &#34;buo.canonical_identifier&#34;,
    &#34;title&#34;: &#34;buo.title&#34;,
    &#34;feature&#34;: &#34;link.feature&#34;,
    &#34;channel&#34;: &#34;link.channel&#34;,
    &#34;campaign&#34;: &#34;link.campaign&#34;,
    &#34;latitude&#34;: &#34;metadata.latitude&#34;,
    &#34;longitude&#34;: &#34;metadata.longitude&#34;,
    &#34;currency_code&#34;: &#34;metadata.currency_type&#34;,
    &#34;customer_id&#34;: &#34;event.user_id&#34;,
    &#34;coupon&#34;: &#34;metadata.coupon&#34;,
    &#34;product_brand&#34;: &#34;metadata.product_brand&#34;,
    &#34;product_category&#34;: &#34;metadata.product_category&#34;,
    &#34;product_id&#34;: &#34;metadata.sku&#34;,
    &#34;product_name&#34;: &#34;metadata.product_name&#34;,
    &#34;product_variant&#34;: &#34;metadata.product_variant&#34;,
    &#34;product_unit_price&#34;: &#34;metadata.price&#34;,
    &#34;product_quantity&#34;: &#34;event.quantity&#34;,
    &#34;currency_type&#34;: &#34;event.currency&#34;,
    &#34;order_tax&#34;: &#34;event.tax&#34;
  },
  &#34;commands&#34;: {
    &#34;launch&#34;: &#34;initialize&#34;,
    &#34;user_login&#34;: &#34;login,setuserid&#34;,
    &#34;user_register&#34;: &#34;completeregistration&#34;,
    &#34;show_offers&#34;: &#34;clickad&#34;,
    &#34;cart_add&#34;: &#34;addtocart&#34;,
    &#34;wishlist_add&#34;: &#34;addtowishlist&#34;,
    &#34;payment&#34;: &#34;addpaymentinfo&#34;,
    &#34;level_up&#34;: &#34;achievelevel&#34;,
    &#34;email_signup&#34;: &#34;subscribe&#34;,
    &#34;product&#34;: &#34;viewitem&#34;,
    &#34;share&#34;: &#34;share&#34;,
    &#34;rate&#34;: &#34;rate&#34;,
    &#34;search&#34;: &#34;search&#34;,
    &#34;invite&#34;: &#34;invite&#34;,
    &#34;order&#34;: &#34;initiatepurchase&#34;,
    &#34;record_score&#34;: &#34;record_score&#34;,
    &#34;teal_custom_event&#34;: &#34;teal_custom_event&#34;
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
