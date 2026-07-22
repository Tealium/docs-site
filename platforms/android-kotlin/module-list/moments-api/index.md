---
title: Moments API Module
description: Fetches visitor data using the Moments API.
url: https://docs.tealium.com/platforms/android-kotlin/module-list/moments-api/
---
The Moments API module enables you to retrieve detailed information about visitor profiles from Tealium AudienceStream. This information can be used to enhance the customer experience in your app by accessing various attributes such as audiences, badges, strings, booleans, dates, and numbers.

## Supported Platforms

The following platforms support the Moments API module:

- Android (Kotlin)

## Install

Install the Moments API module using Maven.

### Maven

To install the module using Maven:

1. In your project's top-level `build.gradle` file, add the following Maven repository:
   ```groovy
   maven {
       url "https://maven.tealiumiq.com/android/releases/"
   }
   ```

2. In your project module's `build.gradle` file, add the Maven dependencies for the Tealium library and Moments API Module:
   ```groovy
   dependencies {
       implementation 'com.tealium:kotlin-core:1.6.0'
       implementation 'com.tealium:kotlin-momentsapi:1.0.0'
   }
   ```

## Usage

### Initialize

Initialize the Tealium instance with the Moments API module included in the configuration, as follows:

```kotlin
val config = TealiumConfig(
    application,
    "tealiummobile",
    "demo",
    Environment.DEV,
    modules = mutableSetOf(
        Modules.Lifecycle,
        Modules.VisitorService,
        Modules.MomentsApi
    ),
    dispatchers = mutableSetOf(
        Dispatchers.Collect,
        Dispatchers.TagManagement,
        Dispatchers.RemoteCommands
    )
).apply {
    momentsApiRegion = MomentsApiRegion.UsEast // See possible region options below
    // momentsApiRegion = MomentsApiRegion.Custom("myRegion")
}

Tealium.create("your_instance_name", config)
```


<blockquote>
Setting the region is mandatory. The Moments API module will not initialize if it's missing.
</blockquote>


### Fetch Visitor Data

Use the `fetchEngineResponse` method to retrieve the visitor profile information. This method accepts an engine ID and a response listener to handle the API response.

```kotlin
fun fetchMoments(engineId: String, responseListener: ResponseListener<EngineResponse>) {
    val tealiumInstance = Tealium["your_instance_name"]
    tealiumInstance?.momentsApi?.fetchEngineResponse(engineId, responseListener)
}
```

### Example: Fetch and Handle Moments API Data

```kotlin
fun fetchMoments(engineId: String) {
    val tealiumInstance = Tealium["your_instance_name"]
    tealiumInstance?.momentsApi?.fetchEngineResponse(engineId, object : ResponseListener<EngineResponse> {
        override fun success(data: EngineResponse) {
            Log.d("MomentsAPI", "String attributes: ${data.strings}")
            Log.d("MomentsAPI", "Boolean attributes: ${data.booleans}")
            Log.d("MomentsAPI", "Audiences: ${data.audiences}")
            Log.d("MomentsAPI", "Date attributes: ${data.dates}")
            Log.d("MomentsAPI", "Badges: ${data.badges}")
            Log.d("MomentsAPI", "Numbers: ${data.numbers}")
        }

        override fun failure(errorCode: ErrorCode, message: String) {
            Log.e("MomentsAPI", "Error fetching moments: $errorCode - $message")
        }
    })
}
```

## Visitor Profile Data

The `EngineResponse` object contains various types of attributes returned by the Moments API. The following table shows the available properties and their data types:

| Property   | Data Type             | Description                                                     |
|------------|-----------------------|-----------------------------------------------------------------|
| `audiences`| List<String>          | The list of audiences the visitor is currently assigned to.     |
| `badges`   | List<String>          | The list of badges assigned to the visitor.                     |
| `booleans` | Map<String, Boolean>  | The boolean attributes currently assigned to the visitor.       |
| `dates`    | Map<String, Long>     | The date attributes currently assigned to the visitor (in ms).  |
| `numbers`  | Map<String, Double>   | The number attributes currently assigned to the visitor.        |
| `strings`  | Map<String, String>   | The string attributes currently assigned to the visitor.        |

## Configuration Options

### Region

Configure the Moments API region according to where your AudienceStream profile resides. If uncertain, consult your account manager.

| Enum Case    | Raw Value         |
|--------------|-------------------|
| `MomentsApiRegion.Germany`   | `eu-central-1`    |
| `MomentsApiRegion.UsEast`   | `us-east-1`       |
| `MomentsApiRegion.Sydney`    | `ap-southeast-2`  |
| `MomentsApiRegion.Oregon`    | `us-west-2`       |
| `MomentsApiRegion.Tokyo`     | `ap-northeast-1`  |
| `MomentsApiRegion.HongKong` | `ap-east-1`       |
| `MomentsApiRegion.Custom`    | `<custom string>` |

```kotlin
config.momentsApiRegion = MomentsApiRegion.UsEast
```


<blockquote>
The custom option allows for future expansion and should not be used unless directed.
</blockquote>


```kotlin
config.momentsApiRegion = MomentsApiRegion.Custom("custom_region_placeholder")
```

### Referrer

For added security, you can specify a referrer URL. This URL must match the "Domain Allow List" in the Tealium UI, or the Moments API will not return any data. The default referrer URL is:

```
https://tags.tiqcdn.com/utag/<account>/<profile>/<environment>/mobile.html
```

If the provided referrer is not in the allow list, Moments API will not return any data.

```kotlin
config.momentsApiReferrer = "https://yourcustomreferrer.com"
```

## Troubleshooting

### Common Errors

You may encounter errors when requesting data from the Moments API. The following table shows the errors that could occur:

| Error               | Description                                                                                       | Resolution                                                                    |
|--------------------------|---------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------|
| `BAD_REQUEST`            | The request was not properly formatted or contained invalid parameters.                           | Unlikely to occur when using the Moments API module.                         |
| `ENGINE_NOT_ENABLED`     | The Moments API engine is not enabled for your account or the request is not authorized.          | Ensure the Moments API engine is properly configured and enabled.             |
| `VISITOR_NOT_FOUND`      | The Tealium visitor ID does not have moments stored in the database.                              | No data exists yet for this visitor.                                          |
| `UNKNOWN_ERROR`          | The server responded with an unexpected status code.                                              | Consult the documentation or contact support for further assistance.          |
| `NOT_CONNECTED`          | A network error occurred while trying to communicate with the Moments API.                        | Check your network connection and retry.                                      |
| `INVALID_JSON`           | The data returned by the Moments API could not be decoded.                                        | Contact support. The response contained an unexpected data type.              |
