---
title: SMARTASSISTANT 1.1 タグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでSMARTASSISTANT 1.1タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/smartassistant-11-tag/
---
SMARTASSISTANTを使用すると、ビジネスは専門的なアドバイスをより迅速に共有するためのガイド付き販売ソリューションを作成でき、ショッパーはより自信を持って賢い購入決定をするための有益で即時のサポートを受けることができます。

## タグのヒント

マッピングを使用して、標準の構成値を動的に上書きします。

## タグ構成

まず、Tealiumのタグマーケットプレイスに移動し、SMARTASSISTANT 1.1タグを追加します（[タグの追加方法]()について詳しくはこちら）。

タグを追加した後、以下の構成を行います：

* **アドバイザーコード**：SMARTASSISTANTから提供されたアドバイザーコード。
* **サブドメイン**：アドバイザーコンテキストパスの最初の部分。  
例：`//{subdomain}.smartassistant.com/advisor-fe-web`
* **Div ID**：`advisor-container` divが追加されるページ上のDiv IDです。
* **アドバイザーコンテナDiv ID**：アドバイザーが配置されるページ上の統合コンテナです。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

| 変数                     | 説明             |
|:-------------------------|:-----------------|
| アドバイザーコード       | (`advisorCode`)  |
| サブドメイン             | (`subdomain`)    |
| Div ID                   | (`divId`)        |
| アドバイザーコンテナDiv ID | (`advisorDivId`) |
