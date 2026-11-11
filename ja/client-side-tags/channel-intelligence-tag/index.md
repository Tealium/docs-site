---
title: Channel Intelligenceタグ構成ガイド
description: この記事では、Channel Intelligenceタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/channel-intelligence-tag/
---
## タグの仕様と要件

### 仕様

* **名前**: TrueTag
* **ベンダー**: Channel Intelligence
* **タイプ**: コンバージョントラッキング

### 必須要件

**サービス**: Channel Intelligenceアカウント

**構成**:

* ベンダーID
* 本番ドメイン

## タグの構成

### タグの追加

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

### タグの構成

1. **タイトル**:（必須）タグインスタンスを識別するための、わかりやすいタイトルを入力します。
1. **タグバージョン**:（必須）タグインスタンスで読み込むバージョンを選択します。
  * V1: Tealium固有のタグバージョンを読み込みます
  * V2: `channelinteligence.com`から外部の`.js`ライブラリを配信します

1. **VID**:（任意）Channel Intelligenceから提供された数値のベンダーIDを入力します。このフィールドは動的に構成することもできます。
1. **ドメイン**:（必須）Channel Intelligenceを実装するドメイン名を入力します。ドメイン名の先頭にピリオドを付けます。例: `.yoursite.com`

### 読み込みルールの適用

[読み込みルール](https://docs.tealium.com/about-load-rules/)では、このタグのインスタンスをいつ、どこで読み込むかを決定します。デフォルトの読み込みルールは、**すべてのページで読み込む**ルールです。特定のページでこのタグを読み込むには、該当する条件を指定した新しい読み込みルールを作成します。

**ベストプラクティス**: デフォルトの**すべてのページで読み込む**の選択は、そのままにしておきます。これにより、サイトのすべてのページでタグが読み込まれます。

### マッピングの構成

[マッピング](https://docs.tealium.com/about-data-mappings/)とは、データレイヤー内のデータソースから、ベンダータグの対応する宛先変数にデータを送信する簡単なプロセスです。

**ベストプラクティス**: このタグは、[Eコマース拡張機能](https://docs.tealium.com/e-commerce-extension/)を使用して注文情報をタグに送信します。必要な注文変数と製品変数を拡張機能で構成し、それぞれの対応する宛先にマッピングできるようにします。拡張機能で、以下の変数のマッピングを必ず構成してください。

* `_corder`: 注文識別子
* `_cquan`: 数量のリスト。リスト内の各数量は、それぞれの製品に対応します
* `_cprod`: 製品IDのリスト。リスト内の各識別子は、それぞれの製品に対応します

**マッピング**ツールボックスで、ベンダーIDを宛先変数にマッピングすることにより、ベンダーIDを動的に構成できます。

## ベンダーのドキュメント

* [TrueTagトラッキングの実装](https://support.google.com/ci-ses/answer/4643079?hl=en)
* [Channel Intelligenceに関するよくある質問](https://support.google.com/ci-ses/answer/4634733?hl=en)