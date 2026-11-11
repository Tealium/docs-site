---
title: Quantcast Cookie Matching Serviceタグ構成ガイド
description: この記事では、タグ管理アカウントでQuantcast Cookie Matching Serviceタグを構成する方法について説明します。このタグは、[Quantcast Audiences]({{< relref "quantcast-audiences-connector" >}})コネクタで使用するQuantcast IDを生成するために使用されます。
url: https://docs.tealium.com/ja/client-side-tags/quantcast-cookie-matching-service-tag/
---

<blockquote>
このタグを`utag`バージョン4.50以降で使用する場合は、`utag.js`の[`always_set_v_id`構成](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id)を`true`に構成する必要があります。この構成により、Cookieの同期に訪問IDを使用できるようになります。詳細については、[utag 4.50リリースノート](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later)および[utag 4.50以降へのアップグレード時のtealium_visitor_idに関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。
</blockquote>


Quantcast Cookie Matching Serviceは、Tealiumの匿名ID CookieをQuantcast訪問IDに関連付けます。

## タグに関するヒント

* 空白のままにすると、Tealium AccountとTealium Profileには現在のアカウントとプロファイルが自動的に入力されます。
* マッピングを使用して、標準の構成値を上書きします。
* カスタムマッピングは、TealiumへのCookie同期リクエストに含まれます。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、以下の構成を構成します。

* **Account Code**：Account Code（P-code）は、`p-`で始まる、大文字と小文字を区別する13文字の英数字コードです。ご不明な点がある場合は、Quantcastの担当者にお問い合わせください。
* **Tealium Account**：（任意）Tealium Account名
* **Tealium Profile**：（任意）Tealium Profile名

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### 標準

|変数|説明|
|---|---|
|Account Code|（`account_code`）|
|Tealium Account|（`tealium_account`）|
|Tealium Profile|（`tealium_profile`）|

## Customer Data Platform（CDP）の構成

このタグは、各訪問について、`quantcast_id`という名前のイベント属性を含むサーバーサイドイベントをセッションごとに1回送信します。この属性を使用して、Quantcast Audiencesコネクタで使用する同名の訪問属性を作成します。

![](https://docs.tealium.com/images/client-side-tags/quantcast-id-attribute.png)

CDPでQuantcast IDを構成するには、次の手順を実行します。

1. `quantcast_id`という名前の文字列型イベント属性を作成します。
1. `quantcast_id`という名前の文字列型訪問属性を作成し、イベント属性から値を構成するエンリッチメントを追加します。
1. Quancast Audiencesコネクタで、訪問属性`quantcast_id`をQuancast Cookie User IDパラメータにマッピングします。