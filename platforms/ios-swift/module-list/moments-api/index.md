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

1. In your Xcode project, select **File &gt; Swift Packages &gt; Add Package Dependency**
1. Enter the repository URL: `https://github.com/tealium/tealium-swift`
1. Configure the version rules. Typically, `&#34;Up to next major&#34;` is recommended. If the current Tealium Swift library version does not appear in the list, reset your Swift package cache.
1. Select the `TealiumMomentsAPI`, `TealiumCore`, and either `TealiumCollect` or `TealiumTagManagement` modules from the list of modules to install and add them to each of your app targets in your Xcode project, under **Frameworks and Libraries**.

### CocoaPods

Add the following pods to your Podfile:  

```perl
pod &#39;tealium-swift/Core&#39;
pod &#39;tealium-swift/Collect&#39; // or &#39;tealium-swift/TagManagement&#39;
pod &#39;tealium-swift/MomentsAPI&#39;
```

### Carthage

1. Go to the app target&#39;s General configuration page in Xcode.
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

To initialize the module, ensure it&#39;s specified on the `TealiumConfig` `collectors` property.

```swift
config.collectors = [Collectors.MomentsAPI]
config.momentsAPIRegion = .us_east // See possible region options below
```

 Setting the region is mandatory. The Moments API module will not initialize if it&#39;s missing. 

### Fetch Visitor Data

Call the `fetchEngineResponse` method to retrieve personalized visitor data. This should be called whenever updated visitor information is needed, for example, to power in-app personalization use cases.

```swift
func fetchMoments(engineId: String, completion: @escaping (Result&lt;EngineResponse, Error&gt;) -&gt; Void) {
    tealium?.momentsAPI?.fetchEngineResponse(engineID: engineId) { engineResponse in
        switch engineResponse {
        case .success(let response):
            print(&#34;String attributes:&#34;, response.strings ?? [])
            print(&#34;Boolean attributes:&#34;, response.booleans ?? [])
            print(&#34;Audiences:&#34;, response.audiences ?? [])
            print(&#34;Date attributes:&#34;, response.dates ?? [:])
            print(&#34;Badges:&#34;, response.badges ?? [])
            print(&#34;Numbers:&#34;, response.numbers ?? [:])
        case .failure(let error):
            print(&#34;Error fetching moments:&#34;, error.localizedDescription)
            if let suggestion = (error as? LocalizedError)?.recoverySuggestion {
                print(&#34;Recovery suggestion:&#34;, suggestion)
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
| `.custom`    | `&lt;custom string&gt;` |

```swift
config.momentsAPIRegion = .us_east
```

 The custom option allows for future expansion and should not be used unless directed. 

### Referrer

For added security, you can specify a referrer URL. This URL must match the &#34;Domain Allow List&#34; in the Tealium UI, or the Moments API will not return any data. The default referrer URL is:

```
https://tags.tiqcdn.com/utag/{account}/{profile}/{environment}/mobile.html
```

Specify a custom referrer URL as shown below:

```swift
let config = TealiumConfig(
    account: &#34;tealiummobile&#34;,
    profile: &#34;demo&#34;,
    environment: &#34;prod&#34;
)
config.momentsAPIReferrer = &#34;https://example.com/&#34;
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
