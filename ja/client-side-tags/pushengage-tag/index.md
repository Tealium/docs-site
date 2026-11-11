---
title: PushEngageタグ構成ガイド
description: この記事では、タグ管理アカウントでPushEngageタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/pushengage-tag/
---
PushEngageは、コンテンツサイトの管理者が訪問を自動的にセグメント化し、Webプッシュメッセージを送信することで、訪問とのエンゲージメントを高めるのに役立つブラウザプッシュ通知プラットフォームです。このクラウドベースのツールは、通知トリガーの構成、顧客のセグメント化、自動応答、A/Bテストなどの機能を提供します。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を行います。

* **APIキー**：PushEngageのAPIキーです。APIキーを使用すると、PushEngageサービスにアクセスできます。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリーは次のとおりです。

### 標準

|変数|説明|
|---|---|
|APIキー（`apiKey`）|［文字列］|
|セグメント名（`segmentName`）|［文字列／配列］|
|プロファイルID（`profileId`）|［文字列］|
|日数（`days`）|［数値／配列］|

### イベント

|変数|説明|
|---|---|
|購読時に購読者をセグメントに追加|`init`|
|サイトのページ読み込み時に購読者をセグメントに追加|`add-to-segment`|
|購読者を動的セグメントに追加|`add-to-dynamic-segment`|
|購読者をセグメントから削除|`remove-to-segment`|
|購読者にプロファイルIDを追加|`add-to-profile`|