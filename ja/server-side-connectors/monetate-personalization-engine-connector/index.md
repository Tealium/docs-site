---
title: Monetate Personalization Engine コネクタ構成ガイド
description: この記事では、Monetate コネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/monetate-personalization-engine-connector/
---
## 要件

* Monetate アカウント
* API ユーザー名と API キー
* データスキーマ

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加したら、次の項目を構成します。

* **API ユーザー名**：（必須）API ユーザー名を入力します。API ユーザー名は、アカウントの **Settings > Sites > API Keys** で確認できます。
* **秘密鍵**：（必須）アカウントに登録されている公開鍵に対応する秘密鍵を指定します。秘密鍵は RSA アルゴリズムで生成し、PEM PKCS #8 形式に変換する必要があります。詳細については、[Monetate：API キーの概要](https://support.monetate.com/hc/en-us/articles/115001851123-API-Keys-Overview)および [API キーの生成](#generate-api-keys)を参照してください。
* **クライアント ID**：（必須）クライアント ID を指定します。クライアント ID は、アカウントの **Settings > API Documentation > Monetate Data API > Base URL** で確認できます。たとえば、URL が `https://api.monetate.net/api/data/v1/abc/production/` の場合、クライアント ID は `abc` です。

コネクタを構成したら、**Done** をクリックします。

**Test Connection** をクリックし、指定した認証情報で API に接続できることを確認します。

## API キーの生成

安全な通信を確保するため、Monetate API では公開鍵と秘密鍵のペアを使用します。キーペアは、無料で広く利用されている OpenSSL コマンドラインツールを使用して生成できます。

次のコマンドを実行します。

```bash
openssl genrsa -out my_key.pem 4096
openssl pkcs8 -topk8 -inform PEM -outform PEM -in my_key.pem -out my_private_key.pem -nocrypt
openssl rsa -in my_key.pem -pubout -outform PEM -out my_public_key.pem
```

これらのコマンドは、RSA アルゴリズム（キーサイズ 4096 ビット）を使用して新しいキーを生成し、暗号化せずに PKCS#8 形式へ変換します。これが秘密鍵です。最後の行では、公開鍵が PEM 形式で出力されます。

生成したら、各ファイルをテキストエディターで開き、対応するキーと値をコピーします。Monetate アカウントに公開鍵を登録し、コネクタ構成画面で秘密鍵を指定します。

## アクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
| データレコードの作成または更新（リアルタイム） | ✓ | ✓ |
| データレコードの作成または更新（バッチ） | ✓ | ✓ |

**Continue** をクリックして、コネクタのアクションを構成します。アクション名を入力し、リストからアクションタイプを選択します。

### データレコードの更新（リアルタイム）

#### パラメーター

| パラメーター | 説明 |
|---| ---|
|スキーマ |（必須）レコードを作成または更新するスキーマを選択します。 |
|データレコード |（必須）属性をデータレコードのフィールドにマッピングします。主キーフィールドの値が同じレコードがスキーマ内にすでに存在する場合、データが更新されます。タイプが `event` のスキーマには、`event time` タイプのフィールドが必要です。明示的にマッピングしない場合、フィールド値のデフォルトは現在時刻になります。日付属性は ISO 8601 形式（`YYYY-MM-DDThh:mm:ss`）に変換されます。 |


<blockquote>
詳細については、[Engine API：データの送信](https://knowledge.monetate.com/hc/en-us/articles/115005090746)を参照してください。
</blockquote>


### データレコードの作成または更新（バッチ）

#### バッチ制限

このアクションでは、ベンダーへの大量のデータ転送に対応するため、バッチリクエストを使用します。次のいずれかのしきい値に達するまで、リクエストはキューに追加されます。

* リクエストの最大数：500
* 最も古いリクエストからの最大経過時間：10 分
* リクエストの最大サイズ：5 MB

#### パラメーター

| パラメーター | 説明 |
|---| ---|
|スキーマ |（必須）レコードを作成または更新するスキーマを選択します。 |
|データレコード |（必須）属性をデータレコードのフィールドにマッピングします。主キーフィールドの値が同じレコードがスキーマ内にすでに存在する場合、データが更新されます。タイプが `event` のスキーマには、`event time` タイプのフィールドが必要です。明示的にマッピングしない場合、この値のデフォルトは現在時刻になります。日付属性は ISO 8601 形式（`YYYY-MM-DDThh:mm:ss`）に変換されます。 |

## ベンダーのドキュメント

* [Monetate：API キーの概要](https://support.monetate.com/hc/en-us/articles/115001851123-API-Keys-Overview)