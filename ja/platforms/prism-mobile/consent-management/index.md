---
title: 同意
description: Tealium Prism SDK から同意データを渡し、サーバー側で同意を適用します。
url: https://docs.tealium.com/ja/platforms/prism-mobile/consent-management/
---
現在、Tealium Prism では同意管理を利用できません。SDK は、同意に基づいてイベントを保持、ブロック、またはフィルタリングしません。ローカル構成またはリモート構成に同意セクションが含まれている場合、SDK はメッセージをログに記録し、そのセクションを無視します。

## 推奨されるアプローチ

1. 同意管理プラットフォーム（CMP）で選択された同意内容を Prism データレイヤーに渡し、すべてのイベントに含めます。
1. [同意オーケストレーション](https://docs.tealium.com/about-consent-orchestration/)を使用して、サーバー側で同意を適用します。

ユーザーが選択内容を変更するたびに、データレイヤーを更新します。属性名は任意です。以下の例では、`consent_categories` を使用します。



```kotlin
val consentCategories = DataList.create {
    add("analytics")
    add("marketing")
}

tealium.dataLayer.put("consent_categories", consentCategories, Expiry.FOREVER)
```


```swift
tealium.dataLayer.put(key: "consent_categories", converting: ["analytics", "marketing"], expiry: .forever)
```


```javascript
await tealium.dataLayer.put("consent_categories", ["analytics", "marketing"], "forever");
```



サーバー側での適用は、Tealium に到達したイベントに対して行われます。Firebase などのオンデバイスディスパッチャーは、データをベンダーに直接送信します。これらのディスパッチャーには、各ベンダーが提供する同意管理機能を使用してください。