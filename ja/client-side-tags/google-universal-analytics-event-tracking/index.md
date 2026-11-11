---
title: Google Universal Analyticsイベントトラッキング
description: このガイドでは、タグ管理アカウントのGoogle Universal Analyticsタグでカスタムイベントをトラッキングする2つの方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/google-universal-analytics-event-tracking/
---

<blockquote>
2023年7月1日以降、Google Universal Analyticsプロパティではヒットの処理が停止されています。このタグは非推奨となり、タグマーケットプレイスでは利用できなくなりました。現在のタグについては、[Google Analytics 4](https://docs.tealium.com/google-analytics-4-ga4-tag/)を参照してください。
</blockquote>


## 概要

タグ管理アカウントでGoogle Universal Analytics（GUA）のカスタムイベントを構成するには、主に2つの方法があります。1つ目の方法では、データマッピングを使用して各イベント属性を個別に構成します。これは最も一般的な方法で、大半のシナリオに対応できます。2つ目の方法ではJavaScriptを使用します。より高度な方法ですが、複数のイベントを一度にトリガーできます。

* データマッピングを使用した単一イベント
* 「GA Events」配列を使用した複数イベント

## データマッピングによるイベントのトラッキング

この方法では、データマッピングを使用してデータレイヤー変数を必要なGUAイベント変数にマッピングします（[Google Analyticsで想定されるイベントフィールド](https://developers.google.com/analytics/devguides/collection/analyticsjs/events)の詳細を参照してください）。GUAの各イベントフィールドに対応する変数を作成する必要があります。

* eventCategory
* eventAction
* eventLabel
* eventValue

これらの変数はGUA固有のものになるため、他のイベント変数と簡単に区別できるよう、名前の先頭に「ga\_」を付けることをお勧めします。その後、「データ値を構成」拡張機能を使用して、各イベントのGUAイベント変数を想定される値に構成します。

データマッピングを使用してGUAイベントトラッキングを構成するには、次の手順に従います。

1. **イベント変数を作成する**  
GUAの各イベントフィールドに対応する変数を作成します。（[データレイヤー変数の追加](https://docs.tealium.com/data-layer-variables/)の詳細を参照してください。）
  * ga\_eventaction
  * ga\_eventCategory
  * ga\_eventLabel
  * ga\_eventValue
1. **データマッピングを追加する**  
各変数から対応するGUAフィールドへのデータマッピングを追加します。（[データマッピングの詳細](https://docs.tealium.com/ja/tag-management/data-mappings/manage/)を参照してください。）
1. **「データ値を構成」拡張機能を追加する**  
GUAでトラッキングする各イベントについて、[「データ値を構成」拡張機能](https://docs.tealium.com/set-data-values-extension/)を追加します。この拡張機能を使用してGUAイベント変数を想定される値に構成し、イベントを識別する条件を指定します。  

<blockquote>
これらの拡張機能ではGUA変数のみを構成するため、スコープをGUAタグに構成してください。
</blockquote>

 この例では、`Fall Promo`動画で`video_play`イベントが発生したときに条件が一致します。  

変更を保存してパブリッシュし、テストします。

## GA Events配列によるイベントのトラッキング

この方法では、GUAタグテンプレートの`ga_events`という特殊な配列変数を使用します。この変数を使用すると、1回の呼び出しで複数のイベントをトリガーしたり、マッピングを省略したりできます。この方法では、`ga_events`に対するマッピングを1つだけ使用し、その後JavaScriptコードを使用してGUAイベントオブジェクトをプッシュします。拡張機能やマッピングとして構成する代わりに、GUAの変数とイベントを直接構成できるため、GUAで多数のカスタムイベントをトラッキングする実装に便利です。


<blockquote>
この方法はGoogle Universal Analyticsでのみサポートされています。
</blockquote>


GUAイベントトラッキングで`ga_events`配列を使用するには、次の手順に従います。

1. `ga_events_array`という名前の新しいデータレイヤー変数を作成します。
1. GUAタグで、`ga_events_array`から`ga_events`へのデータマッピングを追加します。
1. [JavaScriptコード](https://docs.tealium.com/advanced-javascript-code-extension/)拡張機能で、次のコードをテンプレートとして使用し、`ga_events_array`変数を構成します。スコープを「すべてのタグ」またはGUAタグに構成します。

```js
b.ga_events_array = [
  {eventCategory:"cat1", eventAction:"action1", eventLabel:"label1", eventValue:"1"},
  {eventCategory:"cat2", eventAction:"action2", eventLabel:"label2", eventValue:"2"}
]
```

## GUAトラッキングからTealiumトラッキングへの変換

この方法では、既存のGUAイベントトラッキングをTealiumトラッキングへ簡単に変換することもできます。

イベントトラッキング用のGUAコードスニペットの例：

```js
ga('send', {
    hitType       : 'event',
    eventCategory : 'Videos',
    eventAction   : 'play',
    eventLabel    : 'Fall Campaign'
});
```

基本的な命名規則を維持したまま、GUAイベントフィールドを使用して`ga_events`変数を構成することで、これをTealiumトラッキングに変換できます。

```js
utag.link({
    ga_events : [{
        eventCategory : 'Videos',
        eventAction   : 'play',
        eventLabel    : 'Fall Campaign'
    }]
});
```

この方法では、GUAタグテンプレート変数を直接構成するため、マッピングが不要になります。