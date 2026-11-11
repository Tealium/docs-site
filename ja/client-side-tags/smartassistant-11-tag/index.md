---
title: SMARTASSISTANT 1.1タグ構成ガイド
description: この記事では、タグ管理アカウントでSMARTASSISTANT 1.1タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/smartassistant-11-tag/
---
SMARTASSISTANTを使用すると、企業は専門的なアドバイスを迅速に提供するためのガイド付き販売ソリューションを作成できます。また、購入者は役立つサポートをすぐに受けられるため、より確信を持って賢明な購入判断を下せます。

## タグに関するヒント

マッピングを使用して、標準の構成値を動的に上書きします。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、次の構成を構成します。

* **Advisor Code**：SMARTASSISTANTから提供されたAdvisor Code。
* **Subdomain**：アドバイザーコンテキストパスの最初の部分。  
例：`//{subdomain}.smartassistant.com/advisor-fe-web`
* **Div ID**：`advisor-container` divが追加されるページ上のDiv ID。
* **Advisor Container Div ID**：アドバイザーが配置される、ページ上の統合コンテナ。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

| 変数                     | 説明             |
|:-------------------------|:-----------------|
| Advisor Code             | (`advisorCode`)  |
| Subdomain                | (`subdomain`)    |
| Div ID                   | (`divId`)        |
| Advisor Container Div ID | (`advisorDivId`) |