---
title: Install
description: Learn to install Tealium for C#.
url: https://docs.tealium.com/platforms/csharp/install/
---## Requirements

* [Tealium Customer Data Hub account](https://docs.tealium.com/introduction-to-customer-data-hub/)
* Visual Studio or other C# compliant IDE

## Sample App

To help to familiarize yourself with the Tealium library, the tracking methods, and best practice implementation, explore the Tealium for C# [sample app](https://github.com/Tealium/tealium-c-sharp/tree/master/tealiumcsharp/Sample).

## Install

To install the Tealium library for C#:

1. Download the code for the [Tealium C# Library](https://github.com/Tealium/tealium-c-sharp).

2. Import the `TealiumCSharp` folder into your solution:

      ```csharp
      using TealiumCSharp;
      ```

## Initialize

To initialize Tealium:  

1. Create instance of the `Config` class with the [`Config()`](https://docs.tealium.com/platforms/csharp/api/#config) constructor method, as shown in the following example:

      ```csharp
      Config config = new Config(
                  "ACCOUNT",
                        "PROFILE",
                        "ENVIRONMENT",
                        "VISITOR_ID",
                        new string[] {
                                    AppDataModule.Name,
                                    CollectModule.Name,
                                    LoggerModule.Name
                        },
                        null,
                        null);
      ```

2. Create an instance of the `Tealium` class with the [`Tealium()`](https://docs.tealium.com/platforms/csharp/api/#tealium) constructor method, passing the `Config` instance as an argument, as shown in the following example:

      ```csharp
      Tealium tealium = new Tealium(config);
      ```

## Xamarin Mobile Applications

If you are building a mobile application in Xamarin then make use of the [Xamarin integration](https://docs.tealium.com/platforms/xamarin/) which has prebuilt bindings to our [iOS](https://docs.tealium.com/platforms/ios-swift/) and [Android](https://docs.tealium.com/platforms/android-java/) SDKs.
