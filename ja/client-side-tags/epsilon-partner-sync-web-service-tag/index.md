---
title: EpsilonパートナーシンクWebサービスタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでEpsilonパートナーシンクWebサービスタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/epsilon-partner-sync-web-service-tag/
---
Epsilonは、マーケターが予測、活性化、そして測定可能なビジネス成果を証明するのを支援する豊富な50年の歴史を持つ、結果ベースのマーケティングのリーダーです。

## タグ構成

まず、タグマーケットに移動し、EpsilonパートナーシンクWebサービスタグを追加します（[タグの追加方法](https://docs.tealium.com/manage-tags/)について詳しくはこちら）。

タグを追加した後、以下の構成を行います：

* **広告主識別子**： `dtm_cid`
* **セカンダリ広告主識別子**： `dtm_cmagic`
* **ページ訪問フォームID**： `dtm_fid`

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### タグ構成

| 変数 | データタイプ| 説明 |
|---|---|---|
| `dtm_cid`  | 文字列 |会社ID |
| `dtm_cmagic`  | 文字列 |セカンダリ会社ID |
|  `dtm_fid`  | 文字列 |フォームID|
| `dtm_cookie_id`  | 文字列 |クッキーID |
| `dtm_user_id`  | 文字列 |ユーザーID |
|  `dtm_token_sc`  | 文字列 |dtm_token_sc|
|  `dtmc_tcf_string`  | 文字列 |dtmc_tcf_string|
| `cachebuster`  | 文字列 |キャッシュバスター |
