---
title: Quantcast Cookie Matching Serviceタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでQuantcast Cookie Matching Serviceタグを構成する方法について説明します。このタグは、[Quantcast Audiences]({{< relref "quantcast-audiences-connector" >}})コネクタで使用するQuantcast IDを生成するために使用されます。
url: https://docs.tealium.com/ja/client-side-tags/quantcast-cookie-matching-service-tag/
---
 このタグを`utag`バージョン4.50以降で使用する場合、`utag.js`の[`always_set_v_id`構成]()を`true`に構成する必要があります。この構成により、訪問IDがクッキー同期に利用可能になります。詳細については、[utag 4.50リリースノート]()と[utag 4.50&#43;へのアップグレード時のtealium_visitor_idに関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。

Quantcast Cookie Matching Serviceは、Tealiumの匿名IDクッキーとQuantcastの訪問IDを関連付けます。

## タグのヒント

* 空白の場合、TealiumアカウントとTealiumプロファイルは現在のアカウントとプロファイルで自動的に入力されます。
* 標準の構成値を上書きするためにマッピングを使用します。
* カスタムマッピングはTealiumへのクッキー同期リクエストに含まれます。

## タグ構成

まず、タグマーケットプレイスに移動し、Quantcast Cookie Matching Serviceタグを追加します（[タグの追加方法]()について詳しくはこちら）。

タグを追加した後、以下の構成を行います：

* **アカウントコード**：アカウントコード（P-code）は、`p-`で始まる13文字の大文字小文字を区別する英数字のコードです。質問がある場合は、Quantcastの担当者にお問い合わせください。
* **Tealiumアカウント**：（オプション）あなたのTealiumアカウント名
* **Tealiumプロファイル**：（オプション）あなたのTealiumプロファイル名

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|アカウントコード| (`account_code`)|
|Tealiumアカウント| (`tealium_account`)|
|Tealiumプロファイル| (`tealium_profile`)|

## AudienceStream構成

このタグは、`quantcast_id`という名前のイベント属性を持つ各訪問に対して、セッションごとにサーバーサイドイベントを送信します。この属性を使用して、Quantcast Audiencesコネクタで使用する同じ名前の訪問属性を作成します。

![](/images/client-side-tags/quantcast-id-attribute.png)

AudienceStreamでQuantcast IDを構成するには：

1. `quantcast_id`という名前の文字列イベント属性を作成します。
1. イベント属性から値を構成するエンリッチメントを持つ`quantcast_id`という名前の文字列訪問属性を作成します。
1. Quancast Audiencesコネクタで、訪問属性`quantcast_id`をQuancast Cookie User IDパラメータにマッピングします。
