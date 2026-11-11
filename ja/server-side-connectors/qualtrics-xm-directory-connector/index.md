---
title: Qualtrics XM Directoryコネクタ構成ガイド
description: この記事では、Qualtrics XM Directoryコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/qualtrics-xm-directory-connector/
---
## API情報

このコネクタは、次のベンダーAPIを使用します。

* API名：Qualtrics XM Directory API
* APIバージョン：v3
* APIエンドポイント：`https://ca1.qualtrics.com`
* ドキュメント：[Qualtrics XM Directory API](https://api.qualtrics.com/api-reference/docs/api-reference.md)

## コネクタアクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
|ディレクトリ連絡先の作成または更新| ✓| ✓|
|連絡先トランザクションの作成| ✓| ✓|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、次の構成を構成します。

* **データセンターID**
  * データセンターIDは、**Account Settings** &gt; **Qualtrics IDs** &gt; **IDs** &gt; **Box User**の順に移動すると確認できます。
* **クライアントID**
  * Qualtrics XM Directory APIへのアクセス権を持つWebアプリケーションのクライアントIDを指定します。
  * クライアントIDは、**Account Settings** **&gt; Qualtrics IDs &gt;** **OAuth Client Manager**の順に移動すると確認できます。
  * Qualtrics XM Directory APIのOAuth Client Managerページには、次の**グラントタイプ**が含まれている必要があります。
    * `client_credentials`。また、**スコープ**は`manage:contact_transactions`、`manage:directory_contacts`、`read:directories`、`read:mailing_lists`である必要があります。
  * 詳細については、[OAuth認証（クライアント資格情報）](https://api.qualtrics.com/api-reference/docs/Instructions/oauth-authentication.md)および[OAuth 2.0スコープ](https://api.qualtrics.com/api-reference/docs/Instructions/oauthscopes.md)を参照してください。
* **クライアントシークレット**
  * Webアプリケーションのクライアントシークレットを指定します。


<blockquote>
Qualtrics内でアプリケーションを作成する際は、Tealium環境に一致するようにリダイレクトURLを構成してください。たとえば、SSOが有効な顧客の場合は[https://sso.tealiumiq.com/oauth/qualtrics/callback.html](https://sso.tealiumiq.com/oauth/qualtrics/callback.html)、標準の顧客の場合は[https://my.tealiumiq.com/oauth/qualtrics/callback.html](https://my.tealiumiq.com/oauth/qualtrics/callback.html)を使用します。
</blockquote>


## アクション構成 — パラメータとオプション

**続行**をクリックして、コネクタアクションを構成します。アクションの名前を入力し、リストからアクションタイプを選択します。

### アクション — ディレクトリ連絡先の作成または更新

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|更新方法|  <ul><li>（必須）適用する更新方法を選択します。<ul><li>**作成のみ**：既存の連絡先を検索し、見つからない場合は新しい連絡先を作成します。</li><li>**更新のみ**：既存の連絡先を検索して更新します。</li><li>**作成または更新**：既存の連絡先を検索し、見つかった場合は更新し、それ以外の場合は新しい連絡先を作成します。</li></ul> </li></ul> |
|ディレクトリ|  <ul><li>（必須）連絡先を作成または更新するディレクトリを選択します。</li></ul> |
|名|
|姓|
|メールアドレス|
|電話番号|
|外部参照|
|言語|
|購読解除済み|
|名|
|姓|
|メールアドレス|
|電話番号|
|外部参照|
|言語|
|購読解除済み|
|埋め込みデータ|  <ul><li>埋め込みデータオブジェクトには、連絡先に関連付ける追加のメタデータが含まれます。</li><li>このユーザー定義データには、出生地、性別、雇用状況などのデータを含めることができます。</li></ul> |
|連絡先ID|
|名|
|姓|
|メールアドレス|
|電話番号|
|外部参照|
|言語|
|購読解除済み|

### アクション — 連絡先トランザクションの作成

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|ディレクトリ|  <ul><li>（必須）連絡先を作成または更新するディレクトリを選択します。</li></ul> |
|メーリングリスト|  <ul><li>（必須）連絡先トランザクションを作成するメーリングリストを選択します。</li></ul> |
|連絡先ID|
|名|
|姓|
|メールアドレス|
|電話番号|
|外部参照|
|言語|
|購読解除済み|
|トランザクション日|