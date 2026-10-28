---
title: 変換
description: オンデバイスのイベント変換を使用して、Tealium Prism SDKのディスパッチを変更、拡張、またはフィルタリングします。
url: https://docs.tealium.com/ja/platforms/prism-mobile/transformations/
---
変換を使用すると、ディスパッチャーに送信される前にディスパッチを変更、拡張、またはフィルタリングできます。特定の条件やスコープに基づいてデータを変換するカスタムビジネスロジックを実装するには、変換を使用します。

## 仕組み

変換はディスパッチパイプライン内の定義された時点で実行され、イベントがディスパッチャーに到達する前に、そのイベントを変更、拡張、または破棄できます。

変換のスコープによって、実行されるタイミングが決まります。

* **コレクターの後**：データ収集後、ディスパッチャーがイベントを受信する前に実行されます。すべてのディスパッチャーに適用するデータ拡張に使用します。
* **すべてのディスパッチャー**：各ディスパッチャーに対して実行されます。
* **特定のディスパッチャー**：指定されたディスパッチャーに対してのみ実行されます。送信先固有のフィルタリングやデータマスキングに使用します。

各変換には条件を含めることができ、ディスパッチペイロードに特定のデータが存在する場合にのみ適用されます。

## 一般的な変換パターン

### データ拡張

既存の値に基づいて、ディスパッチにデータを追加します。たとえば、購入金額に基づいてユーザーセグメントを追加します。

### データフィルタリング

機密データや不要なデータを、ディスパッチャーに到達する前にディスパッチから削除します。ペイロードから除去する機密キーのリストを構成します。

### 条件に基づくディスパッチの破棄

特定の条件に基づいてディスパッチを破棄します。ディスパッチ全体を破棄するには、`applyTransformation`メソッドから`nil`（Swift）または`null`（Kotlin）を返します。たとえば、本番環境ではテストイベントを破棄します。

### スコープ固有の変換

パイプラインの各段階で異なる変換を適用します。すべてのディスパッチャーに適用するデータ拡張には`afterCollectors`を使用し、特定の送信先に固有のフィルタリングには`dispatchers`を使用します。

## UIでの変換の構成

変換は、モバイルプロファイル内で拡張機能として構成します。タグ管理の拡張機能と同じように機能しますが、モバイル固有のスコープが含まれます。

UIで拡張機能を追加するには、次の手順を実行します。

1. モバイルプロファイルにログインし、**拡張機能**に移動します。
1. **拡張機能を追加**を選択し、拡張機能の種類を選択します。
1. 拡張機能を構成し、そのスコープを指定します。
1. 変更を保存してパブリッシュします。

UIでは、次のモバイル固有のスコープを使用できます。

| スコープ | 説明 |
| :--- | :--- |
| コレクターの後 | データ収集後、すべてのディスパッチャーより前に適用されます。 |
| すべてのディスパッチャー | すべてのディスパッチャーに適用されます。 |

## 高度な構成

実行時にのみ判明する値にロジックが依存する場合や、リモート構成に関係なく変換が確実に実行されるようにする必要がある場合は、変換をプログラムで構成します。たとえば、ユーザーの同意状態に基づいて、特定のディスパッチャーをスコープとするPII除去トランスフォーマーを動的に登録できます。また、プラットフォームにパブリッシュする前に動作をテストするため、開発中にデータ拡張変換を固定することもできます。

### プログラムによる構成


<blockquote>
React Nativeでは、プログラムによる変換構成は利用できません。Tealiumモバイルプロファイルで変換を構成してください。
</blockquote>


参照用のスコープ定数：



```kotlin
TransformationScope.AfterCollectors
TransformationScope.AllDispatchers
TransformationScope.Dispatchers("my_dispatcher")
```


```swift
TransformationScope.afterCollectors
TransformationScope.allDispatchers
TransformationScope.dispatchers(["my_dispatcher"])
```



例：コードで変換を構成します。




```kotlin
class DataEnrichmentSettingsBuilder(transformationId: String) :
    TransformationSettingsBuilder<DataEnrichmentSettingsBuilder>(
        transformationId,
        "DataEnrichmentTransformer"
    ) {
    override fun onBuildConfiguration(): DataObject = DataObject.create {
        put("enable_enrichment", true)
        put("enrichment_type", "user_data")
    }
}

val enrichmentTransformation = DataEnrichmentSettingsBuilder("user_enrichment")
    .setScope(TransformationScope.AfterCollectors)
    .setCondition(Rule.just(Condition.isDefined("user_id")))

config.addTransformation(enrichmentTransformation)
```


```swift
class DataEnrichmentSettingsBuilder: TransformationSettingsBuilder {
    init(id: String) {
        super.init(id: id, transformerId: "DataEnrichmentTransformer")
    }

    override func build() -> DataObject {
        var settings = super.build()
        let configuration: DataObject = [
            "enable_enrichment": true,
            "enrichment_type": "user_data",
            "source": "user_profile"
        ]
        settings.set(converting: configuration, key: "configuration")
        return settings
    }
}

let enrichmentTransformation = DataEnrichmentSettingsBuilder(id: "user_enrichment")
    .setScope(.afterCollectors)
    .setConditions(.just(Condition.isDefined(variable: "user_id")))

config.setTransformation(enrichmentTransformation)
```



### JSON構成

リモート構成またはローカル構成では、変換をJSON形式で定義することもできます。

```json
{
  "transformation_id": "user_enrichment",
  "transformer_id": "MyCustomTransformer",
  "scope": "aftercollectors",
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

カスタムトランスフォーマーを作成するには、`Transformer`プロトコルを実装します。




```kotlin
class MyCustomTransformer : Transformer {
    override val id: String = "MyCustomTransformer"
    override val version: String = "1.0.0"

    override fun applyTransformation(
        transformation: TransformationSettings,
        dispatch: Dispatch,
        scope: DispatchScope,
        completion: Callback<Dispatch?>
    ): Disposable {
        val enableEnrichment: Boolean =
            transformation.configuration.getBoolean("enable_enrichment") ?: true

        if (enableEnrichment) {
            dispatch.addAll(DataObject.create { put("transformed", "true") })
        }

        // Return the modified dispatch
        completion.onComplete(dispatch)

        // Or return null to drop the dispatch entirely
        // completion.onComplete(null)

        return Disposables.disposed()
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
                           completion: @escaping (Dispatch?) -> Void) -> any Disposable {
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

        return Disposables.disposed()
    }
}
```

