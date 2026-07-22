---
title: In-App Purchase Module
description: The In-App Purchase module adds automatic tracking of in-app purchases to your app.
url: https://docs.tealium.com/platforms/android-kotlin/module-list/in-app-purchase/
--- 

## What is an in-app purchase?

An in-app purchase is additional content, services, or a subscription that you buy inside the app. Some examples of in-app purchases include:

* Upgrade to remove ads
* Game credits
* Virtual currency
* Extra game levels
* Unlock more features

Examples of purchases that are not considered in-app purchases include:

* Purchasing clothes or other items in an e-commerce app.
* Using Google Pay to complete a purchase.

## Install

Install the In-App Purchase module using Maven (Recommended) or manually.

### Maven

To install the module using Maven:

1. In your project's top-level `build.gradle` file, add the following Maven repository:
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
2. In your project module's `build.gradle` file, add the following Maven dependencies:
      ```groovy
      dependencies {
            implementation 'com.tealium:kotlin-core:1.6.0'
            implementation 'com.tealium:kotlin-inapp-purchase:1.0.2'
      }
      ```

Ensure you are using the latest version of kotlin-core.

### Manual

To install the In-App Purchase module manually:

1. Download the Tealium [In-App Purchase](https://github.com/Tealium/tealium-kotlin/tree/main/inapppurchase) module.

2. Copy the file `tealium-kotlin.inapppurchase-1.0.2.aar` into your project's `<PROJECT_ROOT>/<MODULE>/libs` directory.

3. Add the Tealium library dependency to your project module’s `build.gradle` file:
      ```groovy
      dependencies {
            implementation(name:'tealium-kotlin.inapppurchase-1.0.2', ext:'aar')
      }
      ```

## Initialize

Initialize the In-App Purchase module, as shown in the following example:

```kotlin
val config = TealiumConfig(application,
              "ACCOUNT",
              "PROFILE",
              ENVIRONMENT,
              modules = mutableSetOf(Modules.InAppPurchase),
              dispatchers = mutableSetOf(
                Dispatchers.Collect,
                Dispatchers.RemoteCommands)
)
```

## Data Layer

The In-App Purchase module sends the following attributes in the event:

| Variable                    | Description                                                         | Example |
|:----------------------------|:--------------------------------------------------------------------|:--|
| `purchase_order_id`         | The order ID of the purchase.                                       | "1234567890" |
| `purchase_timestamp`        | The timestamp of the purchase in ISO 8601 format.                   | "2022-01-17T14:42:28Z" |
| `purchase_quantity`         | The total number of items purchased.                                | "2" |
| `purchase_skus`             | An array of the product IDs purchased.                              | ["premium_upgrade", "sub"] |
| `purchase_state`            | 1 = Purchased, 2 = Pending, 0 = Unspecified (See [Android Developers: Purchase.PurchaseState](https://developer.android.com/reference/com/android/billingclient/api/Purchase.PurchaseState) to learn more about this attribute.) | "1" |
| `purchase_is_auto_renewing` | Set to `true` if the subscription will auto-renew.                  | true |
| `autotracked`               | Set to `true` to indicate that the event was tracked automatically. | true |
| `tealium_event`             | The name of the event.                                              | "in_app_purchase" |

