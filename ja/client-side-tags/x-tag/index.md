---
title: X（旧Twitter）タグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでX（旧Twitter）タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/x-tag/
---
Xは、あなたが興味を持つ最新の話題、アイデア、意見、ニュースにつながるリアルタイム情報ネットワークです。

## タグのヒント
*   必要に応じて新しいdivを追加するためにContent Modification Extensionを使用します
*   指定されたDiv IDの内容はXボタン（ボタンは単なるリンク）で上書きされます

## タグの構成

新しいタグを追加するためにタグマーケットプレイスに行きます。詳細は、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際には、以下の構成を行います：

* **ボタンタイプ**： `Share`（投稿）、`Follow`、`mention`、または`hashtag`。
* **言語**：ドロップダウンリストから言語を選択します。
* **Div ID**：Xリンク（ボタン）を追加するDiv ID。divの内容を上書きします。ページにすでにリンクが定義されている場合は空白にします。
* **サイズ**：`Standard`または`Large`。
* **カウント表示**：`None`、`Horizontal`、または`Vertical`。
* **フォロー**：Xアカウント（`@`は含めない）
* **リンクテキスト**：デフォルトのテキストを使用する場合は空白にします。
* **投稿するメッセージ**：Shareボタン用のメッセージ
* **共有URL**：現在のURLを使用する場合は空白にします。例：http://www.tealium.com
* **クエリストリングの追加**：オプション。`/share?`の後にクエリストリングに追加します。例：utm_source=website in http://x.com/share?utm_source=website

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細は、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数にデータを送信するプロセスです。詳細は、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは以下の通りです：

### スタンダード

| 変数 | 説明 |
|:---------|:------------|
| `type` | ボタンの種類 |
| `divid` | Div ID |
| `lang` | 言語 |
| `size` | サイズ |
| `count` | カウントボックスの位置 |
| `follow` | フォロー |
| `text` | テキスト |
| `url` | URL |
| `post` | 投稿テキスト |
| `dnt` | テーラリングのオプトアウト |

### 投稿

| 変数 | 説明 |
|:---------|:-----|:------------|
| `via` | スクリーン名 |
| `related` | 関連アカウント |
| `counturl` | 長いURL |
| `hashtags` | ハッシュタグの文字列または配列 |

### フォロー

| 変数 | 説明 |
|:---------|:------------|
| `width` | 幅 |
| `align` | 整列 |
| `screen_name` | スクリーン名 |
| `show-screen-name` | スクリーン名の表示 |
| `show-count` | カウントボックスの表示 |

