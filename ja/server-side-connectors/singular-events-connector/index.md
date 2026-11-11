---
title: Singular Eventsコネクタ構成ガイド
description: この記事では、Singular Eventsコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/singular-events-connector/
---
## コネクタアクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
|インストールイベント| ✗| ✓|
|インストール後イベント| ✗| ✓|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、以下の構成を構成します。

* **APIキー**：APIキーは必須です。クライアントは、[Singularのポータル](https://app.singular.net/#/sdk)内のアカウントからAPIキーを取得できます。

## アクション構成 - パラメータとオプション

**続行**をクリックして、コネクタアクションを構成します。アクションの名前を入力し、リストからアクションタイプを選択します。

### アクション - インストールイベント

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|デバイスID| <ul><li>少なくとも1つのデバイス識別子が必要です。例：<ul><li>広告主識別子（`idfa`）</li><li>iOSアプリのベンダー識別子（`idfv`）</li><li>Android広告ID（`aifa`）</li><li>Android用のAndroid ID（`andi`）</li></ul></li><li>詳細については、次の[APIドキュメント](https://support.singular.net/hc/en-us/articles/4411780525979-Types-of-Device-IDs)を参照してください。</li></ul> |
|プラットフォーム| `Android`または`iOS`。|
|アプリケーション名| <ul><li>アプリケーションのパッケージ名（Android）またはバンドルID（iOS）。</li><li>例：`com.mycompany.app`</li></ul> |
|IPアドレス| <ul><li>デバイスセッションのIPアドレス（小数点またはコロンを含む）。</li><li>IPv4とIPv6の両方がサポートされています。</li></ul> |
|デバイスメーカー| <ul><li>デバイスハードウェアのメーカー。通常は消費者向けの名称です。</li><li>例：`Samsung`、`LG`、`Apple`。</li></ul> |
|デバイスモデル| <ul><li>デバイスハードウェアのモデル。</li><li>例：`iPhone 8`または`Galaxy S10`</li></ul> |
|デバイスビルド| <ul><li>URLエンコードされたデバイスのビルド。</li><li>例：`Build%2F13D15`。</li></ul> |
|OSバージョン| <ul><li>デバイス上のOSのバージョン。</li><li>例：`9.2`。</li></ul> |
|言語および国コード| <ul><li>2文字の言語コードと国コードをアンダースコアで区切った、デバイスのIETFロケールタグ。</li><li>例：`en_US`。</li></ul> |
|オプションパラメータ| <ul><li>その他すべてのオプションパラメータをここに追加します。</li><li>サポートされているパラメータの詳細については、[Singular APIドキュメント](https://support.singular.net/hc/en-us/articles/360048588672#Event_Notification_Endpoint)を参照してください。</li></ul> |

### アクション - インストール後イベント

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|イベント名| <ul><li>Singularでレポートするイベントの名前。</li><li>例：`ViewItem`</li></ul> |
|アプリケーション名| <ul><li>モバイルアプリケーションのパッケージ名（Android）またはバンドルID（iOS）。</li><li>例：`com.yourcompany.app`</li></ul> |
|デバイスID| <ul><li>少なくとも1つのデバイス識別子が必要です。例：<ul><li>広告主識別子（`idfa`）</li><li>iOSアプリのベンダー識別子（`idfv`）</li><li>Android広告ID（`aifa`）</li><li>Android用のAndroid ID（`andi`）</li></ul></li><li>詳細については、次の[APIドキュメント](https://support.singular.net/hc/en-us/articles/4411780525979-Types-of-Device-IDs)を参照してください。</li></ul> |
|プラットフォーム| AndroidまたはiOS。|
|IPアドレス| <ul><li>デバイスの未加工のIPアドレス（小数点またはコロンを含む）。</li><li>IPv4とIPv6の両方がサポートされています。</li></ul> |
|デバイスメーカー| <ul><li>デバイスハードウェアのメーカー。通常は消費者向けの名称です。</li><li>例：`Samsung`、`LG`、`Apple`</li></ul> |
|デバイスモデル| <ul><li>デバイスハードウェアのモデル。</li><li>例：`iPhone XS`または`Galaxy S10`</li></ul> |
|デバイスビルド| <ul><li>URLエンコードされたデバイスのビルド。</li><li>例：`Build%2F13D15`</li></ul> |
|OSバージョン| <ul><li>デバイス上のOSのバージョン。</li><li>例：`9.2`</li></ul> |
|言語および国コード| <ul><li>2文字の言語コードと国コードをアンダースコアで区切った、デバイスのIETFロケールタグ。</li><li>例：`en_US`</li></ul> |
|オプションパラメータ| <ul><li>その他すべてのオプションパラメータをここに追加します。</li><li>詳細については、[Singularのサーバー間連携に関するドキュメント](https://support.singular.net/hc/en-us/articles/360048588672#Event_Notification_Endpoint)を参照してください。</li></ul> |