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
`window.ClicktaleEventHandler([&#34;Tealium Audience: AUDIENCE NAME&#34;, ...]);`
* **リプレイリンクを送信**を`True`に構成して、サーバーサイド属性`clicktale_replay_link`としてClicktaleリプレイリンクを利用可能にします。
* リプレイリンクの生成を有効にするために、Clicktaleの担当者に連絡してください。
* サーバーサイドの属性は現在のアカウントとプロファイルに表示されます。
* `tealium_profile`を上書きするためにマッピングを使用します。

## タグの構成

新しいタグを追加するためにタグマーケットプレイスに移動します。タグの追加方法については、[タグの概要]()の記事を参照してください。

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
  * 例：`ClicktaleEventHandler([&#34;Tealium Audience: AUDIENCE NAME&#34;, ...]);.`
* **イベントをClickTaleに送信**
  * イベントデータをClicktaleに送信するために**True**を選択します。

## ロードルールの適用

[ロードルール]()は、このタグのインスタンスをいつどこでロードするかを決定します。&#39;すべてのページでロード&#39;ルールはデフォルトのロードルールです。特定のページでこのタグをロードするには、関連する条件で新しいロードルールを作成します。

* 訪問のマウスの動きを追跡したいページでこのタグをロードします。
* このタグは、ページが完全にレンダリングされた後にロードすることをお勧めします。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは次のとおりです：

### 標準

|変数| 説明|
|---| ---|
|`partition`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;パーティション。&lt;/li&gt;&lt;li&gt;データが送信されるパーティション。&lt;/li&gt;&lt;li&gt;この変数にマップして、サーバーパーティションの値を動的に構成します。&lt;/li&gt;&lt;/ul&gt; |
|`project_guid`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;プロジェクトGUID。&lt;/li&gt;&lt;li&gt;プロジェクトガイドフィールドを構成するためにこの変数にマップします。&lt;/li&gt;&lt;/ul&gt; |
|`send_replay_link`|  &lt;ul&gt;&lt;li&gt;文字列、ブール値&lt;/li&gt;&lt;li&gt;Clicktaleリプレイリンクを送信&lt;/li&gt;&lt;li&gt;値は**true**または**false**。&lt;/li&gt;&lt;/ul&gt; |
|`send_audiences`|  &lt;ul&gt;&lt;li&gt;文字列、ブール値&lt;/li&gt;&lt;li&gt;すべてのオーディエンスを送信。&lt;/li&gt;&lt;li&gt;値は**true**または**false**。&lt;/li&gt;&lt;/ul&gt; |
|`tealium_account`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;Tealiumアカウント。&lt;/li&gt;&lt;/ul&gt; |
|`tealium_profile`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;Tealiumプロファイル。&lt;/li&gt;&lt;/ul&gt; |
|`SendEventsToClicktale`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;Clicktaleにイベントを送信するためにオンに切り替えます&lt;/li&gt;&lt;/ul&gt; |

## ベンダーのドキュメンテーション

* [統合のリクエスト方法](https://uxanalyser.zendesk.com/hc/en-gb/articles/4405613239186 &#34;https://uxanalyser.zendesk.com/hc/en-gb/articles/4405613239186&#34;)
* [ライブシグナルの実装](https://uxanalyser.zendesk.com/hc/en-gb/articles/4409749139346-Live-Signals &#34;https://uxanalyser.zendesk.com/hc/en-gb/articles/4409749139346-Live-Signals&#34;)
* [Tealium統合](http://wiki.clicktale.com/Article/Tealium_Integration)
* [よくある質問](http://wiki.clicktale.com/Article/Frequently_asked_questions)


