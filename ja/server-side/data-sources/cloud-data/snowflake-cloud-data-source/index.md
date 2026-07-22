---
title: Snowflakeクラウドデータソース
url: https://docs.tealium.com/ja/server-side/data-sources/cloud-data/snowflake-cloud-data-source/
---
クラウドデータソースの構成に関する一般的な概要については、[manage-cloud-data-source](https://docs.tealium.com/manage-cloud-data-source/)を参照してください。

## ユーザーロール

Tealiumが選択したSnowflakeのテーブルまたはビューからのみデータをポーリングできるようにするには、データベース、スキーマ、ウェアハウス、および接続したいテーブルまたはビューに対して`USAGE`権限を持つカスタムユーザーロールを作成します。

詳細については、[Snowflake: カスタムロール](https://docs.snowflake.com/en/user-guide/security-access-control-overview#custom-roles)および[Snowflake: アクセス制御権限](https://docs.snowflake.com/en/user-guide/security-access-control-privileges)を参照してください。

## データタイプ

Snowflakeデータソースは、すべてのSnowflakeデータタイプをサポートしています。データが正しくインポートされるように、以下のガイドラインに従ってSnowflakeデータタイプをマッピングしてください：

| Snowflake | Tealium |
|:----------|:--------|
| 数値データタイプ  | 数値属性 |
| 文字列およびバイナリデータタイプ | 文字列属性 |
| 論理データタイプ | ブール属性|
| 日付および時間データタイプ| 日付属性 |
| 配列 | 文字列の配列、数値の配列、またはブールの配列|
| オブジェクト、バリアント、地理、幾何、およびベクターデータタイプ| 文字列属性 |

Snowflakeデータタイプの詳細については、[Snowflake: データタイプの概要](https://docs.snowflake.com/en/sql-reference/intro-summary-data-types)を参照してください。

## 接続の作成

Snowflakeへの接続を作成するには、次のアカウント情報が必要です：

* ホスト名
* 接続ウェアハウス
* データベース名
* データベーススキーマ
* 接続ロール
* Snowflakeユーザー名


<blockquote>
接続情報は、Snowflakeデータアカウントの構成によっては大文字と小文字を区別する場合があることに注意してください。
</blockquote>


新しい接続を構成するには、次の接続詳細を入力します。

* **Snowflake接続構成名**：再利用可能な接続構成の名前を提供します。
* **アカウント識別子**：`http://`プレフィックスなしのSnowflakeアカウント識別子を次の形式で入力します：
    * Snowflakeアカウント名を使用する場合：`ACCOUNT_NAME.snowflakecomputing.com`。
    * リージョン内のSnowflakeアカウントロケータを使用する場合：`ACCOUNT_LOCATOR.CLOUD_REGION_ID.CLOUD.snowflakecomputing.com`。
* **接続ウェアハウス**：この接続に使用するSnowflakeウェアハウスの名前。
* **データベース名**：接続するSnowflakeデータベースの名前。
* **データベーススキーマ**：接続するSnowflakeデータベーススキーマの名前。
* **接続ロール**：Snowflakeでユーザーに割り当てられたロール。このロールは`USAGE`権限を持っている必要があります。

詳細については、[Snowflake: カスタムロール](https://docs.snowflake.com/en/user-guide/security-access-control-overview#custom-roles)および[Snowflake: アクセス制御権限](https://docs.snowflake.com/en/user-guide/security-access-control-privileges)を参照してください。

### 認証

RSAキーペアを使用してSnowflake接続を認証する方法は3つあります：

* **新しいキーペアを生成**するTealium。
* **プライベートキーファイルをアップロード**するTealium以外で生成したもの。
* **既存のキーペアを再利用**するTealiumで以前に生成またはアップロードしたもの。

いずれの場合も、指定されたテーブルまたはビューにアクセスが必要なSnowflakeユーザーアカウントに対応する公開キーを割り当てる必要があります。

セキュリティ要件に基づいて、次のキーアルゴリズムから選択します：**RSA-2048**、**RSA-3072**、または**RSA-4096**。

#### 認証を構成する手順

1. **ユーザー名**：必要なデータベース、スキーマ、ウェアハウス、およびテーブルまたはビューにアクセスするSnowflakeユーザーのユーザー名を入力します。
1. **認証**：次のいずれかの資格情報オプションを選択します：
   * **新しいキーペアを生成**：RSAアルゴリズムを選択します。Tealiumはプライベートキー（一度だけ表示）と公開キーを表示します。キーをダウンロードして安全に保管してください。
   * **プライベートキーファイルをアップロード**：既存のプライベートキーファイルをアップロードします。ファイルが暗号化されている場合は、それを解除するためのパスフレーズを入力します。
   * **既存のキーを再利用**：既存の生成されたキーとアップロードされたキーからキーを選択します。関連する公開キーが正しいSnowflakeユーザーにすでに割り当てられていることを確認します。
1. **ダウンロード**：公開キーファイルをダウンロードします。キーは`-----BEGIN PUBLIC KEY-----`と`-----END PUBLIC KEY-----`の間のテキストのみです。
1. **割り当て**：次のSQLコマンドでSnowflakeユーザーに公開キーを割り当てます：

   ```sql
   ALTER USER your_username
   SET RSA_PUBLIC_KEY='your_public_key';
   ```

   詳細については、[Snowflake: Snowflakeユーザーに公開キーを割り当てる](https://docs.snowflake.com/en/user-guide/key-pair-auth#assign-the-public-key-to-a-snowflake-user)を参照してください。
1. （オプション）キーが正しく割り当てられたことを確認するために、キーのフィンガープリントをコピーします。[Snowflake: ユーザーの公開キーフィンガープリントを確認する](https://docs.snowflake.com/en/user-guide/key-pair-auth#verify-the-user-s-public-key-fingerprint)を参照してください。

Snowflakeに接続した後、**テーブル選択**リストからデータソーステーブルを選択します。

## クエリ構成

一般的な概要については、を参照してください。

**タイムスタンプ + インクリメント**および**タイムスタンプ**クエリモードの場合、選択されたタイムスタンプ列は次のいずれかのSnowflakeデータタイプでなければなりません：`TIMESTAMP_LTZ`、`TIMESTAMP_TZ`、または`TIMESTAMP_NTZ`。

詳細については、[Snowflake: 日付および時間データタイプ](https://docs.snowflake.com/en/sql-reference/data-types-datetime#timestamp-ltz-timestamp-ntz-timestamp-tz)を参照してください。

**インクリメント**クエリモードの場合、選択された数値列は、追加されるたびに値が増加する必要があります。自動インクリメント列の推奨定義は次のとおりです：

```sql
COL1 NUMBER AUTOINCREMENT START 1 INCREMENT 1
```