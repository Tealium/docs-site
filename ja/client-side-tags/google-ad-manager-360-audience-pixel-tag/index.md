---
title: Google Ad Manager 360 Audience Pixelタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでGoogle Ad Manager 360 Audience Pixelタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/google-ad-manager-360-audience-pixel-tag/
---
Google Ad Manager 360で広告を配信せずにファーストパーティのオーディエンスセグメントを作成するには、Audience Pixelタグをサイトやモバイルアプリに追加します。このピクセルタグは追加料金なしで使用でき、Ad Managerのインプレッションの配信に対して課金されることはありません。また、このタグを使用すると、Googleマーケティングプラットフォームのクッキーまたはモバイル広告IDの代わりに、パブリッシャーが提供する識別子（PPID）をオーディエンスセグメンテーションに使用できます。

## タグのヒント

* マッピングを使用してタグの構成を上書きまたは動的に構成します。
* パブリッシャーが提供するID（PPID）は、それに対してマップされた値が入力されている場合にのみURLに追加する必要があります。
* PPIDの値の要件は次のとおりです：
    * 英数字（`[0-9 a-z A-Z]`）またはUUID HEX表現（`8-4-4-4-12`）。（ハイフンが許可されています）
    * 次の正規表現を使用して値を強制することができます：`^([0-9a-zA-Z]{32,150})$|^([0-9a-fA-F]{8}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{12})$`

## タグの構成

新しいタグを追加するためにタグマーケットプレイスに移動します。タグの追加方法については、[タグの概要](https://docs.tealium.com/about-tags/)の記事を参照してください。

タグを追加する際には、以下の構成を行います：

* **ネットワークコード**：パブリッシャーのGoogle Ad Managerネットワーク識別子。**Admin > Global Settings**またはAd Manager URLで見つけることができます。
* **セグメントID**：セグメント識別子（`dc_seg`）。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。ロードルールについての詳細は、[ロードルール](https://docs.tealium.com/about-load-rules/)のドキュメンテーションを参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは次のとおりです：

### スタンダード

| 変数 | 説明 |
| --- | --- |
| ネットワークコード（`network_code`） | 文字列 |
| セグメントID（`segment_id`） | 文字列 |
| パブリッシャーが提供するID（`publisher_provided_id`） | 文字列 |


