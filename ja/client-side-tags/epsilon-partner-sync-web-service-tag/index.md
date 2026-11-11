---
title: Epsilon Partner Sync Web Serviceタグ構成ガイド
description: この記事では、タグ管理アカウントでEpsilon Partner Sync Web Serviceタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/epsilon-partner-sync-web-service-tag/
---

Epsilonは、マーケターによる測定可能なビジネス成果の予測、実現、実証を50年にわたって支援してきた豊富な実績を持つ、成果重視型マーケティングのリーダーです。

## タグの構成

タグマーケットプレイスに移動し、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を行います。

* **広告主識別子**：`dtm_cid`
* **セカンダリ広告主識別子**：`dtm_cmagic`
* **ページ訪問フォームID**：`dtm_fid`

## データマッピング

データマッピングでは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### タグの構成

| 変数 | データ型 | 説明 |
|---|---|---|
| `dtm_cid` | 文字列 | 会社ID |
| `dtm_cmagic` | 文字列 | セカンダリ会社ID |
| `dtm_fid` | 文字列 | フォームID |
| `dtm_cookie_id` | 文字列 | Cookie ID |
| `dtm_user_id` | 文字列 | ユーザーID |
| `dtm_token_sc` | 文字列 | dtm_token_sc |
| `dtmc_tcf_string` | 文字列 | dtmc_tcf_string |
| `cachebuster` | 文字列 | キャッシュバスター |