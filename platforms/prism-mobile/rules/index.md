---
title: Rules
description: Use the native rules engine in the Tealium Prism SDK to control when modules execute their functionality.
url: https://docs.tealium.com/platforms/prism-mobile/rules/
---
LoadRules provide a way to control when modules in the Tealium Prism SDK execute their operations. Use rules to define conditional logic that determines whether data collection, event dispatching, or other module operations should occur based on the current state of your application data.

## How it works

Rules control whether a module processes a given dispatch. Each rule is a logical expression that evaluates fields in the current dispatch payload. If the expression is false, the module skips that dispatch.

A rule consists of one or more conditions. A condition checks a specific variable against a value using an operator such as equals, contains, or greater than. Multiple conditions combine with AND, OR, or NOT logic.

Rules are evaluated per dispatch — each time an event is tracked, not at startup.

## Configure rules in the UI

Rules can be configured in your Tealium mobile profile.

1. Log in to your mobile profile and go to **Load Rules**.
1. Select **Add Rule**.
1. Define the conditions and logical operators for your rule.
1. Assign the rule to the relevant module.
1. Save and publish your changes.


Verify the exact UI steps with the SDK team before publishing this section.


## Advanced

Build rules in code when the conditions can&#39;t be expressed statically or need to be locked in. For example, you might construct a rule that checks available memory at launch and disables heavy analytics modules on low-memory devices, or hard-code a rule that always filters out internal test users regardless of what the remote settings specify.

### Programmatic configuration

#### Conditions

A `Condition` represents a single criterion that checks if data in your application meets specific requirements.



```kotlin
// Check if user type equals &#34;premium&#34;
val condition = Condition.equals(
    ignoreCase = false,
    variable = &#34;user_type&#34;,
    target = &#34;premium&#34;
)

// Check if purchase amount is greater than 100
val condition = Condition.isGreaterThan(
    orEqual = false,
    variable = JSONPath[&#34;order&#34;][&#34;amount&#34;],
    number = &#34;100&#34;
)
```


```swift
// Check if user type equals &#34;premium&#34;
let condition = Condition.equals(ignoreCase: false,
                                variable: &#34;user_type&#34;,
                                target: &#34;premium&#34;)

// Check if purchase amount is greater than 100
let condition = Condition.isGreaterThan(orEqual: false,
                                       variable: JSONPath[&#34;order&#34;][&#34;amount&#34;],
                                       number: &#34;100&#34;)
```



#### Rules

A `Rule` allows you to combine multiple conditions using logical operators:



```kotlin
// Simple rule with just one condition
val simpleRule = Rule.just(condition)

// AND rule - all results must be true
val andRule = Rule.and(listOf(rule1, rule2, rule3))

// OR rule - at least one result must be true
val orRule = Rule.or(listOf(rule1, rule2))

// NOT rule - negates the result
val notRule = Rule.not(anotherRule)
```


```swift
// Simple rule with just one condition
let simpleRule = Rule.just(condition)

// AND rule - all results must be true
let andRule = Rule.and([rule1, rule2, rule3])

// OR rule - at least one result must be true
let orRule = Rule.or([rule1, rule2])

// NOT rule - negates the result
let notRule = Rule.not(anotherRule)
```



#### Condition types

**Existence checks**

```swift
Condition.isDefined(variable: &#34;user_id&#34;)
Condition.isNotDefined(variable: &#34;guest_session&#34;)
Condition.isEmpty(variable: &#34;shopping_cart&#34;)
Condition.isNotEmpty(variable: &#34;user_preferences&#34;)
```

**Equality comparisons**

```swift
Condition.equals(ignoreCase: false, variable: &#34;status&#34;, target: &#34;active&#34;)
Condition.equals(ignoreCase: true, variable: &#34;country&#34;, target: &#34;USA&#34;)
Condition.doesNotEqual(ignoreCase: false, variable: &#34;user_type&#34;, target: &#34;guest&#34;)
```

**String operations**

