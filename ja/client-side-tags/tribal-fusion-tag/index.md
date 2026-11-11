---
title: Tribal Fusionタグ構成ガイド
description: この記事では、タグ管理アカウントでTribal Fusion Tagタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/tribal-fusion-tag/
---
## 要件

* Tribal Fusionアカウント

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、以下の項目を構成します。

* **タイトル**：（必須）タグインスタンスを識別するための分かりやすいタイトルを入力します。
* **Client**：（必須）Tribal Fusionから提供された数値のクライアントIDを入力します。例：746537
* **d**：（任意）Tribal Fusionピクセルで指定されている「d」パラメータの値をこのフィールドに構成します。注：デフォルトでは「30」が選択されています。この値を送信しない場合は、「N/A」を選択します。
* **ev**：（必須）Tribal Fusionがトラッキングピクセルで指定した「ev」パラメータの値を選択します。デフォルトでは「1」に構成されています。
* **デフォルトページ名**：このタグでトラッキングするデフォルトのページ名を入力します。例：「homepage」注：この値を上書きする場合は、マッピングツールボックスを使用します（[マッピングの構成](#Setting_up_Mappings)を参照）。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。読み込みルールの詳細については、[読み込みルール](https://docs.tealium.com/about-load-rules/)のドキュメントを参照してください。

<blockquote>
このタグを「すべてのページ」で読み込むと、タグのパフォーマンスが最適化されます。
</blockquote>


## データマッピング

[マッピング](https://docs.tealium.com/about-data-mappings/)とは、データレイヤー内のデータソースから、ベンダータグの対応する宛先変数へデータを送信する簡単なプロセスです。このタグのマッピングツールボックスには、事前定義された宛先変数は用意されていません。ただし、タグの宛先として機能するカスタム変数（「ユーザー定義」変数）を指定できます。

このタグでは、「デフォルトページ名」の値をマッピング経由で送信できます。ドロップダウンリストから適切なデータソースを選択し、隣接するテキストフィールドに宛先を入力します。


<blockquote>
[Eコマース拡張機能](https://docs.tealium.com/e-commerce-extension/)を追加し、`_corder`変数を構成することをお勧めします。これにより、拡張機能は注文IDの値を、対応するタグの宛先にマッピングできます。
</blockquote>


## ベンダーのドキュメント

* [Tribal Fusionについて](http://exponential.com/marketing-services/audience-engagement-solutions/tribal-fusion/)
* [広告主向けFAQ](https://www.tribalfusion.com/SmartAdvertisers/faqs.html)