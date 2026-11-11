---
title: Schema Appタグ構成ガイド
description: この記事では、タグ管理アカウントでSchema Appタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/schema-app-tag/
---
## タグに関するヒント

* アカウントIDは、アプリケーションの **Integrations > JavaScript** で確認できます。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[about-tags](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、以下の項目を構成します。

* **アカウントID**：Schema AppのアカウントID。
* **出力キャッシュ**：出力キャッシュを有効にします。デフォルト値は`False`です。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリーは以下のとおりです。

### 標準

|変数| 型 | 説明|
|---| ---| ---|
| `account_id` | 文字列 | アカウントID。|
| `output_cache` | ブール値 | 出力キャッシュを有効にします。|
| `base_url` | 文字列 | ベースURL/APIエンドポイント。|