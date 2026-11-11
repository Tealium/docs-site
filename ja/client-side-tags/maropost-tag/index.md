---
title: Maropostタグ構成ガイド
description: この記事では、Maropostタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/maropost-tag/
---
## タグの構成

まず、タグマーケットプレイスに移動し、Maropost Web Trackingタグをプロファイルに追加します（[タグの追加](https://docs.tealium.com/manage-tags/#add-a-tag)を参照）。

タグを追加する際は、以下の項目を構成します。

* Account ID：MaropostアカウントIDに対応する整数
* Website ID：トラッキング対象の特定のWebサイトに対応する整数
* Tracking Script File Name：Webトラッキング用JavaScript関数のファイル名を安全に難読化した文字列。アカウントおよびWebサイトごとに一意です。ファイル名にはスクリプトのバージョンが埋め込まれています。

## 読み込みルール

[読み込みルール](https://docs.tealium.com/about-load-rules/)では、サイト上でこのタグのインスタンスをいつ、どこで読み込むかを指定します。

推奨される読み込みルール：**すべてのページ**

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

Maropost Web Trackingタグの宛先変数は、**Data Mapping**タブに組み込まれています。使用可能なカテゴリは次のとおりです。

### 標準

|**宛先名**| **説明**|
|---| ---|
|Account ID| MaropostアカウントID。構成値を上書きする場合に使用します。|
|Website ID| WebサイトのID。ベンダー構成値を動的に上書きする場合に使用します。|
|Tracking Script File Name| Webトラッキング関数のファイル名を安全に難読化した文字列。構成値を動的に上書きする場合に使用します。|