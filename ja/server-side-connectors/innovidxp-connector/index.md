---
title: InnovidXPコネクタ構成ガイド
description: この記事では、InnovidXPコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/innovidxp-connector/
---
## 構成

コネクタマーケットプレイスにアクセスし、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタ概要](https://docs.tealium.com/about-connectors/)の記事を参照してください。

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


<blockquote>
`servertrack`および`RAND`パラメータはTealiumによって自動的に構成されます。
</blockquote>


|**パラメータ**| **説明**|
|---| ---|
|訪問ID (`VISITORID`)|  <ul><li>(必須) 訪問のユニークID。</li><li>サーバー間リクエストにエンコードするURLパラメータ。</li><li>例：`0123456789ABCDEF`。</li></ul> |
|ユーザーエージェント (`UA`)|  <ul><li>該当する場合、ユーザーエージェント。</li><li>例：`Mozilla/5.0`。</li></ul> |
|ブラウザ言語 (`LANG`)|  <ul><li>該当する場合、ブラウザ言語。</li><li>例：`en`。</li></ul> |

#### セッションパラメータ (`_cvar`)

以下の表は、詳細なセッションレベルの追跡情報をリストしています：

|**パラメータ**| **説明**|
|---| ---|
|`appid`|  <ul><li>アプリのID。</li><li>例：`com.myapp.appster`。</li></ul> |
|`appname`|  <ul><li>アプリの名前。</li><li>例：My Application。</li></ul> |
|`country`|  <ul><li>国。</li><li>例：`US`。</li></ul> |
|`deviceid`|  <ul><li>デバイスID。</li><li>例：`e3f5536a141811db40efd6400f1d0a4e`。</li></ul> |
|`deviceidtype`|  <ul><li>デバイスIDのタイプ。</li><li>例：`AAID`または`IDFA`。</li></ul> |
|`ip`|  <ul><li>(必須) モバイルデバイスのIPアドレス。</li><li>例：`8.8.8.8`。</li></ul> |
|`lang`|  <ul><li>ユーザー言語。</li><li>例：`en`。</li></ul> |
|`medium`|  <ul><li>(必須) モバイルアプリの場合は`app`に構成。</li><li>例：`app`。</li></ul> |
|`os`|  <ul><li>オペレーティングシステム。</li><li>例：`ANDROID`。</li></ul> |
|`source`|  <ul><li>(必須) データを提供するパートナーの名前を識別します。</li><li>例：`myApplication`</li></ul> |
|`ua`|  <ul><li>ユーザーエージェント。</li><li>例：`Mozilla/5.0`。</li></ul> |
|`user`|  <ul><li>ユーザーID。</li><li>クライアントが提供するプライベートなユニークユーザー識別子、例えば請求システムからの内部ID。</li><li>例：`U1234`。</li></ul> |

#### アクションパラメータ (`cvar`)

以下の表は、詳細なアクションごとの追跡情報をリストしています：

|**パラメータ**| **説明**|
|---| ---|
|アクション名|  <ul><li>(必須) 実行されているアクションの名前。</li><li>例：`INSTALL`。</li></ul> |
|`adchannel`|  <ul><li>広告チャンネル名。</li><li>例：`Social`。</li></ul> |
|`campaign`|  <ul><li>キャンペーン名。</li><li>例：`NY_Acquisition`。</li></ul> |
|`currency`|  <ul><li>収益の通貨。</li><li>例：`USD`。</li></ul> |
|`id`|  <ul><li>個々のユーザーアクションのアクションID、例えば注文ID。</li><li>例：`42342`。</li></ul> |
|`preattributed`|  <ul><li>イベントがすでに帰属されているかどうか。</li><li>例：`1`。</li></ul> |
|`prod`|  <ul><li>製品名。</li><li>例：`angry birds`。</li></ul> |
|`promo`|  <ul><li>ユーザーが使用したプロモーションコード。</li><li>例：`ABCD`。</li></ul> |
|`rev`|  <ul><li>収益額。</li><li>指定されていない場合はデフォルトで提供されます。</li><li>例：`12`。</li></ul> |
|`ts`|  <ul><li>イベントの正確なUnixタイムスタンプ、UTC形式。</li><li>提供されていない場合はデフォルトで提供されます。</li><li>例：`1538996046`。</li></ul> |
