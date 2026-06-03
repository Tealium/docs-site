---
title: Remote Command: Usabilla
description: Tealium remote command integration for Usabilla on Android and Swift/iOS.
url: https://docs.tealium.com/platforms/remote-commands/integrations/usabilla/
---
## Requirements

* Usabilla app ID and form ID
* One of these mobile libraries:
  * [Tealium for Android-Kotlin](/platforms/android-kotlin/) (1.0.0&#43;)
  * [Tealium for Android-Java](/platforms/android-java/) (5.9.0&#43; for Usabilla 1.0.0&#43; or &lt;5.9.0 for previous versions)
  * [Tealium for iOS-Swift](/platforms/ios-swift/)
* One of these remote command integrations:
  * [Usabilla Remote Command JSON File](/platforms/remote-commands/integrations/usabilla/#json-template) (Requires Android-Kotlin 1.0.0&#43; or iOS-Swift 2.1.0&#43;)
  * Usabilla Remote Command tag in Tealium iQ Tag Management

## How It Works

The Usabilla integration uses three items:

1. The Usabilla native SDK
2. The remote commands module that wraps the Usabilla methods
3. Either the JSON configuration file or Remote Command tag that translates event tracking into native Usabilla calls

Adding the Usabilla remote command module to your app automatically installs and builds the required Usabilla libraries. If you are using a dependency manager installation, there is no need to install the Usabilla SDK separately.

There are two remote command options: A JSON configuration file, or using iQ Tag Management to configure the mappings. A JSON configuration file is the recommended option for your vendor integration, hosted either remotely or locally within your app. If using iQ Tag Management, add the Remote Command tag for the vendor integration. Learn more about [vendor integrations](/platforms/remote-commands/how-it-works/#vendor-integrations).

## Install

### Dependency Manager




1. In your Xcode project, select **File &gt; Add Packages... &gt; Add Package Dependency**.
2. Enter the repository URL: `https://github.com/tealium/tealium-ios-usabilla-remote-command`.
3. Configure the version rules. Typically, `Up to next major` is recommended. If the current `TealiumUsabilla` version does not appear in the list, then reset your Swift package cache.
4. Select the `TealiumUsabilla` module to install, and select the app target you want the module to be installed in.

If your project has more than one app target and needs `TealiumUsabilla` module in more app targets, you have to manually add them in the **Frameworks, Libraries, and Embedded Content** section.

To install `TealiumUsabilla` in additional app targets:

1. Select your Xcode project in the **Project Navigator**.
2. In your Xcode project, select the app target under the **TARGETS** section.
3. Navigate to **General &gt; Frameworks, Libraries &amp; Embedded Content** and  select the `TealiumUsabilla` module to add it to your app target.

To add additional modules from the Tealium Swift library, follow the [Swift Package Manager](/platforms/ios-swift/install/#swift-package-manager-recommended) instructions.




1. Remove `tealium-swift` and `pod &#34;Usabilla&#34;` if they already exist your Podfile. The dependency for `tealium-swift` is already included in the `TealiumUsabilla` framework.

2. Add the following dependency to your Podfile:  
      ```ruby
      pod &#34;TealiumUsabilla&#34;
      ```  
      The `TealiumUsabilla` pod includes the following `TealiumSwift` dependencies:  
      ```bash
      &#39;tealium-swift/Core&#39;
      &#39;tealium-swift/TealiumDelegate&#39;
      &#39;tealium-swift/RemoteCommands&#39;
      &#39;tealium-swift/TagManagement&#39;
      ```

3. Import the modules `TealiumSwift` and `TealiumUsabilla` in your `TealiumHelper` file, and any other files that access the `Tealium` class or the Usabilla remote command.





1. Remove `tealium-swift` from your Cartfile. The dependency for `tealium-swift` is already included in the `TealiumUsabilla` framework.

2. Remove the following line if it exists in your Cartfile:  
      ```bash
      github &#34;usabilla/usabilla-u4a-ios-swift-sdk&#34;
      ```

3. Add the following dependency to your Cartfile:  
      ```bash
      github &#34;tealium/tealium-ios-usabilla-remote-command&#34;
      ```

Tealium for Swift SDK (version 1.6.5&#43;) requires the `TealiumDelegate` module to be included with your installation.





1. Install [Tealium for Android (Kotlin)](/platforms/android-kotlin/install/) or [Tealium for Android (Java)](/platforms/android-java/install/) and add the Tealium Maven URL to your project’s top-level `build.gradle` file, if you haven&#39;t done so already.

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

2. Import the Tealium-Usabilla remote commands by adding the following dependency in your app project&#39;s `build.gradle` file:  
      ```groovy
      dependencies {
            implementation &#39;com.tealium.remotecommands:usabilla:1.0.0&#39;
      }
      ```



### Manual Installation




The manual installation for Usabilla remote commands requires the [Tealium for Swift](/platforms/ios-swift/) library to be installed. To install the Usabilla remote commands for your iOS project:

1. Install the [Usabilla SDK](https://github.com/usabilla/usabilla-u4a-ios-swift-sdk), if you haven&#39;t already done so.

2. Clone the [Tealium iOS Usabilla remote command](https://github.com/tealium/tealium-ios-usabilla-remote-command) repo and drag the files within the `Sources` folder into your project.

3. Set the [`remoteAPIEnabled`](/platforms/ios-swift/api/tealium-config/#remoteapienabled) configuration flag to `true.`




The manual installation for Usabilla remote commands requires [Tealium for Android (Kotlin)](/platforms/android-kotlin/install/) or [Tealium for Android (Java)](/platforms/android-java/install/) to be installed.

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

2. Add `tealium-usabilla.aar` to `&lt;PROJECT_ROOT&gt;/&lt;MODULE&gt;/libs`.

3. Add the Tealium library dependency to your `build.gradle` file:

      ```groovy
      dependencies {
            implementation(name:&#39;tealium-usabilla&#39;, ext:&#39;aar&#39;)
      }
      ```




## Initialize

For all Tealium libraries, you need to register the Usabilla remote command when you initialize.




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
    let usabilla = UsabillaRemoteCommand() 

    // Local JSON
    //let usabilla = UsabillaRemoteCommand(type: .local(file: &#34;usabilla&#34;))

    // Remote JSON
    //let usabilla = UsabillaRemoteCommand(type: .remote(url: &#34;https://some.domain.com/usabilla.json&#34;))
    remoteCommands.add(usabilla)
}

```



Initialize remote commands with a JSON configuration file or the Remote Command tag for Tealium&#39;s Android (Kotlin) library:
```kotlin
val config = TealiumConfig(application,
        &#34;ACCOUNT&#34;,
        &#34;PROFILE&#34;,
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands, Dispatchers.TagManagement));
val usabilla = UsabillaRemoteCommand(TEALIUM_MAIN, config);

var tealium = Tealium.create(TEALIUM_MAIN, config) {

    // Webview Tag
    remoteCommands?.add(usabilla);

    // Local JSON
    //remoteCommands?.add(usabilla, filename = &#34;usabilla.json&#34;);

    // Remote JSON
    //remoteCommands?.add(usabilla, remoteUrl = &#34;https://some.domain.com/usabilla.json&#34;);
}
```

Additional (optional) [initialization parameters](https://github.com/usabilla/usabilla-u4a-android-sdk#initialization) are available for the Usabilla SDK:

- `usabillaHttpClient = null`  
Overrides the `HttpClient` object, which gives the possibility to inject a custom client to handle all the connections performed by the SDK. Learn more about the [custom HTTP client](https://github.com/usabilla/usabilla-u4a-android-sdk#custom-http-client).
- `usabillaReadyCallback = null`  
Overrides the `UsabillaReadyCallback` object, which is a callback used to communicate when the initialization process ends.
- `autoFragmentManager = false`  
Disables [passive feedback](https://github.com/usabilla/usabilla-u4a-android-sdk#passive-feedback) (enabled by default). Passive feedback requires Android&#39;s `FragmentManager` to be kept up-to-date and monitored using `android.app.Application.ActivityLifecycleCallbacks`.
- `autoFeedbackHandler = false`  
Disables handling of event tracking for passive and [campaign](https://github.com/usabilla/usabilla-u4a-android-sdk#campaigns) feedback forms as well as auto-removing forms that have been submitted or dismissed (enabled by default). Two `android.content.BroadcastReceiver`s are registered to listen for Usabilla events that handle both passive and campaign [feedback form closures](https://github.com/usabilla/usabilla-u4a-android-sdk#feedback-submission-callback).

The following example shows usage of the optional parameters:  
```kotlin
val usabilla = UsabillaRemoteCommand(TEALIUM_MAIN, config,
        usabillaHttpClient = null,
        usabillaReadyCallback = null,
        autoFragmentManager = false,
        autoFeedbackHandler = false);
```




The JSON Remote Command file feature for Android is only available in the Kotlin SDK. Initialize the Remote Command tag for Tealium&#39;s Android (Java) library:     
```java
Tealium.Config config = Tealium.Config.create(application, &#34;ACCOUNT&#34;, &#34;PROFILE&#34;, &#34;ENVIRONMENT&#34;);
Tealium teal = Tealium.createInstance(TEALIUM_MAIN, config);

RemoteCommand usabilla = new UsabillaRemoteCommand(TEALIUM_MAIN, config);
teal.addRemoteCommand(usabilla);
```

Additional (optional) [initialization parameters](https://github.com/usabilla/usabilla-u4a-android-sdk#initialization) are available for the Usabilla SDK:

- `usabillaHttpClient = null`  
Overrides the `HttpClient` object, which gives the possibility to inject a custom client to handle all the connections performed by the SDK. Learn more about the [custom HTTP client](https://github.com/usabilla/usabilla-u4a-android-sdk#custom-http-client).
- `usabillaReadyCallback = null`  
Overrides the `UsabillaReadyCallback` object, which is a callback used to communicate when the initialization process ends.
- `autoFragmentManager = false`  
Disables [passive feedback](https://github.com/usabilla/usabilla-u4a-android-sdk#passive-feedback) (enabled by default). Passive feedback requires Android&#39;s `FragmentManager` to be kept up-to-date and monitored using `android.app.Application.ActivityLifecycleCallbacks`.
- `autoFeedbackHandler = false`  
Disables handling of event tracking for passive and [campaign](https://github.com/usabilla/usabilla-u4a-android-sdk#campaigns) feedback forms as well as auto-removing forms that have been submitted or dismissed (enabled by default). Two `android.content.BroadcastReceiver`s are registered to listen for Usabilla events that handle both passive and campaign [feedback form closures](https://github.com/usabilla/usabilla-u4a-android-sdk#feedback-submission-callback).

The following example shows usage of the optional parameters:  
```java
RemoteCommand usabilla = new UsabillaRemoteCommand(TEALIUM_MAIN, config,
        usabillaHttpClient = null,
        usabillaReadyCallback = null,
        autoFragmentManager = false,
        autoFeedbackHandler = false);
```




## JSON Template

If you are configuring remote commands using a [JSON configuration file](/platforms/remote-commands/how-it-works/#json-configuration-file), refer to the following template to get started. The template includes common mappings used in a standard e-commerce installation. Edit the mappings as needed.

```json
{
  &#34;config&#34;: {
    &#34;appId&#34;: &#34;YOUR_APP_ID&#34;,
    &#34;debugEnabled&#34;: true
  },
  &#34;mappings&#34;: {
      &#34;event_name&#34;: &#34;event&#34;,
      &#34;display_campaigns&#34;: &#34;canDisplayCampaigns&#34;,
      &#34;dismiss_automatically&#34;: &#34;dismissAutomatically&#34;,
      &#34;form_id&#34;: &#34;formId&#34;,
      &#34;form_ids&#34;: &#34;formIds&#34;,
      &#34;customer_first_name&#34;: &#34;custom.customer_first_name&#34;
},
  &#34;commands&#34;: {
    &#34;launch&#34;: &#34;initialize&#34;,
    &#34;display_campaigns&#34;: &#34;candisplaycampaigns&#34;,
    &#34;dismiss&#34;: &#34;dismissautomatically&#34;,
    &#34;button_click&#34;: &#34;sendevent&#34;,
    &#34;load_form&#34;: &#34;loadfeedbackform&#34;,
    &#34;set_variables&#34;: &#34;setcustomvariable&#34;,
    &#34;reset&#34;: &#34;resetcampaigndata&#34;
  }
}
```

## Track

Events are tracked automatically for successful and unsuccessful form loads, as well as both passive and campaign feedback forms.

## Supported Methods

We map a command to each Usabilla method or property. To trigger a Usabilla method or property, pass the corresponding command in the specified format.

| Remote Command       | Usabilla Method/Property |
| :-- | :-- |
| `initialize`           | `initialize()`           |
| `sendevent`            | `sendEvent()`            |
| `debugenabled`         | `debugEnabled`           |
| `displaycampaigns`     | `canDisplayCampaigns`    |
| `loadfeedbackform`     | `loadFeedbackForm()`     |
| `preloadfeedbackforms` | `preloadFeedbackForms()` |
| `removecachedforms`    | `removeCachedForms()`    |
| `dismissautomatically` | `dismissAutomatically`   |
| `setcustomvariable`    | `customVariables`        |
| `resetcampaigndata`    | `resetCampaignData()`    |

Since the Usabilla SDK is integrated with the Tealium SDK, you may trigger any native Usabilla functionality given the corresponding tag configuration.

### SDK Setup

#### Initialize

The Usabilla SDK is initialized automatically upon launch. The Usabilla API key is set in the tag configuration.

| Remote Command | Usabilla Method |
|---|---|
| `initialize`  | `initialize()` |

Usabilla Developer Guide: Initial SDK Setup

- [iOS](https://github.com/usabilla/usabilla-u4a-ios-swift-sdk#initialization)
- [Android](https://github.com/usabilla/usabilla-u4a-android-sdk#initialization)

#### Debug

| Remote Command | Usabilla Property |
|---|---|
| `debugenabled`  | `debugEnabled` |

|  Parameter | Type |
|---|---|
|  `debugEnabled` (required) | Bool |

Usabilla Developer Guide: Initial SDK Setup

- [iOS](https://github.com/usabilla/usabilla-u4a-ios-swift-sdk#debugmode)  
- [Android](https://github.com/usabilla/usabilla-u4a-android-sdk#debug-mode)

#### Campaign Toggling

| Remote Command | Usabilla Property |
| :--- | :---|
| `displaycampaigns`  | `canDisplayCampaigns` |

|  Parameter | Type |
|---|---|
|  `canDisplayCampaigns` (required) | Bool |

Usabilla Developer Guide: Campaign Toggling

- [iOS](https://github.com/usabilla/usabilla-u4a-ios-swift-sdk#campaign-toggling)

Campaign toggling is not available for Android

### Targeting Options

#### Send Events

|  Remote Command | Usabilla Method |
|---|---|
| `sendevent`  | `sendEvent()` |

|  Parameter | Type |
|---|---|
|  `event` (required) | String |

Usabilla Developer Guide: Targeting Options

- [iOS](https://github.com/usabilla/usabilla-u4a-ios-swift-sdk#targeting-options)
- [Android](https://github.com/usabilla/usabilla-u4a-android-sdk#targeting-options)

### Set Custom Variables

|  Remote Command | Usabilla Property |
|---|---|
| `setcustomvariable`  | `customVariables` |

|  Parameter | Type |
|----|---|
| `custom.###` (required) | String |

Usabilla Developer Guide: Set Custom Variables

- [iOS](https://github.com/usabilla/usabilla-u4a-ios-swift-sdk#custom-variables)
- [Android](https://github.com/usabilla/usabilla-u4a-android-sdk#custom-variables)

### Forms

#### Load Feedback Form

|  Remote Command | Usabilla Method |
|---|---|
| `loadfeedbackform`  | `loadFeedbackForm` |

|  Parameter | Type | Example |
|----|---|---|
| `formId` (required) | String |  |
| `fragmentId` (Android only) | Integer | `R.id.activity_main` |

Usabilla Developer Guide: Load Feedback Form

- [iOS](https://github.com/usabilla/usabilla-u4a-ios-swift-sdk#loading-a-form)
- [Android](https://github.com/usabilla/usabilla-u4a-android-sdk#loading-a-form)

#### Preload Feedback Forms

|  Remote Command | Usabilla Method |
|---|---|
| `preloadfeedbackforms`  | `preloadFeedbackForms` |

|  Parameter | Type |
|----|---|
| `formIds` (required) | [String] |

Usabilla Developer Guide: Preload Feedback Forms

- [iOS](https://github.com/usabilla/usabilla-u4a-ios-swift-sdk#preloading-a-form)
- [Android](https://github.com/usabilla/usabilla-u4a-android-sdk#preloading-a-form)

#### Remove Cached Forms

|  Remote Command | Usabilla Method |
|---|---|
| `removecachedforms`  | `removeCachedForms` |

Usabilla Developer Guide: Remove Cached Forms

- [iOS](https://github.com/usabilla/usabilla-u4a-ios-swift-sdk#preloading-a-form)
- [Android](https://github.com/usabilla/usabilla-u4a-android-sdk#reset-passive-forms)

#### Dismiss Automatically

| Remote Command | Usabilla Property |
|---|---|
| `dismissautomatically`  | `dismissAutomatically` |

|  Parameter | Type |
|---|---|
|  `dismissAutomatically` (required) | Bool |

Usabilla Developer Guide: Manual Dismiss

- [iOS](https://github.com/usabilla/usabilla-u4a-ios-swift-sdk#handle-manual-dismiss)
- [Android](https://github.com/usabilla/usabilla-u4a-android-sdk#dismissing-forms)

#### Reset

| Remote Command | Usabilla Property |
|---|---|
| `resetcampaigndata`  | `resetCampaignData` |

Usabilla Developer Guide: Resetting All Campaigns

- [iOS](https://github.com/usabilla/usabilla-u4a-ios-swift-sdk#resetting-all-campaigns)
- [Android](https://github.com/usabilla/usabilla-u4a-android-sdk#reset-campaigns-data)