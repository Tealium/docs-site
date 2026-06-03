---
title: Trinoクラウドデータソース
description: この記事では、Trinoクラウドデータソースの構成方法について説明します。
url: https://docs.tealium.com/ja/administration/early-access/data-sources/trino-cloud-data-source/
---
 Trinoクラウドデータソースは現在アーリーアクセス中で、選ばれた顧客のみが利用可能です。Trinoを始めるにはTealiumサポートに連絡してください。

クラウドデータソースの構成の一般的な概要については、を参照してください。

## データタイプ

Trinoデータソースは、すべてのTrinoデータタイプをサポートしています。データが正しくインポートされるように、以下のガイドラインに従ってTrinoデータタイプをマッピングしてください：

| Trino | Tealium |
|:----------|:--------|
| 整数型（SMALLINT, INTEGER, BIGINT）、十進数、浮動小数点型（REAL, DOUBLE） | 数値属性 |
| 文字型（CHAR, VARCHAR）、バイナリ型（VARBINARY）、UUID、IPADDRESS、およびJSON | 文字列属性 |
| ブール型 | ブール属性 |
| 日付および時間型（DATE, TIME, TIMESTAMP） | 日付属性 |
| 配列 | 文字列の配列、数値の配列、またはブールの配列 |
| マップ、行、その他の複雑な型 | 文字列属性 |

Trinoデータタイプの詳細については、[Trino: データタイプ](https://trino.io/docs/current/language/types.html)を参照してください。

## 接続の作成

Tealium Trinoクラウドデータソースは、ユーザー名とパスワードによる認証をサポートしています。新しい接続を構成するには、以下の接続詳細を入力してください：

* **Trino接続構成名**：再利用可能な接続構成の名前を提供します。
* **ホスト名**：Trinoサーバーのホスト名。`http://`または`https://`のプレフィックスは含めないでください。
* **ポート**：（オプション）Trinoサーバーのポート番号。指定されていない場合、デフォルトのポート8080が使用されます。
* **カタログ**：接続するカタログの名前。
* **スキーマ**：（オプション）カタログ内で接続するスキーマの名前。

### 認証

Trino接続を認証するには、以下の資格情報を入力します：

* **ユーザー名**：Trinoサーバーへの認証に使用するユーザー名。
* **パスワード**：ユーザー名に関連付けられたパスワード。

Trinoに接続した後、**テーブル選択**リストからデータソーステーブルを選択します。

## クエリ構成

一般的な概要については、を参照してください。

Trinoについては、以下の要件に注意してください：

* **タイムスタンプ &#43; インクリメント**および**タイムスタンプ**クエリモード：選択されたタイムスタンプ列は、`TIMESTAMP`または`TIMESTAMP WITH TIME ZONE`のタイプでなければなりません。
詳細については、[Trino: 日付および時間のタイプ](https://trino.io/docs/current/language/types.html#date-and-time)を参照してください。
* **インクリメント**クエリモード：選択された数値列は、追加される各行に対して値が増加し、整数型（SMALLINT, INTEGER, BIGINT）のいずれかでなければなりません。

Trinoデータタイプの詳細については、[Trino: データタイプ](https://trino.io/docs/current/language/types.html)を参照してください。
