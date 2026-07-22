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

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタについて](https://docs.tealium.com/about-connectors/)の記事を参照してください。

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
|From|  <ul><li>送信者のメールアドレス。</li><li>登録済みで確認済みの送信者署名が必要です。</li><li>このエンドポイントについての詳細は、<https://postmarkapp.com/developer/api/email-api#send-a-single-email>を参照してください。</li></ul> |
|To|  <ul><li>受信者のメールアドレス。</li><li>アドレスの最大数は50です。</li></ul> |
|CC|  <ul><li>CC受信者のメールアドレス。</li><li>アドレスの最大数は50です。</li></ul> |
|BCC|  <ul><li>BCC受信者のメールアドレス。</li><li>アドレスの最大数は50です。</li></ul> |
|Subject|  <ul><li>メールの件名。</li></ul> |
|Tag|  <ul><li>送信メールをカテゴライズし、詳細な統計を取得するためのメールタグ。</li></ul> |
|HTML Body|  <ul><li>Text Bodyが指定されていない場合は必須です。</li></ul> |
|Text Body|  <ul><li>HTML Bodyが指定されていない場合は必須です。</li></ul> |
|Reply To|  <ul><li>返信先のメールアドレスを上書きします。</li><li>送信者署名で構成された返信先にデフォルト構成されます。</li></ul> |
|Headers|  <ul><li>含めるカスタムヘッダーのリスト。</li></ul> |
|Track Opens|  <ul><li>真または偽。</li><li>このメールの開封トラッキングを有効にします。</li></ul> |
|Track Links|  <ul><li>このメールのHTMLまたはテキスト本文のリンクのリンクトラッキングを有効にします。</li><li>可能なオプション: **なし**, **HtmlAndText**, **HtmlOnly**, **TextOnly**。</li></ul> |
|Metadata|  <ul><li>カスタムメタデータのキーと値のペア。</li></ul> |

### アクション - テンプレートを使用してメールを送る

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Template ID|  <ul><li>メッセージの送信時に使用するテンプレート。</li><li>Template Aliasが指定されていない場合は必須です。</li><li>このエンドポイントについての詳細は、<https://postmarkapp.com/developer/api/templates-api#email-with-template>を参照してください。</li></ul> |
|Template Alias|  <ul><li>このメッセージの送信時に使用するテンプレートのエイリアス。</li><li>Template IDが指定されていない場合は必須です。</li></ul> |
|Template Model|  <ul><li>指定されたテンプレートに適用するモデルで、HTML Body、Text Body、およびSubjectを生成します。</li></ul> |
|Inline CSS|  <ul><li>真または偽。</li><li>デフォルトでは、指定されたテンプレートにHTML Bodyが含まれている場合、スタイルブロックはレンダリングされたHTMLコンテンツのインライン属性として適用されます。</li><li>このリクエストフィールドに`false`を渡すことで、この動作をオプトアウトできます。</li></ul> |
|From|  <ul><li>送信者のメールアドレス。</li><li>登録済みで確認済みの送信者署名が必要です。</li></ul> |
|To|  <ul><li>受信者のメールアドレス。</li><li>アドレスの最大数は50です。</li></ul> |
|CC|  <ul><li>CC受信者のメールアドレス。</li><li>アドレスの最大数は50です。</li></ul> |
|BCC|  <ul><li>BCC受信者のメールアドレス。</li><li>アドレスの最大数は50です。</li></ul> |
|Tag|  <ul><li>送信メールをカテゴライズし、詳細な統計を取得するためのメールタグ。</li></ul> |
|Reply To|  <ul><li>返信先のメールアドレスを上書きします。</li><li>送信者署名で構成された**返信先**にデフォルト構成されます。</li></ul> |
|Headers|  <ul><li>含めるカスタムヘッダーのリスト。</li></ul> |
|Track Opens|  <ul><li>真または偽。</li><li>このメールの開封トラッキングを有効にします。</li></ul> |
|Track Links|  <ul><li>このメールのHTMLまたはテキスト本文のリンクのリンクトラッキングを有効にします。</li><li>可能なオプション: **なし**, **HtmlAndText**, **HtmlOnly**, **TextOnly**。</li></ul> |