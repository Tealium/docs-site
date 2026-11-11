---
title: Yextコンバージョンタグ構成ガイド
description: この記事では、タグ管理アカウントでYextコンバージョンタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/yext-conversion-tag/
---## タグに関するヒント

* マッピングを使用して、標準の構成値を上書きします。
* IDマッピングに値が構成されている場合、コンバージョンが発生します。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリーは次のとおりです。

### 標準

|変数|説明|
|---|---|
|`optin`| <ul><li>オプトイン</li></ul> |
|`cid`| <ul><li>顧客識別番号（CID）</li></ul> |
|`value`| <ul><li>値</li></ul> |