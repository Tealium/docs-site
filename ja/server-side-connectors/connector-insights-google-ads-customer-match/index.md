---
title: コネクターインサイト：Google Ads カスタマーマッチ
description: インサイトは、ベンダーからの追加コネクターデータをTealiumアカウントに取り込み、そのパフォーマンスを評価するのに役立ちます。
url: https://docs.tealium.com/ja/server-side-connectors/connector-insights-google-ads-customer-match/
---
Google Ads カスタマーマッチコネクターインサイトは、Google Ads カスタマーマッチコネクターと統合し、Googleからのユーザーリストデータをあなたのアカウントに取り込みます。この記事では、この機能にアクセスしてデータを探索する方法を示します。

## コネクターインサイトの概要

Google Ads カスタマーマッチコネクターのインサイトは、Googleによって受信されたユーザーリストデータを要約します。これらのインサイトは、ユーザーリストの名前とそのサイズの要約で提示されます。

## カスタムオーディエンスパラメータ

Google Ads カスタマーマッチインサイトは、コネクターアクションで構成されたGoogle Adsリストについて、以下の情報を提供します：

* **ディスプレイ用サイズ** は、このリストに含まれるユーザーの数をGoogleディスプレイネットワーク上で推定します。
* **検索用サイズ** は、Googleドメインにおけるこのリストのユーザー数を推定し、Google Ads検索キャンペーンでターゲティング可能です。
* **マッチ率パーセンテージ** は、このリストのユーザーがGoogleユーザーと一致する割合を表示します。

ユーザー数がまだ確定していない場合、これらの値はnullです。

![](/images/server-side-connectors/connector-insights-google-ads-customer-match.png)

## コネクターインサイトの使用

コネクターインサイトにアクセスするには、**AudienceStream &gt; Audience Connectors** に移動し、**Google Ads Customer Match (Tealium-Provided Credentials) Connector** コネクターを検索して **Insights** をクリックします。

![](/images/server-side-connectors/connector-insights-btn.png)

## Google Ads カスタムオーディエンスインサイトの理解

Google Ads カスタマーマッチインサイトは、構成されたオーディエンスに関する情報を提供するために [Google Ads API user_list query](https://developers.google.com/google-ads/api/fields/v14/user_list) を実行します。

|**パラメータ**| **説明**|
|----|----|
| リスト名 | ユーザーリストの名前。 | 
| 説明 | ユーザーリストの説明。 | 
| メンバーシップステータス | ユーザーリストがオープンまたはアクティブかどうかを示します。オープンなユーザーリストのみがさらにユーザーを蓄積し、ターゲティングされることができます。 | 
| ディスプレイ用サイズ | Googleディスプレイネットワーク上のこのユーザーリストの推定ユーザー数。ユーザー数がまだ確定していない場合、この値はnullです。 | 
| 検索用サイズ | `google.com`ドメイン内のこのユーザーリストの推定ユーザー数。これらは検索キャンペーンでターゲティング可能なユーザーです。ユーザー数がまだ確定していない場合、この値はnullです。 | 

## オフラインユーザーデータジョブ

ジョブIDの概要は、Google Adsプラットフォームでのレコードの処理状況を示します：

![](/images/server-side-connectors/connector-insights-google-ads-customer-match-offline-user-data-jobs.png)

## 追加リソース

* [カスタマーマッチについて - Google Ads ヘルプ](https://support.google.com/google-ads/answer/6379332?hl=ja)
* [カスタマーマッチオーディエンス - Display &amp; Video 360 ヘルプ](https://support.google.com/displayvideo/answer/9539301)
* [Google Ads API: user_list](https://developers.google.com/google-ads/api/fields/v14/user_list)
* [Google Ads カスタマーマッチ (Tealium提供の資格情報) コネクター構成ガイド]()