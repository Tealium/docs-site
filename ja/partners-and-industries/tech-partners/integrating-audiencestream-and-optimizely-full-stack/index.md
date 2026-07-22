---
title: AudienceStreamとOptimizely Full Stackの統合
description: この記事では、Tealium AudienceStreamとOptimizely Full Stackを統合するためのベストプラクティスについて説明します。
url: https://docs.tealium.com/ja/partners-and-industries/tech-partners/integrating-audiencestream-and-optimizely-full-stack/
---## 前提条件

* Tealiumの訪問者プロファイルのVisitor ID
* Optimizelyの機能または実験のUser ID

## 仕組み

Tealium AudienceStreamのオーディエンスとバッジをOptimizely Full Stack内で活用することで、特定の機能や実験をユーザーの一部に対してターゲット設定することができます。

## 制限事項と考慮事項

* データレイヤー濃縮APIを呼び出すとネットワーク遅延が発生するため、環境内でローカルにキャッシュされたプロファイルを使用して、クリティカルパス外で行う必要があります。
* Optimizely Full Stackのプロジェクトは、属性の上限が100です。

## Tealium SDK: VisitorService

Tealium Software Development Kit（SDK）内のVisitorServiceは、データレイヤー濃縮APIのラッパーで、データレイヤー濃縮の呼び出しを更新し、キャッシュする複雑さを管理するために使用できます。

以下のTealium SDKには、組み込みのデータレイヤー濃縮プロファイルがあります：

### iOS用Swift

