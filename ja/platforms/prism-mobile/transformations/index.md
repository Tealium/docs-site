---
title: 変換
description: Tealium Prism SDKでデバイス上のイベント変換を使用してディスパッチを変更、エンリッチメント、またはフィルタリングします。
url: https://docs.tealium.com/ja/platforms/prism-mobile/transformations/
---
変換は、ディスパッチャーに送信される前にディスパッチを変更、エンリッチメント、またはフィルタリングする方法を提供します。特定の条件とスコープに基づいてデータを変換するカスタムビジネスロジックを実装するために変換を使用します。

## 動作方法

変換はディスパッチパイプラインの定義されたポイントで実行され、ディスパッチャーに到達する前にイベントを変更、エンリッチメント、またはドロップすることができます。

変換のスコープは、それがいつ実行されるかを決定します：

* **コレクターの後**：データ収集の後、どのディスパッチャーがイベントを受け取る前に実行します。すべてのディスパッチャーに適用されるエンリッチメントにこれを使用します。
* **すべてのディスパッチャー**：すべてのディスパッチャーで実行します。
* **特定のディスパッチャー**：名前付きのディスパッチャーのみで実行します。目的地固有のフィルタリングやデータマスキングにこれを使用します。

各変換には条件を含めることができるため、ディスパッチペイロードに特定のデータが存在する場合にのみ適用されます。

## 一般的な変換パターン

### データエンリッチメント

既存の値に基づいてディスパッチに追加データを追加します。例えば、購入額に基づいてユーザーセグメントを追加します。

### データフィルタリング

ディスパッチャーに到達する前にディスパッチから機密または不要なデータを削除します。ペイロードから削除する機密キーのリストを構成します。

### 条件付きディスパッチドロッピング

特定の条件に基づいてディスパッチをドロップします。`applyTransformation`メソッドから`nil`（Swift）または`null`（Kotlin）を返して、ディスパッチを完全にドロップします。例えば、本番環境でテストイベントをドロップします。

### スコープ固有の変換

異なるパイプラインステージで異なる変換を適用します。すべてのディスパッチャーに適用されるエンリッチメントに`afterCollectors`を使用し、単一の目的地に固有のフィルタリングに`dispatcher(id:)`を使用します。

## UIでの変換の構成

変換はモバイルプロファイル内の拡張機能として構成され、タグ管理拡張機能と同様に機能しますが、モバイル固有のスコープが含まれます。

UIで拡張機能を追加するには：

1. モバイルプロファイルにログインして**拡張機能**に移動します。
1. **拡張機能を追加**を選択し、拡張機能タイプを選択します。
1. 拡張機能を構成し、そのスコープを構成します。
1. 変更を保存して公開します。

UIで利用可能なモバイル固有のスコープ：

| スコープ | 説明 |
| :--- | :--- |
| コレクターの後 | データ収集後、どのディスパッチャーにも適用される前に適用されます。 |
| すべてのディスパッチャー | すべてのディスパッチャーに適用されます。 |

## 上級

ロジックがランタイムでのみ知られている値に依存する場合や、リモート構成に関係なく変換が実行されることを保証する必要がある場合に、プログラムで変換を構成します。例えば、ユーザーの同意状態に基づいて特定のディスパッチャーにスコープされたPII削除トランスフォーマーを動的に登録するか、プラットフォームに公開する前に動作をテストするために開発中にデータエンリッチメント変換をロックインするかもしれません。

### プログラムによる構成


<blockquote>
プログラムによる変換構成はReact Nativeでは利用できません。Tealiumモバイルプロファイルで変換を構成してください。
</blockquote>


参照用のスコープ定数：



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



コードで変換を構成する例：



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



### JSON構成

変換はJSON形式でリモートまたはローカル構成で定義することもできます：

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

## カスタムトランスフォーマーの作成

カスタムトランスフォーマーを作成するには、`Transformer`プロトコルを実装します：



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

