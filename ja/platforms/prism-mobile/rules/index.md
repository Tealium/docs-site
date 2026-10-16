---
title: ルール
description: Tealium Prism SDKのネイティブルールエンジンを使用して、モジュールが機能を実行するタイミングを制御します。
url: https://docs.tealium.com/ja/platforms/prism-mobile/rules/
---
LoadRulesは、Tealium Prism SDKのモジュールが操作を実行するタイミングを制御する方法を提供します。ルールを使用して条件ロジックを定義し、アプリケーションデータの現在の状態に基づいてデータ収集、イベントディスパッチ、またはその他のモジュール操作が発生するかどうかを決定します。

## 動作原理

ルールは、モジュールが特定のディスパッチを処理するかどうかを制御します。各ルールは、現在のディスパッチペイロードのフィールドを評価する論理式です。式が偽の場合、モジュールはそのディスパッチをスキップします。

ルールは1つ以上の条件で構成されます。条件は、等しい、含む、またはより大きいなどの演算子を使用して特定の変数を値と比較します。複数の条件はAND、OR、またはNOTロジックで組み合わせられます。

ルールはディスパッチごとに評価されます。イベントが追跡されるたびに評価され、起動時には評価されません。

## UIでのルール構成

ルールはTealiumモバイルプロファイルで構成できます。

1. モバイルプロファイルにログインし、**Load Rules**に移動します。
1. **Add Rule**を選択します。
1. ルールの条件と論理演算子を定義します。
1. ルールを関連するモジュールに割り当てます。
1. 変更を保存して公開します。

## 高度な構成

条件が静的に表現できない場合やロックが必要な場合は、コードでルールを構築します。たとえば、起動時に利用可能なメモリをチェックし、メモリが少ないデバイスで重い分析モジュールを無効にするルールを構築するか、リモート構成に関係なく内部テストユーザーを常にフィルタリングするルールをハードコードすることができます。

### プログラムによる構成


<blockquote>
プログラムによるルール構成はReact Nativeでは利用できません。ルールはTealiumモバイルプロファイルまたは構成JSONで構成してください。
</blockquote>


#### 条件

`Condition`は、アプリケーションのデータが特定の要件を満たしているかどうかをチェックする単一の基準を表します。



```kotlin
// ユーザータイプが「プレミアム」であるかチェック
val condition = Condition.equals(
    ignoreCase = false,
    variable = "user_type",
    target = "premium"
)

// 購入金額が100より大きいかチェック
val condition = Condition.isGreaterThan(
    orEqual = false,
    variable = JSONPath["order"]["amount"],
    number = "100"
)
```


```swift
// ユーザータイプが「プレミアム」であるかチェック
let condition = Condition.equals(ignoreCase = false,
                                variable = "user_type",
                                target = "premium")

// 購入金額が100より大きいかチェック
let condition = Condition.isGreaterThan(orEqual = false,
                                       variable = JSONPath["order"]["amount"],
                                       number = "100")
```



#### ルール

`Rule`を使用すると、複数の条件を論理演算子を使用して組み合わせることができます：



```kotlin
// 条件が1つだけのシンプルなルール
val simpleRule = Rule.just(condition)

// ANDルール - すべての結果が真である必要がある
val andRule = Rule.and(listOf(rule1, rule2, rule3))

// ORルール - 少なくとも1つの結果が真である必要がある
val orRule = Rule.or(listOf(rule1, rule2))

// NOTルール - 結果を否定する
val notRule = Rule.not(anotherRule)
```


```swift
// 条件が1つだけのシンプルなルール
let simpleRule = Rule.just(condition)

// ANDルール - すべての結果が真である必要がある
let andRule = Rule.and([rule1, rule2, rule3])

// ORルール - 少なくとも1つの結果が真である必要がある
let orRule = Rule.or([rule1, rule2])

// NOTルール - 結果を否定する
let notRule = Rule.not(anotherRule)
```



#### 条件タイプ

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

#### データアクセス

ペイロードのルートレベルのデータには、単純な文字列キーを使用します：

```swift
let condition = Condition.equals(ignoreCase: false,
                                variable: "user_id",
                                target: "12345")
```

ネストされたデータ構造にアクセスするには、オブジェクトや配列をナビゲートするために`JSONPath`を使用します：

```swift
// payload.user.profile.subscription.typeにアクセス
let path = JSONPath["user"]["profile"]["subscription"]["type"]
let condition = Condition.equals(ignoreCase: false,
                                variable: path,
                                target: "premium")

// payload.items[0].priceにアクセス
let arrayPath = JSONPath["items"][0]["price"]
```

#### 複雑なルール構成

複数の条件をネストされたロジックで組み合わせます：



```kotlin
// (プレミアムユーザーまたはVIPユーザー) AND (メンテナンスモードではない)
val complexRule = Rule.and(listOf(
    Rule.or(listOf(
        Rule.just(Condition.equals(false, "subscription", "premium")),
        Rule.just(Condition.equals(false, "vip_status", "true"))
    )),
    Rule.not(Rule.just(Condition.equals(false, "maintenance_mode", "true")))
))
```


```swift
// (プレミアムユーザーまたはVIPユーザー) AND (メンテナンスモードではない)
let complexRule = Rule.and([
    .or([
        .just(Condition.equals(ignoreCase: false, variable: "subscription", target: "premium")),
        .just(Condition.equals(ignoreCase: false, variable: "vip_status", target: "true"))
    ]),
    .not(.just(Condition.equals(ignoreCase: false, variable: "maintenance_mode", target: "true")))
])
```



### JSON構成

SDK構成JSONでリモートまたはローカル構成のためにルールを定義できます：

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

## APIリファレンス

詳細なクラスとメソッドの署名については、APIリファレンスドキュメントを参照してください：

* [Rules (Swift)](https://docs.tealium.com/tealium-prism-swift/Rules.html)
* [Rule (Swift)](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Enums/Rule.html)
* [Condition (Swift)](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Structs/Condition.html)
* [Rules (Kotlin)](https://docs.tealium.com/tealium-prism-kotlin/)