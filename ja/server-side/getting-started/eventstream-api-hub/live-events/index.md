---
title: ライブイベント
description: ライブイベントを使用して、リアルタイムでのイベントの管理と検査を行います。これを使用して、データソースからのテストイベントが受信されていることを確認します。
url: https://docs.tealium.com/ja/server-side/getting-started/eventstream-api-hub/live-events/
---
## ライブイベントの使用

まず、**Validate > Live Events** に移動し、**All Data Sources** リストから新しいデータソースを選択して、**Apply** をクリックします。

![](https://docs.tealium.com/images/server-side/eventstream-getting-started-live-events-select-data-sources.png)

チャートは、そのデータソースからイベントが到着するのを待っています。

次に、テストイベントをトリガーするために、サイトまたはアプリに戻ります。HTTP APIを使用している場合は、テストイベントのURLを新しいブラウザウィンドウに貼り付けるだけです。インストールが正常に機能していれば、テストイベントはチャート上で青いバーとして画面に表示されます。

## イベントの詳細

バーをクリックしてイベントの詳細を見ます。イベント名（`search`）とデータソース（`My Sample App`）がトップヘッダーセクションに目立って表示されていることに注意してください。イベント名の下には、イベントに含まれるすべてのデータ属性のリストがあり、その中にはすべてのイベントに自動的に構成されるものもあります。

![](https://docs.tealium.com/images/server-side/eventstream-getting-started-live-events-event-details.png)
<!-- GAP: replace eventstream-getting-started-live-events-event-details.png with an updated screenshot of the search event details showing the updated tab bar with Valid, Warn, Invalid, and No Spec counts -->

異なるイベント名を試してみたり、イベントに追加のパラメータを追加してみてください。

イベントが届かない場合は、以下を確認してください：

* データソースを追加した後に保存して公開しましたか？
* インストールコード内のデータソースキーはインターフェースで提供されたものと一致していますか？
* アカウント名とプロファイル名はインストールコード内で正しく構成されていますか？

素晴らしいです、データソースが機能しており、EventStreamがデータを受信していることが確認できたので、イベント仕様を見てみましょう。