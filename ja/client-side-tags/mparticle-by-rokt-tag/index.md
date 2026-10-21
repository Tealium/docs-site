---
title: mParticle by Rokt タグ構成ガイド
description: この記事では、Tealiumタグ管理アカウントでmParticle by Roktタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/mparticle-by-rokt-tag/
---
## タグのヒント

マッピングを使用してください:
  * イベントトリガーを構成します。
  * イベント固有のパラメータをイベント名にマップします。
  * 標準構成値を動的に上書きします。
  * Eコマース拡張値を動的に上書きします。


<blockquote>
新しいアイデンティティ、属性、および配置マッピングを使用するには、タグテンプレートの更新が必要です。既存のマッピングは古いテンプレートで引き続き機能します。
</blockquote>


## タグの構成

タグマーケットプレイスにアクセスして新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、以下の構成を構成します:

* **mParticle API Key**: あなたのmParticle APIキー。
* **Development Mode**: 非本番環境の場合は `True` に構成します。
* **Send Page View**: タグがロードされるたびにページビューイベントを自動的に追跡するには `True` に構成します。
* **First-Party Domain**: (オプション) Roktカスタムドメイン。Roktファーストパーティドメイン統合を使用する場合は、カスタムドメインを入力します。例: `rkt.yourcompany.com`。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数へデータを送信するプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは以下の通りです:

### タグ構成

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `account_id` | 文字列 | mParticleアカウントID。 |
| `isDevelopmentMode` | ブール値 | 開発モード。 |
| `domain` | 文字列 | ファーストパーティドメイン。 |

### ユーザーID

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `userIdentities.email` | 文字列 | メールアドレス。 |
| `userIdentities.email_sha256` | 文字列 | ハッシュ化されたメールアドレス。 |
| `userIdentities.mobile_number` | 文字列 | E.164形式の携帯電話番号。 |
| `userIdentities.mobile_sha256` | 文字列 | ハッシュ化された携帯電話番号。 |
| `userIdentities.customerid` | 文字列 | 顧客またはアカウント識別子。 |
| `userIdentities.other` | 文字列 | (非推奨) ハッシュ化されたメールアドレス。`userIdentities.email_sha256`を代わりに使用してください。 |

### ユーザー属性

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `firstname` | 文字列 | 名前。 |
| `firstnamesha256` | 文字列 | ハッシュ化された名前。 |
| `lastname` | 文字列 | 姓。 |
| `lastnamesha256` | 文字列 | ハッシュ化された姓。 |
| `mobile_number` | 文字列 | 携帯電話番号。 |
| `mobilesha256` | 文字列 | ハッシュ化された携帯電話番号。 |
| `mobile` | 文字列 | (非推奨) 携帯電話番号。`mobile_number`を代わりに使用してください。 |
| `age` | 文字列 | 年齢。 |
| `gender` | 文字列 | 性別。 |
| `city` | 文字列 | 市。 |
| `state` | 文字列 | 州。 |
| `zip` | 文字列 | 郵便番号。 |
| `zipsha256` | 文字列 | ハッシュ化された郵便番号。 |
| `zip4sha256` | 文字列 | ハッシュ化された郵便番号+4。 |
| `billingzipsha256` | 文字列 | ハッシュ化された請求郵便番号。 |
| `billingzip4sha256` | 文字列 | ハッシュ化された請求郵便番号+4。 |
| `dob` | 文字列 | 生年月日。 |
| `title` | 文字列 | 肩書き。 |
| `language` | 文字列 | 言語。 |
| `value` | 文字列 | 価値。 |
| `predictedltv` | 文字列 | LTV。 |

### ページビュー属性

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `pageName` | 文字列 | ページ名。 |
| `url` | 文字列 | URL。 |

### Eコマース

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `confirmationref` | 文字列 | 確認番号（`_corder`を上書き）。 |
| `amount` | 文字列 | 金額（`_csubtotal`を上書き）。 |
| `currency` | 文字列 | 通貨（`_ccurrency`を上書き）。 |

### 配置を選択

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `identifier` | 文字列 | Rokt配置識別子。 |
| `cartItems` | オブジェクトの配列 | カート内のアイテム。各アイテムは構造化されたオブジェクトです。 |

### イベント固有のパラメータ

| パラメータ | 説明 |
|:------|:------------|
| `email` | メール |
| `firstname` | 顧客の名前 |
| `lastname` | 顧客の姓 |
| `paymenttype` | 支払いタイプ |
| `shippingtype` | 配送タイプ |
| `shippingmethod` | 配送方法 |
| `paymentServiceProvider` | 支払いサービスプロバイダ |
| `ccbin` | ccbin |
| `billingaddress1` | 請求先住所 |
| `billingaddress2` | 請求先住所2 |
| `billingzipcode` | 請求先郵便番号 |
| `mobile` | 携帯/セル |
| `mobile_number` | 携帯番号 |
| `mobilesha256` | 携帯SHA256 |
| `firstnamesha256` | 名前SHA256 |
| `lastnamesha256` | 姓SHA256 |
| `zipsha256` | 郵便番号SHA256 |
| `zip4sha256` | 郵便番号4SHA256 |
| `billingzipsha256` | 請求郵便番号SHA256 |
| `billingzip4sha256` | 請求郵便番号4SHA256 |
| `country` | 国 |
| `language` | 言語 |
| `age` | 年齢 |
| `gender` | 性別 |
| `identifier` | ページ識別子 |
| `cartItems` | カートアイテム |
| `pageView` | ページビュー |
| `selectPlacements` | 配置を選択 |