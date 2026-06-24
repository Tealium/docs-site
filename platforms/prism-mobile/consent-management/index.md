---
title: Consent
description: Implement consent management in the Tealium Prism SDK.
url: https://docs.tealium.com/platforms/prism-mobile/consent-management/
---
This page explains how to integrate your Consent Management Provider (CMP) with Prism.

## How it works

When you enable consent integration, the SDK intercepts each event before it reaches a dispatcher and processes it as follows:

1. An event is tracked and passed to the consent manager.
1. If a consent decision has not been received yet, the event is held in an internal queue.
1. When the CMP adapter emits a consent decision, the SDK retrieves the queued events and applies the consent purposes to each one.
1. The SDK checks whether the Tealium purpose ID (set by `setTealiumPurposeId`) is present in the decision. If it is not, the SDK drops all events for all dispatchers.
1. Each remaining event is evaluated against the dispatcher configuration. For each dispatcher, the SDK checks whether all required purposes for that dispatcher are present in the decision. Events that do not satisfy the required purposes for a dispatcher are dropped for that dispatcher.
1. Events that pass the purpose check are sent to the dispatcher.

### Implicit and explicit decisions

When the SDK receives an implicit decision, it dispatches events that match required purposes. These events are also retained for refire (send again) later.

When the SDK later receives an explicit decision, it refires retained events to dispatchers listed in dispatchers in the consent builder configuration. This captures data from events sent before explicit consent.

## Enable consent integration

Call `enableConsentIntegration()` on your `TealiumConfig` to connect your CMP adapter. Supply enforced consent configuration to map purpose IDs to dispatchers.



```kotlin
import com.tealium.prism.core.api.Tealium
import com.tealium.prism.core.api.TealiumConfig
import com.tealium.prism.core.api.modules.Modules

val config = TealiumConfig.Builder(
    accountName = &#34;my_account&#34;,
    profileName = &#34;my_profile&#34;,
    environment = Environment.PROD,
    modules = listOf(Modules.collect())
).enableConsentIntegration(cmpAdapter) { settings -&gt;
    settings
        .setTealiumPurposeId(&#34;tealium&#34;)
        .addPurpose(&#34;tracking&#34;, setOf(Modules.Types.COLLECT))
        .setRefireDispatcherIds(setOf(Modules.Types.COLLECT))
}.build()

val tealium = Tealium.create(config)
```


```swift
#if COCOAPODS
import TealiumPrism
#else
import TealiumPrismCore
#endif

var config = TealiumConfig(account: &#34;my_account&#34;,
                           profile: &#34;my_profile&#34;,
                           environment: &#34;prod&#34;,
                           modules: [Modules.collect()],
                           settingsUrl: &#34;https://tags.tiqcdn.com/dle/my_account/my_profile/settings.json&#34;)

config.enableConsentIntegration(with: cmpAdapter) { enforcedConfiguration in
    enforcedConfiguration
        .setTealiumPurposeId(&#34;tealium&#34;)
        .addPurpose(&#34;tracking&#34;, dispatcherIds: [Modules.Types.collect])
        .setRefireDispatcherIds([Modules.Types.collect])
}

let tealium = Tealium.create(config: config)
```



Event dispatch prerequisites:

* The CMP adapter returns a `ConsentDecision`.
* A consent configuration is found for that adapter.

If consent is not yet available, events queue until a decision is received.

## Implement the CMP adapter

Implement a CMP adapter to connect your CMP to the SDK. A CMP adapter uses the following properties:

| Property          | Type     | Description |
| :---------------- | :------- | :---------- |
| `id`              | `String` | Unique identifier for this adapter. Used to match against consent configuration. |
| `consentDecision` | `Observable&lt;ConsentDecision?&gt;` | Observable stream of consent decisions from the user. |
| `allPurposes`     | `Set&lt;String&gt;?` | All possible purposes from the CMP, if available. |

`allPurposes` is optional. The examples below use a non-null set for clarity.



