---
title: Amazon Advertising Cookie Matching Serviceタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでAmazon Advertising Cookie Matching Serviceタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/amazon-advertising-cookie-matching-service-tag/
---
 このタグを`utag`バージョン4.50以降で使用する場合、`utag.js`の[`always_set_v_id`構成]()を`true`に構成する必要があります。この構成により、訪問IDがクッキー同期に利用可能になります。詳細については、[utag 4.50リリースノート]()および[utag 4.50&#43;へのアップグレード時のtealium_visitor_idに関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。

Amazon Advertising Cookie Matching Serviceは、ユーザーがTealium Visitor IDをAmazonシステム内のAmazon cookie IDと関連付けることを可能にします。その後、Tealium Visitor IDはAmazon Advertising DSP AudienceStreamコネクタ構成の識別子として使用できます。

## タグのヒント

* このタグは、Tealium訪問セッションごとに一度だけ発火します。
* AmazonはTealium Visitor IDを受け取り、それをAmazon Cookie IDとマッチングします。その後、Tealium Visitor IDはAmazon Advertising DSP AudienceStreamコネクタでクッキー識別子として使用できます。

## タグ構成

新しいタグを追加するために、タグマーケットプレイスに移動します。詳細については、[タグについて]()を参照してください。

タグを追加する際には、以下の構成を行います：

* **Region**: データ収集の地理的な地域。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて]()を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数にデータを送信するプロセスです。詳細については、[データマッピングについて]()を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
| `region`  | String | 地域  |
| `tealium_visitor_id`  | String | Tealium訪問ID  |
