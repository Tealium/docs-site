---
title: CleverTapコネクタ構成ガイド
description: この記事では、Clevertapコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/clevertap-connector/
---
## 構成

コネクタマーケットプレイスにアクセスし、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタについて]()を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **アカウントID**
  * あなたのCleverTapアカウントID。詳細については、[CleverTap：認証](https://developer.clevertap.com/docs/authentication)を参照してください。
* **アカウントパスコード**
  * あなたのCleverTapアカウントパスコード。詳細については、[CleverTap：認証](https://developer.clevertap.com/docs/authentication)を参照してください。

## アクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
| ユーザーの追加または更新 | ✓ | ✗ |
| イベントの送信 | ✗ | ✓ |

アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### ユーザーの追加または更新

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| プロファイルデータ | ユーザープロファイルのプロパティ。キーと値のペアとして渡されます。注：`Phone`は`&#43;[国コード][電話番号]`の形式でフォーマットする必要があります（例：`&#43;12125551212`）。このエンドポイントについての詳細は、[Clevertap: Upload User Profiles API](https://developer.clevertap.com/docs/upload-user-profiles-api)を参照してください。 |
| Identity | ユニークなユーザーを識別するためのID、例えばユーザーのメールアドレス、電話番号、またはユーザーをタグ付けするために使用するその他の識別子です。ユーザーを識別するために、identity、FBID、GPID、または`objectId`のいずれかのパラメータに値を構成する必要があります。 |
| FBID | Facebook IDによってユニークなユーザーを識別します。 |
| GPID | Google Plus IDによってユニークなユーザーを識別します。 |
| Object ID | CleverTap Global Object IDによってユニークなユーザーを識別します。 |
| TS | イベントが発生した日時をUNIXエポックでフォーマットします（例：2023年1月1日 00:00:00 UTCの場合は`1672531200`）。デフォルト値は現在のタイムスタンプです。 |

### イベントの送信

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| イベント名 | イベントの名前。このエンドポイントについての詳細は、[CleverTap: Upload Events API](https://developer.clevertap.com/docs/upload-events-api)を参照してください。 |
| イベントデータ | イベントを説明するイベントプロパティ。キーと値のペアとして渡されます。 |
| Identity | ユニークなユーザーを識別するためのIDです。ユーザーのメールアドレス、電話番号、またはユーザーをタグ付けするために使用するその他の識別子が該当します。ユーザーを識別するために、identity、FBID、GPID、または`objectId`のいずれかのパラメータに値を構成する必要があります。 |
| FBID | Facebook IDによってユニークなユーザーを識別します。 |
| GPID | Google Plus IDによってユニークなユーザーを識別します。 |
| Object ID | CleverTap Global Object IDによってユニークなユーザーを識別します。 |
| TS | イベントが発生した日時をUNIXエポックでフォーマットします（例：2023年1月1日 00:00:00 UTCの場合は`1672531200`）。デフォルト値は現在のタイムスタンプです。 |