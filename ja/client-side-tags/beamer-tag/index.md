---
title: Beamerタグ構成ガイド
description: この記事では、タグ管理アカウントでBeamerタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/beamer-tag/
---
## 仕組み

Beamerは、重要なニュース、最新製品、特別オファーなどのお知らせをユーザーやサイト訪問に送信できる、通知センターおよび変更履歴プラグインです。

## タグに関するヒント

* ウィジェット構成はマッピングを使用して指定します。
* 要素IDを追加しない場合、デフォルトではページの右下隅に通知アイコンが表示されます。
* `callback`、`onclick`、`onopen`、および`onclose`関数は、関数名を文字列としてマッピングするか、関数への参照をマッピングすることで呼び出せます。関数名を指定する場合、その関数はwindowレベルで定義されている必要があります。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、以下の構成を行います。

* **製品ID**  
製品IDは、Beamerダッシュボードの上部バーに表示される一意の識別コードです。
* **セレクター**  
パネルを表示するトリガーとして使用するDOM要素のHTML識別子です。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリーは以下のとおりです。

### 標準

| 変数               | 説明           |
|:-------------------|:---------------|
| Beamer顧客ID       | (`product_id`) |

### ウィジェット構成

| 変数                                       | 説明                          |
|:-------------------------------------------|:------------------------------|
| セレクターID                               | (`selector`)                  |
| 表示モード                                 | (`display`)                   |
| 表示位置                                   | (`display_position`)          |
| 上オフセット                               | (`top`)                       |
| 右オフセット                               | (`right`)                     |
| 下オフセット                               | (`bottom`)                    |
| 左オフセット                               | (`left`)                      |
| 埋め込み切り替え [`true`/`false`]          | (`embed`)                     |
| ボタン切り替え [`true`/`false`]            | (`button`)                    |
| ボタン位置                                 | (`button_position`)           |
| アイコン                                   | (`icon`)                      |
| バウンス切り替え [`true`/`false`]          | (`bounce`)                    |
| 通知プロンプト                             | (`notification_prompt`)       |
| 通知プロンプトの遅延                       | (`notification_prompt_delay`) |
| 言語                                       | (`language`)                  |
| フィルター                                 | (`filter`)                    |
| URLによるフィルター切り替え [`true`/`false`] | (`filter_by_url`)             |
| モバイル切り替え [`true`/`false`]          | (`mobile`)                    |
| 遅延読み込み切り替え [`true`/`false`]      | (`lazy`)                      |
| アラート切り替え [`true`/`false`]          | (`alert`)                     |
| 遅延                                       | (`delay`)                     |
| コールバック関数                           | (`callback`)                  |
| Onclick関数                                | (`onclick`)                   |
| Onopen関数                                 | (`onopen`)                    |
| Onclose関数                                | (`onclose`)                   |

### ユーザーデータ

| 変数               | 説明               |
|:-------------------|:-------------------|
| ユーザーの名       | (`user_firstname`) |
| ユーザーの姓       | (`user_lastname`)  |
| ユーザーのメール   |                    |
| ユーザーID         | (`user_id`)        |

### ボタン位置

| 変数                              | 説明           |
|:----------------------------------|:---------------|
| 左下 (`bottom-left`)              | `bottom-left`  |
| 右下 (`bottom-right`)             | `bottom-right` |
| 左上 (`top-left`)                 | `top-left`     |
| 右上 (`top-right`)                | `top-right`    |

### 表示

| 変数                  | 説明     |
|:----------------------|:---------|
| 左 (`left`)           | `left`   |
| 右 (`right`)          | `right`  |
| アプリ内 (`in-app`)   | `in-app` |
| ポップアップ (`popup`) | `popup`  |

### 表示位置

| 変数                              | 説明           |
|:----------------------------------|:---------------|
| 下 (`bottom`)                     | `bottom`       |
| 左下 (`bottom-left`)              | `bottom-left`  |
| 右下 (`bottom-right`)             | `bottom-right` |
| 左 (`left`)                       | `left`         |
| 左下 (`left-bottom`)              | `left-bottom`  |
| 左上 (`left-top`)                 | `left-top`     |
| 右 (`right`)                      | `right`        |
| 右下 (`right-bottom`)             | `right-bottom` |
| 右上 (`right-top`)                | `right-top`    |
| 上 (`top`)                        | `top`          |
| 左上 (`top-left`)                 | `top-left`     |
| 右上 (`top-right`)                | `top-right`    |

### アイコン

| 変数                                  | 説明           |
|:--------------------------------------|:---------------|
| 塗りつぶしベル (`bell_full`)          | `bell_full`    |
| 線画ベル (`bell_lines`)               | `bell_lines`   |
| 炎 (`flame`)                          | `flame`        |
| 代替の炎 (`flame_alt`)                | `flame_alt`    |
| アラート吹き出し (`alert_bubble`)     | `alert_bubble` |
| アラート円形アイコン (`alert_circle`) | `alert_circle` |
| メガホン (`bullhorn`)                 | `bullhorn`     |
| 画びょう (`thumbtack`)                | `thumbtack`    |

### 通知プロンプト

| 変数                      | 説明      |
|:--------------------------|:----------|
| ポップアップ (`popup`)    | `popup`   |
| サイドバー (`sidebar`)    | `sidebar` |