```swift
Condition.contains(ignoreCase: false, variable: &#34;page_url&#34;, string: &#34;/checkout&#34;)
Condition.doesNotContain(ignoreCase: true, variable: &#34;user_agent&#34;, string: &#34;bot&#34;)
Condition.startsWith(ignoreCase: false, variable: &#34;event_name&#34;, prefix: &#34;purchase_&#34;)
Condition.endsWith(ignoreCase: false, variable: &#34;page_path&#34;, suffix: &#34;.html&#34;)
```

**Numeric comparisons**

```swift
Condition.isGreaterThan(orEqual: false, variable: &#34;order_total&#34;, number: &#34;100.00&#34;)
Condition.isGreaterThan(orEqual: true, variable: &#34;user_age&#34;, number: &#34;18&#34;)
Condition.isLessThan(orEqual: false, variable: &#34;cart_items&#34;, number: &#34;10&#34;)
Condition.isLessThan(orEqual: true, variable: &#34;session_duration&#34;, number: &#34;3600&#34;)
```

**Regular expressions**

```swift
Condition.regularExpression(variable: &#34;email&#34;, regex: &#34;^[A-Za-z0-9&#43;_.-]&#43;@(.&#43;)$&#34;)
```

#### Data access

For data at the root level of your payload, use simple string keys:

```swift
let condition = Condition.equals(ignoreCase: false,
                                variable: &#34;user_id&#34;,
                                target: &#34;12345&#34;)
```

For nested data structures, use `JSONPath` to navigate through objects and arrays:

```swift
// Accesses payload.user.profile.subscription.type
let path = JSONPath[&#34;user&#34;][&#34;profile&#34;][&#34;subscription&#34;][&#34;type&#34;]
let condition = Condition.equals(ignoreCase: false,
                                variable: path,
                                target: &#34;premium&#34;)

// Accesses payload.items[0].price
let arrayPath = JSONPath[&#34;items&#34;][0][&#34;price&#34;]
```

#### Complex rule compositions

Combine multiple conditions with nested logic:



```kotlin
// (Premium users OR VIP users) AND (not in maintenance mode)
val complexRule = Rule.and(listOf(
    Rule.or(listOf(
        Rule.just(Condition.equals(false, &#34;subscription&#34;, &#34;premium&#34;)),
        Rule.just(Condition.equals(false, &#34;vip_status&#34;, &#34;true&#34;))
    )),
    Rule.not(Rule.just(Condition.equals(false, &#34;maintenance_mode&#34;, &#34;true&#34;)))
))
```


```swift
// (Premium users OR VIP users) AND (not in maintenance mode)
let complexRule = Rule.and([
    .or([
        .just(Condition.equals(ignoreCase: false, variable: &#34;subscription&#34;, target: &#34;premium&#34;)),
        .just(Condition.equals(ignoreCase: false, variable: &#34;vip_status&#34;, target: &#34;true&#34;))
    ]),
    .not(.just(Condition.equals(ignoreCase: false, variable: &#34;maintenance_mode&#34;, target: &#34;true&#34;)))
])
```



### JSON configuration

Rules can be defined in SDK settings JSON for remote or local configuration:

```json
{
  &#34;load_rules&#34;: {
    &#34;premium_users&#34;: {
      &#34;id&#34;: &#34;premium_users&#34;,
      &#34;conditions&#34;: {
        &#34;operator&#34;: &#34;equals&#34;,
        &#34;variable&#34;: {&#34;key&#34;: &#34;user_type&#34;},
        &#34;filter&#34;: {&#34;value&#34;: &#34;premium&#34;}
      }
    }
  },
  &#34;modules&#34;: {
    &#34;analytics_collector&#34;: {
      &#34;enabled&#34;: true,
      &#34;rules&#34;: {
        &#34;operator&#34;: &#34;or&#34;,
        &#34;children&#34;: [&#34;premium_users&#34;, &#34;high_value_orders&#34;]
      }
    }
  }
}
```

## API reference

For detailed class and method signatures, see the API reference documentation:

* [Rules (Swift)](/tealium-prism-swift/Rules.html)
* [Rule (Swift)](/tealium-prism-swift/TealiumPrismCore/Enums/Rule.html)
* [Condition (Swift)](/tealium-prism-swift/TealiumPrismCore/Structs/Condition.html)
* [Rules (Kotlin)](/tealium-prism-kotlin/)
