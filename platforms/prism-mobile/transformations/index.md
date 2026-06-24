---
title: Transformations
description: Modify, enrich, or filter dispatches in the Tealium Prism SDK using on-device event transformations.
url: https://docs.tealium.com/platforms/prism-mobile/transformations/
---
Transformations provide a way to modify, enrich, or filter dispatches before they are sent to dispatchers. Use transformations to implement custom business logic that transforms your data based on specific conditions and scopes.

## How it works

A transformation runs at a defined point in the dispatch pipeline and can modify, enrich, or drop an event before it reaches a dispatcher.

A transformation&#39;s scope determines when it runs:

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

Configure transformations programmatically when the logic depends on values only known at runtime or when you need to guarantee a transformation runs regardless of remote settings. For example, you might dynamically register a PII-stripping transformer scoped to a specific dispatcher based on a user&#39;s consent state, or lock in a data enrichment transformation during development to test behavior before publishing it to the platform.

### Programmatic configuration

Scope constants for reference:



```kotlin
TransformationScope.AFTER_COLLECTORS
TransformationScope.ALL_DISPATCHERS
TransformationScope.dispatcher(&#34;my_dispatcher&#34;)
```


```swift
TransformationScope.afterCollectors
TransformationScope.allDispatchers
TransformationScope.dispatcher(id: &#34;my_dispatcher&#34;)
```



Example: configure a transformation in code:



```kotlin
val enrichmentTransformation = TransformationSettings(
    id = &#34;user_enrichment&#34;,
    transformerId = &#34;DataEnrichmentTransformer&#34;,
    scopes = listOf(TransformationScope.AFTER_COLLECTORS),
    configuration = mapOf(
        &#34;enable_enrichment&#34; to true,
        &#34;enrichment_type&#34; to &#34;user_data&#34;
    ),
    conditions = Rule.just(Condition.isDefined(&#34;user_id&#34;))
)

config.setTransformation(enrichmentTransformation)
```


```swift
let enrichmentTransformation = TransformationSettings(
    id: &#34;user_enrichment&#34;,
    transformerId: &#34;DataEnrichmentTransformer&#34;,
    scopes: [.afterCollectors],
    configuration: [
        &#34;enable_enrichment&#34;: true,
        &#34;enrichment_type&#34;: &#34;user_data&#34;,
        &#34;source&#34;: &#34;user_profile&#34;
    ],
    conditions: .just(Condition.isDefined(variable: &#34;user_id&#34;))
)

config.setTransformation(enrichmentTransformation)
```



### JSON configuration

Transformations can also be defined in JSON format for remote or local configuration:

```json
{
  &#34;transformation_id&#34;: &#34;user_enrichment&#34;,
  &#34;transformer_id&#34;: &#34;MyCustomTransformer&#34;,
  &#34;scopes&#34;: [&#34;aftercollectors&#34;],
  &#34;configuration&#34;: {
    &#34;enable_enrichment&#34;: true,
    &#34;enrichment_type&#34;: &#34;user_data&#34;,
    &#34;source&#34;: &#34;user_profile&#34;
  },
  &#34;conditions&#34;: {
    &#34;operator&#34;: &#34;defined&#34;,
    &#34;variable&#34;: {&#34;key&#34;: &#34;user_id&#34;}
  }
}
```

## Create a custom transformer

To create a custom transformer, implement the `Transformer` protocol:



```kotlin
class MyCustomTransformer : Transformer {
    override val id: String = &#34;MyCustomTransformer&#34;
    override val version: String = &#34;1.0.0&#34;

    override fun applyTransformation(
        transformation: TransformationSettings,
        dispatch: Dispatch,
        scope: DispatchScope,
        completion: (Dispatch?) -&gt; Unit
    ) {
        val enableEnrichment: Boolean =
            transformation.configuration.get(&#34;enable_enrichment&#34;) ?: true

        val modifiedDispatch = dispatch.toMutableDispatch()

        if (enableEnrichment) {
            modifiedDispatch.enrich(mapOf(&#34;transformed&#34; to &#34;true&#34;))
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
    static let moduleType = &#34;MyCustomTransformer&#34;
    var id: String { Self.moduleType }
    let version: String = &#34;1.0.0&#34;

    func applyTransformation(_ transformation: TransformationSettings,
                           to dispatch: Dispatch,
                           scope: DispatchScope,
                           completion: @escaping (Dispatch?) -&gt; Void) {
        let enableEnrichment: Bool =
            transformation.configuration.get(key: &#34;enable_enrichment&#34;) ?? true

        var modifiedDispatch = dispatch

        if enableEnrichment {
            modifiedDispatch.enrich(data: [&#34;transformed&#34;: &#34;true&#34;])
        }

        // Return the modified dispatch
        completion(modifiedDispatch)

        // Or return nil to drop the dispatch entirely
        // completion(nil)
    }
}
```


