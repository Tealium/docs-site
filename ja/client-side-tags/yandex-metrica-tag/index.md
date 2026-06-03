---
title: Yandex.Metricaタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでYandex.Metricaタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/yandex-metrica-tag/
---
Yandex.Metricaは、サイトのコンバージョン率を向上させるための無料ツールです。Metricaを使用すると、ウェブサイトの主要な効果指標を監視し、ユーザーの行動を分析し、広告キャンペーンの効率を評価することができます。

## タグのヒント

マッピングを使用して、標準の構成値を動的に上書きします。

## タグの構成

新しいタグを追加するために、タグマーケットプレイスに移動します。タグの追加方法については、[タグの概要]()の記事を参照してください。

タグを追加する際には、以下の構成を行います：

* **タグID**: YandexタグID
* **クリックマップ**: サイト上のユーザー活動の詳細な記録：マウスの動き、スクロール、クリック
* **リンクの追跡**: 外部リンクとダウンロードリンクの追跡構成
* **正確なバウンス率の追跡**: 15000ミリ秒（15秒）後に非バウンスイベントが登録される、正確なバウンス率を有効にする
* **Webvisor**: Webvisorはユーザーの行動をビデオ形式で再現し、彼らがサイトで何をしているかを知らせます：ページの移動方法、マウスカーソルの移動方法、リンクのクリック方法。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。ロードルールについての詳細は、[ロードルール]()のドキュメンテーションを参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数へのデータ送信のプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング]()を参照してください。

利用可能なカテゴリーは以下の通りです：

### 標準

| 変数 | 説明 |
| --- | --- |
| Base Url (base\_url) | \[文字列\] |
| Hit Event Url (url) | \[文字列\] |
| Tag ID (tagId) | \[文字列\] |
| Click Map (clickmap) | \[ブール値\] |
| Track Links (trackLinks) | \[ブール値\] |
| Accurate Track Bounce (accurateTrackBounce) | \[ブール値\] |
| Webvisor (webvisor) | \[ブール値\] |
| E-commerce Data Layer (ecommerce) | \[文字列/ブール値\] |

### E-commerce

| 変数 | 説明 |
| --- | --- |
| Order Id (order\_id) (override \_corder) | \[文字列/数値\] |
| Order Coupon Code (order\_coupon\_code) (override \_cpromo) | \[文字列\] |
| Order Total (order\_total) (override \_ctotal) | \[数値/文字列\] |
| Order Currency (order\_currency) (override \_ccurrency) | \[文字列\] |
| Goal ID (goal\_id) | \[数値/文字列\] |
| List of Product IDs (id) (override \_csku) | \[配列\] |
| List of Product Names (name) (override \_cprodname) | \[配列\] |
| List of Product Brands (brand) (override \_cbrand) | \[配列\] |
| List of Product Categories (category) (override \_ccat) | \[配列\] |
| List of Product Coupons (coupon) | \[配列\] |
| List of Product Prices (price) (override \_cprice) | \[配列\] |
| List of Product Quantities (quantity) (override \_cquan) | \[配列\] |
| List of Product Positions (position) | \[配列\] |
| List of Product Variants (variant) | \[配列\] |

### イベント

イベントのマッピングについては、[イベントマッピングの作成](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

| 変数 | 説明 |
| --- | --- |
| Hit (Send Page View Event) (hit) | hit |
| View Product (detail) | detail |
| Add Product (add) | add |
| Remove Product (remove) | remove |
| Purchase (purchase) | purchase |

### イベント固有のパラメータ

イベントのマッピングについては、[イベントマッピングの作成](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

| 変数 | 説明 |
| --- | --- |
| Hit (hit) | hit |
| View Product (detail) | detail |
| Add Product (add) | add |
| Remove Product (remove) | remove |
| Purchase (purchase) | purchase |

