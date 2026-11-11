---
title: Eloquaタグ構成ガイド
description: この記事では、Eloquaタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/eloqua-tag/
---
## タグ構成のヒント

* Eloqua JavaScript（JS）ファイルがDOM Ready時に実行されるように、**Wait = Yes**のデフォルト構成を維持します。
* フォームトラッキングでは、マッピングを使用して次のパラメーターに値を構成します。
  * `form_tracking`（オン）
  * `elqFormName`
  * `elqFormGUIDElement`

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[about-tags](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、次の項目を構成します。

* **サイトID**：サイトID番号。
* **ファーストパーティCookieのドメイン名**：ファーストパーティCookieのドメイン名。

## ロードルール

すべてのページでタグをロードするか、タグをロードする条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリーは次のとおりです。

### 標準

| 変数 | 説明 |
|:---------|:------------|
| `form_tracking` | フォームトラッキング。 |
| `elqFormName` | フォーム名。 |
| `elqFormGUIDElement` | フォーム要素。 |
| `base_url` | JavaScriptファイルのURL。 |
| `elqDomainName` | ファーストパーティCookieのドメイン名。 |
| `page_url` | ページURL。 |