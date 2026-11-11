---
title: InnovidXPコネクタ構成ガイド
description: この記事では、InnovidXPコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/innovidxp-connector/
---
## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加したら、次の構成を構成します。

* **クライアントホスト**
  * クライアント固有のコレクターホスト名。
  * InnovidXPから提供される固定値。
  * 例：`collector-1233.tvsquared.com`。

* **サイトID**
  * クライアント固有のコレクターサイトID。
  * InnovidXPから提供される固定値。
  * 例：`TV1234-1`。

コネクタを構成したら、**完了**をクリックします。

## アクション

| アクション名 | ビジタープロファイル | イベントデータ |
| --- | :---: | :---: |
|イベントを追跡| ✓| ✓|

### イベントを追跡

#### URLパラメータ

次の表に、サーバー間リクエストでエンコードするURLパラメータを示します。


<blockquote>
`servertrack`パラメータと`RAND`パラメータは、Tealiumによって自動的に構成されます。
</blockquote>


|**パラメータ**| **説明**|
|---| ---|
|ビジターID（`VISITORID`）|  <ul><li>（必須）ビジターの一意のID。</li><li>サーバー間リクエストでエンコードするURLパラメータ。</li><li>例：`0123456789ABCDEF`。</li></ul> |
|ユーザーエージェント（`UA`）|  <ul><li>該当する場合はユーザーエージェント。</li><li>例：`Mozilla/5.0`。</li></ul> |
|ブラウザー言語（`LANG`）|  <ul><li>該当する場合はブラウザー言語。</li><li>例：`en`。</li></ul> |

#### セッションパラメータ（`_cvar`）

次の表に、詳細なセッションレベルのトラッキング情報を示します。

|**パラメータ**| **説明**|
|---| ---|
|`appid`|  <ul><li>アプリのID。</li><li>例：`com.myapp.appster`。</li></ul> |
|`appname`|  <ul><li>アプリの名前。</li><li>例：My Application。</li></ul> |
|`country`|  <ul><li>国。</li><li>例：`US`。</li></ul> |
|`deviceid`|  <ul><li>デバイスID。</li><li>例：`e3f5536a141811db40efd6400f1d0a4e`。</li></ul> |
|`deviceidtype`|  <ul><li>デバイスIDのタイプ。</li><li>例：`AAID`または`IDFA`。</li></ul> |
|`ip`|  <ul><li>（必須）モバイルデバイスのIPアドレス。</li><li>例：`8.8.8.8`。</li></ul> |
|`lang`|  <ul><li>ユーザーの言語。</li><li>例：`en`。</li></ul> |
|`medium`|  <ul><li>（必須）モバイルアプリの場合は`app`に構成します。</li><li>例：`app`。</li></ul> |
|`os`|  <ul><li>オペレーティングシステム。</li><li>例：`ANDROID`。</li></ul> |
|`source`|  <ul><li>（必須）データを提供するパートナーの名前を識別します。</li><li>例：`myApplication`</li></ul> |
|`ua`|  <ul><li>ユーザーエージェント。</li><li>例：`Mozilla/5.0`。</li></ul> |
|`user`|  <ul><li>ユーザーID。</li><li>課金システムの内部IDなど、クライアントから提供される非公開の一意なユーザー識別子。</li><li>例：`U1234`。</li></ul> |

#### アクションパラメータ（`cvar`）

次の表に、アクション単位の詳細なトラッキング情報を示します。

|**パラメータ**| **説明**|
|---| ---|
|アクション名|  <ul><li>（必須）実行されるアクションの名前。</li><li>例：`INSTALL`。</li></ul> |
|`adchannel`|  <ul><li>広告チャネル名。</li><li>例：`Social`。</li></ul> |
|`campaign`|  <ul><li>キャンペーン名。</li><li>例：`NY_Acquisition`。</li></ul> |
|`currency`|  <ul><li>収益の通貨。</li><li>例：`USD`。</li></ul> |
|`id`|  <ul><li>注文IDなど、個々のユーザーアクションのアクションID。</li><li>例：`42342`。</li></ul> |
|`preattributed`|  <ul><li>イベントがすでにアトリビューション済みかどうか。</li><li>例：`1`。</li></ul> |
|`prod`|  <ul><li>製品名。</li><li>例：`angry birds`。</li></ul> |
|`promo`|  <ul><li>ユーザーがプロモーションコードを使用した場合は、そのコード。</li><li>例：`ABCD`。</li></ul> |
|`rev`|  <ul><li>収益額。</li><li>指定しない場合は、デフォルト値が使用されます。</li><li>例：`12`。</li></ul> |
|`ts`|  <ul><li>UTC形式によるイベントの正確なUnixタイムスタンプ。</li><li>指定しない場合は、デフォルト値が使用されます。</li><li>例：`1538996046`。</li></ul> |