---
title: Moments API Module
description: Fetches visitor data using the Moments API.
url: https://docs.tealium.com/platforms/ios-swift/module-list/moments-api/
---
The Moments API module enables you to retrieve detailed information about visitor profiles from the Tealium AudienceStream. This information can be used to enhance the customer experience in your app by accessing various attributes such as audiences, badges, strings, booleans, dates, and numbers.

## Supported Platforms

The following platforms support the Moments API module:

- iOS
- macOS
- tvOS
- watchOS

## Install

Install the Moments API module using Swift Package Manager, CocoaPods, or Carthage.

### Swift Package Manager (Recommended)

1. In your Xcode project, select **File > Swift Packages > Add Package Dependency**
1. Enter the repository URL: `https://github.com/tealium/tealium-swift`
1. Configure the version rules. Typically, `"Up to next major"` is recommended. If the current Tealium Swift library version does not appear in the list, reset your Swift package cache.
1. Select the `TealiumMomentsAPI`, `TealiumCore`, and either `TealiumCollect` or `TealiumTagManagement` modules from the list of modules to install and add them to each of your app targets in your Xcode project, under **Frameworks and Libraries**.

### CocoaPods

Add the following pods to your Podfile:  

```perl
pod 'tealium-swift/Core'
pod 'tealium-swift/Collect' // or 'tealium-swift/TagManagement'
pod 'tealium-swift/MomentsAPI'
```

### Carthage

1. Go to the app target's General configuration page in Xcode.
2. Add the following framework to the **Embedded Binaries** section:  

   ```
   TealiumMomentsAPI.xcframework
   ```

3. Add the required import statements to your project:  

   ```swift
   import TealiumCore
   import TealiumCollect // or import TealiumTagManagement
   import TealiumMomentsAPI
   ```

## Usage

### Initialize

To initialize the module, ensure it's specified on the `TealiumConfig` `collectors` property.

```swift
config.collectors = [Collectors.MomentsAPI]
config.momentsAPIRegion = .us_east // See possible region options below
```


<blockquote>
Setting the region is mandatory. The Moments API module will not initialize if it's missing.
</blockquote>


### Fetch Visitor Data

Call the `fetchEngineResponse` method to retrieve personalized visitor data. This should be called whenever updated visitor information is needed, for example, to power in-app personalization use cases.

```swift
func fetchMoments(engineId: String, completion: @escaping (Result<EngineResponse, Error>) -> Void) {
    tealium?.momentsAPI?.fetchEngineResponse(engineID: engineId) { engineResponse in
        switch engineResponse {
        case .success(let response):
            print("String attributes:", response.strings ?? [])
            print("Boolean attributes:", response.booleans ?? [])
            print("Audiences:", response.audiences ?? [])
            print("Date attributes:", response.dates ?? [:])
            print("Badges:", response.badges ?? [])
            print("Numbers:", response.numbers ?? [:])
        case .failure(let error):
            print("Error fetching moments:", error.localizedDescription)
            if let suggestion = (error as? LocalizedError)?.recoverySuggestion {
                print("Recovery suggestion:", suggestion)
            }
        }
        completion(engineResponse)
    }
}
```

## Visitor Profile Data

The `EngineResponse` object contains various types of attributes returned by the Moments API. The following table shows the available properties and their data types:

| Property   | Data Type             | Description                                                     |
|------------|-----------------------|-----------------------------------------------------------------|
| `audiences`| `[String]`          | The list of audiences the visitor is currently assigned to.     |
| `badges`   | `[String]`          | The list of badges assigned to the visitor.                     |
| `booleans` | `[String: Bool]`  | The boolean attributes currently assigned to the visitor.       |
| `dates`    | `[String: Int64]`     | The date attributes currently assigned to the visitor (in ms).  |
| `numbers`  | `[String: Double]`   | The number attributes currently assigned to the visitor.        |
| `strings`  | `[String: String]`  | The string attributes currently assigned to the visitor.        |

## Configuration Options

### Region

Configure the Moments API region according to where your AudienceStream profile resides. If uncertain, consult your account manager.

| Enum Case    | Raw Value         |
|--------------|-------------------|
| `.germany`   | `eu-central-1`    |
| `.us_east`   | `us-east-1`       |
| `.sydney`    | `ap-southeast-2`  |
| `.oregon`    | `us-west-2`       |
| `.tokyo`     | `ap-northeast-1`  |
| `.hong_kong` | `ap-east-1`       |
| `.custom`    | `<custom string>` |

```swift
config.momentsAPIRegion = .us_east
```


<blockquote>
The custom option allows for future expansion and should not be used unless directed.
</blockquote>


### Referrer

For added security, you can specify a referrer URL. This URL must match the "Domain Allow List" in the Tealium UI, or the Moments API will not return any data. The default referrer URL is:

```
https://tags.tiqcdn.com/utag/{account}/{profile}/{environment}/mobile.html
```

Specify a custom referrer URL as shown below:

```swift
let config = TealiumConfig(
    account: "tealiummobile",
    profile: "demo",
    environment: "prod"
)
config.momentsAPIReferrer = "https://example.com/"
tealium = Tealium(config: config) { _ in
    // Initialization complete
}
```

## Troubleshooting

### Common Errors

You may encounter errors when requesting data from the Moments API. The following table shows the errors that could occur:

| Error                        | Description                                                                                       | Resolution                                                                    |
|----------------------------------|---------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------|
| `.badRequest`                    | The request was not properly formatted or contained invalid parameters.                           | Unliklely to occur when using the Moments API module.                         |
| `.forbidden`                     | The Moments API engine is not enabled for your account or the request is not authorized.          | Ensure the Moments API engine is properly configured and enabled.             |
| `.notFound`                      | The Tealium visitor ID does not have moments stored in the database.                              | No data exists yet for this visitor.                                          |
| `.unsuccessful(statusCode: Int)` | The server responded with an unexpected status code.                                              | Consult the documentation or contact support for further assistance.          |
| `.missingVisitorID`              | The visitor ID was not provided in the request.                                                   | Unliklely to occur when using the Moments API module.                         |
| `URLError`                       | A network error occurred while trying to communicate with the Moments API.                        | Check your network connection and retry.                                      |
| `URLError(.cannotDecodeRawData)` | The data returned by the Moments API could not be decoded.                                        | Contact support. The response contained an unexpected data type.              |
