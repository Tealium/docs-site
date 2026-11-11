---
title: SiteCatalyst での複数イベントの発火とイベントシリアル化
description: 以下では、2015 年 9 月 2 日にリリースされた SiteCatalyst テンプレートで利用可能になった変更について説明します。タグ名は「SiteCatalyst」および「SiteCatalyst AppMeasurement for JS」です。
url: https://docs.tealium.com/ja/client-side-tags/sitecatalyst-firing-multiple-events-and-event-serialization/
---

## この機能を含む最新のテンプレートを使用しているか確認するにはどうすればよいですか？

テンプレートの先頭には、テンプレート ID と `YYYYMMDD` 形式の日付で始まる日付（タイムスタンプ）があります。この機能は `20150827` テンプレートで追加されました。

```
//~~tv:19004.h27.20150827
```


<blockquote>
このタイムスタンプはタグテンプレートの更新日です（このテンプレートが本番環境で利用可能になる日付よりも前になります）。<br><br>
この機能は、それ以降のテンプレート（例：`20150929`）でも利用できます。
</blockquote>


## イベントシリアル化

データレイヤーに `myevent` があり、マッピングツールボックスでこれが `click:event5` にマッピングされている場合、以下を実行すると、シリアル番号 `12345` を使用して `event5` が発火します。

`utag.view( \{ myevent : "click:12345" \} );`

## 複数イベントの発火

更新されたテンプレートでは、別のマッピングを追加し、データレイヤーでカンマ区切りの文字列リストを使用することで、2 つ以上のイベントを発火できます。以下の例では、マッピングに「product-view:prodView」を構成し、データレイヤー変数「myevent」の値リストにも「product-view」文字列を追加しています。

`utag.view( \{ myevent : "product-view,click:12345" \} );`

JavaScript は配列を文字列に変換し、その際にカンマを追加するため、以下の配列は文字列内のカンマ区切りリストと同様に機能します。

`utag.view( \{ myevent : ["product-view", "click:12345"] \} );`

### 注記

* マッピングされた変数にスペースが含まれる可能性がある場合は、Extension を使用して値をクリーンアップしてください。テンプレートでは変数値の操作（文字列のクリーンアップなど）は行われません。

* 値のリストがあり、マッピングで複数の一致が見つかった場合でも、イベントは 1 回だけ発火します（たとえば、`s.events` には 1 回だけ追加されます）。

* 以下のブログリンクによると、Adobe ではサーバー側でイベントをシリアル化する別の方法も提供しているようです。この機能は実装では不要になっており、Adobe の UI でレポート構成を使用して実現できます。
 
## ベンダー情報

このタイムスタンプはタグテンプレートの更新日です（このテンプレートが本番環境で利用可能になる日付よりも前になります）。<br><br>
この機能は、それ以降のテンプレート（例：`20150929`）でも利用できます。

* [Omniture SiteCatalyst 内でのイベントシリアル化](https://blogs.adobe.com/digitalmarketing/analytics/event-serialization-inside-omniture-sitecatalyst/)
* [イベントシリアル化](https://helpx.adobe.com/analytics/using/event-serialization.html)
* [Adobe Analytics のオンデマンド指標のご紹介](http://blogs.adobe.com/digitalmarketing/analytics/say-hello-to-on-demand-metrics-in-adobe-analytics/)