---
title: ルール
description: Tealium Prism SDK のネイティブルールエンジンを使用して、モジュールが機能を実行するタイミングを制御します。
url: https://docs.tealium.com/ja/platforms/prism-mobile/rules/
---
LoadRules を使用すると、Tealium Prism SDK のモジュールが処理を実行するタイミングを制御できます。ルールを使用して条件ロジックを定義し、アプリケーションデータの現在の状態に基づいて、データ収集、イベント送信、その他のモジュール処理を実行するかどうかを決定します。

## 仕組み

ルールは、モジュールが特定のディスパッチを処理するかどうかを制御します。各ルールは、現在のディスパッチペイロード内のフィールドを評価する論理式です。式が false の場合、モジュールはそのディスパッチをスキップします。

ルールは、1 つ以上の条件で構成されます。条件は、equals、contains、greater than などの演算子を使用して、特定の変数を値と比較します。複数の条件は、AND、OR、または NOT ロジックで組み合わせます。

ルールはディスパッチごと、つまり起動時ではなくイベントがトラッキングされるたびに評価されます。

## UI でルールを構成する

ルールは、Tealium モバイルプロファイルで構成できます。

1. モバイルプロファイルにログインし、**Load Rules** に移動します。
1. **Add Rule** を選択します。
1. ルールの条件と論理演算子を定義します。
1. ルールを該当するモジュールに割り当てます。
1. 変更を保存してパブリッシュします。

## 高度な構成

条件を静的に表現できない場合や、条件を固定する必要がある場合は、コードでルールを作成します。たとえば、起動時に使用可能なメモリを確認し、メモリの少ないデバイスでは負荷の高い分析モジュールを無効にするルールを作成できます。また、リモート構成の内容にかかわらず、社内テストユーザーを常に除外するルールをハードコードすることもできます。

### プログラムによる構成


<blockquote>
React Native では、プログラムによるルール構成を使用できません。Tealium モバイルプロファイルまたは構成 JSON でルールを構成してください。
</blockquote>


#### 条件

`Condition` は、アプリケーション内のデータが特定の要件を満たしているかどうかを確認する単一の基準を表します。



```kotlin
// Check if user type equals "premium"
val condition = Condition.isEqual(
    ignoreCase = false,
    variable = "user_type",
    target = "premium"
)

// Check if purchase amount is greater than 100
val amountCondition = Condition.isGreaterThan(
    orEqual = false,
    variable = JsonPath["order"]["amount"],
    number = "100"
)
```


```swift
// Check if user type equals "premium"
let condition = Condition.equals(ignoreCase: false,
                                variable: "user_type",
                                target: "premium")

// Check if purchase amount is greater than 100
let amountCondition = Condition.isGreaterThan(orEqual: false,
                                             variable: JSONPath["order"]["amount"],
                                             number: "100")
```



#### ルール

`Rule` を使用すると、論理演算子で複数の条件を組み合わせることができます。



```kotlin
// Simple rule with just one condition
val simpleRule = Rule.just(condition)

// AND rule - all results must be true
val andRule = Rule.all(listOf(rule1, rule2, rule3))

// OR rule - at least one result must be true
val orRule = Rule.any(listOf(rule1, rule2))

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



#### 条件の種類

**存在チェック**

```swift
Condition.isDefined(variable: "user_id")
Condition.isNotDefined(variable: "guest_session")
Condition.isEmpty(variable: "shopping_cart")
Condition.isNotEmpty(variable: "user_preferences")
```

**等価比較**

```swift
Condition.equals(ignoreCase: false, variable: "status", target: "active")
Condition.equals(ignoreCase: true, variable: "country", target: "USA")
Condition.doesNotEqual(ignoreCase: false, variable: "user_type", target: "guest")
```

**文字列操作**

```swift
Condition.contains(ignoreCase: false, variable: "page_url", string: "/checkout")
Condition.doesNotContain(ignoreCase: true, variable: "user_agent", string: "bot")
Condition.startsWith(ignoreCase: false, variable: "event_name", prefix: "purchase_")
Condition.endsWith(ignoreCase: false, variable: "page_path", suffix: ".html")
```

**数値比較**

```swift
Condition.isGreaterThan(orEqual: false, variable: "order_total", number: "100.00")
Condition.isGreaterThan(orEqual: true, variable: "user_age", number: "18")
Condition.isLessThan(orEqual: false, variable: "cart_items", number: "10")
Condition.isLessThan(orEqual: true, variable: "session_duration", number: "3600")
```

**正規表現**

```swift
Condition.regularExpression(variable: "email", regex: "^[A-Za-z0-9+_.-]+@(.+)$")
```

#### データへのアクセス

ペイロードのルートレベルにあるデータには、単純な文字列キーを使用します。

```swift
let condition = Condition.equals(ignoreCase: false,
                                variable: "user_id",
                                target: "12345")
```

ネストされたデータ構造では、`JSONPath` を使用してオブジェクトや配列内を移動します。

```swift
// Accesses payload.user.profile.subscription.type
let path = JSONPath["user"]["profile"]["subscription"]["type"]
let condition = Condition.equals(ignoreCase: false,
                                variable: path,
                                target: "premium")

// Accesses payload.items[0].price
let arrayPath = JSONPath["items"][0]["price"]
```

#### 複雑なルールの構成

ネストされたロジックを使用して、複数の条件を組み合わせます。



```kotlin
// (Premium users OR VIP users) AND (not in maintenance mode)
val complexRule = Rule.all(listOf(
    Rule.any(listOf(
        Rule.just(Condition.isEqual(false, "subscription", "premium")),
        Rule.just(Condition.isEqual(false, "vip_status", "true"))
    )),
    Rule.not(Rule.just(Condition.isEqual(false, "maintenance_mode", "true")))
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



### JSON 構成

リモート構成またはローカル構成用の SDK 構成 JSON でルールを定義できます。

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
    "DeviceData": {
      "module_type": "DeviceData",
      "enabled": true,
      "rules": {
        "operator": "or",
        "children": ["premium_users", "high_value_orders"]
      }
    }
  }
}
```

## API リファレンス

クラスとメソッドの詳細なシグネチャについては、API リファレンスドキュメントを参照してください。

* [ルール（Swift）](https://docs.tealium.com/tealium-prism-swift/Rules.html)
* [Rule（Swift）](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Enums/Rule.html)
* [Condition（Swift）](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Structs/Condition.html)
* [ルール（Kotlin）](https://docs.tealium.com/tealium-prism-kotlin/)