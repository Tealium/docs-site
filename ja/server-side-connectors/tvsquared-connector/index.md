---
title: TVSquaredコネクタ構成ガイド
description: この記事では、TVSquaredコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/tvsquared-connector/
---
## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|イベントを追跡する| ✓| ✓|

## 構成を構成する

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタ概要](https://docs.tealium.com/about-connectors/)の記事を参照してください。

コネクタを追加した後、次の構成を構成します：

* **クライアントホスト**
  * クライアント固有のコレクターホスト名。
  * TVSquaredから提供される静的な値。
  * 例：`collector-1233.tvsquared.com`。

* **サイトID**
  * クライアント固有のコレクターサイトID。
  * TVSquaredから提供される静的な値。
  * 例：`TV1234-1`。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - イベントを追跡する

#### URLパラメータ

以下の表は、サーバー間リクエストでエンコードするURLパラメータを一覧表示します：


<blockquote>
`servertrack`と`RAND`パラメータはTealiumによって自動的に構成されます。
</blockquote>


|**パラメータ**| **説明**|
|---| ---|
|訪問ID (`VISITORID`)|  <ul><li>必須。</li><li>訪問の一意のID。</li><li>サーバー間リクエストでエンコードするURLパラメータ。</li><li>例：`0123456789ABCDEF`</li></ul> |
|ユーザーエージェント (`UA`)|  <ul><li>該当する場合はユーザーエージェント。</li><li>例：`Mozilla/5.0`</li></ul> |
|ブラウザ言語 (`LANG`)|  <ul><li>該当する場合はブラウザの言語。</li><li>例：`en`</li></ul> |

#### セッションパラメータ (`_cvar`)

以下の表は、詳細なセッションレベルの追跡情報を一覧表示します：

|**パラメータ**| **説明**|
|---| ---|
|`appid`|  <ul><li>アプリのID。</li><li>アプリID</li><li>例：`com.myapp.appster`</li></ul> |
|`appname`|  <ul><li>アプリの名前。</li><li>アプリ名 </li><li>例：My Application</li></ul> |
|`country`|  <ul><li>国</li><li>例：`US`</li></ul> |
|`deviceid`|  <ul><li>デバイスID</li><li>例：`e3f5536a141811db40efd6400f1d0a4e`</li></ul> |
|`deviceidtype`|  <ul><li>デバイスIDのタイプ。</li><li>`deviceid`フィールドのタイプ。</li><li>例：`AAID`または`IDFA`</li></ul> |
|`ip`|  <ul><li>必須</li><li>IPアドレス。</li><li>モバイルデバイスのIPアドレス。</li><li>例：`8.8.8.8`</li></ul> |
|`lang`|  <ul><li>ユーザーの言語</li><li>例：`en`</li></ul> |
|`medium`|  <ul><li>必須。</li><li>モバイルアプリの場合は`app`に構成します。</li><li>例：`app`</li></ul> |
|`os`|  <ul><li>オペレーティングシステム</li><li>例：`ANDROID`</li></ul> |
|`source`|  <ul><li>必須</li><li>データを提供するパートナーの名前を識別します。</li><li>例：`myApplication`</li></ul> |
|`ua`|  <ul><li>ユーザーエージェント。</li><li>例：`Mozilla/5.0`</li></ul> |
|`user`|  <ul><li>ユーザーID。</li><li>クライアントが提供するプライベートな一意のユーザー識別子、例えば請求システムからの内部ID。</li><li>例：`U1234`</li></ul> |

#### アクションパラメータ (`cvar`)

以下の表は、詳細なアクションごとの追跡情報を一覧表示します：

|**パラメータ**| **説明**|
|---| ---|
|アクション名|  <ul><li>必須。</li><li>実行されるアクションの名前。</li><li>例：`INSTALL`</li></ul> |
|`adchannel`|  <ul><li>広告チャンネル</li><li>広告チャンネルの名前。</li><li>例：`Social`</li></ul> |
|`campaign`|  <ul><li>キャンペーン</li><li>キャンペーン名。</li><li>例：`NY_Acquisition`</li></ul> |
|`currency`|  <ul><li>通貨</li><li>収益の通貨。</li><li>例：`USD`</li></ul> |
|`id`|  <ul><li>アクションID</li><li>個々のユーザーアクションの識別子、例えば注文ID。</li><li>例：`42342`</li></ul> |
|`preattributed`|  <ul><li>事前に属性付けされた</li><li>イベントがすでに属性付けされているかどうか。</li><li>例：`1`</li></ul> |
|`prod`|  <ul><li>製品</li><li>関連する製品のエリア。</li><li>例：`angry birds`</li></ul> |
|`promo`|  <ul><li>プロモーションコード</li><li>ユーザーが使用したプロモーションコード。</li><li>例：`ABCD`</li></ul> |
|`rev`|  <ul><li>収益</li><li>収益額。</li><li>指定されていない場合、デフォルトで供給されます。</li><li>例：`12`</li></ul> |
|`ts`|  <ul><li>Unixタイムスタンプ</li><li>イベントの正確なUnixタイムスタンプ、UTC形式。</li><li>提供されていない場合、デフォルトで提供されます。</li><li>例：`1538996046`</li></ul> |
