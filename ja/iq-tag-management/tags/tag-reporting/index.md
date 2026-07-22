---
title: タグレポート
description: タグレポートビューでは、サイトに実装されたタグの使用状況とパフォーマンスデータを表示します。
url: https://docs.tealium.com/ja/iq-tag-management/tags/tag-reporting/
---
このビューは、サイト訪問、Tealiumホストのサーバーリクエスト、ベンダータグのロードなど、さまざまなパフォーマンスメトリクスを解釈するのに役立ちます。タグレポートは基本的なIT目的のためのものであり、分析ツールとして考えるべきではありません。


<blockquote>
タグレポートは、Tealiumプラットフォームを通じて流れるデータを完全に処理し、表示するのに最大48時間かかることがあります。日付範囲が過去24〜48時間のみを含む場合、レポートにデータが表示されない場合があります。ベストプラクティスとして、現在の日付の少なくとも48時間前の終了日を入力します。
</blockquote>


## タグレポートの表示

タグレポートのチャートを表示するには、次の手順を使用します：

1. 左側のサイドバーで、**クライアントサイドツール > タグレポート**をクリックします。  
過去7日間のすべてのプロファイルのタグ**使用状況**と**運用**レポートが表示されます。
1. **パースペクティブ**ドロップダウンリストからプロファイルを選択します。  
選択したプロファイルの**タグ使用状況と運用**レポートが表示されます。
1. **日付**フィールドで、カレンダードロップダウンを使用して日付範囲を選択します。  
    ![](https://docs.tealium.com/images/iq-tag-management/whiteui-tiq-tag-usage-reports-select-date-range.jpg)  
    選択した時間枠のレポートが表示されます。

## タグレポートについて

タグレポートの各チャートには、**トレンド**と**累積**の2つの異なるビューがあります。

* **トレンド**  
このビューは、選択した日付範囲でデータがどのようにトレンドまたは変動するかを表示します。

* **累積**  
このビューは、終了日範囲で選択した日付までにキャプチャされたすべてのデータポイントの合計を表示します。次の例に示すように：  

    ![](https://docs.tealium.com/images/iq-tag-management/whiteui-tiq-tag-reporting-trending-and-cumulative-views.jpg)

次のセクションでは、各レポートタイプで伝えられる情報について説明します。

### 訪問レポート

**訪問レポート**は、指定した期間の訪問（セッション）数を表示します。


<blockquote>
このレポートを表示するには、`utag.js`バージョン4.26以降が必要です。`utag.js`テンプレートの更新についての詳細は、ナレッジベースの記事[Best Practices for Updating to the Latest Version of utag.js](https://support.tealiumiq.com/en/support/solutions/articles/36000363470)を参照してください。
</blockquote>


訪問、またはセッションとは、訪問がサイトを通じてナビゲートする時間のことです。訪問は最初のページリクエストで始まり、訪問がサイトから離れるか、所定の時間が経過する（通常は30分）と終了します。

### ローダータグレポート

**ローダータグレポート**は、指定した期間中に発生するタグリクエスト（ロード）の数を表示します。`utag.js`、`utag.sync.js`、および`mobile.html`ファイルリクエストのロードがプロットされます。

![](https://docs.tealium.com/images/iq-tag-management/whiteui-tiq-tag-reporting-loader-tag-details.jpg)

### ベンダータグ

**ベンダータグレポート**は、指定した日付範囲内の特定の日にベンダータグ（`utag.\*.js`）がロードされた回数を表示します。


<blockquote>
**タグエラー**と**タグキル**のデータは収集されず、常に`0`と表示されます。
</blockquote>


![](https://docs.tealium.com/images/iq-tag-management/whiteui-tiq-tag-reporting-vendor-tags-report.jpg)
