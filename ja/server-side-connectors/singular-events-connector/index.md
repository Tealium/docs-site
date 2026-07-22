---
title: シングラーエベントコネクタ構成ガイド
description: この記事では、シングラーエベントコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/singular-events-connector/
---
## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|イベントのインストール| ✗| ✓|
|インストール後のイベント| ✗| ✓|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタ概要](https://docs.tealium.com/about-connectors/)の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **APIキー**：APIキーが必要です。クライアントは、[シングラーのポータル](https://app.singular.net/#/sdk)から自分のアカウント内でAPIキーを取得できます。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - イベントのインストール

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|デバイスID|  <ul><li>少なくとも1つのデバイス識別子が必要です。例えば：  <ul><li>広告主識別子 (`idfa`)</li><li>iOSアプリのベンダー識別子 (`idfv`)</li><li>Android広告ID ( `aifa`),</li><li>Android ID ( `andi`) for Android.</li></ul> </li><li>詳細情報は以下の[APIドキュメンテーション](https://support.singular.net/hc/en-us/articles/4411780525979-Types-of-Device-IDs)を参照してください。</li></ul> |
|プラットフォーム| `Android` または `iOS`.|
|アプリケーション名|  <ul><li>アプリケーションのパッケージ名（Android）またはバンドルID（iOS）。</li><li>例：`com.mycompany.app`</li></ul> |
|IPアドレス|  <ul><li>デバイスセッションのIPアドレス（小数点またはコロン付き）。</li><li>IPv4とIPv6の両方がサポートされています。</li></ul> |
|デバイスメーカー|  <ul><li>デバイスハードウェアのメーカー名。通常は消費者向けの名前です。</li><li>例：`Samsung`、`LG`、または `Apple`。</li></ul> |
|デバイスモデル|  <ul><li>デバイスハードウェアのモデル。</li><li>例：`iPhone 8` または `Galaxy S10`</li></ul> |
|デバイスビルド|  <ul><li>デバイスのビルド、URLエンコードされています。</li><li>例：`Build%2F13D15`。</li></ul> |
|OSバージョン|  <ul><li>デバイス上のOSのバージョン。</li><li>例：`9.2`。</li></ul> |
|言語 &amp; 国コード|  <ul><li>デバイスのIETFローカルタグ。2文字の言語コードと国コードをアンダースコアで区切ります。</li><li>例：`en_US`。</li></ul> |
|オプションパラメータ|  <ul><li>ここにすべてのオプションパラメータを追加します。</li><li>サポートされているパラメータの詳細については、[シングラーAPIドキュメンテーション](https://support.singular.net/hc/en-us/articles/360048588672#Event_Notification_Endpoint)を参照してください。</li></ul> |

### アクション - インストール後のイベント

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|イベント名|  <ul><li>シングラーで報告するイベントの名前。</li><li>例：`ViewItem`</li></ul> |
|アプリケーション名|  <ul><li>モバイルアプリケーションのパッケージ名（Android）またはバンドルID（iOS）。</li><li>例：`com.yourcompany.app`</li></ul> |
|デバイスID|  <ul><li>少なくとも1つのデバイス識別子が必要です。例えば：  <ul><li>広告主識別子 (`idfa`)</li><li>iOSアプリのベンダー識別子 (`idfv`)</li><li>Android広告ID ( `aifa`),</li><li>Android ID ( `andi`) for Android.</li></ul> </li><li>詳細情報は以下の[APIドキュメンテーション](https://support.singular.net/hc/en-us/articles/4411780525979-Types-of-Device-IDs)を参照してください。</li></ul> |
|プラットフォーム| Android または iOS.|
|IPアドレス|  <ul><li>デバイスの生のIPアドレス（小数点またはコロン付き）。</li><li>IPv4とIPv6の両方がサポートされています。</li></ul> |
|デバイスメーカー|  <ul><li>デバイスハードウェアのメーカー名。通常は消費者向けの名前です。</li><li>例：`Samsung`、`LG`、または `Apple`</li></ul> |
|デバイスモデル|  <ul><li>デバイスハードウェアのモデル。</li><li>例：`iPhone XS` または `Galaxy S10`</li></ul> |
|デバイスビルド|  <ul><li>デバイスのビルド、URLエンコードされています。</li><li>例：`Build%2F13D15`</li></ul> |
|OSバージョン|  <ul><li>デバイス上のOSのバージョン。</li><li>例：`9.2`</li></ul> |
|言語 &amp; 国コード|  <ul><li>デバイスのIETFローカルタグ。2文字の言語コードと国コードをアンダースコアで区切ります。</li><li>例：`en_US`</li></ul> |
|オプションパラメータ|  <ul><li>ここにすべてのオプションパラメータを追加します。</li><li>詳細情報は、[シングラーサーバー間ドキュメンテーション](https://support.singular.net/hc/en-us/articles/360048588672#Event_Notification_Endpoint)を参照してください。</li></ul> |