[VisitorSevice Module](https://docs.tealium.com/ja/platforms/ios-swift/module-list/visitor-service/)開発者ドキュメンテーションに記載されているように、`TealiumVisitorServiceDelegate`を実装します。

```swift
**func** **profileDidUpdate**(profile: TealiumVisitorProfile?) {
        **guard let** profile = profile **else { return }**

        // Return the current Audiences for which the user is assigned
       **if let** currentVisitorAudiences = profile.audiences {
            print("Visitor audiences: \(currentVisitorAudiences)")

            // Check if an Audience is assigned to a user by id
            **if** currentVisitorAudiences[id: "106"] {
                print("Visitor is a member of audience id 106")
                // ... Visitor is a member of this audience, take appropriate action
            }

            // Check if an Audience is assigned to a user by name
            **if** currentVisitorAudiences[name: "ios users"] {
                print("Visitor is a member of audience iOS Users")
                // ... Visitor is a member of this audience, take appropriate action
            }
        }
}
```

#### 最新の訪問者プロファイルを取得する

最新の訪問者プロファイルを取得するには、以下の例のように`getCachedProfile`を使用します：

```swift
**self**.tealium?.visitorService()?.getCachedProfile(completion: {
prfile **in**
  **guard let** profile = profile **else** { **return** }
})
```

プロファイルから、`audiences`と`badges`から以下の属性情報が必要です：

* **audiences**
    * id: String, name: String 
    * ``` id: "tealiummobile\_demo\_103", name: "iOS Users" ``` 
* **badges**
    * id: String, value: Bool 
    * ``` id: "2815", value: true ``` 

この情報を使用して、Optimizelyに渡される他の属性とともに、これら2つのプロファイル属性の内容を含む単一の変数を作成します。作成したら、この属性を`activate`、`isFeatureEnabled`、または`getEnabledFeatures`のパラメータとして渡すことができます。

#### オーディエンスとバッジを単一の属性変数にマージする

以下の例を使用して、オーディエンスとバッジを単一の属性変数にマージします：

```swift
/*
Merged profiles.audience and profiles.badges into attributes array using array append or + notation.
NOTE: Ensure you include any existing attributes you may already be passing.
*/

let attributes = profile.audiences + profile.badges

```

#### 例：getEnabledFeatures

```swift
let enabledFeatures = optimizely.getEnabledFeatures(userId: "user_123",
  attributes: attributes)
```

#### 例：Activate

```swift
do {
	let variation = try optimizelyClient.activate("app_redesign", userId:userId, attributes: attributes )
  if (variation.variationKey == "control") {
    // Execute code for variation A
  } else if (variation.variationKey == "treatment") {
    // Execute code for variation B
  }
} catch {
  // Execute code for users who don't qualify for the experiment
}

```

### Android

VisitorServiceを含む新しいAndroid SDKが現在開発中です。

#### Tealium Data Layer Enrichment Public API

SDKがVisitorServiceを実装していない言語で現在のユーザーのTealiumプロファイルを取得するには、[Data Layer Enrichment Public API](https://docs.tealium.com/data-layer-enrichment-api/)を参照してください。


<blockquote>
Data Layer Enrichment APIをサーバーサイドのコードで使用する場合、ユーザープロファイルをローカルサーバーに保存し、更新リクエストをバックグラウンドで行うことを検討してください（約100ミリ秒以下）。
</blockquote>


あなたの実装があなたのユースケースに適していることを確認するために、Optimizelyの代表者に連絡してください。

Data Layer Enrichment APIは、以下の例のような訪問者プロファイルのJSONを返します：

```json
{
     "metrics" : {
            "5117" : 6.0,
            "22" : 6.0
     },
     "dates" : {
            "5111" : 1420223771043
     },
     "properties" : {
            "17" : "http://tags.tiqcdn.com/utag/acct/prof/env/mobile.html",
            "account" : "tealiummobile",
            "5123" : "set",
            "profile" : "demo"
      },
      "flags" : { "5115" : true },
      "current_visit"  {
          "metrics" : {
              "7" : 6.0
           },
           "dates" : {
               "5202" : 1420225387000
           },
           "properties" : {
               "48" : "Chrome",
               "45" : "Mac OS X",
               "44" : "Chrome",
               "47" : "browser",
               "46" : "Mac desktop"
           },
          "flags" : { }
        },
       "badges" : { "5113" : true },
       "audiences" : {
            "tealiummobile_demo_101" : "Sample Audience"
       }
}
```

#### Optimizelyで属性を設定する

Tealiumのオーディエンスやバッジを対象としたフィーチャーフラグ/フィーチャー実験または実験をターゲットにするために、Optimizely Full Stackインターフェース内でTealiumのオーディエンスとバッジごとに1つの"属性"を作成します。

![](https://docs.tealium.com/images/tech-partners/optimizely-set-up-attributes.jpg)

作成する属性は、JSONオブジェクトのキー要素と一致する必要があります。ターゲットにしたい定期的で一貫したオーディエンスのためにこれらの属性を作成します。例えば、前述のサンプルJSONでは、Optimizelyで以下の属性を作成します：

* Audiences: `tealium_mobile_demo_101`
* Badges: `5113`


<blockquote>
プロジェクトごとの属性の上限は100です。使用する予定のTealiumのオーディエンスとバッジのためだけに属性を作成してください。
</blockquote>


#### 属性を編集する

属性は、OptimzelyのAPIを呼び出す際に渡すユーザーの特性で、これを使用してオーディエンスを作成することができます。属性をクリックして、属性キーまたはオプションの属性説明フィールドを編集し、**Save Attribute**をクリックして変更を保存します。

#### Optimizelyのオーディエンスを設定する

Optimizely Full Stackインターフェース内で属性を作成した後、以下の手順を使用してオーディエンスを作成します：

1. **Audience**タブをクリックします。
1. **Create New Audience**をクリックします。
1. オーディエンスの名前と説明を入力します。
1. Custom Attributesの下で、前の手順で作成したTealiumの属性を選択します。  
    ![](https://docs.tealium.com/images/tech-partners/optimizely-create-new-audience.jpg)
1. オーディエンスを必要に応じて設定したら、**Save**をクリックします。

#### TealiumのオーディエンスとバッジをOptimizelyに渡す

コード内で、オーディエンスとバッジのセクションを使用して属性パラメータを作成し、Optimizelyに渡すことができるように、JSONオブジェクトを解析します。以下の例を参照してください。


<blockquote>
すでにOptimizelyを通じて属性を渡している場合は、その要素を属性パラメータに含めることを確認してください。
</blockquote>


```js
/* Function to merge array objects */

function extend(dest, src) {
  for(var key in src) {
    dest[key] = src[key];
  }
  return dest;
}

var request = new XMLHttpRequest()
request.open('GET','https://visitor-service.tealiumiq.com/{account}/{profile}/{visitor_id}', true)

request.onload = function() {
var tealium_audiences = JSON.parse(this.response);
var attributes = tealium_audiences.audiences
attributes = extend(attributes, tealium_audiences.badges);
}

// Send request
request.send()

```

上記の例の結果は以下のようになります：

```js
var attributes = {
  "5113": 'true',
  "tealiummobile_101": "Sample Audience"
};
```

属性変数は、以下の例のように、getFeatureEnabledおよびactivate関数を使用してOptimizelyに渡すことができます：

```js
var enabled = optimizelyClientInstance.isFeatureEnabled('mens_preview_widget', userId, attributes);
```

