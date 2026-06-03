---
title: Install Referrer Module
description: Provides the automatic collection of app installation referrer information (when available) and adds it to the data layer.
url: https://docs.tealium.com/platforms/android-kotlin/module-list/install-referrer/
---
## Install

Install the Install Referrer module with Maven or manually.

### Maven

To install the Install Referrer module with Maven:

1. In your project&#39;s top-level `build.gradle` file, add the following Maven repository:
      ```groovy
      maven {
            url &#34;https://maven.tealiumiq.com/android/releases/&#34;
      }
      ```  
2. In your project module&#39;s `build.gradle` file, add the following Maven dependency:
      ```groovy
      dependencies{
            // only required if you do not have this reference
            implementation &#39;com.tealium:kotlin-core:1.6.0&#39;
            implementation &#39;com.tealium:kotlin-install-referrer:1.1.1&#39;
            // only required if you do not already have this reference and require lifecycle tracking
            implementation &#39;com.tealium:kotlin-lifecycle:1.2.0&#39;
            // Google&#39;s Install Referrer API
            implementation &#39;com.android.installreferrer:installreferrer:1.0&#39;
      }
      ```  
The [Google Install Referrer API](https://developer.android.com/google/play/installreferrer/library) is a dependency for this module, but is not automatically added for you. Add the module to your build.


### Manual

To install the Install Referrer module manually:

1. Download the Tealium [Install Referrer](https://github.com/Tealium/tealium-kotlin/tree/master/installreferrer) module.

2. In your top-level `build.gradle` file, verify the following:  
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

3. Copy the file `tealium-kotlin.installreferrer-1.1.1.aar` into your project&#39;s `&lt;PROJECT_ROOT&gt;/&lt;MODULE&gt;/libs` directory.

4. Add the Tealium library dependency to your project module’s `build.gradle` file:
      ```groovy
      dependencies {
            // only required if you do not already have this reference
            implementation(name:&#39;tealium-kotlin-1.6.0&#39;, ext:&#39;aar&#39;)
            implementation(name:&#39;tealium-kotlin.installreferrer-1.1.1&#39;, ext:&#39;aar&#39;)
            // only required if you do not already have this reference and require lifecycle tracking
            implementation(name:&#39;tealium-kotlin.lifecycle-1.2.0&#39;, ext:&#39;aar&#39;)
            // Google&#39;s Install Referrer API
            implementation &#39;com.android.installreferrer:installreferrer:1.0&#39;
      }
      ```

## Data Layer

Expect the following referral data as retrieved from the Google Play

```
&#34;install_referrer&#34; - the referrer URL of the install package
&#34;install_referrer_begin_timestamp&#34; - the timestamp, in seconds, of when the referral click happened
&#34;install_referrer_click_timestamp&#34; - the timestamp, in seconds, of when the installation began
```

## Additional Considerations

**Delete the Stored Referrer**  
To delete the stored install referrer string, call the `remove()` method on the Tealium data layer.
```kotlin
// remove one or all of the following keys from the data layer
tealium.dataLayer.remove(InstallReferrerConstants.KEY_INSTALL_REFERRER)
tealium.dataLayer.remove(InstallReferrerConstants.KEY_INSTALL_REFERRER_BEGIN_TIMESTAMP)
tealium.dataLayer.remove(InstallReferrerConstants.KEY_INSTALL_REFERRER_CLICK_TIMESTAMP)
```
