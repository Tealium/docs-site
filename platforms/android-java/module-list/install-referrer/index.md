---
title: Install Referrer Module
description: Provides the automatic collection of app installation referrer information (when available) and adds it to the data layer.
url: https://docs.tealium.com/platforms/android-java/module-list/install-referrer/
---

## Requirements

* [Tealium for Android](https://docs.tealium.com/platforms/android-java/) (5.0.0+) ([solution for 4.x](#solution-for-tealium-sdk-4-x))

## Install

Install the Install Referrer module with Maven or manually.

### Maven

To install the Install Referrer module with Maven:

1. In your project's top-level `build.gradle` file, add the following Maven repository:
      ```groovy
      maven {
            url "https://maven.tealiumiq.com/android/releases/"
      }
      ```  
2. In your project module's `build.gradle` file, add the following Maven dependency:
      ```groovy
      dependencies{
            // only required if you do not have this reference
            implementation 'com.tealium:library:5.8.0'
            implementation 'com.tealium:installreferrer:1.1.3'
            // only required if you do not already have this reference and require lifecycle tracking
            implementation 'com.tealium:lifecycle:1.1.4'
            // Google's Install Referrer API
            implementation 'com.android.installreferrer:installreferrer:1.0'
      }
      ```  
      
<blockquote>
The [Google Install Referrer API](https://developer.android.com/google/play/installreferrer/library) is a dependency for this module, but is not automatically added for you. Add the module to your build.
</blockquote>


3. In the same block where you instantiate the Tealium library (after instantiating Tealium), add the following:

      ```java
      // import the Tealium InstallReferrer module in the import section
      import com.tealium.installreferrer.InstallReferrerReceiver;

      // substitute the example instance name here with the same instance name you used when initializing the Tealium library
      private static final String TEALIUM_INSTANCENAME = "INSTANCE_NAME";

      // call this to store the referrer as Persistent data - recommended
      InstallReferrerReceiver.setReferrerPersistent(applicationContext, TEALIUM_INSTANCENAME);

      // call this to store the referrer as Volatile data (reset at app restart/terminate) - not recommended in most cases
      InstallReferrerReceiver.setReferrerVolatile(applicationContext, TEALIUM_INSTANCENAME);
      ```

### Manual

To install the Install Referrer module manually:

1. Download the Tealium [Install Referrer](https://github.com/Tealium/tealium-android/tree/master/Modules/InstallReferrer) module.

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

3. Copy the file `tealium.installreferrer-1.1.2.aar` into your project's `<PROJECT_ROOT>/<MODULE>/libs` directory.

4. Add the Tealium library dependency to your project module’s `build.gradle` file:
      ```groovy
      dependencies {
            // only required if you do not already have this reference
            implementation(name:'tealium-5.6.1', ext:'aar')
            implementation(name:'tealium.installreferrer-1.1.2', ext:'aar')
            // only required if you do not already have this reference and require lifecycle tracking
            implementation(name:'tealium.lifecycle-1.1.2', ext:'aar')
            // Google's Install Referrer API
            implementation 'com.android.installreferrer:installreferrer:1.0'
      }
      ```


## Sample Value

Expect to receive the following URL-formatted data in the `INSTALL_REFERRER` variable, assuming that your incoming URL contained all the specified campaign information.

```
utm_medium=test_medium&
utm_term=test_term&
utm_content=test_content&
utm_campaign=test_name
```

## Additional Considerations

**Delete the Stored Referrer**  
To delete the stored install referrer string, call the standard methods provided by the Tealium library to remove variables from persistent or volatile storage. The key name for the variable is exposed by the `InstallReferrerReceiver` class. The following example removes the stored install referrer from both persistent and volatile data. This code has no effect and does not throw an error, if the variable doesn't already exist.  

```java
// remove from persistent data store
instance.getDataSources().getPersistentDataSources().edit().remove(InstallReferrerReceiver.KEYNAME).apply();

// remove from volatile data store (session only)
instance.getDataSources().getVolatileDataSources().remove(InstallReferrerReceiver.KEYNAME);
```

## Solution for Tealium SDK 4.x

The Install Referrer module is only compatible with Tealium SDK 5.x.

To achieve this functionality on SDK 4.x, use the following code:

```xml
// Android Manifest
<receiver
    android:name="com.tealium.InstallReferrerReceiver"
    android:exported="true">
    <intent-filter>
        <action android:name="com.android.vending.INSTALL_REFERRER" />
    </intent-filter>
</receiver>
```

```java
// Class for retrieving install referrer
public class InstallReferrerReceiver extends BroadcastReceiver {

    private static final String INSTALL_REFERRER = "INSTALL_REFERRER";

    public void onReceive(Context context, Intent intent) {
        if (intent != null) {
            return;
        }
        Bundle extras = intent.getExtras();
        if (extras == null) {
            return;
        }
        String referrer = extras.getString("referrer");

        if (StringUtils.isNotBlank(referrer)) {
            Tealium.getGlobalCustomData().edit().putString(INSTALL_REFERRER, referrer).apply();
        }
    }
}
```
## API Reference

For the complete reference of methods for the Install Referrer module, see the [`InstallReferrerReceiver`](https://tealium.github.io/tealium-android/com/tealium/installreferrer/InstallReferrerReceiver.html) class in the Tealium SDK for Android API.
