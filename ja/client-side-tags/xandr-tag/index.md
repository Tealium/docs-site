---
title: Xandrタグ構成ガイド（非推奨）
description: この記事では、タグ管理アカウントでXandrタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/xandr-tag/
---

<blockquote>
Xandrタグは非推奨となり、サポートも終了しています。[Xandr Universal Pixelタグ](https://docs.tealium.com/xandr-universal-pixel-tag/)への移行をお勧めします。
</blockquote>


## 要件

* Xandrアカウント

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の項目を構成します。

* **Title**：（必須）タグインスタンスを識別するための分かりやすいタイトルを入力します。
* **Add**：（必須）Xandrから提供されたAdd値を入力します。Addの値を入力した場合、下のIDを入力する必要はありません。
* **IDs**：（必須）Xandrから提供されたIDを入力します。IDを入力した場合、上のAddの値を入力する必要はありません。
* **t**：（必須）tの値を入力します。通常、この値は1または2です。JavaScriptピクセルの場合は1、画像ピクセルの場合は2を入力します。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。読み込みルールの詳細については、[読み込みルール](https://docs.tealium.com/about-load-rules/)のドキュメントを参照してください。

## データマッピング

[マッピング](https://docs.tealium.com/about-data-mappings/)とは、データレイヤー内のデータソースから、ベンダータグの対応する宛先変数へデータを送信するシンプルなプロセスです。

これらのタグ構成を動的に指定する場合にのみ、以下の宛先変数へマッピングする必要があります。いずれか一方を構成すれば、もう一方を構成する必要はありません。

* **add**
Add情報を含むデータソースをマッピングします。

* **id**
ID情報を含むデータソースをマッピングします。

## ベンダーのドキュメント

* [Xandr Wiki](https://wiki.xandr.com/)