---
title: Simility タグ構成ガイド
description: この記事では、Tealium iQ タグ管理アカウントで Simility タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/simility-tag/
---
## 前提条件

* Simility アカウント

## タグの構成

まず、タグマーケットプレイスにアクセスし、プロファイルに Simility タグを追加します（[タグの追加](https://docs.tealium.com/manage-tags/#add-a-tag)を参照）。

タグを追加した後、以下の構成を行います：

1. **顧客ID**: Simility からサインアップ時に受け取った一意の識別子です。顧客IDは必須で、このフィールドに指定するか、データマッピングを通じて動的に構成できます。
1. **ゾーン**: データをホスティングしているデータセンターの場所です。利用可能なオプションは `US`（デフォルト）と `EU` です。
1. **Simility Lite**: デフォルトでONになっています。`OFF`にする場合は、地理位置情報、マウスの動きなど、追加のユーザー情報を送信する必要があります。
1. **Simility Lite レベル**: Simility サポートチームから受け取った数値（小数）です。


<blockquote>
**Simility Lite** および **Simility Lite レベル** の構成は高度な構成です。これらの詳細については、Simility サポートチームにお問い合わせください。
</blockquote>


## ロードルール

[ロードルール](https://docs.tealium.com/about-load-rules/)は、サイト上でこのタグのインスタンスをいつ、どこでロードするかを決定します。

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグ宛先にマッピングする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

Simility タグの宛先変数は、そのデータマッピングタブに組み込まれています。利用可能なカテゴリは以下の通りです：

### 標準

| 宛先名               | 説明                                                                                                      |
|:---------------------|:---------------------------------------------------------------------------------------------------------|
| Simility 顧客ID      | (必須) Simility からサインアップ時に提供された顧客/アカウントID                                          |
| Simility Lite        | Simility Liteが有効かどうかを判断するブール値（`true`/`false`）                                         |
| Simility Lite レベル | Simility サポートチームから受け取った小数値                                                              |
| ゾーン               | データをホスティングしているデータセンターの場所。マッピングする変数が `us` または `eu` を含むことを確認してください。 |
| セッションID         | (必須) ユーザーセッションの一意のID                                                                      |
| イベントタイプ       | (必須) ユーザー活動に関連するイベントのカンマ区切り文字列                                                |


<blockquote>
標準宛先へのマッピングは、対応するタグ構成を上書きします。
</blockquote>


#### トランザクション情報

トランザクションデータ（例：ユーザー、注文、トランザクション、アプリケーション、プロファイルなど）を送信することができます。データはペイロードの `transaction_info` オブジェクトを通じて送信されます。

| 宛先名               | 説明                                                                                                      |
|:--------------------|:---------------------------------------------------------------------------------------------------------|
| エンティティ         | ペイロードのエンティティタイプ；`transaction_info` オブジェクトを使用する場合は必須                      |
| トランザクションID   | トランザクションの一意のID；`transaction_info` オブジェクトを使用する場合は必須                          |
| 名                   | ユーザーの名前                                                                                           |
| 姓                   | ユーザーの姓                                                                                             |
| ユーザーID           | ユーザーのユーザー名                                                                                     |
| メール               | ユーザーのメールID                                                                                       |
| 初回注文か           | ユーザーの初回注文かどうかを判断するブール値（`true`/`false`）                                          |
| リトライ回数         | 注文を行う試みの回数                                                                                     |
| カスタムフィールド   | ユーザーのトランザクションに関連するカスタムデータ。`custom` をカスタムパラメータ名で置き換えてください。例：`field.order_categories` |
| カスタムネストフィールド | トランザクションデータをネスト形式で送信します。例：`field.order_details.is_first_order`                |

**例のペイロード**

トランザクション情報のマッピングが `transaction_info` オブジェクト内にラップされているのに対し、すべての非トランザクションマッピングはオブジェクトの外にあります。

```javascript
var similityContext = {
    "customer_id": "acme",
    "session_id": "1234",
    "user_id" : "user1234",
    "simility_lite": true,
    "transaction_info": [{
      "entity": "orders",
      "id": "xyz101",
      "fields": {
          "first_name": "John",
          "last_name": "Doe",
          "user_id": "user1234",
          "email": "johndoe@example.com",
          "order_categories": ["123", "456", "789"],
          "order_details": { "is_first_order": true, "num_retries": 1 },
       }
   }]
  };
```

### E-コマース

Simility タグは E-コマース対応しているため、デフォルトの E-コマース拡張マッピングを自動的に使用します。以下の場合を除き、手動でのマッピングは通常必要ありません：

* 拡張マッピングを上書きしたい場合
* 拡張で提供されていない E-コマース変数が必要な場合

| 宛先名               | 説明                    | E-コマース拡張変数 |
|:--------------------|:-----------------------|:------------------|
| 注文ID              | 一意の注文ID            | `_corder`         |
| 注文合計             | 注文の総額              | `_ctotal`         |
| 顧客ID              | (必須) 一意の顧客ID     | `_ccustid`        |
| 製品IDリスト         | 製品IDの配列            | `_cprod`          |
| 名称リスト           | 製品名の配列            | `_cprodname`      |
| カテゴリリスト       | 製品カテゴリの配列      | `_ccat`           |
| 数量リスト           | 製品数量の配列          | `_cquan`          |
| 価格リスト           | 製品価格の配列          | `_cprice`         |

## ベンダー文書

* [Simility Javascript](https://simility.com/developer/#devicerecon-javascript)
