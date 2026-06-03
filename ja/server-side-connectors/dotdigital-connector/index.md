---
title: dotdigitalコネクタ構成ガイド
description: この記事では、dotdigitalコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/dotdigital-connector/
---## 仕組み

dotdigitalコネクタは、デジタルマーケティングの専門ホームにSaaS技術ソリューションとツールを提供し、メールマーケティングプラットフォームを提供します。

## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|キャンペーンをトリガー| ✓| ✓|
|トリガーされたキャンペーンを使用してメールを送信| ✓| ✓|
|SMSを送信| ✓| ✓|
|連絡先を作成または更新| ✓| ✗|
|連絡先をアドレス帳に追加| ✓| ✗|
|連絡先をアドレス帳から削除| ✓| ✗|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法については、[コネクタ概要]()の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **APIユーザー名**
  * APIユーザーのユーザー名。
  * APIを使用するためには、まずAPIユーザーを作成する必要があります。
  * これらのAPIユーザーの資格情報（ユーザー名/パスワード）は、各操作/メソッド呼び出しを認証し、正しいアカウントに接続されていることを確認するために必要です。
  * 構成情報については、次のベンダーのドキュメンテーションを参照してください：[APIの使用開始](https://developer.dotmailer.com/docs/getting-started-with-the-api)

* **APIパスワード**
  * APIユーザーのパスワード。

* **リージョンID**
  * すべてのAPIエンドポイントに含めるべきリージョンID。
  * APIエンドポイントは **構成 &amp;gt; アクセス &amp;gt; APIユーザー** の下にあります。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - キャンペーンをトリガー

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|キャンペーンID|  &lt;ul&gt;&lt;li&gt;リクエストボディ内に含める必要があるキャンペーンのID。&lt;/li&gt;&lt;/ul&gt; |
|アドレス帳ID|  &lt;ul&gt;&lt;li&gt;キャンペーンを送信するアドレス帳のID。&lt;/li&gt;&lt;li&gt;アドレス帳IDまたは連絡先IDのいずれかを指定する必要があります。&lt;/li&gt;&lt;/ul&gt; |
|連絡先ID|  &lt;ul&gt;&lt;li&gt;キャンペーンを送信する連絡先のID。&lt;/li&gt;&lt;li&gt;アドレス帳IDまたは連絡先IDのいずれかを指定する必要があります。&lt;/li&gt;&lt;/ul&gt; |
|送信日|  &lt;ul&gt;&lt;li&gt;キャンペーンを送信したい日時。&lt;/li&gt;&lt;/ul&gt; |

### アクション - トリガーされたキャンペーンを使用してメールを送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|宛先アドレス|  &lt;ul&gt;&lt;li&gt;受信者のメールアドレス。&lt;/li&gt;&lt;/ul&gt; |
|キャンペーンID|  &lt;ul&gt;&lt;li&gt;トリガーされたキャンペーンのID。&lt;/li&gt;&lt;li&gt;このエンドポイントに関する詳細情報は、次のベンダーのドキュメンテーションを参照してください：[トリガーされたキャンペーンを使用してトランザクションメールを送信](https://developer.dotmailer.com/docs/send-transactional-email-using-a-triggered-campaign)。&lt;/li&gt;&lt;/ul&gt; |
|パーソナライゼーション値|  &lt;ul&gt;&lt;li&gt;各パーソナライゼーション値はキーと値のペアです。&lt;/li&gt;&lt;/ul&gt; |

### アクション - SMSを送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|電話番号|  &lt;ul&gt;&lt;li&gt;連絡先の携帯電話番号。&lt;/li&gt;&lt;/ul&gt; |
|メッセージ|  &lt;ul&gt;&lt;li&gt;連絡先の携帯電話に送信するSMSメッセージ。&lt;/li&gt;&lt;/ul&gt; |

### アクション - 連絡先を作成または更新

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|メール|  &lt;ul&gt;&lt;li&gt;連絡先のメールアドレス。&lt;/li&gt;&lt;li&gt;このエンドポイントに関する詳細情報は、次のベンダーのドキュメンテーションを参照してください：[連絡先の作成](https://developer.dotmailer.com/docs/create-contact)。&lt;/li&gt;&lt;/ul&gt; |
|データフィールド|  &lt;ul&gt;&lt;li&gt;各連絡先データフィールドはキーと値のペアです。&lt;/li&gt;&lt;/ul&gt; |
|オプトインタイプ|  &lt;ul&gt;&lt;li&gt;連絡先のオプトインタイプ。&lt;/li&gt;&lt;/ul&gt; |
|メールタイプ|  &lt;ul&gt;&lt;li&gt;連絡先のメールタイプ。&lt;/li&gt;&lt;/ul&gt; |
|連絡先ID|  &lt;ul&gt;&lt;li&gt;連絡先のID。&lt;/li&gt;&lt;li&gt;連絡先を更新するためには、これを構成する必要があります。&lt;/li&gt;&lt;/ul&gt; |

### アクション - 連絡先をアドレス帳に追加

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|アドレス帳ID|  &lt;ul&gt;&lt;li&gt;アドレス帳のID。&lt;/li&gt;&lt;li&gt;このエンドポイントに関する詳細情報は、次のベンダーのドキュメンテーションを参照してください：[連絡先をアドレス帳に追加](https://developer.dotmailer.com/docs/add-contact-to-address-book)。&lt;/li&gt;&lt;/ul&gt; |
|メール|  &lt;ul&gt;&lt;li&gt;連絡先のメールアドレス。&lt;/li&gt;&lt;li&gt;このエンドポイントに関する詳細情報は、次のベンダーのドキュメンテーションを参照してください：[連絡先の作成](https://developer.dotmailer.com/docs/create-contact)。&lt;/li&gt;&lt;/ul&gt; |
|データフィールド|  &lt;ul&gt;&lt;li&gt;各連絡先データフィールドはキーと値のペアです。&lt;/li&gt;&lt;/ul&gt; |
|オプトインタイプ|  &lt;ul&gt;&lt;li&gt;連絡先のオプトインタイプ。&lt;/li&gt;&lt;/ul&gt; |
|メールタイプ|  &lt;ul&gt;&lt;li&gt;連絡先のメールタイプ。&lt;/li&gt;&lt;/ul&gt; |

### アクション - 連絡先をアドレス帳から削除

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|アドレス帳ID|  &lt;ul&gt;&lt;li&gt;アドレス帳のID。&lt;/li&gt;&lt;li&gt;このエンドポイントに関する詳細情報は、次のベンダーのドキュメンテーションを参照してください：[連絡先をアドレス帳から削除](https://developer.dotmailer.com/docs/delete-contact-from-address-book)。&lt;/li&gt;&lt;/ul&gt; |
|連絡先ID|  &lt;ul&gt;&lt;li&gt;削除する連絡先のID。&lt;/li&gt;&lt;/ul&gt; |