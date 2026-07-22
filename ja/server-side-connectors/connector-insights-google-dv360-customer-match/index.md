---
title: コネクターインサイト：Google DV360 カスタマーマッチコネクター
description: この記事では、Google DV360 カスタマーマッチコネクターのコネクターインサイトにアクセスし、インサイトデータを探索する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/connector-insights-google-dv360-customer-match/
---
Google DV360 カスタマーマッチコネクターインサイトは、Google DV360 カスタマーマッチコネクターと統合し、Googleからあなたのアカウントにユーザーリストデータをもたらします。Google DV360 カスタマーマッチコネクターのインサイトは、Googleによって受信されたユーザーリストデータを要約します。これらのインサイトは、ユーザーリストの名前とサイズの要約で提示されます。

## コネクターインサイトへのアクセス

**Connect > Connectors** に移動し、**Google DV360 カスタマーマッチ** コネクターを見つけ、アクションを選択します。アクション画面で、**Insights** タブをクリックします。

![](https://docs.tealium.com/images/server-side-connectors/insights/using-connector-insights-google-dv360-customer-match.png)

## カスタマーマッチインサイト

Google DV360 カスタマーマッチインサイトは、コネクターアクションで構成されたGoogle DV360リストに関する情報を提供します。

* **ディスプレイ用サイズ**: このユーザーリストのGoogleディスプレイネットワークにおける推定ユーザー数。
* **検索用サイズ**: このユーザーリストのGoogleドメインにおける推定ユーザー数で、Google DV360検索キャンペーンでターゲティング可能です。ユーザー数がまだ確定していない場合、これらの値はnullになります。
* **マッチ率パーセンテージ**: カスタマーマッチリストのマッチ率を示します。ユーザー数がまだ確定していない場合、これらの値はnullになります。

![](https://docs.tealium.com/images/server-side-connectors/insights/values-connector-insights-google-dv360-customer-match.png)

## オーディエンス情報

Google DV360 カスタマーマッチインサイトは、[Google Ads API searchStream](https://developers.google.com/google-ads/api/fields/v14/user_list) を使用して、構成されたオーディエンスに関する情報を提供します。

| 列 |  説明 |
| ----- |----- |
| リスト名 |  ユーザーリストの名前| 
| 説明| ユーザーリストの説明| 
| メンバーシップステータス| ユーザーリストがオープンまたはアクティブかどうかを示します。オープンなユーザーリストのみがさらにユーザーを蓄積し、ターゲティングされることができます。| 
| ディスプレイ用サイズ| このユーザーリストのGoogleディスプレイネットワークにおける推定ユーザー数。ユーザー数がまだ確定していない場合、この値はnullです。| 
| 検索用サイズ| このユーザーリストのGoogleドメインにおける推定ユーザー数。これらは検索キャンペーンでターゲティング可能なユーザーです。ユーザー数がまだ確定していない場合、この値はnullです。| 


<blockquote>
Tealiumは、Google DV 360から直接リスト統計を取得しますが、このインサイトと[Google DV 360 カスタマーマッチコネクター](https://docs.tealium.com/google-dv-360-customer-match-connector/)のコネクターリクエストの総量との間に差が生じることがあります。
</blockquote>


## オフラインユーザーデータジョブ

**Job ID** の要約は、Google DV360プラットフォームでのレコードの処理状況を示します。

![](https://docs.tealium.com/images/server-side-connectors/insights/connector-insights-google-dv360-customer-match-offline-user-data-jobs.png)

## 追加リソース

* [Google Ads: カスタマーマッチについて](https://support.google.com/google-ads/answer/6379332?hl=ja)
* [Google Display & Video 360: カスタマーマッチオーディエンス](https://support.google.com/displayvideo/answer/9539301)
* [Google Ads API: user_list](https://developers.google.com/google-ads/api/fields/v14/user_list)
* [google-dv-360-customer-match-connector](https://docs.tealium.com/google-dv-360-customer-match-connector/)