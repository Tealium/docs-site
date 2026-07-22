---
title: Beamerタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでBeamerタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/beamer-tag/
---
## 仕組み

Beamerは、通知センターとチェンジログプラグインで、重要なニュース、最新の製品、特別なオファーなど、ユーザーやサイト訪問に告知を送ることができます。

## タグのヒント

* ウィジェットの構成はマッピングを通じて構成されます。
* デフォルトでElement IDを追加しない場合、Beamerはページの右下隅に通知アイコンを表示します。
* コールバック、onclick、onopen、onclose関数を提供することができます。関数の名前（文字列として）または関数への参照をマッピングを通じて提供します。関数の名前を提供する場合、関数はウィンドウレベルで定義されていると想定されます。

## タグの構成

まず、Tealiumのタグマーケットプレイスに移動し、Beamerタグを追加します（[タグの追加方法](https://docs.tealium.com/manage-tags/)について詳しくはこちら）。

タグを追加したら、以下の構成を行います：

* **製品ID**  
製品IDは、Beamerダッシュボードのトップバーに表示される一意の識別コードです。
* **セレクタ**  
パネルを表示するトリガーとして使用されるDOM要素のHTML識別子。

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

| 変数               | 説明          |
|:-------------------|:--------------|
| Beamer Customer ID | (`product_id`) |

### ウィジェット構成

| 変数                                      | 説明                       |
|:------------------------------------------|:----------------------------|
| セレクタID                               | (`selector`)                |
| 表示モード                               | (`display`)                 |
| 表示位置                                 | (`display_position`)        |
| 上部オフセット                           | (`top`)                     |
| 右部オフセット                           | (`right`)                   |
| 下部オフセット                           | (`bottom`)                  |
| 左部オフセット                           | (`left`)                    |
| 埋め込みトグル [`true`/`false`]           | (`embed`)                   |
| ボタントグル [`true`/`false`]             | (`button`)                  |
| ボタン位置                               | (`button_position`)         |
| アイコン                                 | (`icon`)                    |
| バウンストグル [`true`/`false`]           | (`bounce`)                  |
| 通知プロンプト                           | (`notification_prompt`)     |
| 通知プロンプト遅延                       | (`notification_prompt_delay`)|
| 言語                                     | (`language`)                |
| フィルタ                                 | (`filter`)                  |
| URLによるフィルタトグル [`true`/`false`] | (`filter_by_url`)           |
| モバイルトグル [`true`/`false`]           | (`mobile`)                  |
| レイジートグル [`true`/`false`]           | (`lazy`)                    |
| アラートトグル [`true`/`false`]           | (`alert`)                   |
| 遅延                                     | (`delay`)                   |
| コールバック関数                         | (`callback`)                |
| Onclick関数                              | (`onclick`)                 |
| Onopen関数                               | (`onopen`)                  |
| Onclose関数                              | (`onclose`)                 |

### ユーザーデータ

| 変数            | 説明              |
|:----------------|:-------------------|
| ユーザー名      | (`user_firstname`) |
| ユーザー姓      | (`user_lastname`)  |
| ユーザーメール  |                    |
| ユーザーID      | (`user_id`)        |

### ボタン位置

| 変数                              | 説明            |
|:----------------------------------|:---------------|
| 左下 (`bottom-left`)              | `bottom-left`  |
| 右下 (`bottom-right`)             | `bottom-right` |
| 左上 (`top-left`)                 | `top-left`     |
| 右上 (`top-right`)                | `top-right`    |

### 表示

| 変数                  | 説明       |
|:----------------------|:-----------|
| 左 (`left`)           | `left`     |
| 右 (`right`)          | `right`    |
| アプリ内 (`in-app`)   | `in-app`   |
| ポップアップ (`popup`) | `popup`    |

### 表示位置

| 変数                                  | 説明            |
|:--------------------------------------|:---------------|
| 下 (`bottom`)                         | `bottom`       |
| 左下 (`bottom-left`)                  | `bottom-left`  |
| 右下 (`bottom-right`)                 | `bottom-right` |
| 左 (`left`)                           | `left`         |
| 左下 (`left-bottom`)                  | `left-bottom`  |
| 左上 (`left-top`)                     | `left-top`     |
| 右 (`right`)                          | `right`        |
| 右下 (`right-bottom`)                 | `right-bottom` |
| 右上 (`right-top`)                    | `right-top`    |
| 上 (`top`)                            | `top`          |
| 左上 (`top-left`)                     | `top-left`     |
| 右上 (`top-right`)                    | `top-right`    |

### アイコン

| 変数                                  | 説明            |
|:--------------------------------------|:---------------|
| ベルフル (`bell_full`)                | `bell_full`    |
| ベルライン (`bell_lines`)              | `bell_lines`   |
| フレーム (`flame`)                     | `flame`        |
| フレームオルト (`flame_alt`)           | `flame_alt`    |
| アラートバブル (`alert_bubble`)        | `alert_bubble` |
| アラートサークル (`alert_circle`)      | `alert_circle` |
| ブルホーン (`bullhorn`)               | `bullhorn`     |
| サムタック (`thumbtack`)               | `thumbtack`    |

### 通知プロンプト

| 変数                        | 説明       |
|:----------------------------|:-----------|
| ポップアップ (`popup`)       | `popup`    |
| サイドバー (`sidebar`)      | `sidebar`  |

