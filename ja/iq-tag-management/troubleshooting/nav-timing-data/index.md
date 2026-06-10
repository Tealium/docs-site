---
title: ナビゲーションタイミングデータ
description: この記事では、ウェブサイトのパフォーマンスを測定するために使用できるナビゲーションタイミングデータを有効にする方法について説明します。
url: https://docs.tealium.com/ja/iq-tag-management/troubleshooting/nav-timing-data/
---
[Navigation Timing API](https://developer.mozilla.org/en-US/docs/Web/API/Navigation_timing_API &#34;Navigation Timing API&#34;)は、ウェブサイトのパフォーマンスを測定するために使用できるデータを提供します。このAPIは、同じ目的で使用されてきた他のJavaScriptベースのメカニズムとは異なり、より有用で正確なエンドツーエンドの遅延データを提供することができます。

## ナビゲーションタイミングデータを有効にする

1. Tealium Collectテンプレートを最新バージョンのテンプレートに更新します。
1. 情報を収集したいトラフィックの割合に対するサンプリングレートを構成します。
    サンプリングレートは、収集されるイベントデータに限定されており、サンプリングが5%に構成されていても、TealiumはAudienceStream、EventStore、および/またはEventDB（Tealium Collect）に対して100%のイベントデータをトリガーします。
1. 更新を保存/公開します。

## データ

以下のデータポイントはTealium Collectタグ内でキャプチャされます：

* `timing.domain` = タイミングデータが収集されたドメイン
* `timing.pathname` = タイミングデータが収集されたパス名（ウェブページ）
* `timing.query_string` = タイミングデータが収集されたURLのクエリ文字列値
* `timing.timestamp` = タイミングデータが収集された日時（クライアントのウェブブラウザのエポック時間）
* `timing.dns` = `t.domainLookupEnd` - `t.domainLookupStart`
* `timing.connect` = `t.connectEnd` - `t.connectStart`
* `timing.response` = `t.responseEnd` - `t.responseStart`
* `timing.dom_loading_to_interactive` = `t.domInteractive` - `t.domLoading`
* `timing.dom_interactive_to_complete` = `t.domComplete` - `t.domInteractive`
* `timing.load` = `t.loadEventEnd` - `t.loadEventStart`
* `timing.time_to_first_byte` = `t.responseStart` - `t.connectEnd`
* `timing.front_end` = `t.loadEventStart` - `t.responseEnd`
* `timing.fetch_to_response` = `t.responseStart` - `t.fetchStart`
* `timing.fetch_to_complete` = `t.domComplete` - `t.fetchStart`
* `timing.fetch_to_interactive` = `t.domInteractive` - `t.fetchStart`

このデータは、キー`tealium_timing`のローカル保存に保存されます。

次のページの読み込み時に、ローカル保存が読み込まれ、データがデータレイヤーに追加されます。

すべてのデータを持っていないため、同じページイベントコールでナビゲーションタイミングデータを送信することはできません。例えば、`interactive`イベントでCollectタグを発火させた可能性が高いため、ロードイベントのタイミングデータはありません。これは、別のコールをトリガーする必要があり、契約で構成されたイベント数が2倍になることを意味します。したがって、契約のイベント数にネガティブな影響を与えないように、次のページビューで送信します。

## EventDBの要件

EventDBでデータソースを宣言するには、以下の手順を実行します：

1. **Tag Management &gt; Data Layer**に移動します。
1. **Add Data Source**ドロップダウンメニューをクリックし、**Bulk Import Data Sources from CSV**を選択します。
1. 以下をインターフェースに貼り付けます：

```
&#34;timing.domain&#34;,&#34;UDO Variable&#34;,&#34;&#34;,&#34;www.tealiumecommerce.com&#34;
&#34;timing.pathname&#34;,&#34;UDO Variable&#34;,&#34;&#34;,&#34;/&#34;
&#34;timing.query\_string&#34;,&#34;UDO Variable&#34;,&#34;&#34;,&#34;&#34;
&#34;timing.timestamp&#34;,&#34;UDO Variable&#34;,&#34;&#34;,1459274326166
&#34;timing.dns&#34;,&#34;UDO Variable&#34;,&#34;&#34;,75
&#34;timing.connect&#34;,&#34;UDO Variable&#34;,&#34;&#34;,1
&#34;timing.response&#34;,&#34;UDO Variable&#34;,&#34;&#34;,1
&#34;timing.dom\_loading\_to\_interactive&#34;,&#34;UDO Variable&#34;,&#34;&#34;,3987
&#34;timing.dom\_interactive\_to\_complete&#34;,&#34;UDO Variable&#34;,&#34;&#34;,3570
&#34;timing.load&#34;,&#34;UDO Variable&#34;,&#34;&#34;,2
&#34;timing.time\_to\_first\_byte&#34;,&#34;UDO Variable&#34;,&#34;&#34;,1002
&#34;timing.front\_end&#34;,&#34;UDO Variable&#34;,&#34;&#34;,7570
&#34;timing.fetch\_to\_response&#34;,&#34;UDO Variable&#34;,&#34;&#34;,1082
&#34;timing.fetch\_to\_complete&#34;,&#34;UDO Variable&#34;,&#34;&#34;,8653
&#34;timing.fetch\_to\_interactive&#34;,&#34;UDO Variable&#34;,&#34;&#34;,5083
```

これにより、データソースが宣言され、可視化ツールがデータにアクセスできるようになります。この手順はEventStoreでは必要ありません。

以下は、ページの読み込みにどれだけ時間がかかるかを確認できるサンプルレポートです。例えば、ページが3秒以内（3000ミリ秒）に読み込まれる必要がある要件がある場合、&#34;Chelsa Tee&#34;と&#34;Tealium Ecommerce Demo&#34;のページが改善が必要であることがわかります。

![](/images/iq-tag-management/page-performance-visualization.png)
