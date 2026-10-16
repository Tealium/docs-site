---
title: Transformations
description: Modify, enrich, or filter dispatches in the Tealium Prism SDK using on-device event transformations.
url: https://docs.tealium.com/platforms/prism-mobile/transformations/
---
Transformations provide a way to modify, enrich, or filter dispatches before they are sent to dispatchers. Use transformations to implement custom business logic that transforms your data based on specific conditions and scopes.

## How it works

A transformation runs at a defined point in the dispatch pipeline and can modify, enrich, or drop an event before it reaches a dispatcher.

A transformation's scope determines when it runs:

* **After collectors**: Runs after data collection, before any dispatcher receives the event. Use this for enrichment that applies to all dispatchers.
* **All dispatchers**: Runs for every dispatcher.
* **Specific dispatcher**: Runs only for a named dispatcher. Use this for destination-specific filtering or data masking.

Each transformation can include conditions, so it only applies when specific data is present in the dispatch payload.

## Common transformation patterns

### Data enrichment

Add additional data to dispatches based on existing values. For example, add a user segment based on purchase amount.

### Data filtering

Remove sensitive or unwanted data from dispatches before they reach dispatchers. Configure a list of sensitive keys to strip from the payload.

### Conditional dispatch dropping

Drop dispatches based on specific conditions. Return `nil` (Swift) or `null` (Kotlin) from the `applyTransformation` method to drop a dispatch entirely. For example, drop test events in production.

### Scope-specific transformations

Apply different transformations at different pipeline stages. Use `afterCollectors` for enrichment that applies to all dispatchers, and `dispatcher(id:)` for filtering specific to a single destination.

## Configure transformations in the UI

Transformations are configured in your mobile profile as extensions. They work identically to tag management extensions, but include mobile-specific scopes.

To add an extension in the UI:

1. Log in to your mobile profile and go to **Extensions**.
1. Select **Add Extension** and choose an extension type.
1. Configure the extension and set its scope.
1. Save and publish your changes.

Mobile-specific scopes available in the UI:

| Scope | Description |
| :--- | :--- |
| After Collectors | Applied after data collection, before any dispatchers. |
| All Dispatchers | Applied to all dispatchers. |

## Advanced

Configure transformations programmatically when the logic depends on values only known at runtime or when you need to guarantee a transformation runs regardless of remote settings. For example, you might dynamically register a PII-stripping transformer scoped to a specific dispatcher based on a user's consent state, or lock in a data enrichment transformation during development to test behavior before publishing it to the platform.

### Programmatic configuration


<blockquote>
Programmatic transformation configuration is not available in React Native. Configure transformations in your Tealium mobile profile.
</blockquote>


Scope constants for reference:



```kotlin
TransformationScope.AFTER_COLLECTORS
TransformationScope.ALL_DISPATCHERS
TransformationScope.dispatcher("my_dispatcher")
```


```swift
TransformationScope.afterCollectors
TransformationScope.allDispatchers
TransformationScope.dispatcher(id: "my_dispatcher")
```



Example: configure a transformation in code:




```kotlin
val enrichmentTransformation = TransformationSettings(
    id = "user_enrichment",
    transformerId = "DataEnrichmentTransformer",
    scopes = listOf(TransformationScope.AFTER_COLLECTORS),
    configuration = mapOf(
        "enable_enrichment" to true,
        "enrichment_type" to "user_data"
    ),
    conditions = Rule.just(Condition.isDefined("user_id"))
)

config.setTransformation(enrichmentTransformation)
```


```swift
let enrichmentTransformation = TransformationSettings(
    id: "user_enrichment",
    transformerId: "DataEnrichmentTransformer",
    scopes: [.afterCollectors],
    configuration: [
        "enable_enrichment": true,
        "enrichment_type": "user_data",
        "source": "user_profile"
    ],
    conditions: .just(Condition.isDefined(variable: "user_id"))
)

config.setTransformation(enrichmentTransformation)
```



### JSON configuration

Transformations can also be defined in JSON format for remote or local configuration:

```json
{
  "transformation_id": "user_enrichment",
  "transformer_id": "MyCustomTransformer",
  "scopes": ["aftercollectors"],
  "configuration": {
    "enable_enrichment": true,
    "enrichment_type": "user_data",
    "source": "user_profile"
  },
  "conditions": {
    "operator": "defined",
    "variable": {"key": "user_id"}
  }
}
```

## Create a custom transformer

To create a custom transformer, implement the `Transformer` protocol:




```kotlin
class MyCustomTransformer : Transformer {
    override val id: String = "MyCustomTransformer"
    override val version: String = "1.0.0"

    override fun applyTransformation(
        transformation: TransformationSettings,
        dispatch: Dispatch,
        scope: DispatchScope,
        completion: (Dispatch?) -> Unit
    ) {
        val enableEnrichment: Boolean =
            transformation.configuration.get("enable_enrichment") ?: true

        val modifiedDispatch = dispatch.toMutableDispatch()

        if (enableEnrichment) {
            modifiedDispatch.enrich(mapOf("transformed" to "true"))
        }

        // Return the modified dispatch
        completion(modifiedDispatch)

        // Or return null to drop the dispatch entirely
        // completion(null)
    }
}
```


```swift
class MyCustomTransformer: Transformer {
    static let moduleType = "MyCustomTransformer"
    var id: String { Self.moduleType }
    let version: String = "1.0.0"

    func applyTransformation(_ transformation: TransformationSettings,
                           to dispatch: Dispatch,
                           scope: DispatchScope,
                           completion: @escaping (Dispatch?) -> Void) {
        let enableEnrichment: Bool =
            transformation.configuration.get(key: "enable_enrichment") ?? true

        var modifiedDispatch = dispatch

        if enableEnrichment {
            modifiedDispatch.enrich(data: ["transformed": "true"])
        }

        // Return the modified dispatch
        completion(modifiedDispatch)

        // Or return nil to drop the dispatch entirely
        // completion(nil)
    }
}
```


