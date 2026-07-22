---
title: PushEngageタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでPushEngageタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/pushengage-tag/
---
PushEngageは、コンテンツウェブサイトの管理者が自動的にセグメント化し、ウェブプッシュメッセージを送信することで訪問とのエンゲージメントを促進するブラウザプッシュ通知プラットフォームです。このクラウドベースのツールは、通知トリガーの構成、顧客セグメンテーション、自動応答、A/Bテストなどの機能を提供します。

## タグ構成

まず、タグマーケットプレイスに移動し、PushEngageタグを追加します（[タグの追加方法](https://docs.tealium.com/manage-tags/)について詳しくはこちら）。

タグを追加したら、以下の構成を行います：

* **APIキー**：あなたのPushEngage APIキー。APIキーを使用すると、PushEngageサービスにアクセスできます。

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### スタンダード

|変数| 説明|
|---| ---|
|APIキー (`apiKey`)| [文字列]|
|セグメント名 (`segmentName`)| [文字列/配列]|
|プロファイルID (`profileId`)| [文字列]|
|日数 (`days`)| [数値/配列]|

### イベント

|変数| 説明|
|---| ---|
|購読時に購読者にセグメントを追加| `init`|
|サイトのページロード時に購読者にセグメントを追加| `add-to-segment`|
|購読者にダイナミックセグメントを追加| `add-to-dynamic-segment`|
|購読者をセグメントから削除| `remove-to-segment`|
|購読者にプロファイルIDを追加| `add-to-profile`|

