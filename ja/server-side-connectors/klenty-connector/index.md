---
title: Klentyコネクタ構成ガイド
description: この記事では、Klaviyoコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/klenty-connector/
---
## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|見込み客作成| ✓| ✓|
|見込み客更新| ✓| ✓|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタ概要]()の記事を参照してください。

コネクタを追加した後、次の構成を構成します：

* **APIキー**  
Kenty REST APIにアクセスするには、APIキーを生成するKlentyアカウントが必要です。このAPIキーを取得するには、次の手順を使用します：
  * Klentyアカウントにログインします。
  * **構成 &gt; ユーザー構成 &gt; Klenty APIキー**に移動します。
  * **APIキー生成**キーアイコンをクリックします。
  * 詳細については、[KlentyのAPIドキュメンテーション](http://support.klenty.com/articles/2530207-klenty-api)を参照してください。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - 見込み客作成

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|ユーザー名|  &lt;ul&gt;&lt;li&gt;アカウントに関連付けられたユーザー名。&lt;/li&gt;&lt;li&gt;詳細については、[Klentyのドキュメンテーション](http://support.klenty.com/articles/2530207-klenty-api)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|メール|  &lt;ul&gt;&lt;li&gt;見込み客のメールアドレス。&lt;/li&gt;&lt;/ul&gt; |
|名|  &lt;ul&gt;&lt;li&gt;見込み客の名前。&lt;/li&gt;&lt;/ul&gt; |
|電話|  &lt;ul&gt;&lt;li&gt;見込み客の電話番号。&lt;/li&gt;&lt;/ul&gt; |
|会社|  &lt;ul&gt;&lt;li&gt;見込み客に関連付けられた会社。&lt;/li&gt;&lt;/ul&gt; |
|フルネーム|  &lt;ul&gt;&lt;li&gt;見込み客のフルネーム。&lt;/li&gt;&lt;/ul&gt; |
|姓|  &lt;ul&gt;&lt;li&gt;見込み客の姓。&lt;/li&gt;&lt;/ul&gt; |
|ミドルネーム|  &lt;ul&gt;&lt;li&gt;見込み客のミドルネーム。&lt;/li&gt;&lt;/ul&gt; |
|部門|  &lt;ul&gt;&lt;li&gt;見込み客に関連付けられた部門。&lt;/li&gt;&lt;/ul&gt; |
|会社ドメイン|  &lt;ul&gt;&lt;li&gt;見込み客に関連付けられた会社のドメイン。&lt;/li&gt;&lt;/ul&gt; |
|タイトル|  &lt;ul&gt;&lt;li&gt;見込み客のタイトル。&lt;/li&gt;&lt;/ul&gt; |
|場所|  &lt;ul&gt;&lt;li&gt;見込み客の場所。&lt;/li&gt;&lt;/ul&gt; |
|市区町村|  &lt;ul&gt;&lt;li&gt;見込み客に関連付けられた市区町村。&lt;/li&gt;&lt;/ul&gt; |
|国|  &lt;ul&gt;&lt;li&gt;見込み客に関連付けられた国。&lt;/li&gt;&lt;/ul&gt; |
|リスト|  &lt;ul&gt;&lt;li&gt;見込み客に関連付けられたリスト。&lt;/li&gt;&lt;/ul&gt; |
|タグ|  &lt;ul&gt;&lt;li&gt;見込み客に関連付けられたタグ。&lt;/li&gt;&lt;/ul&gt; |

### アクション - 見込み客更新

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|ユーザー名|  &lt;ul&gt;&lt;li&gt;アカウントに関連付けられたユーザー名。&lt;/li&gt;&lt;li&gt;詳細については、[Klentyのドキュメンテーション](http://support.klenty.com/articles/2530207-klenty-api)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|見込み客識別子|  &lt;ul&gt;&lt;li&gt;見込み客の識別子、通常はメール。&lt;/li&gt;&lt;/ul&gt; |
|メール|  &lt;ul&gt;&lt;li&gt;見込み客のメールアドレス。&lt;/li&gt;&lt;/ul&gt; |
|名|  &lt;ul&gt;&lt;li&gt;見込み客の名前。&lt;/li&gt;&lt;/ul&gt; |
|電話|  &lt;ul&gt;&lt;li&gt;見込み客の電話番号。&lt;/li&gt;&lt;/ul&gt; |
|会社|  &lt;ul&gt;&lt;li&gt;見込み客に関連付けられた会社。&lt;/li&gt;&lt;/ul&gt; |
|フルネーム|  &lt;ul&gt;&lt;li&gt;見込み客のフルネーム。&lt;/li&gt;&lt;/ul&gt; |
|姓|  &lt;ul&gt;&lt;li&gt;見込み客の姓。&lt;/li&gt;&lt;/ul&gt; |
|ミドルネーム|  &lt;ul&gt;&lt;li&gt;見込み客のミドルネーム。&lt;/li&gt;&lt;/ul&gt; |
|部門|  &lt;ul&gt;&lt;li&gt;見込み客に関連付けられた部門。&lt;/li&gt;&lt;/ul&gt; |
|会社ドメイン|  &lt;ul&gt;&lt;li&gt;見込み客に関連付けられた会社のドメイン。&lt;/li&gt;&lt;/ul&gt; |
|タイトル|  &lt;ul&gt;&lt;li&gt;見込み客のタイトル。&lt;/li&gt;&lt;/ul&gt; |
|場所|  &lt;ul&gt;&lt;li&gt;見込み客の場所。&lt;/li&gt;&lt;/ul&gt; |
|市区町村|  &lt;ul&gt;&lt;li&gt;見込み客に関連付けられた市区町村。&lt;/li&gt;&lt;/ul&gt; |
|国|  &lt;ul&gt;&lt;li&gt;見込み客に関連付けられた国。&lt;/li&gt;&lt;/ul&gt; |
|リスト|  &lt;ul&gt;&lt;li&gt;見込み客に関連付けられたリスト。&lt;/li&gt;&lt;/ul&gt; |
|タグ|  &lt;ul&gt;&lt;li&gt;見込み客に関連付けられたタグ。&lt;/li&gt;&lt;/ul&gt; |
