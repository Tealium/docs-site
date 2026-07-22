---
title: Ad Identifier Module
description: Provides the ability to make use of the device "Ad Identifier" (ADID) to help identify interactions with display ad networks.
url: https://docs.tealium.com/platforms/android-java/module-list/adid/
---


## Requirements

* [Google Play Services SDK](https://developers.google.com/android/guides/setup)

## Install

Install the Ad Identifier module with Maven or manually.

### Maven

To install the Ad Identifier module with Maven:

1. In your project's top-level `build.gradle` file, add the following Maven repository:
      ```groovy
      maven {
            url "https://maven.tealiumiq.com/android/releases/"
      }
      ```

2. In your project module's `build.gradle` file, add the following Maven dependency:
      ```groovy
      dependencies{
            implementation 'com.tealium:library:5.8.0' //only required if you do not have this reference
            implementation 'com.tealium:adidentifier:1.0.4'
            implementation 'com.tealium:lifecycle:1.1.4' //only required if you do not already have this reference and require lifecycle tracking
      }
      ```

3. In the same block where you instantiate the Tealium library, after instantiating Tealium, add the following:  
      ```java
      // import the Tealium AdIdentifier module in the import section
      import com.tealium.adidentifier.AdIdentifier;

      // context to pass to AdIdentifier module
      Context mContext = this;

      // substitute the example instance name here with the same instance name you used when initializing the Tealium library
      private static final String TEALIUM_INSTANCENAME = "INSTANCE_NAME";

      // call this to store the referrer as Persistent data - recommended
      AdIdentifier.setIdPersistent(TEALIUM_INSTANCENAME, mContext);

      // call this to store the referrer as Volatile data (reset at app restart/terminate) - not recommended in most cases
      AdIdentifier.setIdVolatile(TEALIUM_INSTANCENAME, mContext);
      ```

### Manual

To install the Ad Identifier module manually:

1. Download the Tealium [AdIdentifier](https://github.com/Tealium/tealium-android/tree/master/Modules/AdIdentifier) module.

2. In your top-level `build.gradle` file, verify the following:  
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

3. Copy the file `tealium.adidentifier-1.0.4.aar` into your project's `<PROJECT_ROOT>/<MODULE>/libs` directory.

4. Add the Tealium library dependency to your project module’s `build.gradle` file:
      ```groovy
      dependencies {
            // only required if you do not already have this reference
            implementation (name:'tealium-5.8.0', ext:'aar')
            implementation (name:'tealium.adidentifier-1.0.4', ext:'aar')
            // only required if you do not already have this reference and require lifecycle tracking
            implementation (name:'tealium.lifecycle-1.1.4', ext:'aar')
      }
      ```

## Additional Considerations

*  **Blocked Access**  
If the user has not allowed access to the Ad Identifier, the module sets the `google_adid` variable to the string "Ad Tracking Disabled", which is handled in your Tealium iQ configuration to ensure you pass the expected data to your third-party vendors.

* **Delete the Ad Identifier**  
To delete the stored Ad Identifier string, call the standard methods provided by the Tealium library to remove variables from persistent or volatile storage. The key name for the variable is exposed by the `TealiumAdIdentifier` class. Here's an example to remove the stored Ad Identifier from both persistent and volatile data. This code has no effect and does not throw an error if the variable doesn't already exist.

      ```java
      // import the Tealium AdIdentifier module in the import section
      import com.tealium.adidentifier.AdIdentifier;

      private static final String TEALIUM_INSTANCENAME = "INSTANCE_NAME";
      final Tealium instance = Tealium.getInstance(TEALIUM_INSTANCENAME);

      // remove from persistent data store
      instance.getDataSources().getPersistentDataSources().edit().remove(AdIdentifier.KEY_GOOGLE_ADID).apply();

      // remove from volatile data store (session only)
      instance.getDataSources().getVolatileDataSources().remove(AdIdentifier.KEY_GOOGLE_ADID);
      ```

## Data Layer

The Ad Identifier module adds the following variables to the data layer:

| Variable | Type | Description | Example |
| --- | --- | --- | --- |     
| `google_adid` | `String` | The Google Ad Identifier ID | `ca-app-pub-0123456789012345~0123456789` |

## API Reference

For the complete reference of methods for the Ad Identifier module, see the [`AdIdentifier`](https://tealium.github.io/tealium-android/com/tealium/adidentifier/AdIdentifier.html) class in the Tealium SDK for Android API.
