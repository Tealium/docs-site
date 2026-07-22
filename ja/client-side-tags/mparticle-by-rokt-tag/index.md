---
title: mParticle by Rokt タグ構成ガイド
description: この記事では、Tealium iQ タグ管理アカウントで mParticle by Rokt タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/mparticle-by-rokt-tag/
---
## タグのヒント

マッピングを使用してください:
  * イベントトリガーを構成します。
  * イベント固有のパラメータをイベント名にマップします。
  * 標準構成値を動的にオーバーライドします。
  * E-Commerce 拡張値を動的にオーバーライドします。

## タグの構成

タグマーケットプレイスにアクセスして新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、以下の構成を構成します:

* **mParticle API Key**: あなたの mParticle API キー。
* **Development Mode**: 非本番環境の場合は `True` に構成します。
* **Send Page View**: タグがロードされるたびにページビューイベントを自動的に追跡するために `True` に構成します。
* **First-Party Domain**: (オプション) Rokt カスタムドメイン。Rokt ファーストパーティドメイン統合を使用する場合、カスタムドメインを入力します。例: `rkt.yourcompany.com`。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数へデータを送信するプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは以下の通りです:

### タグ構成

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `account_id` | 文字列 | mParticle アカウントID。 |
| `isDevelopmentMode` | ブール値 | 開発モード。 |
| `domain` | 文字列 | ファーストパーティドメイン。 |

### ユーザーID

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `userIdentities.email` | 文字列 | メールアドレス。 |
| `userIdentities.other` | 文字列 | ハッシュ化されたメールアドレス。 |

### ユーザー属性

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `firstname` | 文字列 | 名前。 |
| `lastname` | 文字列 | 姓。 |
| `mobile` | 文字列 | 携帯番号。 |
| `age` | 文字列 | 年齢。 |
| `gender` | 文字列 | 性別。 |
| `city` | 文字列 | 市区町村。 |
| `state` | 文字列 | 州。 |
| `zip` | 文字列 | 郵便番号。 |
| `dob` | 文字列 | 生年月日。 |
| `title` | 文字列 | 職位。 |
| `language` | 文字列 | 言語。 |
| `value` | 文字列 | 価値。 |
| `predictedltv` | 文字列 | 予測LTV。 |
| `cartItems` | 文字列の配列 | カートアイテムの配列。 |

### ページビュー属性

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `pageName` | 文字列 | ページ名。 |
| `url` | 文字列 | URL。 |

### E-Commerce

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `confirmationref` | 文字列 | 確認番号（`_corder`をオーバーライド）。 |
| `amount` | 文字列 | 金額（`_csubtotal`をオーバーライド）。 |
| `currency` | 文字列 | 通貨（`_ccurrency`をオーバーライド）。 |

### イベント固有のパラメータ

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください

| イベント | 説明 |
|:------|:------------|
| `email` | メールアドレス。 |
| `firstname` | 顧客の名前。 |
| `lastname` | 顧客の姓。 |
| `paymenttype` | 支払いタイプ。 |
| `shippingtype` | 配送タイプ。 |
| `ccbin` | クレジットカードBIN。 |
| `billingaddress1` | 請求先住所。 |
| `billingaddress2` | 請求先住所2行目。 |
| `billingzipcode` | 請求先郵便番号。 |
| `mobile` | 携帯/セル。 |
| `country` | 国。 |
| `language` | 言語。 |
| `age` | 年齢。 |
| `gender` | 性別。 |
| `identifier` | ページ識別子。 |
| `cartItems` | カートアイテムの配列。 |
| `pageView` | ページビュー。 |
| `selectPlacements` | 配置を選択。 |
