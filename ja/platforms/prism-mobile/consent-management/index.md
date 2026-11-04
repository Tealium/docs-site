---
title: 同意
description: Tealium Prism SDK から同意データを渡し、サーバー側で同意を適用します。
url: https://docs.tealium.com/ja/platforms/prism-mobile/consent-management/
---
現在、Tealium Prism では同意管理を利用できません。SDK は、同意に基づいてイベントを保持、ブロック、またはフィルタリングしません。ローカル構成またはリモート構成に同意セクションが含まれている場合、SDK はメッセージをログに記録し、そのセクションを無視します。

## 推奨される方法

1. 同意管理プラットフォーム（CMP）から Prism データレイヤーに同意の選択内容を渡し、すべてのイベントにその情報が含まれるようにします。
1. [同意オーケストレーション](https://docs.tealium.com/about-consent-orchestration/)を使用して、サーバー側で同意を適用します。

ユーザーが選択内容を変更するたびに、データレイヤーを更新します。属性名は任意です。以下の例では `consent_categories` を使用しています。



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



サーバー側での適用は、Tealium に到達したイベントに対して行われます。Firebase などのデバイス上のディスパッチャーは、ベンダーにデータを直接送信します。これらのディスパッチャーには、各ベンダー独自の同意制御を使用してください。