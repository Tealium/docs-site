---
title: mParticle by Roktタグ構成ガイド
description: この記事では、Tealiumタグ管理アカウントでmParticle by Roktタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/mparticle-by-rokt-tag/
---
## タグに関するヒント

マッピングを使用して、以下を行います。
  * イベントトリガーを構成する。
  * イベント固有のパラメータをイベント名にマッピングする。
  * 標準構成値を動的に上書きする。
  * Eコマース拡張機能の値を動的に上書きする。


<blockquote>
v3アップデートで追加された新しいID、属性、プレースメントのマッピングを使用するには、タグテンプレートの更新が必要です。既存のマッピングは、古いテンプレートでも引き続き機能します。
</blockquote>


## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、以下を構成します。

* **mParticle APIキー**：mParticle APIキー。
* **開発モード**：非本番環境では、開発モードを`True`に構成します。
* **ページビューを送信**：タグが読み込まれるたびにページビューイベントを自動的に追跡するには、`True`に構成します。
* **ファーストパーティドメイン**：（任意）Roktカスタムドメイン。Roktのファーストパーティドメイン連携を使用する場合は、カスタムドメインを入力します。例：`rkt.yourcompany.com`。

## ロードルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは以下のとおりです。

### タグの構成

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `account_id` | 文字列 | mParticleアカウントID。 |
| `isDevelopmentMode` | ブール値 | 開発モード。 |
| `domain` | 文字列 | ファーストパーティドメイン。 |

### ユーザーID

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `userIdentities.email` | 文字列 | メールアドレス。 |
| `userIdentities.email_sha256` | 文字列 | ハッシュ化されたメールアドレス。 |
| `userIdentities.mobile_number` | 文字列 | E.164形式の携帯電話番号。 |
| `userIdentities.mobile_sha256` | 文字列 | ハッシュ化された携帯電話番号。 |
| `userIdentities.customerid` | 文字列 | 顧客またはアカウントの識別子。 |
| `userIdentities.other` | 文字列 | （非推奨）ハッシュ化されたメールアドレス。代わりに`userIdentities.email_sha256`を使用してください。 |

### ユーザー属性

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `firstname` | 文字列 | 名。 |
| `firstnamesha256` | 文字列 | ハッシュ化された名。 |
| `lastname` | 文字列 | 姓。 |
| `lastnamesha256` | 文字列 | ハッシュ化された姓。 |
| `mobile_number` | 文字列 | 携帯電話番号。 |
| `mobilesha256` | 文字列 | ハッシュ化された携帯電話番号。 |
| `mobile` | 文字列 | （非推奨）携帯電話番号。代わりに`mobile_number`を使用してください。 |
| `age` | 文字列 | 年齢。 |
| `gender` | 文字列 | 性別。 |
| `city` | 文字列 | 市区町村。 |
| `state` | 文字列 | 州。 |
| `zip` | 文字列 | 郵便番号。 |
| `zipsha256` | 文字列 | ハッシュ化された郵便番号。 |
| `zip4sha256` | 文字列 | ハッシュ化されたZIP+4コード。 |
| `billingzipsha256` | 文字列 | ハッシュ化された請求先郵便番号。 |
| `billingzip4sha256` | 文字列 | ハッシュ化された請求先ZIP+4コード。 |
| `dob` | 文字列 | 生年月日。 |
| `title` | 文字列 | 肩書。 |
| `language` | 文字列 | 言語。 |
| `value` | 文字列 | 値。 |
| `predictedltv` | 文字列 | LTV。 |

### ページビュー属性

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `pageName` | 文字列 | ページ名。 |
| `url` | 文字列 | URL。 |

### Eコマース

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `confirmationref` | 文字列 | 確認番号（`_corder`を上書き）。 |
| `amount` | 文字列 | 金額（`_csubtotal`を上書き）。 |
| `currency` | 文字列 | 通貨（`_ccurrency`を上書き）。 |

### プレースメントの選択

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `identifier` | 文字列 | Roktプレースメント識別子。 |
| `cartItems` | オブジェクトの配列 | カートの明細項目。各項目は構造化オブジェクトです。 |

### イベント固有のパラメータ

| パラメータ | 説明 |
|:------|:------------|
| `email` | メールアドレス |
| `firstname` | 顧客の名 |
| `lastname` | 顧客の姓 |
| `paymenttype` | 支払いタイプ |
| `shippingtype` | 配送タイプ |
| `shippingmethod` | 配送方法 |
| `paymentServiceProvider` | 決済サービスプロバイダー |
| `ccbin` | ccbin |
| `billingaddress1` | 請求先住所 |
| `billingaddress2` | 請求先住所2 |
| `billingzipcode` | 請求先郵便番号 |
| `mobile` | 携帯電話 |
| `mobile_number` | 携帯電話番号 |
| `mobilesha256` | 携帯電話番号のSHA256 |
| `firstnamesha256` | 名のSHA256 |
| `lastnamesha256` | 姓のSHA256 |
| `zipsha256` | 郵便番号のSHA256 |
| `zip4sha256` | ZIP+4コードのSHA256 |
| `billingzipsha256` | 請求先郵便番号のSHA256 |
| `billingzip4sha256` | 請求先ZIP+4コードのSHA256 |
| `country` | 国 |
| `language` | 言語 |
| `age` | 年齢 |
| `gender` | 性別 |
| `identifier` | ページ識別子 |
| `cartItems` | カート項目 |
| `pageView` | ページビュー |
| `selectPlacements` | プレースメントの選択 |