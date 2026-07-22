---
title: Emailiciousコネクタ構成ガイド
description: この記事では、Customer Data HubアカウントでEmailiciousコネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/emailicious-connector/
---## コネクタのアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|購読者を作成し、リストに追加する| ✓| ✗|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタについて](https://docs.tealium.com/about-connectors/)の記事を参照してください。

コネクタを追加した後、次の構成を構成します：

* **ユーザー名**
  * Emailiciousアカウントのユーザー名。
  * 詳細については、[Emailicious API](https://emailicious-api.readthedocs.io/en/latest/topics/authentication.html)のドキュメンテーションを参照してください。

* **パスワード**
  * Emailiciousアカウントのパスワード。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - 購読者を作成し、リストに追加する

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|アカウント名|  <ul><li>Emailiciousアカウントの名前。</li><li>詳細については、次を参照してください：<https://emailicious-api.readthedocs.io/en/latest/topics/introduction.html></li></ul> |
|リストID|  <ul><li>購読者が追加されるリストの一意の識別子。</li><li>詳細については、次を参照してください：[https://emailicious-api.readthedocs.io/en/latest/resources/subscribers.html#post--api-v1-lists-(int-list_id)-subscribers](https://emailicious-api.readthedocs.io/en/latest/resources/subscribers.html#post--api-v1-lists-(int-list_id)-subscribers)</li></ul> |
|メール|  <ul><li>購読者のメール。</li></ul> |
|名前|  <ul><li>購読者の名前。</li></ul> |
|姓|  <ul><li>購読者の姓。</li></ul> |
|性別|  <ul><li>購読者の性別。</li></ul> |
|生年月日|  <ul><li>購読者の生年月日。</li></ul> |
|言語|  <ul><li>購読者の言語。</li></ul> |
|地域|  <ul><li>購読者の地域。</li></ul> |
