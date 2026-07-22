---
title: SiteCatalystで複数のイベントを発火させるとイベントのシリアライズ
description: 以下は、2015年9月2日にリリースされたSiteCatalystテンプレートで利用可能な変更を説明しています。タグ名は「SiteCatalyst」と「SiteCatalyst AppMeasurement for JS」です。
url: https://docs.tealium.com/ja/client-side-tags/sitecatalyst-firing-multiple-events-and-event-serialization/
---

## この機能を持つ最新のテンプレートを持っているかどうかはどうやって知るのですか？

テンプレートの上部には、テンプレートIDと日付（タイムスタンプ）があり、フォーマットは`YYYYMMDD`です。この機能は`20150827`のテンプレートに追加されました。

```
//~~tv:19004.h27.20150827
```


<blockquote>
このタイムスタンプは、タグテンプレートの更新日付であり（これは、このテンプレートが本番環境で利用可能になる日付よりも早いです）。<br><br>
また、この機能は後のテンプレート（例えば、`20150929`）でも期待できます。
</blockquote>


## イベントのシリアライズ

データレイヤーに`myevent`があり、これがマッピングツールボックスで`click:event5`にマッピングされている場合、次のようにするとシリアライズ番号`12345`で`event5`がトリガーされます。

`utag.view( \{ myevent : "click:12345" \} );`

## 複数のイベントの発火

更新されたテンプレートでは、別のマッピングを追加し、データレイヤーの文字列リストを使用して2つ以上のイベントを許可します。以下の例では、マッピングに"product-view:prodView"があり、データレイヤー変数"myevent"の値リストに"product-view"文字列を追加しています。

`utag.view( \{ myevent : "product-view,click:12345" \} );`

JavaScriptが配列を文字列に変換し、その過程でカンマを追加するので、次の配列は文字列内のカンマ区切りリストと同じように動作します：

`utag.view( \{ myevent : ["product-view", "click:12345"] \} );`

### 注意

* マッピング変数にスペースが含まれることを想定している場合は、Extensionを使用して値をクリーンアップします。テンプレートは変数値の操作（例えば、文字列のクリーンアップ）を行いません。

* 値のリストとマッピングの複数のマッチがある場合、イベントは一度だけ発火します（例えば、`s.events`に一度だけ追加されます）。

* 下記のブログリンクでは、Adobeがサーバーサイドでイベントのシリアライズを行う別の方法を持っているようです。この機能は実装で不要になり、AdobeのUIでのレポート構成で行うことができます。

## ベンダー情報

このタイムスタンプは、タグテンプレートの更新日付であり（これは、このテンプレートが本番環境で利用可能になる日付よりも早いです）。<br><br>
また、この機能は後のテンプレート（例えば、`20150929`）でも期待できます。

* [Omniture Sitecatalyst内のイベントシリアライゼーション](https://blogs.adobe.com/digitalmarketing/analytics/event-serialization-inside-omniture-sitecatalyst/)
* [イベントシリアライゼーション](https://helpx.adobe.com/analytics/using/event-serialization.html)
* [Adobe Analyticsのオンデマンドメトリクスにこんにちは](http://blogs.adobe.com/digitalmarketing/analytics/say-hello-to-on-demand-metrics-in-adobe-analytics/)
