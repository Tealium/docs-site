---
title: Postmarkコネクタ構成ガイド
description: この記事では、Customer Data HubアカウントでPostmarkコネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/postmark-connector/
---

## コネクタのアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|メールを送る| ✓| ✓|
|テンプレートを使用してメールを送る| ✓| ✓|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタについて]()の記事を参照してください。

コネクタを追加した後、次の構成を構成します：

* **サーバートークン**
  * サーバーレベルの権限を必要とするリクエストに使用されます。
  * このトークンは、Postmarkサーバーの認証情報タブで見つけることができます。
  * 詳細については、[Postmark: 開発者のAPI概要](https://postmarkapp.com/developer/api/overview)を参照してください。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - メールを送る

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|From|  &lt;ul&gt;&lt;li&gt;送信者のメールアドレス。&lt;/li&gt;&lt;li&gt;登録済みで確認済みの送信者署名が必要です。&lt;/li&gt;&lt;li&gt;このエンドポイントについての詳細は、&lt;https://postmarkapp.com/developer/api/email-api#send-a-single-email&gt;を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|To|  &lt;ul&gt;&lt;li&gt;受信者のメールアドレス。&lt;/li&gt;&lt;li&gt;アドレスの最大数は50です。&lt;/li&gt;&lt;/ul&gt; |
|CC|  &lt;ul&gt;&lt;li&gt;CC受信者のメールアドレス。&lt;/li&gt;&lt;li&gt;アドレスの最大数は50です。&lt;/li&gt;&lt;/ul&gt; |
|BCC|  &lt;ul&gt;&lt;li&gt;BCC受信者のメールアドレス。&lt;/li&gt;&lt;li&gt;アドレスの最大数は50です。&lt;/li&gt;&lt;/ul&gt; |
|Subject|  &lt;ul&gt;&lt;li&gt;メールの件名。&lt;/li&gt;&lt;/ul&gt; |
|Tag|  &lt;ul&gt;&lt;li&gt;送信メールをカテゴライズし、詳細な統計を取得するためのメールタグ。&lt;/li&gt;&lt;/ul&gt; |
|HTML Body|  &lt;ul&gt;&lt;li&gt;Text Bodyが指定されていない場合は必須です。&lt;/li&gt;&lt;/ul&gt; |
|Text Body|  &lt;ul&gt;&lt;li&gt;HTML Bodyが指定されていない場合は必須です。&lt;/li&gt;&lt;/ul&gt; |
|Reply To|  &lt;ul&gt;&lt;li&gt;返信先のメールアドレスを上書きします。&lt;/li&gt;&lt;li&gt;送信者署名で構成された返信先にデフォルト構成されます。&lt;/li&gt;&lt;/ul&gt; |
|Headers|  &lt;ul&gt;&lt;li&gt;含めるカスタムヘッダーのリスト。&lt;/li&gt;&lt;/ul&gt; |
|Track Opens|  &lt;ul&gt;&lt;li&gt;真または偽。&lt;/li&gt;&lt;li&gt;このメールの開封トラッキングを有効にします。&lt;/li&gt;&lt;/ul&gt; |
|Track Links|  &lt;ul&gt;&lt;li&gt;このメールのHTMLまたはテキスト本文のリンクのリンクトラッキングを有効にします。&lt;/li&gt;&lt;li&gt;可能なオプション: **なし**, **HtmlAndText**, **HtmlOnly**, **TextOnly**。&lt;/li&gt;&lt;/ul&gt; |
|Metadata|  &lt;ul&gt;&lt;li&gt;カスタムメタデータのキーと値のペア。&lt;/li&gt;&lt;/ul&gt; |

### アクション - テンプレートを使用してメールを送る

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Template ID|  &lt;ul&gt;&lt;li&gt;メッセージの送信時に使用するテンプレート。&lt;/li&gt;&lt;li&gt;Template Aliasが指定されていない場合は必須です。&lt;/li&gt;&lt;li&gt;このエンドポイントについての詳細は、&lt;https://postmarkapp.com/developer/api/templates-api#email-with-template&gt;を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|Template Alias|  &lt;ul&gt;&lt;li&gt;このメッセージの送信時に使用するテンプレートのエイリアス。&lt;/li&gt;&lt;li&gt;Template IDが指定されていない場合は必須です。&lt;/li&gt;&lt;/ul&gt; |
|Template Model|  &lt;ul&gt;&lt;li&gt;指定されたテンプレートに適用するモデルで、HTML Body、Text Body、およびSubjectを生成します。&lt;/li&gt;&lt;/ul&gt; |
|Inline CSS|  &lt;ul&gt;&lt;li&gt;真または偽。&lt;/li&gt;&lt;li&gt;デフォルトでは、指定されたテンプレートにHTML Bodyが含まれている場合、スタイルブロックはレンダリングされたHTMLコンテンツのインライン属性として適用されます。&lt;/li&gt;&lt;li&gt;このリクエストフィールドに`false`を渡すことで、この動作をオプトアウトできます。&lt;/li&gt;&lt;/ul&gt; |
|From|  &lt;ul&gt;&lt;li&gt;送信者のメールアドレス。&lt;/li&gt;&lt;li&gt;登録済みで確認済みの送信者署名が必要です。&lt;/li&gt;&lt;/ul&gt; |
|To|  &lt;ul&gt;&lt;li&gt;受信者のメールアドレス。&lt;/li&gt;&lt;li&gt;アドレスの最大数は50です。&lt;/li&gt;&lt;/ul&gt; |
|CC|  &lt;ul&gt;&lt;li&gt;CC受信者のメールアドレス。&lt;/li&gt;&lt;li&gt;アドレスの最大数は50です。&lt;/li&gt;&lt;/ul&gt; |
|BCC|  &lt;ul&gt;&lt;li&gt;BCC受信者のメールアドレス。&lt;/li&gt;&lt;li&gt;アドレスの最大数は50です。&lt;/li&gt;&lt;/ul&gt; |
|Tag|  &lt;ul&gt;&lt;li&gt;送信メールをカテゴライズし、詳細な統計を取得するためのメールタグ。&lt;/li&gt;&lt;/ul&gt; |
|Reply To|  &lt;ul&gt;&lt;li&gt;返信先のメールアドレスを上書きします。&lt;/li&gt;&lt;li&gt;送信者署名で構成された**返信先**にデフォルト構成されます。&lt;/li&gt;&lt;/ul&gt; |
|Headers|  &lt;ul&gt;&lt;li&gt;含めるカスタムヘッダーのリスト。&lt;/li&gt;&lt;/ul&gt; |
|Track Opens|  &lt;ul&gt;&lt;li&gt;真または偽。&lt;/li&gt;&lt;li&gt;このメールの開封トラッキングを有効にします。&lt;/li&gt;&lt;/ul&gt; |
|Track Links|  &lt;ul&gt;&lt;li&gt;このメールのHTMLまたはテキスト本文のリンクのリンクトラッキングを有効にします。&lt;/li&gt;&lt;li&gt;可能なオプション: **なし**, **HtmlAndText**, **HtmlOnly**, **TextOnly**。&lt;/li&gt;&lt;/ul&gt; |