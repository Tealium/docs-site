---
title: Appcuesコネクタ構成ガイド
description: この記事では、Appcuesコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/appcues-connector/
---## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|ユーザープロファイルの更新| ✓| ✗|
|ユーザーイベントの記録| ✗| ✓|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタ概要]()の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **アカウントID**
  * あなたのAppcuesアカウントID。
  * アカウント構成ページで見つけることができます。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - ユーザープロファイルの更新

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|ユーザーID|  &lt;ul&gt;&lt;li&gt;更新するプロファイルのエンドユーザーID。&lt;/li&gt;&lt;/ul&gt; |
|プロパティ|  &lt;ul&gt;&lt;li&gt;ユーザーの保存されたプロファイルに更新する任意のキー値データを含むオブジェクト。&lt;/li&gt;&lt;li&gt;詳細については、[Appcues HTTP API (Developer)](http://docs.appcues.com/article/254-http-api)を参照してください。&lt;/li&gt;&lt;/ul&gt; |

### アクション - ユーザーイベントの記録

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|ユーザーID|  &lt;ul&gt;&lt;li&gt;更新するプロファイルのエンドユーザーID。&lt;/li&gt;&lt;/ul&gt; |
|イベント名|  &lt;ul&gt;&lt;li&gt;イベント名。&lt;/li&gt;&lt;li&gt;最大127文字。&lt;/li&gt;&lt;li&gt;これは特定のイベントをグループ化し、ターゲティングする主なメカニズムです。&lt;/li&gt;&lt;li&gt;詳細については、[Appcues HTTP API (Developer)](http://docs.appcues.com/article/254-http-api)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|タイムスタンプ|  &lt;ul&gt;&lt;li&gt;イベントが発生した時間。&lt;/li&gt;&lt;li&gt;整数形式（Unix時間として）または文字列形式（ISO 8601準拠の日付、例えば **2016-01-13T13:05:22.000Z**）。&lt;/li&gt;&lt;/ul&gt; |
|イベント属性|  &lt;ul&gt;&lt;li&gt;イベント属性&lt;/li&gt;&lt;/ul&gt; |
