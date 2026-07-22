---
title: Clicktale Carmelタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでClicktale Carmelタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/clicktale-carmel-tag/
---## タグのヒント

* マッピングを使用して標準の構成値を上書きします。
* Clicktaleにオーディエンスとバッジを渡すには：
  * このデータの受信を有効にするために、Clicktaleの担当者に連絡してください。
  * バッジをマッピングするときは、Clicktaleに表示される名前を入力します。
  * **すべてのオーディエンスを送信**を`True`に構成して、次の形式ですべてのオーディエンスをClicktaleに送信します：  
`window.ClicktaleEventHandler(["Tealium Audience: AUDIENCE NAME", ...]);`
* **リプレイリンクを送信**を`True`に構成して、サーバーサイド属性`clicktale_replay_link`としてClicktaleリプレイリンクを利用可能にします。
* リプレイリンクの生成を有効にするために、Clicktaleの担当者に連絡してください。
* サーバーサイドの属性は現在のアカウントとプロファイルに表示されます。
* `tealium_profile`を上書きするためにマッピングを使用します。

## タグの構成

新しいタグを追加するためにタグマーケットプレイスに移動します。タグの追加方法については、[タグの概要](https://docs.tealium.com/about-tags/)の記事を参照してください。

タグを追加するときは、次の構成を行います：

* **タイトル**
  * 必須。
  * タグインスタンスを識別します。
  * Clicktale Carmelがデフォルトの名前です。
  * 同じベンダーから複数のタグを使用する場合は、一意の名前を割り当てます
* **パーティション**
  * データが送信されるパーティション。
  * 例：**www07**
* **プロジェクトGUID / PTC ID**
  * ClicktaleプロジェクトGUID
  * 例：**11111111-1111-1111-1111-11111111111**
* **リプレイリンクを送信**
  * サーバーサイド属性としてClicktaleリプレイリンクを利用可能にするために**True**を選択します。
* **すべてのオーディエンスを送信**
  * 各オーディエンスをClicktaleに送信する形式のウィンドウに**True**を選択します。
  * 例：`ClicktaleEventHandler(["Tealium Audience: AUDIENCE NAME", ...]);.`
* **イベントをClickTaleに送信**
  * イベントデータをClicktaleに送信するために**True**を選択します。

## ロードルールの適用

[ロードルール](https://docs.tealium.com/about-load-rules/)は、このタグのインスタンスをいつどこでロードするかを決定します。'すべてのページでロード'ルールはデフォルトのロードルールです。特定のページでこのタグをロードするには、関連する条件で新しいロードルールを作成します。

* 訪問のマウスの動きを追跡したいページでこのタグをロードします。
* このタグは、ページが完全にレンダリングされた後にロードすることをお勧めします。

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは次のとおりです：

### 標準

|変数| 説明|
|---| ---|
|`partition`|  <ul><li>文字列</li><li>パーティション。</li><li>データが送信されるパーティション。</li><li>この変数にマップして、サーバーパーティションの値を動的に構成します。</li></ul> |
|`project_guid`|  <ul><li>文字列</li><li>プロジェクトGUID。</li><li>プロジェクトガイドフィールドを構成するためにこの変数にマップします。</li></ul> |
|`send_replay_link`|  <ul><li>文字列、ブール値</li><li>Clicktaleリプレイリンクを送信</li><li>値は**true**または**false**。</li></ul> |
|`send_audiences`|  <ul><li>文字列、ブール値</li><li>すべてのオーディエンスを送信。</li><li>値は**true**または**false**。</li></ul> |
|`tealium_account`|  <ul><li>文字列</li><li>Tealiumアカウント。</li></ul> |
|`tealium_profile`|  <ul><li>文字列</li><li>Tealiumプロファイル。</li></ul> |
|`SendEventsToClicktale`|  <ul><li>文字列</li><li>Clicktaleにイベントを送信するためにオンに切り替えます</li></ul> |

## ベンダーのドキュメンテーション

* [統合のリクエスト方法](https://uxanalyser.zendesk.com/hc/en-gb/articles/4405613239186 "https://uxanalyser.zendesk.com/hc/en-gb/articles/4405613239186")
* [ライブシグナルの実装](https://uxanalyser.zendesk.com/hc/en-gb/articles/4409749139346-Live-Signals "https://uxanalyser.zendesk.com/hc/en-gb/articles/4409749139346-Live-Signals")
* [Tealium統合](http://wiki.clicktale.com/Article/Tealium_Integration)
* [よくある質問](http://wiki.clicktale.com/Article/Frequently_asked_questions)


