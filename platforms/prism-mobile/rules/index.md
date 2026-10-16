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

## Advanced

Build rules in code when the conditions can't be expressed statically or need to be locked in. For example, you might construct a rule that checks available memory at launch and disables heavy analytics modules on low-memory devices, or hard-code a rule that always filters out internal test users regardless of what the remote settings specify.

### Programmatic configuration


<blockquote>
Programmatic rule configuration is not available in React Native. Configure rules in your Tealium mobile profile or settings JSON.
</blockquote>


#### Conditions

A `Condition` represents a single criterion that checks if data in your application meets specific requirements.



```kotlin
// Check if user type equals "premium"
val condition = Condition.equals(
    ignoreCase = false,
    variable = "user_type",
    target = "premium"
)

// Check if purchase amount is greater than 100
val condition = Condition.isGreaterThan(
    orEqual = false,
    variable = JSONPath["order"]["amount"],
    number = "100"
)
```


```swift
// Check if user type equals "premium"
let condition = Condition.equals(ignoreCase: false,
                                variable: "user_type",
                                target: "premium")

// Check if purchase amount is greater than 100
let condition = Condition.isGreaterThan(orEqual: false,
                                       variable: JSONPath["order"]["amount"],
                                       number: "100")
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
Condition.isDefined(variable: "user_id")
Condition.isNotDefined(variable: "guest_session")
Condition.isEmpty(variable: "shopping_cart")
Condition.isNotEmpty(variable: "user_preferences")
```

**Equality comparisons**

```swift
Condition.equals(ignoreCase: false, variable: "status", target: "active")
Condition.equals(ignoreCase: true, variable: "country", target: "USA")
Condition.doesNotEqual(ignoreCase: false, variable: "user_type", target: "guest")
```

**String operations**

```swift
Condition.contains(ignoreCase: false, variable: "page_url", string: "/checkout")
Condition.doesNotContain(ignoreCase: true, variable: "user_agent", string: "bot")
Condition.startsWith(ignoreCase: false, variable: "event_name", prefix: "purchase_")
Condition.endsWith(ignoreCase: false, variable: "page_path", suffix: ".html")
```

**Numeric comparisons**

```swift
Condition.isGreaterThan(orEqual: false, variable: "order_total", number: "100.00")
Condition.isGreaterThan(orEqual: true, variable: "user_age", number: "18")
Condition.isLessThan(orEqual: false, variable: "cart_items", number: "10")
Condition.isLessThan(orEqual: true, variable: "session_duration", number: "3600")
```

**Regular expressions**

```swift
Condition.regularExpression(variable: "email", regex: "^[A-Za-z0-9+_.-]+@(.+)$")
```

#### Data access

For data at the root level of your payload, use simple string keys:

```swift
let condition = Condition.equals(ignoreCase: false,
                                variable: "user_id",
                                target: "12345")
```

For nested data structures, use `JSONPath` to navigate through objects and arrays:

```swift
// Accesses payload.user.profile.subscription.type
let path = JSONPath["user"]["profile"]["subscription"]["type"]
let condition = Condition.equals(ignoreCase: false,
                                variable: path,
                                target: "premium")

// Accesses payload.items[0].price
let arrayPath = JSONPath["items"][0]["price"]
```

#### Complex rule compositions

Combine multiple conditions with nested logic:




```kotlin
// (Premium users OR VIP users) AND (not in maintenance mode)
val complexRule = Rule.and(listOf(
    Rule.or(listOf(
        Rule.just(Condition.equals(false, "subscription", "premium")),
        Rule.just(Condition.equals(false, "vip_status", "true"))
    )),
    Rule.not(Rule.just(Condition.equals(false, "maintenance_mode", "true")))
))
```


```swift
// (Premium users OR VIP users) AND (not in maintenance mode)
let complexRule = Rule.and([
    .or([
        .just(Condition.equals(ignoreCase: false, variable: "subscription", target: "premium")),
        .just(Condition.equals(ignoreCase: false, variable: "vip_status", target: "true"))
    ]),
    .not(.just(Condition.equals(ignoreCase: false, variable: "maintenance_mode", target: "true")))
])
```



### JSON configuration

Rules can be defined in SDK settings JSON for remote or local configuration:

```json
{
  "load_rules": {
    "premium_users": {
      "id": "premium_users",
      "conditions": {
        "operator": "equals",
        "variable": {"key": "user_type"},
        "filter": {"value": "premium"}
      }
    }
  },
  "modules": {
    "analytics_collector": {
      "enabled": true,
      "rules": {
        "operator": "or",
        "children": ["premium_users", "high_value_orders"]
      }
    }
  }
}
```

## API reference

For detailed class and method signatures, see the API reference documentation:

* [Rules (Swift)](https://docs.tealium.com/tealium-prism-swift/Rules.html)
* [Rule (Swift)](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Enums/Rule.html)
* [Condition (Swift)](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Structs/Condition.html)
* [Rules (Kotlin)](https://docs.tealium.com/tealium-prism-kotlin/)
