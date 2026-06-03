---
title: インポート状況の確認
description: この記事では、インポートされたファイルの状況を確認する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/file-import/file-transfer-service/view-import-status/
---
 ファイルインポートエラーの詳細については、カスタム[Bulk Download Logs](https://support.tealiumiq.com/en/support/solutions/articles/36000363442-tealium-tools-bulk-download-logs)ツールを使用してください。

## インポート活動の確認

ファイルインポートデータソースを構成し、ファイルのインポートを開始した後、**データソースダッシュボード**でデータソースを展開し、**ステータス**タブをクリックしてインポート活動を確認できます。このページでは、過去1か月間のレポートが表示され、エラーの有無にかかわらず処理された行数の詳細がグラフィカル形式で示されます。グラフの直下に表形式のビューが表示されます。

![](/images/server-side/data-sources/file-import/file-import-status-chart.png)

ファイル行は、マルチテナント環境の地域負荷に基づいて変動する速度で処理されますが、ほとんどのファイルは24時間以内に処理されます。

エラーが発生した場合、グラフの赤いエリアにマウスを合わせると、エラーの内訳が表示されます。ツールチップには一般的なエラーが表示され、AWS S3にホストされているすべてのエラーの詳細レポートへのリンクが含まれています。グラフの任意のバーにマウスを合わせると、処理された行数の詳細が表示されます。

![](/images/server-side/data-sources/file-import/file-import-status-file-list.png)

## インポートされたイベントの確認

ファイルからインポートされたイベントを確認するには、**ライブイベント**画面に移動し、ドロップダウンリストからファイルインポートデータソースを選択します。詳細については、[About Live Events]()を参照してください。