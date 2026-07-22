---
title: Mobile Concepts
description: Learn the basics of the mobile solution.
url: https://docs.tealium.com/platforms/getting-started-mobile/mobile-concepts/
---
## Tealium Collect (Recommended)

Tealium Collect is a lightweight data collection module that sends user events from your mobile app to the Tealium Customer Data Hub. The Tealium Collect module lets you integrate third-party vendors as server-side connectors instead of as installed SDKs.

Tealium Collect uses [event batching](https://docs.tealium.com/platforms/getting-started-mobile/event-batching/) and other power-saving techniques to provide the following benefits to mobile applications:

- Reduced app size and memory footprint
- Optimized network traffic
- Minimal battery usage

Learn more about sending data [server-side](https://docs.tealium.com/platforms/getting-started-mobile/server-side/).

## Tag Management

Tag Management is the module that enables Tealium iQ Tag Management within your mobile app. This client-side solution uses a hidden webview to run standard web-based vendor tags in your app. Use the Tag Management module to integrate with third-party vendors that do not support a server-side API.

Benefits of the Tag Management module include:

- Advanced data layer customization using [iQ Tag Management extensions](https://docs.tealium.com/about-extensions/).
- Support client-side and server-side using the [Tealium Collect tag](https://docs.tealium.com/tealium-collect-tag/).


<blockquote>
Avoid using both the Tealium Collect module and the Tealium Collect tag (through the Tag Management module), as this will result in duplicate tracking.
</blockquote>


Learn more about the [client-side](https://docs.tealium.com/platforms/getting-started-mobile/client-side/) solution.

## Data Layer
The data layer is a vendor-neutral and user-friendly representation of the activity you track on your digital properties. In addition to the standard built-in data layer variables provided by each platform installation, you will populate custom data layer variables with dynamic values from your app.

Learn more about the [data layer variables](https://docs.tealium.com/platforms/getting-started-mobile/data-layer/) available on mobile.

## Remote Commands
Remote commands are a client-side solution for triggering functionality in your native app. Use remote commands for custom native features or to integrate with third-party SDKs. Configure remote commands with a JSON file or a remote command tag in Tealium iQ Tag Management.

Learn more about [remote commands](https://docs.tealium.com/platforms/remote-commands/).

## Lifecycle Tracking
Each platform has its own lifecycle module, which enables automatic tracking of app lifecycle events (launch, wake, sleep) and associated data.

## Mobile Profiles
An app that uses the Tag Management module must have a corresponding profile in iQ Tag Management that has been activated for mobile use. A mobile profile includes the built-in mobile data layer variables and additional settings for the Tealium SDK that can be adjusted without needing to deploy an app update.

Learn more about [creating a mobile profile](https://docs.tealium.com/creating-a-mobile-profile/).

## Data Management
Some data layer variables need to remain consistent throughout your app's lifecycle. Instead of including these variables with every tracking call, use one of the storage solutions to set less volatile data layer variables.

### Persistent Storage
Data layer variables added to persistent storage are kept until the user uninstalls the app or manually clears the app's data. Each persistent data variable is included in every tracking automatically.

### Volatile Storage
Data layer variables added to volatile storage are kept until the app is cleared from memory, such as a force-close or restart. Each volatile data variable is included in every tracking call automatically. Volatile data is not stored on disk and does not contribute to the app's disk usage footprint on the device.

### Migrating Libraries
If you upgrade from an older library (Java, Objective-C, or Swift 1.x) to a newer one (Kotlin or Swift 2.x) your persistent data is migrated automatically. The migrated data includes user consent preferences, lifecycle data, and the Tealium Visitor ID.

Learn more about the latest [Tealium for Kotlin](https://docs.tealium.com/platforms/android-kotlin/data-layer/) and [Tealium for Swift](https://docs.tealium.com/platforms/ios-swift/data-layer/) libraries.
