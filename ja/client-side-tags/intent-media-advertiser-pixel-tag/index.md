---
title: Intent Media 広告主ピクセルタグ構成ガイド
description: この記事では、Tealium iQタグ管理（TiQ）アカウントでIntent Media広告主ピクセルタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/intent-media-advertiser-pixel-tag/
---## タグのヒント

* 以下のE-Commerce変数を使用します
  * `_corder`
  * `_csubtotal`/`_ctotal`
  * `_ccurrency`
  * `_ccustid`
* ページビュータイプ/ページカテゴリはマッピングで上書き可能です

## タグの構成

新しいタグを追加するためにタグマーケットプレイスに移動します。タグを追加する一般的な手順については、[タグの概要](https://docs.tealium.com/about-tags/)の記事を読んでください。

タグを追加する際には、以下の構成を行います：

* **エンティティID**
  * Intent Media広告主ピクセルによって構成されます。
* **ページビュータイプ**
  * 'HOME', 'LIST', 'DETAILS', 'CART', 'EMAIL', 'EMAIL_CONFIRMATION', 'CONVERSION', 'UNKNOWN'のいずれかでなければなりません。
* **製品カテゴリ**
  * 'HOME', 'FLIGHTS', 'CARS', 'HOTELS', 'PACKAGE', 'EMAIL', 'UNKNOWN'のいずれかでなければなりません。

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### スタンダード

|変数| 説明|
|---| ---|
|`Entity` ID|  <ul><li>エンティティID。</li><li>Intent Media広告主ピクセルによって構成されます。</li></ul> |
|`page_view_type`|  <ul><li>ページビュータイプ。</li><li>以下のいずれかでなければなりません：  <ul><li>HOME</li><li>LIST</li><li>DETAILS</li><li>CART</li><li>EMAIL</li><li>EMAIL\_CONFIRMATION</li><li>CONVERSION</li><li>UNKNOWN</li></ul> </li></ul> |
|`product_category`|  <ul><li>製品カテゴリ。</li><li>以下のいずれかでなければなりません：  <ul><li>HOME</li><li>FLIGHTS</li><li>CARS</li><li>HOTELS</li><li>PACKAGE</li><li>EMAIL</li><li>UNKNOWN</li></ul> </li></ul> |
|`page_id`|  <ul><li>ページID</li></ul> |

### E-Commerce

|変数| 説明|
|---| ---|
|`order_id`|  <ul><li>注文ID。</li><li>デフォルトの`_corder`を上書きします。</li></ul> |
|`order_subtotal`|  <ul><li>注文の小計。</li><li>デフォルトの`_csubtotal`を上書きします。</li></ul> |
|`currency`|  <ul><li>通貨。</li><li>デフォルトの`_ccurrency`を上書きします。</li></ul> |
|`custid`|  <ul><li>顧客ID。</li><li>デフォルトの`_ccustid`（`user_member_id`）を上書きします。</li></ul> |

