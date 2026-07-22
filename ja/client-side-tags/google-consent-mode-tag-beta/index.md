---
title: Google Consent Modeタグ構成ガイド（BETA）
description: この記事では、Tealium iQタグ管理アカウントでGoogle Consent Modeタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/google-consent-mode-tag-beta/
---
Consent mode（ベータ版）を使用すると、ユーザーの同意状況に基づいてGoogleタグの動作を調整できます。AnalyticsとAdsのクッキーに対して同意が得られたかどうかを示すことができます。Googleのタグは動的に適応し、ユーザーから同意が得られた場合にのみ、指定された目的のための測定ツールを利用します。

## ヒント

Google Consent Modeタグがユーザーの同意状況に動的に適応するようにするために、以下を推奨します：
* Consent ManagementからGoogle Consent Modeタグを省略して、常に発火するようにします。
* Google Analytics、Ads、またはFloodlightタグを使用している場合、それらのタグもConsent Managementから省略します。

Google Consent Modeタグを構成する際には、以下を行います：
* **Automatically read from Tealium Consent Cookie**をtrueに構成します。
* Google AdsとGoogle Analyticsの同意値を適切なタグ変数にマッピングします。

## タグ構成

タグマーケットプレイスに移動して新しいタグを追加します。タグの追加方法については、[Tag Overview](https://docs.tealium.com/about-tags/)記事を参照してください。

タグを追加する際には、以下の構成を行います：

* **Automatically read from Tealium Consent Cookie**  
trueに構成すると、Googleの同意はTealium Consent Managerに基づいて構成されます。具体的な動作については、他の構成の説明を参照してください。
* **Ad Storage**  
Tealium Consent Managerとの統合が有効で、部分的な同意が与えられた場合、`ad_storage_consent`の値を`granted`に構成します。全面的な同意が与えられた場合、`granted`が構成されます。
* **Analytics Storage**  
Tealium Consent Managerとの統合が有効で、部分的な同意が与えられた場合、`analytics_storage_consent`の値を`granted`に構成します。全面的な同意が与えられた場合、`granted`が構成されます。
* **Ads Data Redaction Mapping**  
`ads_data_redaction`がtrueで、`ad_storage`が`denied`の場合、Google AdsおよびFloodlightタグによってネットワークリクエストで送信される広告クリック識別子が削除されます。
* **URL Passthrough**  
測定品質を向上させるために、URLパラメータをページ間で情報を渡すことを選択できます。
* **Wait For Update**  
同意ツールが非同期に読み込まれる場合、Googleタグが常に先に実行されるわけではありません。これを考慮に入れて、データを送信するまでの待機時間をミリ秒単位で指定するために`wait_for_update`を指定します。

## データマッピング

マッピングは、[data layer variable](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[data mappings](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|Read From Tealium Consent Cookie| [Boolean]|
|Ad Storage Consent (ad\_storage\_consent)| [String]|
|Analytics Storage Consent (analytics\_storage\_consent)| [String]|
|Ads Data Redaction Mapping (ads\_data\_redaction)| [Boolean]|
|URL Passthrough (url\_passthrough)| [Boolean]|
|Wait For Update (wait\_for\_update)| [Number]|

## ベンダー文書

* [About Google Consent Mode](https://support.google.com/analytics/answer/9976101?hl=en)
* [Google Developers: Adjust tag behavior based on consent](https://developers.google.com/gtagjs/devguide/consent)
