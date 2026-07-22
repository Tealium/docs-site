---
title: コネクターインサイト：Amazon Ads Data Manager
description: Amazon Ads Data Managerのインサイトにアクセスして、オーディエンスデータセットのメトリクスを確認します。
url: https://docs.tealium.com/ja/server-side-connectors/connector-insights-amazon-ads-data-manager/
---
## 概要

Amazon Ads Data Managerコネクターインサイトは、Amazon Adsとの統合であり、Tealiumにオーディエンスデータセットのメトリクスを取り込みます。

## アクセス

**Connect > Connectors** に移動し、**Amazon Ads Data Manager** コネクターを見つけてアクションを選択します。アクション画面で、**Insights** タブをクリックします。

![](https://docs.tealium.com/images/server-side-connectors/connector-insights-btn.png)

## メトリクス

インサイトのサマリーには、以下のデータセットメトリクスが表示されます：

* **Upload Count**: このデータセットのレコードの総数。これには、オーディエンス削除リクエスト、IDなしのレコード、形式が不正なレコードが含まれます。
* **Accepted Count**: このデータセットで受け入れられたレコードの数。
* **Records Resolved**: このデータセットで認識されたユーザーにマッチしたレコードの数。これには重複が含まれます。同じユーザーに対して複数のレコードをアップロードした場合、各ユーザーレコードがIDに解決された数がカウントされます。
* **Records with Identity**: このデータセットで識別子を持って受け取ったレコードの数。
* **Invalid Records**: データセットで拒否されたレコードの数。これには、数値フィールドで文字列を使用するなどの形式が不正なデータや、ハッシュ基準に準拠していないレコードが含まれます。詳細については、[Amazon DSP: ハッシングのためのオーディエンスファイルの形式](https://advertising.amazon.com/help/GCCXMZYCK4RXWS6C)を参照してください。
* **Match Records Percentage**: データセットで成功裏にマッチしたレコードの割合。マッチ率は、**Records Resolved** を **Records with Identity** で割ることによって計算されます。