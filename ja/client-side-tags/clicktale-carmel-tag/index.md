---
title: Clicktale Carmelタグ構成ガイド
description: この記事では、タグ管理アカウントでClicktale Carmelタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/clicktale-carmel-tag/
---## タグに関するヒント

* マッピングを使用して、標準構成値を上書きします。
* オーディエンスとバッジをClicktaleに渡すには、次の手順を実行します。
  * このデータを受信できるようにするには、Clicktaleの担当者にお問い合わせください。
  * バッジをマッピングする場合は、Clicktaleに表示する名前を入力します。
  * すべてのオーディエンスを次の形式でClicktaleに送信するには、**Send All Audiences**を`True`に構成します。  
`window.ClicktaleEventHandler(["Tealium Audience: AUDIENCE NAME", ...]);`
* Clicktaleのリプレイリンクをサーバーサイド属性`clicktale_replay_link`として使用できるようにするには、**Send Replay Link**を`True`に構成します。
* リプレイリンクの生成を有効にするには、Clicktaleの担当者にお問い合わせください。
* サーバーサイド属性は、現在のアカウントとプロファイルに表示されます。
* マッピングを使用して`tealium_profile`を上書きします。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を構成します。

* **タイトル**
  * （必須）タグインスタンスを識別します。
  * デフォルト名はClicktale Carmelです。
  * 同じベンダーのタグを複数使用する場合は、一意の名前を割り当てます。
* **パーティション**
  * データの送信先となるパーティションです。
  * 例：**www07**
* **プロジェクトGUID／PTC ID**
  * ClicktaleのプロジェクトGUIDです。
  * 例：**11111111-1111-1111-1111-11111111111**
* **リプレイリンクを送信**
  * Clicktaleのリプレイリンクをサーバーサイド属性として使用できるようにするには、**True**を選択します。
* **すべてのオーディエンスを送信**
  * 各オーディエンスを指定された形式でClicktaleに送信するには、**True**を選択します。
  * 例：`ClicktaleEventHandler(["Tealium Audience: AUDIENCE NAME", ...]);.`
* **イベントをClickTaleに送信**
  * イベントデータをClicktaleに送信するには、**True**を選択します。

## ロードルールの適用

[ロードルール](https://docs.tealium.com/about-load-rules/)は、このタグのインスタンスをいつ、どこで読み込むかを決定します。「Load on All Pages」ルールがデフォルトのロードルールです。このタグを特定のページで読み込むには、該当する条件を指定して新しいロードルールを作成します。

* 訪問のマウス操作を追跡するページで、このタグを読み込みます。
* ページのレンダリングが完全に終了した後に、このタグを読み込むことをお勧めします。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### 標準

|変数|説明|
|---|---|
|`partition`|<ul><li>文字列</li><li>パーティション。</li><li>データの送信先となるパーティションです。</li><li>サーバーパーティションの値を動的に構成するには、この変数にマッピングします。</li></ul>|
|`project_guid`|<ul><li>文字列</li><li>プロジェクトGUID。</li><li>プロジェクトGUIDフィールドを構成するには、この変数にマッピングします。</li></ul>|
|`send_replay_link`|<ul><li>文字列、ブール値</li><li>Clicktaleのリプレイリンクを送信します。</li><li>値は**true**または**false**です。</li></ul>|
|`send_audiences`|<ul><li>文字列、ブール値</li><li>すべてのオーディエンスを送信します。</li><li>値は**true**または**false**です。</li></ul>|
|`tealium_account`|<ul><li>文字列</li><li>Tealiumアカウント。</li></ul>|
|`tealium_profile`|<ul><li>文字列</li><li>Tealiumプロファイル。</li></ul>|
|`SendEventsToClicktale`|<ul><li>文字列</li><li>オンにすると、イベントがClicktaleに送信されます。</li></ul>|

## ベンダーのドキュメント

* [統合をリクエストする方法](https://uxanalyser.zendesk.com/hc/en-gb/articles/4405613239186 "https://uxanalyser.zendesk.com/hc/en-gb/articles/4405613239186")
* [Live Signalsの実装](https://uxanalyser.zendesk.com/hc/en-gb/articles/4409749139346-Live-Signals "https://uxanalyser.zendesk.com/hc/en-gb/articles/4409749139346-Live-Signals")
* [Tealiumとの統合](http://wiki.clicktale.com/Article/Tealium_Integration)
* [よくある質問](http://wiki.clicktale.com/Article/Frequently_asked_questions)