---
title: InvocaJS Web Integrationタグ構成ガイド
description: この記事では、TealiumアカウントでInvocaJS Web Integrationタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/invocajs-web-integration-tag/
---## タグに関するヒント

* Invoca Network IDとTag IDには、数値のみを使用できます。
* カスタムマーケティングデータを保持するには、マッピングを使用します。
* 変数をタグにマッピングした後、Invocaユーザーインターフェイスで対応するMarketing dataフィールドを追加します。
  * Marketing dataフィールドの追加については、Invocaの担当者にお問い合わせください。
  * Marketing dataフィールド名は、データマッピングと一致している必要はありません。
  * Data Source Typeは**JavaScript Data Layer**に構成します。
  * Data Source Nameは`localStorage.getItem("inv_TEALIUM_MAPPING")`に構成します。  

<blockquote>
`TEALIUM_MAPPING` must match the name of your custom data mapping.
</blockquote>


## タグの構成

新しいタグを追加するには、タグマーケットプレイスに移動します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を行います。

* **Invoca Network ID**
  * Invoca Network IDは、Invocaネットワーク（アカウント）に割り当てられる一意のIDです。
* **Invoca Tag ID**
  * Invoca Tag IDは、Invoca Network内で作成した各タグに割り当てられる一意のIDです。
* **データセンター**：データセンターのリージョンによって、タグを配信するInvocaコンテンツ配信ネットワーク（CDN）が決まります。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。