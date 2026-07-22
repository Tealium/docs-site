---
title: Google Analyticsユーザー削除コネクタ構成ガイド
description: この記事では、Customer Data HubアカウントでGoogle Analyticsユーザー削除コネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/google-analytics-user-deletion-connector/
---
## コネクタのアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|ユーザー削除のリクエスト| ✓| ✗|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタについて](https://docs.tealium.com/ja/server-side/connectors/manage/)の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **クライアントID**
  * [Webサーバーアプリケーション用のOAuth 2.0の使用](https://developers.google.com/identity/protocols/OAuth2WebServer#creatingcred&quot;)に従って認証資格を作成します。
  * 認証済みのリダイレクトURIは、リダイレクトURIを許可するように構成する必要があります：<https://my.tealiumiq.com/oauth/webhook/callback.html>

* **クライアントシークレット**
  * クライアントIDを参照してください。
  * ポップアップがブロックされていないことを確認し、**接続を確立**をクリックします。
  * アカウントにログインし、アクセスを確認します。
  * 一度許可されたら、Customer Data Hubプロファイルを保存してください。  

<blockquote>
この接続フローを通じていくたびに、変更を保存するためにCustomer Data Hubプロファイルを保存することを確認してください。
</blockquote>


## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - ユーザー削除のリクエスト

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|IDタイプ|  <ul><li>ユーザーのタイプ。</li><li>`APP_INSTANCE_ID`、`CLIENT_ID`、または`USER_ID`のいずれかでなければなりません。</li><li>このエンドポイントの詳細については、次を参照してください：[UserDeletion.userDeletionRequest](https://developers.google.com/analytics/devguides/config/userdeletion/v3/reference/userDeletion/userDeletionRequest)</li></ul> |
|ユーザーID|  <ul><li>ユーザーのID。</li><li>これはIDタイプと一致する必要があります。</li><li>例えば、ユーザーIDが</li></ul> |
|削除リクエスト時間|  <ul><li>削除リクエストがGoogle Analyticsに受け取られた時点。</li></ul> |
|WebプロパティID|  <ul><li>WebプロパティID、形式は`UA-XXXXX-YY`。</li><li>`CLIENT_ID`または`USER_ID` IDタイプと一緒に使用するために定義する必要があります。</li></ul> |
|FirebaseプロジェクトID|  <ul><li>あなたのFirebaseプロジェクトの識別子。</li><li>Firebaseで構築されたモバイルアプリと一緒に使用する場合は必須です。</li></ul> |
