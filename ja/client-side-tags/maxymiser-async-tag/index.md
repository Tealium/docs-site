---
title: Maxymiser (Async) タグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでMaxymiser (Async)タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/maxymiser-async-tag/
---
Maxymiserは、クラウドベースのテスト、パーソナライゼーション、クロスチャネル最適化ソリューションを用いて、ブランドがすべてのデジタルインタラクションをシームレスで関連性のあるエンゲージングなカスタマーエクスペリエンスに変える力を与えます。

## タグのヒント

* このタグを使用する前にMaxymiserに連絡し、Maxymiserライブラリが非同期でロードされるように構成されていることを確認してください。
* Maxymiserを同期的にロードする必要がある場合は、Maxymiserのコードを`utag.sync.js`に貼り付けるか、このタグの代わりにMaxymiser (Sync)タグを使用してください。
* 最高のパフォーマンスのために：
  * 高度な構成：**タグタイミング**を**優先**に構成します。
  * このタグをタグリストの一番上に移動させます（最初にロードされるように）。
  * 公開構成：バンドルを有効にします
  * `utag.js`をボディの一番上に移動させます

* マッピングを使用して：
  * ページごとにタグを無効にします。
  * 追加のデータをMaxymiserに渡します（Maxymiserアカウントで有効にする必要があります）。

## タグ構成

まず、タグマーケットプレイスに移動し、Maxymiser (Async)タグを追加します（[タグの追加方法](https://docs.tealium.com/manage-tags/)について詳しくはこちら）。

タグを追加したら、以下の構成を行います：

* **ライブラリURL**：Maxymiserから提供される`mmcore.js`ライブラリURL。  
例：  
`//service.maxymiser.net/cdn/tealium/js/mmcore.js`  
これは`//`で始まるべきです。`http:`や`https:`は含めないでください。

## データマッピング

マッピングとは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### スタンダード

| 変数                             | 説明                                      |
|:---------------------------------|:-------------------------------------------|
| ライブラリURL                    | (`library_url`)                            |
| Maxymiserの無効化                | (`mm_disable`)                             |
| テストコンテンツの非同期ロード   | (`mm_async`) (デフォルトの`true`を上書き)  |
| カスタム                         | (`custom.myvar`)                           |
