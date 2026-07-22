---
title: Google Universal Analytics イベントトラッキング
description: このガイドでは、iQタグ管理アカウントのGoogle Universal Analyticsタグでカスタムイベントをトラッキングするための2つの方法を示します。
url: https://docs.tealium.com/ja/client-side-tags/google-universal-analytics-event-tracking/
---

<blockquote>
2023年7月1日以降、Google Universal Analyticsのプロパティはヒットの処理を停止しました。このタグは廃止され、タグマーケットプレイスではもう利用できません。現在のタグについては、[Google Analytics 4](https://docs.tealium.com/google-analytics-4-ga4-tag/)をご覧ください。
</blockquote>


## 概要

iQタグ管理アカウントでGoogle Universal Analytics（GUA）のカスタムイベントを構成するための主な方法は2つあります。最初の方法は、データマッピングを使用して各イベント属性を個別に構成するものです。これは最も一般的なアプローチで、大半のシナリオをカバーします。2つ目の方法はJavaScriptを使用するもので、より高度ですが、一度に複数のイベントをトリガーすることができます。

* データマッピングを使用した単一イベント
* "GAイベント"配列を使用した複数イベント

## データマッピングを使用したイベントトラッキング

この方法では、データレイヤー変数を必要なGUAイベント変数にマッピングするためにデータマッピングを使用します（[Google Analyticsが期待するイベントフィールド](https://developers.google.com/analytics/devguides/collection/analyticsjs/events)について詳しく学ぶ）。GUAイベントフィールドのそれぞれに対して変数を作成する必要があります：

* eventCategory
* eventAction
* eventLabel
* eventValue

これらの変数はGUA特有のものになるため、他のイベント変数と簡単に区別できるように、名前の前に"ga\_"を付けることをお勧めします。その後、Set Data Values拡張を使用して、各イベントの期待される値にGUAイベント変数を構成します。

データマッピングを使用してGUAイベントトラッキングを構成するには、以下の手順を実行します：

1. **イベント変数の作成**  
GUAイベントフィールドのそれぞれに対して変数を作成します。([データレイヤー変数の追加](https://docs.tealium.com/data-layer-variables/)について詳しく学ぶ。)
  * ga\_eventaction
  * ga\_eventCategory
  * ga\_eventLabel
  * ga\_eventValue
1. **データマッピングの追加**  
各変数に対して、対応するGUAフィールドへのデータマッピングを追加します。([データマッピングについて詳しく学ぶ](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)。)
1. **Set Data Values拡張の追加**  
GUAでトラッキングする各イベントに対して、[Set Data Values拡張](https://docs.tealium.com/set-data-values-extension/)を追加して、GUAイベント変数を期待される値に構成し、イベントを識別する条件を使用します。  

<blockquote>
これらの拡張はGUA変数のみを構成するため、GUAタグにスコープを構成します。
</blockquote>

この例では、条件は`Fall Promo`ビデオで`video_play`イベントが発生したときを識別します。  


変更を保存し、公開してテストします。

## GAイベント配列を使用したイベントトラッキング

この方法では、GUAタグテンプレートからの特別な配列変数`ga_events`を使用して、一度の呼び出しで複数のイベントをトリガーするか、マッピングをバイパスします。この方法では、`ga_events`に対して1つのマッピングを使用し、その後はJavaScriptコードを使用してGUAイベントオブジェクトをプッシュします。この方法は、GUAで多くのカスタムイベントをトラッキングする実装に便利です。なぜなら、それらを拡張やマッピングとして構成するのではなく、GUA変数とイベントを直接構成できるからです。


<blockquote>
この方法はGoogle Universal Analyticsでのみサポートされています。
</blockquote>


GUAイベントトラッキングに`ga_events`配列を使用するには、以下の手順を実行します：

1. `ga_events_array`という新しいデータレイヤー変数を作成します。
1. GUAタグで、`ga_events_array`から`ga_events`へのデータマッピングを追加します。
1. 以下のコードを[Javascript Code](https://docs.tealium.com/advanced-javascript-code-extension/)拡張でテンプレートとして使用し、`ga_events_array`変数を構成します。スコープをAll TagsまたはGUAタグに構成します。 

```js
b.ga_events_array = [
  {eventCategory:"cat1", eventAction:"action1", eventLabel:"label1", eventValue:"1"},
  {eventCategory:"cat2", eventAction:"action2", eventLabel:"label2", eventValue:"2"}
]
```

## GUAトラッキングをTealiumトラッキングに変換

この方法では、既存のGUAイベントトラッキングをTealiumトラッキングに簡単に変換することもできます。

イベントトラッキングのためのGUAコードスニペットの例：

```js
ga('send', {
    hitType       : 'event',
    eventCategory : 'Videos',
    eventAction   : 'play',
    eventLabel    : 'Fall Campaign'
});
```

基本的な命名規則を維持し、GUAイベントフィールドで`ga_events`変数を構成することで、これをTealiumトラッキングに変換できます：

```js
utag.link({
    ga_events : [{
        eventCategory : 'Videos',
        eventAction   : 'play',
        eventLabel    : 'Fall Campaign'
    }]
});
```

このアプローチでは、GUAタグテンプレート変数を直接構成することで、マッピングの必要性をバイパスします。

