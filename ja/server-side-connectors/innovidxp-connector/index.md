---
title: InnovidXPコネクタ構成ガイド
description: この記事では、InnovidXPコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/innovidxp-connector/
---
## 構成

コネクタマーケットプレイスにアクセスし、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタ概要]()の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **クライアントホスト**
  * クライアント固有のコレクターホスト名。
  * InnovidXPによって提供される静的な値。
  * 例：`collector-1233.tvsquared.com`。

* **サイトID**
  * クライアント固有のコレクターサイトID。
  * InnovidXPによって提供される静的な値。
  * 例：`TV1234-1`。

## アクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|イベント追跡| ✓| ✓|

### イベント追跡

#### URLパラメータ

以下の表は、サーバー間リクエストにエンコードするURLパラメータをリストしています：

`servertrack`および`RAND`パラメータはTealiumによって自動的に構成されます。

|**パラメータ**| **説明**|
|---| ---|
|訪問ID (`VISITORID`)|  &lt;ul&gt;&lt;li&gt;(必須) 訪問のユニークID。&lt;/li&gt;&lt;li&gt;サーバー間リクエストにエンコードするURLパラメータ。&lt;/li&gt;&lt;li&gt;例：`0123456789ABCDEF`。&lt;/li&gt;&lt;/ul&gt; |
|ユーザーエージェント (`UA`)|  &lt;ul&gt;&lt;li&gt;該当する場合、ユーザーエージェント。&lt;/li&gt;&lt;li&gt;例：`Mozilla/5.0`。&lt;/li&gt;&lt;/ul&gt; |
|ブラウザ言語 (`LANG`)|  &lt;ul&gt;&lt;li&gt;該当する場合、ブラウザ言語。&lt;/li&gt;&lt;li&gt;例：`en`。&lt;/li&gt;&lt;/ul&gt; |

#### セッションパラメータ (`_cvar`)

以下の表は、詳細なセッションレベルの追跡情報をリストしています：

|**パラメータ**| **説明**|
|---| ---|
|`appid`|  &lt;ul&gt;&lt;li&gt;アプリのID。&lt;/li&gt;&lt;li&gt;例：`com.myapp.appster`。&lt;/li&gt;&lt;/ul&gt; |
|`appname`|  &lt;ul&gt;&lt;li&gt;アプリの名前。&lt;/li&gt;&lt;li&gt;例：My Application。&lt;/li&gt;&lt;/ul&gt; |
|`country`|  &lt;ul&gt;&lt;li&gt;国。&lt;/li&gt;&lt;li&gt;例：`US`。&lt;/li&gt;&lt;/ul&gt; |
|`deviceid`|  &lt;ul&gt;&lt;li&gt;デバイスID。&lt;/li&gt;&lt;li&gt;例：`e3f5536a141811db40efd6400f1d0a4e`。&lt;/li&gt;&lt;/ul&gt; |
|`deviceidtype`|  &lt;ul&gt;&lt;li&gt;デバイスIDのタイプ。&lt;/li&gt;&lt;li&gt;例：`AAID`または`IDFA`。&lt;/li&gt;&lt;/ul&gt; |
|`ip`|  &lt;ul&gt;&lt;li&gt;(必須) モバイルデバイスのIPアドレス。&lt;/li&gt;&lt;li&gt;例：`8.8.8.8`。&lt;/li&gt;&lt;/ul&gt; |
|`lang`|  &lt;ul&gt;&lt;li&gt;ユーザー言語。&lt;/li&gt;&lt;li&gt;例：`en`。&lt;/li&gt;&lt;/ul&gt; |
|`medium`|  &lt;ul&gt;&lt;li&gt;(必須) モバイルアプリの場合は`app`に構成。&lt;/li&gt;&lt;li&gt;例：`app`。&lt;/li&gt;&lt;/ul&gt; |
|`os`|  &lt;ul&gt;&lt;li&gt;オペレーティングシステム。&lt;/li&gt;&lt;li&gt;例：`ANDROID`。&lt;/li&gt;&lt;/ul&gt; |
|`source`|  &lt;ul&gt;&lt;li&gt;(必須) データを提供するパートナーの名前を識別します。&lt;/li&gt;&lt;li&gt;例：`myApplication`&lt;/li&gt;&lt;/ul&gt; |
|`ua`|  &lt;ul&gt;&lt;li&gt;ユーザーエージェント。&lt;/li&gt;&lt;li&gt;例：`Mozilla/5.0`。&lt;/li&gt;&lt;/ul&gt; |
|`user`|  &lt;ul&gt;&lt;li&gt;ユーザーID。&lt;/li&gt;&lt;li&gt;クライアントが提供するプライベートなユニークユーザー識別子、例えば請求システムからの内部ID。&lt;/li&gt;&lt;li&gt;例：`U1234`。&lt;/li&gt;&lt;/ul&gt; |

#### アクションパラメータ (`cvar`)

以下の表は、詳細なアクションごとの追跡情報をリストしています：

|**パラメータ**| **説明**|
|---| ---|
|アクション名|  &lt;ul&gt;&lt;li&gt;(必須) 実行されているアクションの名前。&lt;/li&gt;&lt;li&gt;例：`INSTALL`。&lt;/li&gt;&lt;/ul&gt; |
|`adchannel`|  &lt;ul&gt;&lt;li&gt;広告チャンネル名。&lt;/li&gt;&lt;li&gt;例：`Social`。&lt;/li&gt;&lt;/ul&gt; |
|`campaign`|  &lt;ul&gt;&lt;li&gt;キャンペーン名。&lt;/li&gt;&lt;li&gt;例：`NY_Acquisition`。&lt;/li&gt;&lt;/ul&gt; |
|`currency`|  &lt;ul&gt;&lt;li&gt;収益の通貨。&lt;/li&gt;&lt;li&gt;例：`USD`。&lt;/li&gt;&lt;/ul&gt; |
|`id`|  &lt;ul&gt;&lt;li&gt;個々のユーザーアクションのアクションID、例えば注文ID。&lt;/li&gt;&lt;li&gt;例：`42342`。&lt;/li&gt;&lt;/ul&gt; |
|`preattributed`|  &lt;ul&gt;&lt;li&gt;イベントがすでに帰属されているかどうか。&lt;/li&gt;&lt;li&gt;例：`1`。&lt;/li&gt;&lt;/ul&gt; |
|`prod`|  &lt;ul&gt;&lt;li&gt;製品名。&lt;/li&gt;&lt;li&gt;例：`angry birds`。&lt;/li&gt;&lt;/ul&gt; |
|`promo`|  &lt;ul&gt;&lt;li&gt;ユーザーが使用したプロモーションコード。&lt;/li&gt;&lt;li&gt;例：`ABCD`。&lt;/li&gt;&lt;/ul&gt; |
|`rev`|  &lt;ul&gt;&lt;li&gt;収益額。&lt;/li&gt;&lt;li&gt;指定されていない場合はデフォルトで提供されます。&lt;/li&gt;&lt;li&gt;例：`12`。&lt;/li&gt;&lt;/ul&gt; |
|`ts`|  &lt;ul&gt;&lt;li&gt;イベントの正確なUnixタイムスタンプ、UTC形式。&lt;/li&gt;&lt;li&gt;提供されていない場合はデフォルトで提供されます。&lt;/li&gt;&lt;li&gt;例：`1538996046`。&lt;/li&gt;&lt;/ul&gt; |