```kotlin
import com.tealium.prism.core.api.consent.CmpAdapter
import com.tealium.prism.core.api.consent.ConsentDecision
import com.tealium.prism.core.api.pubsub.Observable
import com.tealium.prism.core.api.pubsub.Observables
import com.tealium.prism.core.api.pubsub.StateSubject

class MyCmpAdapter : CmpAdapter {

    private val _consentDecision: StateSubject&lt;ConsentDecision?&gt; =
        Observables.stateSubject(null)

    override val id: String = &#34;my_cmp&#34;

    override val consentDecision: Observable&lt;ConsentDecision?&gt;
        get() = _consentDecision.asObservableState()

    override val allPurposes: Set&lt;String&gt; = setOf(&#34;tealium&#34;, &#34;tracking&#34;, &#34;functional&#34;)

    fun updateConsent(decision: ConsentDecision) {
        _consentDecision.onNext(decision)
    }
}
```


```swift
#if COCOAPODS
import TealiumPrism
#else
import TealiumPrismCore
#endif

class MyCMPAdapter: CMPAdapter {

    let id = &#34;my_cmp&#34;

    @ReplaySubject&lt;ConsentDecision?&gt;(nil)
    var consentDecision

    let allPurposes: Set&lt;String&gt;? = [&#34;tealium&#34;, &#34;tracking&#34;, &#34;functional&#34;]

    func updateConsent(_ decision: ConsentDecision) {
        _consentDecision.publish(decision)
    }
}
```



## Consent decisions

A `ConsentDecision` represents the user&#39;s current consent state. It contains a decision type and the set of purpose IDs the user has consented to.



```kotlin
import com.tealium.prism.core.api.consent.ConsentDecision

// Implicit: derived from user behavior, such as app launch
val implicitDecision = ConsentDecision(
    decisionType = ConsentDecision.DecisionType.Implicit,
    purposes = setOf(&#34;tealium&#34;)
)

// Explicit: the user has actively accepted consent
val explicitDecision = ConsentDecision(
    decisionType = ConsentDecision.DecisionType.Explicit,
    purposes = setOf(&#34;tealium&#34;, &#34;tracking&#34;, &#34;functional&#34;)
)
```


```swift
// Implicit: derived from user behavior, such as app launch
let implicitDecision = ConsentDecision(
    decisionType: .implicit,
    purposes: [&#34;tealium&#34;]
)

// Explicit: the user has actively accepted consent
let explicitDecision = ConsentDecision(
    decisionType: .explicit,
    purposes: [&#34;tealium&#34;, &#34;tracking&#34;, &#34;functional&#34;]
)
```



| Decision type | Description |
| :------------ | :---------- |
| `Implicit` / `.implicit` | Derived from user behavior, such as opening the app. The SDK may queue events for refire when explicit consent is later given. |
| `Explicit` / `.explicit` | The user actively granted or denied consent. The SDK processes any previously queued events based on the updated purposes. |

## Configure purposes

Use `ConsentConfigurationBuilder` to map CMP purpose IDs to dispatchers and configure event refiring.

| Method | Description |
| :----- | :---------- |
| `setTealiumPurposeId(id)` | The purpose ID required to enable the Tealium SDK. If absent from the decision, events are dropped. |
| `addPurpose(purposeId, dispatcherIds)` | Maps a purpose to the dispatchers that require it. A dispatcher only fires if its required purpose is accepted. |
| `setRefireDispatcherIds(ids)` | Dispatchers that refire previously queued events when explicit consent is received. |



```kotlin
TealiumConfig.Builder(...)
    .enableConsentIntegration(cmpAdapter) { settings -&gt;
        settings
            .setTealiumPurposeId(&#34;tealium&#34;)
            .addPurpose(&#34;tracking&#34;, setOf(Modules.Types.COLLECT))
            .addPurpose(&#34;functional&#34;, setOf(&#34;logger&#34;))
            .setRefireDispatcherIds(setOf(Modules.Types.COLLECT))
    }
```


```swift
config.enableConsentIntegration(with: cmpAdapter) { enforcedConfiguration in
    enforcedConfiguration
        .setTealiumPurposeId(&#34;tealium&#34;)
        .addPurpose(&#34;tracking&#34;, dispatcherIds: [Modules.Types.collect])
        .addPurpose(&#34;functional&#34;, dispatcherIds: [&#34;logger&#34;])
        .setRefireDispatcherIds([Modules.Types.collect])
}
```



For more information, see the API reference:

* [Kotlin consent API reference](/tealium-prism-kotlin/core/com.tealium.prism.core.api.consent/)
* [Swift consent API reference](/tealium-prism-swift/Consent.html)
