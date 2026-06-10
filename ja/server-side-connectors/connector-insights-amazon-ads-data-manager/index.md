---
title: コネクターインサイト：Amazon Ads Data Manager
description: Amazon Ads Data Managerのインサイトにアクセスして、オーディエンスデータセットのメトリクスを確認します。
url: https://docs.tealium.com/ja/server-side-connectors/connector-insights-amazon-ads-data-manager/
---
## 概要

Amazon Ads Data Managerコネクターインサイトは、Amazon Adsとの統合であり、Tealiumにオーディエンスデータセットのメトリクスを取り込みます。

## アクセス

コネクターインサイトにアクセスするには、**Connect &gt; Audience Connectors** に移動し、Amazon Ads Data Managerコネクターアクションを見つけて、**Insights** をクリックします。

![](/images/server-side-connectors/connector-insights-btn.png)

## メトリクス

インサイトのサマリーには、以下のデータセットメトリクスが表示されます：

* **Upload Count**: このデータセットのレコードの総数。これには、オーディエンス削除リクエスト、IDなしのレコード、形式が不正なレコードが含まれます。
* **Accepted Count**: このデータセットで受け入れられたレコードの数。
* **Records Resolved**: このデータセットで認識されたユーザーにマッチしたレコードの数。これには重複が含まれます。同じユーザーに対して複数のレコードをアップロードした場合、アイデンティティに解決された各ユーザーレコードがカウントされます。
* **Records with Identity**: このデータセットで識別子を持って受け取られたレコードの数。
* **Invalid Records**: 形式が不正なデータ（例えば、数値フィールドに文字列を使用する）やハッシュ基準に準拠していないために拒否されたデータセット内のレコードの数。詳細については、[Amazon DSP: ハッシュ用のオーディエンスファイルの形式](https://advertising.amazon.com/help/GCCXMZYCK4RXWS6C)を参照してください。
* **Match Records Percentage**: データセットで成功裏にマッチしたレコードの割合。マッチ率は、**Records Resolved** を **Records with Identity** で割ることによって計算されます。