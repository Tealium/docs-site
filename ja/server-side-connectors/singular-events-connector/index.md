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

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタ概要]()の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **APIキー**：APIキーが必要です。クライアントは、[シングラーのポータル](https://app.singular.net/#/sdk)から自分のアカウント内でAPIキーを取得できます。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - イベントのインストール

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|デバイスID|  &lt;ul&gt;&lt;li&gt;少なくとも1つのデバイス識別子が必要です。例えば：  &lt;ul&gt;&lt;li&gt;広告主識別子 (`idfa`)&lt;/li&gt;&lt;li&gt;iOSアプリのベンダー識別子 (`idfv`)&lt;/li&gt;&lt;li&gt;Android広告ID ( `aifa`),&lt;/li&gt;&lt;li&gt;Android ID ( `andi`) for Android.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;詳細情報は以下の[APIドキュメンテーション](https://support.singular.net/hc/en-us/articles/4411780525979-Types-of-Device-IDs)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|プラットフォーム| `Android` または `iOS`.|
|アプリケーション名|  &lt;ul&gt;&lt;li&gt;アプリケーションのパッケージ名（Android）またはバンドルID（iOS）。&lt;/li&gt;&lt;li&gt;例：`com.mycompany.app`&lt;/li&gt;&lt;/ul&gt; |
|IPアドレス|  &lt;ul&gt;&lt;li&gt;デバイスセッションのIPアドレス（小数点またはコロン付き）。&lt;/li&gt;&lt;li&gt;IPv4とIPv6の両方がサポートされています。&lt;/li&gt;&lt;/ul&gt; |
|デバイスメーカー|  &lt;ul&gt;&lt;li&gt;デバイスハードウェアのメーカー名。通常は消費者向けの名前です。&lt;/li&gt;&lt;li&gt;例：`Samsung`、`LG`、または `Apple`。&lt;/li&gt;&lt;/ul&gt; |
|デバイスモデル|  &lt;ul&gt;&lt;li&gt;デバイスハードウェアのモデル。&lt;/li&gt;&lt;li&gt;例：`iPhone 8` または `Galaxy S10`&lt;/li&gt;&lt;/ul&gt; |
|デバイスビルド|  &lt;ul&gt;&lt;li&gt;デバイスのビルド、URLエンコードされています。&lt;/li&gt;&lt;li&gt;例：`Build%2F13D15`。&lt;/li&gt;&lt;/ul&gt; |
|OSバージョン|  &lt;ul&gt;&lt;li&gt;デバイス上のOSのバージョン。&lt;/li&gt;&lt;li&gt;例：`9.2`。&lt;/li&gt;&lt;/ul&gt; |
|言語 &amp;amp; 国コード|  &lt;ul&gt;&lt;li&gt;デバイスのIETFローカルタグ。2文字の言語コードと国コードをアンダースコアで区切ります。&lt;/li&gt;&lt;li&gt;例：`en_US`。&lt;/li&gt;&lt;/ul&gt; |
|オプションパラメータ|  &lt;ul&gt;&lt;li&gt;ここにすべてのオプションパラメータを追加します。&lt;/li&gt;&lt;li&gt;サポートされているパラメータの詳細については、[シングラーAPIドキュメンテーション](https://support.singular.net/hc/en-us/articles/360048588672#Event_Notification_Endpoint)を参照してください。&lt;/li&gt;&lt;/ul&gt; |

### アクション - インストール後のイベント

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|イベント名|  &lt;ul&gt;&lt;li&gt;シングラーで報告するイベントの名前。&lt;/li&gt;&lt;li&gt;例：`ViewItem`&lt;/li&gt;&lt;/ul&gt; |
|アプリケーション名|  &lt;ul&gt;&lt;li&gt;モバイルアプリケーションのパッケージ名（Android）またはバンドルID（iOS）。&lt;/li&gt;&lt;li&gt;例：`com.yourcompany.app`&lt;/li&gt;&lt;/ul&gt; |
|デバイスID|  &lt;ul&gt;&lt;li&gt;少なくとも1つのデバイス識別子が必要です。例えば：  &lt;ul&gt;&lt;li&gt;広告主識別子 (`idfa`)&lt;/li&gt;&lt;li&gt;iOSアプリのベンダー識別子 (`idfv`)&lt;/li&gt;&lt;li&gt;Android広告ID ( `aifa`),&lt;/li&gt;&lt;li&gt;Android ID ( `andi`) for Android.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;詳細情報は以下の[APIドキュメンテーション](https://support.singular.net/hc/en-us/articles/4411780525979-Types-of-Device-IDs)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|プラットフォーム| Android または iOS.|
|IPアドレス|  &lt;ul&gt;&lt;li&gt;デバイスの生のIPアドレス（小数点またはコロン付き）。&lt;/li&gt;&lt;li&gt;IPv4とIPv6の両方がサポートされています。&lt;/li&gt;&lt;/ul&gt; |
|デバイスメーカー|  &lt;ul&gt;&lt;li&gt;デバイスハードウェアのメーカー名。通常は消費者向けの名前です。&lt;/li&gt;&lt;li&gt;例：`Samsung`、`LG`、または `Apple`&lt;/li&gt;&lt;/ul&gt; |
|デバイスモデル|  &lt;ul&gt;&lt;li&gt;デバイスハードウェアのモデル。&lt;/li&gt;&lt;li&gt;例：`iPhone XS` または `Galaxy S10`&lt;/li&gt;&lt;/ul&gt; |
|デバイスビルド|  &lt;ul&gt;&lt;li&gt;デバイスのビルド、URLエンコードされています。&lt;/li&gt;&lt;li&gt;例：`Build%2F13D15`&lt;/li&gt;&lt;/ul&gt; |
|OSバージョン|  &lt;ul&gt;&lt;li&gt;デバイス上のOSのバージョン。&lt;/li&gt;&lt;li&gt;例：`9.2`&lt;/li&gt;&lt;/ul&gt; |
|言語 &amp;amp; 国コード|  &lt;ul&gt;&lt;li&gt;デバイスのIETFローカルタグ。2文字の言語コードと国コードをアンダースコアで区切ります。&lt;/li&gt;&lt;li&gt;例：`en_US`&lt;/li&gt;&lt;/ul&gt; |
|オプションパラメータ|  &lt;ul&gt;&lt;li&gt;ここにすべてのオプションパラメータを追加します。&lt;/li&gt;&lt;li&gt;詳細情報は、[シングラーサーバー間ドキュメンテーション](https://support.singular.net/hc/en-us/articles/360048588672#Event_Notification_Endpoint)を参照してください。&lt;/li&gt;&lt;/ul&gt; |