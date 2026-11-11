---
title: Comscoreタグ構成ガイド
description: この記事では、Comscoreタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/comscore-tag/
---
## タグに関するヒント

* ファーストパーティCookie機能はデフォルトで有効になっています。この動作を変更するには、`enableFirstPartyCookie`を`false`に構成します。
* IABの透明性と同意に関するフレームワーク（TCF）バージョン2.0を実装する同意管理プラットフォーム（CMP）を使用している場合、ComscoreタグはCMPと連携してユーザーの同意を自動的に収集します。
* `cs_ucfr`パラメーターを`0`（同意なし）または`1`（同意あり）に構成することで、訪問の同意を手動で指定できます。
* ファーストパーティCookie機能が有効な場合、Publisher Tagは利用可能なユーザー同意シグナルを確認し、Cookieの構成が許可されているかどうかを判断します。Webサイトまたはパブリッシャーがユーザー同意要件の適用対象外であることを示すには、`bypassUserConsentRequirementFor1PCookie`を`true`に構成します。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の項目を構成します。

* **ComscoreパブリッシャーID**：Comscoreから提供される7桁以上の番号で、パブリッシャーごとに一意です。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

| 変数 | 型 | 説明 |
|:---------|:-----|:------------|
| `c2` | 文字列 | ComscoreパブリッシャーID |
| `enableFirstPartyCookie` | `String` | ファーストパーティCookieを有効化 |
| `bypassUserConsentRequirementFor1PCookie` | `String` | ユーザー同意を省略 |
| `cs_ucfr` | 文字列 | 同意 |

### 自動収集データ

| 変数 | 型 | 説明 |
|:---------|:-----|:------------|
| `c7` | 文字列 | ページの完全なURL |
| `c8` | 文字列 | 参照元URL |
| `cs_fpcu` | 文字列 | ファーストパーティの`_scor_uid` Cookie値 |

### デモグラフィックデータ

| 変数 | 型 | 説明 |
|:---------|:-----|:------------|
| `cs_fpid` | 文字列 | ファーストパーティ識別子 |
| `cs_fpit` | 文字列 | 識別子の種類 |
| `cs_fpdm` | 文字列 | ファーストパーティのデモグラフィックデータ |
| `cs_fpdt` | 文字列 | デモグラフィックデータの種類 |